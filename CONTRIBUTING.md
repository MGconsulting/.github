# Contributing

Thank you for contributing to MGconsulting. The organization is a
one-engineer practice, so responses are slower than in a full-time
open-source project — please be patient.

## Ground rules

- Public repositories follow the organization's conventions: every change
  goes through a pull request, must pass the checks, and must be reviewed.
- All infrastructure is managed as code. Do not propose UI-only changes to
  settings that are managed by OpenTofu modules.
- Changes to module behavior need tests. Every module in
  `terraform-github-modules` ships mocked tests; a module without them will
  not be merged.

## Getting started

1. Fork the repository and create a feature branch.
2. Install the toolchain from `mise.toml` (`mise install`).
3. Run the local gates before opening a pull request:

   ```sh
   task lint
   task test
   ```

4. Open a pull request against `main` and describe what changed and why.

## Release policy

The `terraform-github-modules` repository is released with semantic
versioning. Consumers pin a release tag; behavioral changes that are not
backward-compatible require a major version.

## Security

Do not include security fixes in ordinary pull requests. Report them through
private vulnerability reporting as described in `SECURITY.md`.
