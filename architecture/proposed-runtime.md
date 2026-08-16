# Proposed Hybrid Agent Runtime

> **Status: architecture proposal only. No implementation or evaluation is claimed.**

## Design objective

Combine deterministic workflow control with stochastic model reasoning while preserving explicit epistemic status, scoped execution authority, and dependency-aware recovery.

## Components

### Goal registry

Stores the original request, authorized clarifications, constraints, completion predicates, subgoal graph, and revision history.

### Event ledger

Append-only history of model proposals, tool requests, authority decisions, external responses, verifier results, state transitions, and interventions. Events receive stable run-scoped IDs.

### Epistemic state store

Maintains versioned planned, believed, observed, verified, stale, and invalidated records with provenance and dependency edges.

### Planner/model policy

Produces hypotheses, plans, and structured action intents. Its output is a proposal and cannot directly modify authoritative state or the environment.

### Orchestrator

Selects the next permitted control transition, applies budgets and deadlines, schedules verification, and manages pause/resume. Deterministic decisions should be replayable from the ledger.

### Authority controller

Evaluates requested capabilities against goal, policy, verified preconditions, freshness, impact, reversibility, and approval requirements.

### Execution adapters

Perform external reads and side effects using stable action IDs, narrow credentials, idempotency/deduplication where available, timeouts, and explicit result envelopes.

### Verifier

Tests postconditions, source consistency, policy compliance, or goal predicates. It records method, evidence, scope, and uncertainty rather than returning an unqualified boolean.

### Dependency and recovery engine

Propagates staleness or invalidation, selects bounded recovery operators, preserves unaffected verified work, and records recovery branches.

### Oversight interface

Prioritizes high-impact, irreversible, uncertain, contradictory, or dependency-central decisions for human review and exposes raw evidence alongside summaries.

## Control invariants

1. Model output is a proposal, not an authoritative state mutation.
2. Every side-effecting action has a stable identity and requested authority scope.
3. Tool output enters as an observation, not automatically as verified truth.
4. Verification is scoped, timestamped, and versioned.
5. Protected actions cannot depend on stale or invalidated state.
6. Non-idempotent retry requires an effect check.
7. Re-sampling a model decision creates a new branch.
8. State invalidation traverses typed dependencies.
9. Goal and policy checks are distinct from task-success checks.
10. Safe halt and human escalation remain available recovery outcomes.

## Example step

1. Planner proposes `restart(service_b)` and cites a verified configuration update plus an observed health failure.
2. Orchestrator checks budget and selects the authority controller.
3. Controller checks whether both preconditions are fresh, confirms scope, and grants a one-action capability.
4. Executor invokes the adapter with an idempotency key.
5. Result is stored as an observation.
6. Verifier queries service version and health through an independent read.
7. The verified postcondition promotes the new service state and satisfies the plan node.
8. If verification contradicts the result, the recovery engine invalidates dependent completion claims and selects re-observation, compensation, or escalation.

## Open design tensions

- deterministic replay versus stale recorded decisions;
- complete provenance versus context and storage cost;
- strict authority gates versus task latency;
- verifier independence versus expense;
- fine dependency graphs versus hidden coupling and maintenance cost;
- human control versus approval overload;
- safe refusal versus availability and task completion.
