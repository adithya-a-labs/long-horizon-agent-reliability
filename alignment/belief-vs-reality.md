# Belief Versus Reality

## Technical problem

An agent acts on an internal representation assembled from prompts, memories, tool outputs, model inferences, and summaries. The external environment is only partially observed and may change between observation and action. The internal representation can therefore be coherent and still disagree with reality.

[ReAct](../literature/core-papers/react.md) demonstrates the value of grounding reasoning in returned observations. [Towards Long-Horizon Agents](../literature/core-papers/towards-long-horizon-agents.md) formalizes the environment as partially observable and the harness context as a lossy construction. Neither implies that every returned observation is current, complete, or trustworthy.

## Failure pathways

1. **Inference becomes fact:** a model-generated summary is stored without retaining its provisional status.
2. **Observation becomes stale:** external state changes after a correct read.
3. **Identity mismatch:** a valid identifier refers to the wrong real-world object.
4. **Partial observation:** the tool returns one view of a distributed or eventually consistent system.
5. **Contradictory evidence:** different tools, sessions, or actors report incompatible state.
6. **Semantic tool failure:** a call returns syntactically valid, plausible data that is wrong.

## Alignment relevance

Belief–reality divergence matters when beliefs authorize action. A model that incorrectly believes a resource is disposable, a user approved an operation, or a goal condition has been reached can take locally rational but globally harmful actions.

This is related to alignment through:

- **situational accuracy:** action selection should depend on justified beliefs about the current situation;
- **corrigibility:** contrary evidence must be able to revise or invalidate internal state;
- **oversight:** reviewers need source evidence, not only the agent's compressed account;
- **safe uncertainty:** insufficient evidence should sometimes produce refusal, re-observation, or escalation rather than confident action.

## Proposed control points

- distinguish inferred, observed, and verified claims;
- record source, timestamp, scope, and verification method;
- attach freshness requirements to action preconditions;
- require re-observation for high-impact actions;
- preserve contradictions rather than prematurely merging them;
- invalidate dependent plans when a premise fails.

These controls are hypotheses. Their costs and effectiveness need experimental evaluation.

## Open questions

- What qualifies as verification in a partially observable environment?
- How should confidence and freshness interact?
- Can an agent recognize that it lacks the evidence needed to act?
- When should human testimony, tool output, and deterministic checks receive different authority?
- How can a system prevent a fluent summary from hiding unresolved contradictory evidence?
