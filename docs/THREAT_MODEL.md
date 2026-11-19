# Threat Model

This is an initial discussion document, not a completed security review or an assurance that any deployment is secure.

## Assets to protect

- Prompts and uploaded documents
- Provider credentials
- User and application identities
- Routing and data-boundary policies
- Audit records
- Local model and service availability

## Trust boundaries

1. Client applications to the gateway
2. Gateway to the local model service
3. Gateway to private providers
4. Gateway to public providers
5. Administrator configuration to running service
6. Service logs and audit storage
7. Organization-controlled network to remote provider networks

The gateway can enforce controls only for requests that pass through it. Preventing clients from reaching providers directly may require network egress controls outside the gateway.

## Threats to consider

- A request is sent to an unapproved external provider.
- A fallback or retry path bypasses policy.
- A caller impersonates another user or application.
- Provider credentials are exposed in logs or configuration.
- An administrator accidentally enables an unsafe route.
- Prompt content is retained unexpectedly.
- A tool, plugin, or adapter sends data outside the gateway.
- A model-generated classification incorrectly labels sensitive content as safe.
- A provider outage causes unintended routing or data disclosure.
- A compromised host exposes locally stored data or credentials.
- A client bypasses the gateway and sends data directly to a model provider.
- A permitted request exposes more content than necessary, or the provider retains or handles it in an unexpected way.

## Intended mitigations

These are design goals, not implemented or independently verified controls.

- External providers disabled by default.
- Explicit provider allowlists.
- Policy evaluation fails closed.
- Authentication for clients and administrators.
- Secrets supplied outside committed configuration.
- Content logging disabled by default.
- Tests for denied requests, retries, and provider failures.
- Local-only mode.
- Clear documentation of data sent by each adapter.
- Deployment guidance for routing covered traffic through the gateway and restricting bypass paths.

## Out of scope for this initial document

- Formal compliance assessment
- Certification or guarantee of an organization's compliance, privacy, safety, or security
- Independent penetration testing
- Security guarantees provided by external model providers
- Protection against a fully compromised host or administrator account
