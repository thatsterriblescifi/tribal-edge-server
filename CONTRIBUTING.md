# Contributing

Thanks for your interest in Tribal Edge Server. The project is currently a design scaffold with no runnable server yet; discussion and documentation contributions are especially useful.

## Before contributing

- Open an issue for significant changes so the design can be discussed first.
- Check the [roadmap](ROADMAP.md) and existing issues for related work.
- Keep contributions focused and explain the problem they solve.
- Do not include real credentials, personal data, confidential prompts, or proprietary datasets in issues, tests, logs, or example files.

## Core security principle

**No provider should receive a request unless policy explicitly permits it.**

Changes to routing, retries, fallback behavior, tools, provider adapters, logging, or configuration should include tests showing that denied requests cannot reach a provider. The gateway can enforce this only for traffic that the deployment actually routes through it; document any required network egress controls.

If policy evaluation fails, the expected behavior is to fail closed: do not send the request to an external provider.

## Pull requests

A pull request should:

1. Describe the problem and the proposed change.
2. Include tests for changed behavior where practical.
3. Update documentation and configuration examples as needed.
4. Identify any new data sent to a provider or written to logs.
5. Avoid adding dependencies without explaining their purpose.

## Provider integrations

Provider adapters should document:

- What data is sent
- How credentials are supplied
- Supported request and response features
- Timeout and retry behavior
- Any provider-specific limitations

Provider adapters must not silently bypass policy enforcement.

## Reporting security issues

Do not report suspected vulnerabilities in a public issue. Follow [SECURITY.md](SECURITY.md).
