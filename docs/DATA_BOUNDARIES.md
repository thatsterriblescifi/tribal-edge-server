# Data Boundaries

This document describes the intended approach to controlling what information may be sent to each model provider. It is design guidance, not an implemented control or legal advice.

Tribal Edge Server is intended to be an organization's AI traffic boundary. It can enforce policy only for requests that are routed through it; deployment-level network controls may be required to prevent bypass.

## Two separate questions

For every request, the system should distinguish:

1. **Can this provider perform the task?**
2. **May this data be sent to this provider?**

A provider being capable of answering a request does not mean policy allows the data transfer.

## Example data classes

The following classes are examples for discussion. A deployment must define classifications appropriate to its organization and obligations.

- **Public:** Information approved for public release.
- **Internal:** Non-public information intended for members of the organization.
- **Confidential:** Sensitive business, research, or personal information.
- **Restricted:** Information that must only be processed through explicitly approved workflows.

## Example policy

| Data class | Local model | Private on-premises provider | Public provider |
|---|---:|---:|---:|
| Public | Allow | Allow | Optional |
| Internal | Allow | Allow | Deny by default |
| Confidential | Allow | Approval required | Deny |
| Restricted | Approval required | Deny | Deny |

This is an example only. It does not establish compliance or replace an organization's own policy and review.

## Recommended safeguards

- Deny external escalation by default.
- Maintain an explicit provider allowlist.
- Require approval when policy says so.
- Show the destination provider and content to be sent before approval.
- Minimize the content sent to the provider.
- Do not assume redaction is complete or reliable.
- Do not allow retries or fallback logic to bypass policy.
- Record decisions without storing full content by default.
- Provide a local-only mode that cannot call external providers.
- Ensure covered clients cannot bypass the gateway to reach model providers directly.

## Important limitation

If any request content is sent to an external provider, that content has crossed the organization's network boundary. The gateway cannot control the provider's systems or handling afterward. Provider terms, retention, training settings, and account configuration are separate considerations and must be reviewed by the operator.
