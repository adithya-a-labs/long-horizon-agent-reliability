# Proposed Workflow-Mechanism Transfer Study

> **Status: proposed; not implemented or run.**

## Question

Which reliability mechanisms documented in deterministic workflow systems transfer to stochastic LLM-driven execution, and which require epistemic adaptation?

## Mechanism ablations

Starting from a minimal agent loop, add one mechanism at a time and then selected combinations:

1. stable run/action identity;
2. append-only event history;
3. bounded retries and deadlines;
4. idempotency keys;
5. durable checkpoints;
6. recorded-decision replay;
7. version pinning;
8. compensation hooks;
9. pause/resume and human approval;
10. epistemic state and dependency invalidation.

The first nine are motivated by the [workflow-system comparison](../../ecosystem/workflow-systems.md). The tenth is the proposed adaptation.

## Critical replay comparison

After a checkpoint, compare:

- **re-sample:** call the same model again with reconstructed context;
- **recorded replay:** reuse the persisted prior model output;
- **explicit branch:** re-sample but create a new lineage and revalidate downstream state.

Recorded replay should improve control-flow reproducibility, but may reuse a decision whose preconditions have become stale. The experiment must score both trajectory similarity and current-state correctness.

## Transfer criteria

A mechanism counts as transferring usefully only if it:

- improves a preregistered reliability outcome;
- does not merely shift failures into silent semantic error;
- has an acceptable cost under matched budgets;
- remains useful across more than one task family and fault class;
- has a clearly specified interaction with stochastic model decisions.

## Primary measures

- duplicate side effects;
- reproducibility after restart;
- recovery success;
- silent divergence;
- operator diagnosis time;
- intervention success;
- cost per correctly completed task;
- performance under model-output variance.

## Interpretation constraints

An event history that improves audit but not automatic success should be reported as an observability result. Idempotency that prevents duplicates but not wrong first actions should be reported as impact containment. No individual mechanism should be called an agent-reliability solution.
