# Dependency-Aware Recovery

> **Status: proposed mechanism; not implemented or validated.**

## Problem

A failed command is often only the visible symptom. If its arguments came from a stale belief, retrying the command repeats the same error. If a contradicted belief informed several later actions, repairing one action leaves the rest of the trajectory contaminated.

## Recovery sequence

1. **Detect:** receive an operational error, contradictory observation, failed verification, policy rejection, or freshness event.
2. **Classify:** distinguish transient execution failure from epistemic, policy, goal, or verifier failure.
3. **Locate root state:** identify the earliest unsupported or changed premise currently supported by evidence.
4. **Traverse dependants:** collect beliefs, plans, arguments, actions, skills, and completion claims that rely on the premise.
5. **Assess effects:** determine which dependent actions were proposed, executed, verified, reversible, or irreversible.
6. **Invalidate selectively:** remove authority from affected state while preserving independent verified work.
7. **Choose operator:** retry, re-observe, re-verify, locally replan, compensate, request approval, or fully replan.
8. **Verify recovery:** check both the immediate repair and removal of downstream contamination.
9. **Record branch:** preserve the failed trajectory and link the recovered branch to it.

## Recovery operators

| Operator | Appropriate when | Unsafe when |
|---|---|---|
| Retry | Failure is transient and action is idempotent or deduplicated | Premise or arguments are wrong; effect may already have occurred |
| Re-observe | State may be stale or partial | Observation source repeats the same hidden fault |
| Re-verify | Evidence exists but prior verification was insufficient | Actor and verifier share the same error source |
| Local replan | A bounded subgraph is affected | Hidden coupling makes the local boundary false |
| Compensate | Completed effect has a defined mitigating action | Compensation is lossy or creates new risk |
| Human escalation | Ambiguity or impact exceeds automatic authority | Reviewer lacks raw evidence or faces approval fatigue |
| Full replan | Dependencies are dense, state is broadly contaminated, or goal changed | Re-executes irreversible work or discards valuable verified progress |

## Recovery invariants

- No retry of a non-idempotent action without checking whether the original effect occurred.
- No protected action may depend on stale or invalidated state.
- Invalidated evidence remains auditable and is never silently overwritten.
- Resampling a model decision creates a new branch.
- Recovery success requires postcondition verification, not absence of an exception.
- Irreversible effects are recorded even if the surrounding plan is later invalidated.

## Relationship to existing evidence

[Self-Healing Agentic Orchestrators](../literature/core-papers/self-healing-orchestrators.md) supports bounded, failure-aware local recovery in controlled settings. [MAST](../literature/core-papers/mast.md) documents compounded trace failures. Deterministic workflow systems provide dependency, retry, and compensation patterns. None directly validates the proposed epistemic dependency mechanism.
