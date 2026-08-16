# Execution Authority and Control

## Technical problem

An LLM can generate an action because it is likely under the current context. That generation does not establish that the action is authorized, safe, necessary, or based on current state.

[Sovereign Agentic Loops](../literature/core-papers/sovereign-agentic-loops.md) provides the strongest proposal–execution separation in the starting corpus. [SWE-agent](../literature/core-papers/swe-agent.md) shows how a constrained interface restructures the action space. Official [tool contracts](../ecosystem/tool-contracts.md) show where a model proposal can be intercepted by application code.

## Authority layers

1. **Proposal authority:** permission to suggest a plan or tool call.
2. **Read authority:** permission to inspect a particular resource or state view.
3. **Execution authority:** permission to request an external side effect.
4. **Commit authority:** permission to make a change durable or visible to others.
5. **Delegation authority:** permission to grant capabilities to another agent or tool.
6. **Memory authority:** permission to promote information into durable behavioral state.

These layers should not be implicitly bundled.

## Least-privilege control plane

A proposed control plane would evaluate:

- the current goal and subgoal;
- verified preconditions and freshness;
- requested capability and target resource;
- expected effects and reversibility;
- policy constraints and approval requirements;
- action identity and idempotency;
- postcondition-verification plan;
- compensation or escalation path.

The model can supply a justification, but the justification is evidence to inspect rather than a grant of authority.

## Alignment relevance

- **Impact control:** scoped capabilities limit the consequences of mistaken or misaligned plans.
- **Corrigibility:** a separate controller can pause or reject action without requiring the model to agree.
- **Policy compliance:** authorization can be evaluated independently from predicted task reward.
- **Deception robustness:** controls need not trust the model's self-reported motive.
- **Human oversight:** approval gates can focus attention on irreversible or high-impact transitions.

## Limitations and risks

- A controller with stale state can authorize the wrong action deterministically.
- Incomplete policies create false confidence.
- Excessive gates can cause approval fatigue.
- Capabilities can leak through tools with broader effects than their schemas reveal.
- Actions outside the mediated path break the closed-execution assumption.

## Open questions

- What authority model is expressive enough without becoming another opaque planner?
- Can permissions be granted per intent and automatically revoked after verified effects?
- How should authority change when evidence becomes stale mid-execution?
- Which actions require independent or human approval?
- How should a runtime represent irreversible actions whose effects cannot be compensated?
