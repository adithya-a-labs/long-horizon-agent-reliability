# Proposed Benchmark and Measurement Design

> **Status: proposed; not implemented or run.**

## Objective

Create a controlled environment in which the external ground truth is known while the agent receives partial, stale, contradictory, or misleading observations. The benchmark should measure whether runtime mechanisms preserve correct state and recover after divergence.

## Candidate task families

### 1. File-and-build workflow

Inspect a project, change interdependent files, run checks, and package an artifact. Faults can alter files concurrently, return stale search results, or report a false successful build.

### 2. Simulated service operations

Diagnose a service, update configuration, restart components, and verify health. Faults can create delayed state propagation, partial restarts, replica disagreement, or misleading health checks.

### 3. Transactional order workflow

Validate inventory, reserve an item, charge a simulated account, arrange delivery, and notify a user. Faults can occur before or after side effects, exposing duplicate-action and compensation problems.

All environments would be local simulations with no real financial, deployment, or external-user effects.

## Fault taxonomy

| Fault | Example | Required distinction |
|---|---|---|
| Timeout before effect | Tool never commits change | Retry may be safe |
| Timeout after effect | Effect occurs but response is lost | Blind retry may duplicate effect |
| Stale observation | Read returns an earlier version | Completed read is not current truth |
| False success | Tool reports success without postcondition | Execution success differs from verified success |
| Partial side effect | Some sub-operations commit | Compensation or selective repair required |
| Contradictory observation | Two replicas return different state | Conflict must remain explicit |
| Concurrent mutation | Another actor changes a dependency | Prior verified state can become stale |
| Memory corruption | Stored premise is altered or poisoned | Provenance and invalidation required |
| Tool-version change | Schema or semantics change mid-run | Version pinning and skill invalidation required |
| Policy rejection | Action is operationally possible but prohibited | Task progress differs from policy compliance |
| Goal revision | Authorized goal changes mid-run | Old plans may need selective invalidation |

## Ground-truth graph

Each task instance should define:

- environment objects and versions;
- true precondition and effect relations;
- workflow dependencies;
- permitted actions and authority scopes;
- reversibility/compensation properties;
- goal and constraint predicates;
- observation functions and injected faults.

This graph allows state correctness and invalidation accuracy to be scored without using an LLM judge for the primary metrics.

## Primary metrics

### Task success

Whether all required goal predicates are satisfied without violating hard constraints.

### State correctness

Agreement between the runtime's authoritative state and benchmark ground truth, weighted by the action impact of each state variable. Planned or provisional beliefs are scored separately from verified claims.

### Silent divergence

A run silently diverges when the runtime continues a consequential action or declares success while at least one critical authoritative claim is false.

### Invalidation precision and recall

- **Precision:** fraction of invalidated nodes that truly depended on the changed premise.
- **Recall:** fraction of truly dependent nodes that were invalidated.

### Recovery work

Additional model calls, tool calls, recomputed nodes, wall time, and tokens after fault detection.

### Duplicate and uncompensated effects

Count repeated non-idempotent actions and side effects remaining inconsistent after recovery.

### Policy and goal fidelity

Score policy violations, unauthorized goal changes, constraint loss, and incorrect termination independently from task success.

## Experimental units and analysis

- Randomize fault location, fault type, dependency density, and timing.
- Use paired task instances across runtime variants.
- Begin with a pilot to estimate variance and select sample size; do not choose a final sample size solely from convenience.
- Report effect sizes and uncertainty intervals alongside hypothesis tests.
- Stratify results by reversible versus irreversible actions and sparse versus dense dependency graphs.
- Treat model/version changes as separate experimental blocks.

## Known validity risks

- Faults designed around the proposed runtime may favor it.
- Simulator ground truth may be much cleaner than real distributed systems.
- Synthetic goals and policies may underrepresent ambiguity.
- Tool faults may be easier to classify than model reasoning failures.
- A benchmark can incentivize mechanisms that exploit its fault distribution.

Mitigation requires withheld fault compositions, adversarial benchmark review, and later validation on recorded real-agent traces.
