# Architecture

This document describes intended architecture, not implemented behavior. Components and interfaces may change as the project develops.

## Boundary model

Tribal Edge Server is intended to run in an organization's controlled environment and mediate AI traffic between its clients and model services. It is an enforcement point for requests that pass through it; it does not automatically control other network traffic. Deployments must route covered AI traffic through the gateway and may need network egress rules to prevent bypass.

The gateway is deployed on the organization's side of its boundary; it does not administer or control another organization's network. An allowed request to a remote provider is a deliberate crossing of the organization's boundary. The gateway can govern the request before it leaves, but cannot control the remote provider's systems or data handling afterward.

## Personal proof-of-concept target

The initial personal proof of concept is intended for one Debian host with one GPU, running both the gateway and a local Ollama service. The goal is to exercise the boundary with routine AI workloads and use a local model when it is sufficient. The initial development target is an Ollama-served model of roughly 30B parameters that runs comfortably on the selected host.

The one-box/one-GPU setup and approximate model size are development targets, not product restrictions, hardware minimums, or universal compatibility promises. Model format, quantization, context size, and host resources affect whether a model runs comfortably. Select and document a model that can be validated on the actual target machine. This project does not claim that such validation has happened yet.

The policy and data-scoping concepts should not depend on this deployment topology: they may also be applicable inside a private datacenter. Datacenter use is a potential application, not a capability this scaffold currently implements or validates; deployment, scaling, availability, and operations would need to be designed and tested for that environment.

## Components

### Client

A user interface, script, or application sends requests to the gateway rather than directly to model providers.

### Gateway

The gateway is the controlled entry point. It should authenticate the caller, validate the request, load applicable policy, select a permitted route, and return a response or a clear policy error.

### Policy engine

The policy engine decides which actions are permitted. It should evaluate the request's identity, workspace, data class, requested operation, and provider destination. A task being suitable for a provider does not mean its data may be sent there.

Policy evaluation must fail closed: if the policy cannot be loaded or evaluated, the gateway must not send the request to an external provider. Caller-supplied or model-generated data labels must not silently become trusted authorization decisions.

### Local model adapter

The local adapter communicates with Ollama or another explicitly supported local model service.

### Escalation provider adapters

Adapters communicate with approved private or public providers. They must only be called after policy permits the transfer.

### Audit events

Audit events should capture routing decisions and provider outcomes while avoiding prompt and response content by default.

## Intended request flow

1. Authenticate the caller.
2. Resolve the applicable user, application, and workspace policy.
3. Determine the request's data class using configured rules or an explicitly identified caller-provided label; apply the deployment's trust rules for that label.
4. Check policy for the local destination before sending the request to a local model.
5. Evaluate any quality or escalation condition. Model-reported confidence is not authorization.
6. Before external transfer, check policy for the specific destination and data class, apply any approval requirement, and minimize the content to be sent.
7. Send only the permitted request to an enabled, approved provider.
8. Return the result and record a minimal audit event without prompt or response content by default.

## Model cascading

A local model may attempt a request before an escalation decision only when policy permits sending it to that local model. Possible quality-routing signals include task rules, tool errors, retrieval results, or a separate evaluator.

A model's self-reported confidence is not sufficient by itself to decide that an answer is correct or that data may leave the premises. Quality routing and data-boundary authorization are separate decisions.

## Deployment considerations

- Keep the initial proof of concept runnable on one Debian host with one GPU and a local Ollama service.
- Do not make a cluster, orchestration platform, or datacenter infrastructure a prerequisite for the proof of concept.
- Keep policy and data-scoping concepts independent of host count so future deployments can reuse them.
- Authenticate and authorize clients and administrators.
- Route covered AI requests through the gateway; use network controls where needed to prevent direct provider access that bypasses it.
- Keep external providers disabled unless deliberately configured and permitted by policy.
- Treat provider credentials, policy files, logs, and audit records as sensitive deployment assets.
- Review every adapter's outbound fields, retry behavior, and error handling.

## Non-goals for the initial design

- Automatic, unreviewed transfer of arbitrary prompts
- Treating an AI-generated sensitivity label as an authoritative security decision
- Logging all prompts and responses by default
- Claiming that local hosting alone guarantees privacy or compliance
- Controlling provider behavior or network activity outside the gateway's deployment boundary
