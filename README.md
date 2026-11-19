# Tribal Edge Server

**Offload “Mundane A.I.” locally. Govern what crosses your AI boundary.**

Tribal Edge Server (T.E.S.) is an early-stage design for a self-hosted, **general-purpose AI computing gateway**—not an edge appliance tied to one predefined corporate task. It has two complementary goals: handle routine “Mundane A.I.” with local models so external services are not used unnecessarily, and enforce an organization-defined boundary that scopes what data may go to which model or provider, and under what policy and approval conditions.

This combines practical local inference with deliberate data-governance controls. Whether a local model can handle a task and whether its data may be sent to a remote provider are separate decisions. The project is intended to support compliance, safety, security, and privacy programs; it does not certify or guarantee any of those outcomes.

> **Local by default. Escalate deliberately. Keep the boundary yours.**

## Project status

This repository is a **design scaffold, not a working server**. It contains no runnable gateway, provider adapters, policy engine, or test suite. Configuration files illustrate design intent and are not executable configuration. Do not use this project to protect production or sensitive workloads.

The first implementation's language and API have not yet been selected. The personal proof-of-concept target is a single-host Debian service; that target is a starting point, not a limit on where the design could be applied. See the [roadmap](ROADMAP.md) for the remaining decisions and work.

## Personal proof-of-concept target

The initial personal-use target is a **single Debian box with one video card (GPU)** running the gateway alongside a local Ollama service. It is intended to prove out handling routine, "mundane AI" workloads locally where a local model is sufficient, while keeping provider escalation subject to explicit policy. The initial local test target is an Ollama-served model around 30B parameters that runs comfortably on that machine.

The one-box/one-GPU setup and model size are practical proof-of-concept targets, not product restrictions, minimum hardware specifications, or a promise that every 30B model will fit. They are also not claims that testing has already been completed. Model format, quantization, context size, and host resources matter; choose a model that runs reliably on the actual test machine.

The design's data-scoping and provider-policy concepts are intended to be useful beyond a personal host, including within a private datacenter. Larger deployments would need their own implementation, deployment, scaling, and operational work; this repository does not yet provide or validate those capabilities.

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
