# Research Questions

These questions narrow the broad reliability problem into comparisons that can be tested. They are not claims of novelty.

## RQ1. Does typed epistemic state improve recovery from state divergence?

When an agent distinguishes planned, believed, observed, verified, stale, and invalidated state, does it recover more accurately than an otherwise matched transcript-only or untyped-checkpoint agent?

**Primary outcomes:** post-recovery state correctness, silent-failure rate, task success, and recovery cost.

**Scope variables:** task horizon, state-change frequency, verifier accuracy, and proportion of consequential actions.

## RQ2. Does dependency-aware invalidation outperform retry and full replanning?

After a premise is contradicted, can the runtime identify and recompute affected downstream state while preserving correct unaffected work?

**Primary outcomes:** residual contamination, repeated side effects, tokens/tool calls, latency, and final correctness.

**Comparators:** blind retry, local command repair, full replan, and dependency-aware selective recovery.

## RQ3. When should an observation be promoted to verified state?

How should promotion policies trade off verification cost, false acceptance, false rejection, and delayed task progress?

**Candidate policies:** automatic promotion, risk-weighted promotion, independent-tool confirmation, deterministic postcondition checks, and human escalation.

**Primary outcomes:** calibration, false-authority rate, verification overhead, and downstream error severity.

## RQ4. Which deterministic-workflow mechanisms transfer to stochastic agent execution?

Do stable run identity, event histories, idempotency, bounded retry, checkpointing, version pinning, and compensation improve agent reliability individually or only in combinations?

**Primary outcomes:** reproducibility, duplicate effects, recovery success, operator diagnosability, and intervention latency.

**Key distinction:** recorded LLM outputs are replayed as events; deliberate re-sampling creates a new branch.

## RQ5. Does separating proposal from execution authority reduce harmful or unjustified actions?

Can a control plane using verified preconditions and scoped capabilities reject unsafe or unsupported actions without unacceptable loss of legitimate task completion?

**Primary outcomes:** policy violations, false blocks, unsafe side effects, completion rate, and escalation burden.

## RQ6. How does verifier correlation affect memory and recovery?

When actor and verifier share a model, context, memory, or task interpretation, how often do they jointly accept false state compared with more independent verification arrangements?

**Primary outcomes:** correlated false acceptance, silent failure, disagreement usefulness, and cost.

## RQ7. Can goal fidelity be measured independently from task success?

Can an agent reach a nominal task endpoint while violating constraints, losing user intent, or adopting an unauthorized proxy—and can trajectory-based metrics detect this?

**Primary outcomes:** task success, constraint satisfaction, unauthorized goal revision, termination accuracy, and reviewer detection.

## RQ8. How should irreversibility change recovery and oversight?

Should high-impact or non-compensable actions require stronger freshness checks, independent verification, or human authorization than reversible actions?

**Primary outcomes:** prevented irreversible error, approval burden, delay, and residual harm after failure.

## Prioritization

The initial experimental sequence should prioritize RQ1–RQ4. They test the repository's central state and workflow-transfer hypotheses. RQ5–RQ8 extend the same runtime toward authority and alignment questions after the state representation is operational.
