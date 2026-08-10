# MGconsulting

Platform engineering for teams that want infrastructure they do not have to
babysit. One engineer, everything as code, nothing configured by hand.

MGconsulting builds and operates application platforms end to end: private
edge hosting, GitHub automation, and the security controls around both.
Every change is code, every change is reviewed, and every change lands
through automation with an auditable trail.

## What we build

- **Application platforms** — private edge hosting on IPv6: hardened Debian,
  Docker, Traefik, Tailscale, and Cloudflare. Services are declared in one
  validated YAML file and deployed by Ansible, with secrets resolved from
  Bitwarden Secrets Manager on the controller so they never enter Git or CI
  logs.
- **GitHub automation** — reusable workflows and OpenTofu modules that give
  an organization safe defaults: SHA-pinned Actions, branch protection,
  plan-then-approve infrastructure changes, and consistent lint, test, and
  security gates across every repository.
- **Security by default** — least privilege everywhere, no shared human
  accounts, short-lived tokens, secret scanning and push protection on, and
  a release process that only ever publishes a verified build of an
  immutable tag.

## Public work

| Repository | What it is |
| --- | --- |
| [`terraform-github-modules`](https://github.com/MGconsulting/terraform-github-modules) | OpenTofu modules for GitHub organizations and personal accounts: repositories, branch protection, teams, rulesets, and Actions policy, with mocked tests and safe defaults. |

The application platform and its automation are private by design: they are
delivered as a managed service, not as code you are invited to read. The
modules above are the public face of how the organization is governed.

## How to work with us

- **Get in touch** — [mateusz.glowacki@protonmail.com](mailto:mateusz.glowacki@protonmail.com).
- **Contribute** — see [`CONTRIBUTING.md`](CONTRIBUTING.md) for the public
  repositories.
- **Report a vulnerability** — see [`SECURITY.md`](SECURITY.md); do not open
  a public issue.
