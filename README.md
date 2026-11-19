# Tribal Edge Server

**An organization-controlled boundary for AI traffic.**

Tribal Edge Server is an early-stage design for a self-hosted gateway that mediates AI requests between an organization's clients, local models, and explicitly permitted remote model services.

Its purpose is to make the organization's AI data boundary enforceable: control what may cross it, where that data may go, and under what policy and approval conditions. The project is intended to support compliance, safety, security, and privacy programs; it does not certify or guarantee any of those outcomes.

> **Local by default. Escalate deliberately. Keep the boundary yours.**

## Project status

This repository is a **design scaffold, not a working server**. It contains no runnable gateway, provider adapters, policy engine, or test suite. Configuration files illustrate design intent and are not executable configuration. Do not use this project to protect production or sensitive workloads.

The first implementation's language, API, and deployment model have not yet been selected. See the [roadmap](ROADMAP.md) for proposed decisions and work.

## Intended boundary

```text
Organization-controlled environment
  Clients --> Tribal Edge Server --> Local model
                       |
                       +--> Explicitly permitted remote model service
```

The gateway is intended to be an enforcement point, not merely a router. That boundary only governs traffic that is actually routed through it. A deployment must prevent covered AI traffic from bypassing the gateway; network egress controls may be needed to enforce that. The gateway cannot control a provider's systems or handling of data after a request is permitted to leave the organization's environment.

## Design principles

- **Local by default:** external providers are off unless explicitly enabled.
- **Policy before transfer:** provider capability does not imply permission to send data.
- **Fail closed:** policy errors or missing configuration must not authorize external transfer.
- **Explicit destinations and approvals:** only configured providers and permitted data classes may be used.
- **Minimal audit data:** record routing decisions without recording prompts or responses by default.
- **No compliance claims:** controls may support an organization's program, but do not establish compliance by themselves.

## Documentation

- [Architecture](docs/ARCHITECTURE.md)
- [Data boundaries](docs/DATA_BOUNDARIES.md)
- [Compliance considerations](docs/COMPLIANCE.md)
- [Threat model](docs/THREAT_MODEL.md)
- [Roadmap](ROADMAP.md)
- [Contributing](CONTRIBUTING.md)
- [Code of conduct](CODE_OF_CONDUCT.md)
- [Security policy](SECURITY.md)

## Scope and limitations

Tribal Edge Server is intended to mediate AI requests and enforce operator-defined data-routing policy. It does not determine which laws or contracts apply, certify a deployment, guarantee that a model is safe or correct, or guarantee privacy merely because a model or gateway is hosted locally. Operators remain responsible for their network controls, configuration, identity systems, provider agreements, retention practices, and review of applicable requirements.

This repository is currently for design discussion. There are no installation or run instructions because there is no implementation yet. Do not put real credentials, personal information, confidential prompts, or proprietary data in issues, pull requests, or example files.
