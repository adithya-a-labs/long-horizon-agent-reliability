# Epistemic-State Transition

```mermaid
stateDiagram-v2
    [*] --> Unverified
    Unverified --> Observed: source event attached
    Observed --> Verified: scoped verification passes
    Observed --> Invalidated: contradicted or provenance fails
    Verified --> Stale: freshness expires or dependency changes
    Verified --> Invalidated: verification revoked or contradiction confirmed
    Stale --> Observed: re-observe current environment
    Stale --> Invalidated: state no longer applies
    Invalidated --> [*]
```

This is a simplified projection of the [two-axis epistemic model](../concepts/epistemic-state.md). Planned and believed are record roles; unverified, verified, stale, and invalidated are statuses. An observation is evidence and does not become verified implicitly.
