# Security Policy

Tribal Edge Server is an early-stage project. Do not assume it is suitable for sensitive or production workloads until its implementation, deployment, and security controls have been independently reviewed.

## Reporting a vulnerability

Please do not report suspected vulnerabilities in a public issue.

Contact the maintainers privately using the security contact listed in the repository’s GitHub security settings. Maintainers should configure private vulnerability reporting before making the repository public. Include:

- A description of the issue
- Affected version or commit, if known
- Steps to reproduce in a test environment
- Potential impact
- Any suggested mitigation

Do not include real secrets, personal information, or confidential data in the report.

## Security priorities

The project prioritizes:

- Preventing unauthorized external data egress
- Secure handling of provider credentials
- Authentication and authorization for callers and administrators
- Safe defaults for routing, retries, and fallbacks
- Minimal and configurable logging
- Clear documentation of provider-specific data flows

## Scope and limitations

This project cannot guarantee that an AI model is correct, that a provider will handle data in a particular way, or that a deployment is secure merely because it runs locally. Operators are responsible for reviewing their configuration, network, providers, and applicable policies.

The gateway is intended to enforce policy for traffic routed through it. It cannot protect requests that bypass it or control a remote provider after an allowed request leaves the organization's environment. See [the architecture](docs/ARCHITECTURE.md) and [compliance considerations](docs/COMPLIANCE.md).
