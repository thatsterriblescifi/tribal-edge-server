# Roadmap

This roadmap describes proposed work. A checked box means the work has been completed and reviewed; unchecked items are not implemented promises. The repository currently contains a design scaffold, not a runnable server.

## 1. Define the project

- [ ] Agree on the initial use cases and non-goals
- [ ] Define supported deployment modes
- [ ] Define the policy terminology: user, application, workspace, data class, provider
- [ ] Review and improve the threat model
- [ ] Decide on the initial implementation language and framework
- [ ] Define the personal proof of concept as a single-host Debian service with one GPU and a local Ollama adapter
- [ ] Select and record a practical Ollama model around 30B parameters that runs comfortably on the proof-of-concept host
- [ ] Keep policy and data-scoping concepts independent of the single-host deployment topology

## 2. Establish safe defaults

- [ ] Define a local-only mode and deployment controls that block remote-provider egress
- [ ] Require explicit provider configuration
- [ ] Make external escalation deny-by-default
- [ ] Define behavior when policy evaluation fails
- [ ] Define behavior when a provider times out or is unavailable
- [ ] Decide what audit metadata is retained
- [ ] Ensure prompt and response content are not logged by default

## 3. Build a minimal gateway

- [ ] Define the client API
- [ ] Implement authentication for callers
- [ ] Implement the Ollama adapter
- [ ] Add health and readiness endpoints
- [ ] Add request size and timeout limits
- [ ] Add tests for malformed and oversized requests

## 4. Add policy-controlled routing

- [ ] Define a versioned policy configuration format
- [ ] Implement local-first routing
- [ ] Implement provider allowlists
- [ ] Implement data-class restrictions
- [ ] Implement optional user approval for escalation
- [ ] Return a clear reason when a request is blocked
- [ ] Test that policy errors fail closed

## 5. Add providers and checks

- [ ] Implement a private OpenAI-compatible endpoint adapter
- [ ] Evaluate public-provider adapters individually
- [ ] Keep provider credentials outside committed configuration
- [ ] Define supported request and response features per adapter
- [ ] Add optional local answer-checking or evaluation hooks
- [ ] Do not treat model-reported confidence as sufficient evidence

## 6. Verify the boundary

- [ ] Create tests that detect unintended external requests
- [ ] Test retries, fallback behavior, tools, and error paths
- [ ] Add a local-only integration test
- [ ] Document what request fields each provider adapter sends
- [ ] Document limits of redaction and data minimization
- [ ] Add an operator-visible escalation event
- [ ] Document deployment controls needed to prevent clients bypassing the gateway

## 7. Deployment and operations

- [ ] Document single-host Debian proof-of-concept installation
- [ ] Document Ollama setup and model selection, including host-specific resource considerations
- [ ] Add example systemd service files
- [ ] Document TLS and reverse-proxy deployment
- [ ] Document backup and restore of policy configuration
- [ ] Document upgrades and rollback
- [ ] Provide a workload benchmarking guide
- [ ] Assess what additional deployment and operational work is needed for private-datacenter use

## 8. Compliance support

- [ ] Map intended gateway controls to operator responsibilities without claiming compliance
- [ ] Document audit-event contents, integrity, access, and retention requirements
- [ ] Document deployment evidence and verification limitations

## Not planned for the initial version

- [ ] Automatic classification that is treated as a security boundary
- [ ] Automatic external escalation without policy checks
- [ ] Claims of regulatory compliance
- [ ] Storing all prompts and responses for analytics
