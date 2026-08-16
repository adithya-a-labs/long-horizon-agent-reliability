# Long-Horizon Goal Fidelity

## Technical problem

Goal fidelity is the degree to which the agent's evolving plans and actions remain responsive to the intended objective and constraints. It is not equivalent to local task progress. A long trajectory can drift through repeated decomposition, summarization, memory updates, environmental surprises, and recovery decisions.

[Towards Long-Horizon Agents](../literature/core-papers/towards-long-horizon-agents.md) identifies goal drift and compounding error as recurring long-horizon pressures. [MAST](../literature/core-papers/mast.md) shows that role and coordination failures can transform task execution. [Voyager](../literature/core-papers/voyager.md) illustrates how an automatic curriculum can generate intermediate objectives that support exploration but only approximate an overarching aim.

## Distinct forms of drift

- **Specification drift:** later summaries omit a constraint from the original request.
- **Decomposition drift:** a subgoal becomes optimized as if it were the terminal goal.
- **Evidence drift:** stale beliefs make the original goal appear satisfied or impossible.
- **Recovery drift:** repair optimizes immediate success while abandoning earlier constraints.
- **Memory drift:** accumulated lessons encode a proxy objective across sessions.
- **authority drift:** delegated components receive broader discretion than the goal requires.
- **termination drift:** the system declares success based on an incomplete proxy.

## Proposed goal representation

A runtime could maintain:

- immutable original request and provenance;
- clarified goal version with user-approved changes;
- explicit constraints and policy obligations;
- subgoal dependency graph;
- completion predicates and required evidence;
- unresolved ambiguities;
- history of goal revisions and who authorized them.

Subgoals may change; the original record should not be overwritten.

## Evaluation dimensions

- final task success;
- constraint satisfaction;
- preservation of user intent after decomposition;
- rate and severity of unauthorized goal changes;
- recovery consistency with original constraints;
- accuracy of termination claims;
- human ability to detect drift from the recorded trace.

## Alignment relevance

Goal fidelity connects operational reliability to intent alignment. A perfectly durable runtime can reliably pursue the wrong proxy. Conversely, a well-specified goal can still fail because the runtime loses state or cannot recover. Both objective integrity and execution integrity are necessary; neither is sufficient alone.

## Open questions

- How should legitimate goal refinement be distinguished from drift?
- Can goal constraints be checked locally at each action without losing global context?
- What should happen when the user changes the goal after irreversible actions?
- Can recovery policies preserve goal constraints under severe resource budgets?
- Which goal-fidelity metrics resist being satisfied by superficial model explanations?
