# .github

The organization repository for MGconsulting. It serves three purposes:

1. **Organization profile** — `profile/README.md`, shown on
   https://github.com/MGconsulting.
2. **Community health files** — `SECURITY.md`, `CONTRIBUTING.md`, `LICENSE`
   inherited by every public repository that does not define its own.
3. **Reusable workflows** — the public part of the organization's GitHub
   Actions catalog, under `.github/workflows/`.

Private defaults and the organization's private workflows (for example the
OpenTofu plan/apply workflow) live in the private `.github-private`
repository.

## Reusable workflows

Every workflow standardizes the environment: it checks out the calling
repository, provisions tooling from the repository's `mise.toml`, installs
Task, restores a dependency cache, runs one Task target, and saves the cache
on trusted runs only.

| Workflow | Runs | Notes |
| --- | --- | --- |
| `lint.yml` | `task lint` | Read-only, `contents: read`. |
| `test.yml` | `task test` | Read-only, `contents: read`. |
| `security.yml` | `task security` | Full history by default; optional SARIF upload and report artifact. |
| `artifact.yml` | `task artifact` | Builds and uploads distributable files; opt-in. |
| `release.yml` | `task release` | Manual-only, tag-pinned; creates the GitHub Release. |

### Repository contract

Calling repositories provide:

- `mise.toml` — pinned tool versions (`task`, language toolchains, linters).
- `Taskfile.yml` — at least `lint` and `test`; `security`, `artifact` and
  `release` only when used.
- `.pre-commit-config.yaml` — the lint rulebook; `task lint` runs
  `pre-commit run --all-files`.

The catalog never encodes a language or toolchain. Each repository picks its
own scanners, test runner, and packaging inside the Task targets.

### Caching

All workflows accept `cache-paths` (newline-separated paths to cache) and
`cache-key-files` (newline-separated files whose contents invalidate the
cache). The cache is restored for every run but saved only from trusted
triggers — never from `pull_request`.

### Releases and artifacts

Releases are manual and immutable: a caller running on `workflow_dispatch`
asks for an existing `v*` tag, `artifact.yml` builds that tag via
`task artifact`, and `release.yml` checks out the same tag, verifies the
commit, runs `task release`, verifies the `SHA256SUMS` manifest if present,
and publishes the GitHub Release.

### Caller example

```yaml
jobs:
  lint:
    uses: MGconsulting/.github/.github/workflows/lint.yml@<commit-sha>
    permissions:
      contents: read

  test:
    uses: MGconsulting/.github/.github/workflows/test.yml@<commit-sha>
    permissions:
      contents: read
```

Pin by commit SHA. This repository follows its own contract: `task lint`
runs pre-commit (yamllint, actionlint) and `task test` validates every
workflow file with actionlint.
