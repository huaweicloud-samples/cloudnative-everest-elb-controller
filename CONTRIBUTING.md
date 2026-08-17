# Contributing to cloudnative-everest-elb-controller

First off, thank you for considering contributing to this project! This document outlines the process for submitting improvements.

## Code of Conduct

Participation in this project is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to huaweicloud-samples@huaweicloud.com.

## How to Contribute

### 1. Fork the Repository

Fork the repository to your own GitHub account and clone it locally:

```bash
git clone https://github.com/<your-username>/cloudnative-everest-elb-controller.git
cd cloudnative-everest-elb-controller
```

### 2. Create a Branch

Create a new branch for your work. Use a descriptive name:

```bash
git checkout -b fix/descriptive-name
# or
git checkout -b feat/descriptive-name
```

### 3. Make Your Changes

- Follow the existing code style and conventions (Go standard formatting via `gofmt`).
- Add or update tests as appropriate.
- Update documentation if your change affects user-facing behavior.
- Ensure all tests pass: `make test`

### 4. DCO Sign-Off

All commits must include a DCO (Developer Certificate of Origin) sign-off. This certifies that you wrote or have the right to submit the code under the project's license.

Sign off your commits by adding the `-s` flag:

```bash
git commit -s -m "fix: descriptive commit message"
```

This produces a commit message like:

```
fix: descriptive commit message

Signed-off-by: Your Name <your.email@example.com>
```

> **DCO Full Text**: See https://developercertificate.org/ for the complete DCO text. By submitting a pull request, you agree to the terms of the DCO.

### 5. Push and Open a Pull Request

Push your branch to your fork and open a Pull Request against the `main` branch of this repository:

```bash
git push origin your-branch-name
```

When opening a PR:

- Link the related Issue (if applicable).
- Fill in the Pull Request template, including the DCO confirmation checkbox.
- Ensure all CI checks pass.

### 6. Code Review

- Maintainers will respond within **5 business days**.
- Feedback may be requested; please address comments by pushing additional commits.
- Merging requires **at least one maintainer approval**.
- Do not force-push after opening a PR (it resets review history).

## Commit Message Guidelines

Use conventional commit prefixes:

| Prefix | Usage |
|---|---|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation only |
| `refactor:` | Code restructuring without behavior change |
| `chore:` | Build, CI, tooling |
| `test:` | Adding or modifying tests |

Example: `fix: webhook fails to inject loadBalancerClass on Service UPDATE`

## Code Standards

- **Language**: Go (module version defined in `go.mod`)
- **Formatting**: `gofmt` / `goimports`
- **Testing**: New code must include unit tests in `_test.go` files
- **Error Handling**: No `panic` in production code; return errors properly
- **No Secrets**: Never commit AK/SK, credentials, or tokens. All secrets must be read from environment variables or Kubernetes Secrets.

## Issue and PR Templates

- Use the [Bug Report](.github/ISSUE_TEMPLATE/bug_report.md) template for bug reports.
- Use the [Feature Request](.github/ISSUE_TEMPLATE/feature_request.md) template for feature proposals.
- Follow the [Pull Request](.github/PULL_REQUEST_TEMPLATE.md) template when submitting PRs.

## License

By contributing, you agree that your contributions will be licensed under the [MIT-0 License](LICENSE).
