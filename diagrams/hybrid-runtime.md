# Hybrid Deterministic–Stochastic Runtime

```mermaid
flowchart TB
    subgraph D["Deterministic control plane"]
        OR["Orchestrator<br/>identity · budgets · deadlines"]
        EL["Append-only event ledger"]
        ES["Epistemic state store"]
        AC["Authority and policy controller"]
        DE["Dependency / recovery engine"]
    end

    subgraph S["Stochastic proposal plane"]
        LM["Language model"]
        PL["Plan / hypothesis / action intent"]
        RV["Optional model-based reviewer"]
    end

    subgraph X["External side-effect plane"]
        AD["Scoped execution adapter"]
        ENV["Environment"]
        DV["Deterministic or independent verifier"]
    end

    ES --> LM
    LM --> PL
    PL --> EL
    EL --> OR
    OR --> AC
    AC -->|"authorized"| AD
    AC -->|"insufficient evidence"| DE
    AD --> ENV
    ENV --> DV
    DV --> EL
    DV --> ES
    RV --> EL
    ES --> DE
    DE --> OR
```

“Deterministic control” means that control decisions can be reconstructed from recorded events and explicit rules. It does not assume that external systems, validators, or model outputs are always correct.
