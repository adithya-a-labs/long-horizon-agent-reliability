# Proposed Dependency-Aware Recovery Study

> **Status: proposed; not implemented or run.**

## Question

After a premise is contradicted, does invalidating and recomputing its actual dependants outperform retrying the failed action or rebuilding the entire plan?

## Recovery policies

1. **Retry only:** repeat the failed action under a fixed budget.
2. **Local repair:** modify the failed command or arguments but leave stored state unchanged.
3. **Full replan:** discard the current plan and begin again from the runtime's current state.
4. **Dependency-aware recovery:** mark the premise invalid, traverse dependency edges, preserve independent verified work, and recompute the affected subgraph.
5. **Oracle dependency recovery:** use benchmark ground-truth dependencies as an upper-bound diagnostic, not a deployable system.

## Experimental factors

- sparse versus dense dependency graphs;
- visible versus hidden dependencies;
- reversible versus irreversible effects;
- single versus interacting faults;
- early versus late fault detection;
- accurate versus noisy dependency extraction;
- low versus high recovery budgets.

## Dependency types

- plan decomposition: subgoal B requires result A;
- data: action argument depends on observation X;
- control: branch selection depends on belief Y;
- authority: permission depends on verified approval Z;
- procedural: skill depends on tool version V;
- goal: completion claim depends on postconditions P and Q.

## Primary outcomes

- residual false state after recovery;
- invalidation precision and recall;
- final task and state correctness;
- repeated or uncompensated side effects;
- preserved correct work;
- recomputation cost and latency;
- recovery-budget exhaustion.

## Expected boundary

H2 predicts an advantage mainly when dependencies are sparse and represented accurately. H3 predicts the advantage will shrink with dense or hidden coupling. A result showing universal superiority would be suspicious and should prompt benchmark-bias analysis.

## Negative-result value

- Low invalidation recall would show that dependency extraction, not recovery policy, is the bottleneck.
- High over-invalidation would suggest full replanning is simpler and equally efficient.
- Strong retry performance would indicate the benchmark contains mostly transient rather than epistemic faults.
- Failure after irreversible actions would identify the need for earlier authority and verification gates rather than better recovery alone.
