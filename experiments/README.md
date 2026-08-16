# Proposed Experiments

> **Status: design only. No experiment in this repository has been run.**

The experimental program begins with deterministic, inspectable fault injection and adds model-in-the-loop execution only after the state and recovery mechanisms can be tested independently.

## Proposed sequence

1. [Benchmark and measurement design](proposed/benchmark-design.md)
2. [Epistemic-state representation ablation](proposed/epistemic-state-ablation.md)
3. [Dependency-aware recovery comparison](proposed/dependency-aware-recovery.md)
4. [Workflow-mechanism transfer study](proposed/workflow-transfer-study.md)
5. [Proposal–execution authority study](proposed/authority-separation.md)

## General comparison policy

- Use the same task instances, model version, prompts, tool schemas, and action budgets across runtime variants.
- Persist seeds, tool responses, model outputs, and verifier decisions.
- Separate deterministic-controller results from model-in-the-loop results.
- Report false blocks and verification cost alongside prevented failures.
- Retain complete failed traces and classify post hoc analyses as exploratory.
- Do not claim general long-horizon reliability from one simulated domain.

## Candidate implementation phases

- **Phase A — deterministic controller:** scripted action proposals isolate state and recovery semantics.
- **Phase B — recorded model traces:** replay fixed model decisions through different runtimes.
- **Phase C — live model:** permit stochastic proposals while recording each decision as an event.
- **Phase D — human oversight pilot:** test whether the state representation actually improves diagnosis and intervention.

Each phase can falsify part of the working position without requiring the later phases to succeed.
