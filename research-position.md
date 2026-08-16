# Working Research Position

## Status of this document

This document records **provisional hypotheses informed by the current literature and system audit**. It is not a statement of established findings. The positions are intended to become more precise, falsifiable, and revisable as experiments are designed and run.

The starting Notion corpus is broad enough to motivate these positions but not sufficient to establish novelty or exhaust the field.

## P1. Long-horizon reliability is a coupled model–systems problem

**Working position:** Agent reliability depends on the base model and on the harness that controls context, tools, state, verification, and recovery.

**Basis:** [SWE-agent](literature/core-papers/swe-agent.md) shows that interface design affects task performance; [MAST](literature/core-papers/mast.md) identifies system-design and verification failures; [Towards Long-Horizon Agents](literature/core-papers/towards-long-horizon-agents.md) formalizes a model–harness coupling.

**Boundary:** This does not imply that model capability is unimportant or that every failure can be repaired externally.

**Falsifier:** If harness interventions fail to improve reliability after controlling for model, task, and budget—or if improvements vanish outside one implementation—the broad position should be narrowed.

## P2. Execution memory should be treated as an evolving epistemic state

**Working position:** Conversation history is an inadequate abstraction for persistent execution. A runtime should represent planned, believed, observed, verified, stale, and invalidated state separately.

**Basis:** ReAct trajectories mix reasoning and observation; Reflexion stores interpreted lessons; memory surveys identify lifecycle and staleness problems; workflow systems persist execution status without native epistemic status.

**Boundary:** The proposed categories have not yet been shown to improve task outcomes or human oversight.

**Falsifier:** If a simpler untyped state representation matches reliability, recovery accuracy, and auditability at lower cost, the extra state machine is unnecessary.

## P3. Writing information and granting it authority should be separate operations

**Working position:** A model, tool, or human may contribute an observation without that observation automatically becoming an authoritative premise for consequential action.

**Basis:** Reflexion can store incorrect diagnoses; Voyager makes retrieved procedural memory executable; the memory-security survey separates lifecycle phases; structured outputs establish shape, not truth.

**Boundary:** Separating write and promotion creates latency and governance complexity and may be unnecessary for low-stakes reversible tasks.

**Falsifier:** If automatic promotion is equally safe and substantially more efficient under realistic corrupted/stale-memory tests, promotion gates should be scoped rather than universal.

## P4. Model-generated state is not verified external state

**Working position:** Plans, summaries, inferred tool results, and self-reflections should remain provisional until supported by an appropriate observation or verification procedure.

**Basis:** ReAct grounds reasoning through observations; WorkflowLLM does not execute generated workflows; SAL validates intents against system state; official tool schemas do not guarantee semantic correctness.

**Boundary:** Verification is itself fallible, and some facts cannot be checked deterministically.

**Falsifier:** The strongest version is false if reliable calibration or trusted generation makes explicit verification redundant in a well-defined task class.

## P5. Recovery should operate over dependencies, not only failed commands

**Working position:** When a state claim is contradicted or invalidated, recovery should identify and reconsider the plans, arguments, actions, and memories that depended on it.

**Basis:** MAST shows compounded trace failures; Self-Healing Orchestrators supports bounded local recovery in controlled faults; workflow DAGs demonstrate explicit dependency propagation.

**Boundary:** Dependency tracking adds overhead and may over-invalidate useful work. The reviewed evidence does not directly validate epistemic dependency graphs.

**Falsifier:** If command-local retry or full replanning consistently dominates dependency-aware recovery on success, cost, and safety, the proposed mechanism is not justified.

## P6. More autonomy requires more observability and controllability

**Working position:** Longer horizons and more consequential actions require stable run identity, inspectable state transitions, authority gates, budgets, pause/resume, and intervention points.

**Basis:** Workflow runtimes operationalize these mechanisms; SAL separates proposal and execution; MAST shows that final-answer evaluation misses trajectory failures.

**Boundary:** More logs are not automatically better oversight. Excessive detail can obscure decisive evidence or create privacy and security risks.

**Falsifier:** If additional observability does not improve detection or intervention—or predictably worsens reviewer performance—the representation must be redesigned.

## P7. Reliability evaluation is multi-objective

**Working position:** Task success, execution completion, state correctness, policy compliance, recovery cost, and goal fidelity should be evaluated separately.

**Basis:** WorkflowLLM separates generation quality from execution; MAST identifies verification failures; Reflexion depends on evaluator choice; SAL evaluates policy blocking and replay as distinct properties.

**Boundary:** The objectives may correlate strongly in some domains, and measuring them independently can be expensive.

**Falsifier:** If one validated metric predicts the other objectives across tasks and failure types, a simpler evaluation may suffice.

## Current synthesis

My present view is that a promising long-horizon runtime would combine deterministic control with stochastic reasoning:

- the model proposes plans, hypotheses, and action intents;
- the runtime persists events and typed epistemic state;
- a policy layer grants scoped authority;
- executors return observations rather than implicit truth;
- verifiers promote, reject, or qualify state;
- dependency tracking determines what becomes stale or invalid;
- recovery retries, repairs, replans, compensates, or escalates under explicit budgets.

This is a research agenda, not a completed architecture. Its value depends on whether controlled experiments show improvements that justify its complexity.
