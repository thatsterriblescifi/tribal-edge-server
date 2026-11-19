# Compliance considerations

Tribal Edge Server is intended to provide an organization-controlled boundary for AI traffic. Its policy enforcement, provider controls, and minimal audit metadata are intended to support an organization's compliance, safety, security, and privacy programs.

The project does not certify, guarantee, or independently establish compliance with any law, regulation, or contractual obligation. Compliance depends on the organization's applicable requirements and the complete operational environment—not on the gateway alone.

## Responsibility and limitations

Operators are responsible for:

- Determining which legal, regulatory, contractual, and internal requirements apply.
- Defining data classes, provider approvals, identity rules, and escalation policies.
- Configuring the gateway and supporting network controls so covered traffic cannot bypass the policy boundary.
- Reviewing provider terms, data handling, retention, training settings, and credentials.
- Securing and operating the gateway, local models, configuration, logs, and audit records.
- Assessing whether the controls and evidence are appropriate for their own compliance program.

The gateway can enforce policy only for requests that pass through it. It cannot control a provider's systems or handling after an allowed request crosses the organization's network boundary. Running a model or gateway locally does not, by itself, guarantee privacy, security, safety, or compliance.

## Design intent

The project intends to support controls such as:

- Explicit allow/deny decisions by data class and provider.
- External transfer disabled unless deliberately enabled.
- Fail-closed handling when policy cannot be evaluated.
- Approval requirements for selected transfers.
- Minimal routing and provider outcome records without prompt or response content by default.
- Tests and deployment guidance for preventing policy bypass.

These are intended design properties, not claims about implemented or independently verified controls. See the [architecture](ARCHITECTURE.md), [data boundaries](DATA_BOUNDARIES.md), and [threat model](THREAT_MODEL.md).
