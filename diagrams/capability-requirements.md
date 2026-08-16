# Increasing Horizon and Reliability Requirements

```mermaid
flowchart LR
    H1["Short, reversible task<br/>few dependencies"] --> R1["Basic requirements<br/>bounded tools · result checks"]
    H2["Multi-step task<br/>persistent intermediate state"] --> R2["Additional requirements<br/>run identity · checkpoints · retries · provenance"]
    H3["Cross-session task<br/>changing environment"] --> R3["Additional requirements<br/>freshness · verification · invalidation · versioning"]
    H4["Consequential long horizon<br/>irreversible or delegated action"] --> R4["Additional requirements<br/>scoped authority · independent oversight · compensation · goal-fidelity checks"]

    H1 --> H2 --> H3 --> H4
    R1 --> R2 --> R3 --> R4
```

The diagram expresses a working design expectation, not an empirical scaling law. Experiments should test which requirements matter at which horizons and impacts.
