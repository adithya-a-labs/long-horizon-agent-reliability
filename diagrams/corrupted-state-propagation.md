# Corrupted-State Propagation and Recovery

```mermaid
flowchart LR
    O["O1: stale tool observation"] -->|"derived_from"| B["B1: false belief"]
    B -->|"planned_from"| P1["P1: select repair plan"]
    B -->|"parameterized_by"| A1["A1: wrong tool argument"]
    P1 --> A1
    A1 -->|"executed"| E1["E1: external side effect"]
    E1 -->|"summarized as"| C1["C1: false completion claim"]
    B -->|"stored as lesson"| M1["M1: contaminated memory"]

    X["Contradictory verified observation"] -.->|"invalidates"| O
    X -.->|"dependency traversal"| B
    X -.->|"invalidate and recompute"| P1
    X -.->|"block retry / inspect effect"| A1
    X -.->|"verify or compensate"| E1
    X -.->|"retract"| C1
    X -.->|"quarantine"| M1
```

A command-local retry addresses A1 but leaves B1, P1, C1, and M1 contaminated. Dependency-aware recovery attempts to identify the affected subgraph and the already-realized external effects.
