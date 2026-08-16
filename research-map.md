# Research Map

## Central question

> How can a long-horizon LLM agent maintain trustworthy execution state and recover when its internal representation of a workflow diverges from the external environment?

The starting literature reaches this question through several partially overlapping lines of work.

## 1. Reasoning and acting

[ReAct](literature/core-papers/react.md) makes the action–observation loop explicit. It demonstrates that an agent can alternate model reasoning with environment interaction, but represents the trajectory primarily as context rather than typed persistent state.

**Open transition:** from a textual trajectory to a state model that distinguishes model inference from external observation.

## 2. Tool use and constrained interfaces

[Toolformer](https://arxiv.org/abs/2302.04761) studies learning when to invoke simple tools. [SWE-agent](literature/core-papers/swe-agent.md) shows that the Agent–Computer Interface changes the model's effective task and failure surface. Official [function-calling and structured-output semantics](ecosystem/tool-contracts.md) provide structural contracts.

**Open transition:** from parseable action proposals to justified, authorized, and verifiable actions.

## 3. Planning and workflow generation

[Tree of Thoughts](https://arxiv.org/abs/2305.10601) searches over candidate reasoning states. [WorkflowLLM](literature/core-papers/workflowllm.md) generates structured workflows and dependencies from requests.

**Open transition:** from a plausible plan graph to a live execution graph whose assumptions can become stale or false.

## 4. Feedback, reflection, and procedural memory

[Reflexion](literature/core-papers/reflexion.md) stores language-level lessons from feedback. [Voyager](literature/core-papers/voyager.md) stores executable, compositional skills and repairs them through environment feedback.

**Open transition:** from successful past behavior to memory with provenance, preconditions, authority scope, freshness, and revocation.

## 5. Persistent memory and integrity

The [long-term-memory security survey](literature/core-papers/long-term-memory-security.md) maps risks across write, store, retrieve, execute, share, and forget/rollback. The broader [memory survey](https://arxiv.org/abs/2603.07670) frames memory through write–manage–read mechanisms.

**Open transition:** from secure storage and retrieval to epistemically typed state: planned, believed, observed, verified, stale, and invalidated.

## 6. Failure diagnosis and recovery

[MAST](literature/core-papers/mast.md) identifies recurring design, coordination, and verification failures in multi-agent traces. [Self-Healing Agentic Orchestrators](literature/core-papers/self-healing-orchestrators.md) provides controlled evidence for failure-aware, bounded local recovery.

**Open transition:** from failure classification to dependency-aware invalidation and selective recomputation.

## 7. Controlled execution

[Sovereign Agentic Loops](literature/core-papers/sovereign-agentic-loops.md) separates stochastic intent generation from a deterministic policy and execution control plane.

**Open transition:** from a controller assumed to know true system state to a controller that explicitly represents partial, stale, conflicting, and verified evidence.

## 8. Durable workflow systems

[Temporal, Airflow, Trigger.dev, and LangGraph](ecosystem/workflow-systems.md) contribute stable identities, event histories, retries, checkpoints, versioning, pause/resume, and observability.

**Open transition:** adapt durable execution to model calls that are stochastic and to state whose semantic correctness is uncertain.

## Resulting research program

The synthesis produces four coupled objects of study:

1. **Epistemic execution state:** what the system plans, believes, observes, verifies, marks stale, and invalidates.
2. **Dependency-aware recovery:** how a state change propagates to plans, actions, memories, and skills.
3. **Execution authority:** what the model may propose versus what a control plane may authorize.
4. **Multi-objective evaluation:** task success, state correctness, policy compliance, recovery cost, and long-horizon goal fidelity.

These are research directions derived from the starting corpus. The repository has not yet demonstrated a new architecture or empirical result.
