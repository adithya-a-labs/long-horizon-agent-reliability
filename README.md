# Long-Horizon Agent Reliability

Independent research on trustworthy execution state, verification, memory integrity, controlled action, and recovery in long-horizon LLM agents.

## Project status

This repository is an early-stage research synthesis and proposed experimental program. It contains a provenance audit, literature analysis, system comparisons, working hypotheses, conceptual models, and experiment designs.

**No experiment described here has been run. No empirical result or claim of novelty is made.** The [Working Research Position](research-position.md) is explicitly provisional and intended to be revised or rejected as evidence develops.

## Central question

> How can long-horizon LLM agents maintain trustworthy execution state and recover reliably when their internal representation of a workflow diverges from the external environment?

Long tasks create more than a context-length problem. Plans depend on observations; observations become stale; tool calls can partially succeed; memories can preserve incorrect diagnoses; and a syntactically valid action can still be unjustified or unauthorized.

The research program therefore separates:

- **planned state:** what the agent intends or predicts;
- **believed state:** its current working hypotheses;
- **observed state:** evidence returned by tools, environments, or people;
- **verified state:** claims supported by a recorded, scoped check;
- **stale state:** formerly usable state that requires revalidation;
- **invalidated state:** contradicted, revoked, or inapplicable state that must lose authority.

See [Epistemic Execution State](concepts/epistemic-state.md) and the [state-transition diagram](diagrams/epistemic-state-transition.md).

## Working direction

The repository investigates a hybrid runtime in which:

1. a language model proposes hypotheses, plans, and action intents;
2. a deterministic orchestrator records events, budgets work, and controls transitions;
3. an authority layer checks policy, scope, freshness, and verified preconditions;
4. scoped adapters perform external actions with stable identities;
5. observations enter the state store without automatically becoming truth;
6. verifiers promote, reject, or qualify claims;
7. dependency-aware recovery invalidates affected state before retry or replanning.

This architecture is a hypothesis, not a completed system. Its value depends on whether it improves state correctness and recovery enough to justify its cost.

## What the starting evidence supports

The audited corpus provides bounded support for several observations:

- [ReAct](literature/core-papers/react.md) shows the value of coupling reasoning to environment observations, but its prompt trajectory is not a typed durable-state model.
- [Reflexion](literature/core-papers/reflexion.md) shows that stored language feedback can improve repeated attempts, while making evaluator and memory-write quality central concerns.
- [Voyager](literature/core-papers/voyager.md) demonstrates reusable executable skills in Minecraft, while exposing questions about preconditions, staleness, and procedural-memory authority.
- [SWE-agent](literature/core-papers/swe-agent.md) provides evidence that interface and harness design change agent performance and failure modes.
- [MAST](literature/core-papers/mast.md) documents recurring design, coordination, and verification failures across 1,642 multi-agent traces.
- Two recent preprints study [bounded self-healing](literature/core-papers/self-healing-orchestrators.md) and [proposal–execution separation](literature/core-papers/sovereign-agentic-loops.md) in controlled settings; their results are not production guarantees.
- [Temporal, Airflow, Trigger.dev, and LangGraph](ecosystem/workflow-systems.md) document durable histories, retries, checkpoints, pause/resume, versioning, and observability. These mechanisms need adaptation because model decisions are stochastic and durable state can still be semantically wrong.

See the complete [evidence ledger](literature/evidence-ledger.md) and [claim–evidence map](provenance/claim-evidence-map.md).

## Repository guide

| Area | Contents |
|---|---|
| [Provenance](provenance/README.md) | Complete 51-record Notion inventory, source access, deduplication, and claim controls |
| [Literature](literature/index.md) | Fifteen unique works, ten deep paper notes, and study comparisons |
| [Ecosystem](ecosystem/index.md) | Workflow systems, agent harnesses, tool contracts, and transfer analysis |
| [Research map](research-map.md) | Path from reasoning and acting to state integrity, recovery, and controlled execution |
| [Working Research Position](research-position.md) | Seven provisional, bounded, and falsifiable positions |
| [Alignment](alignment/README.md) | Belief–reality divergence, memory integrity, execution authority, oversight, and goal fidelity |
| [Research questions](questions/research-questions.md) | Eight scoped questions and ten [falsifiable hypotheses](questions/hypotheses.md) |
| [Proposed experiments](experiments/README.md) | Fault benchmark, state ablation, recovery, workflow transfer, and authority studies—all unrun |
| [Concepts](concepts/epistemic-state.md) | Epistemic state, dependency-aware recovery, and a working failure taxonomy |
| [Architecture](architecture/proposed-runtime.md) | Proposed hybrid runtime and control invariants |
| [Diagrams](diagrams/README.md) | Seven Mermaid explanations of the research model |
| [Schemas](schemas/epistemic-state.schema.json) | Candidate machine-readable state record |

## Evidence policy

The complete starting knowledge base is a 51-record Notion database audited on 16 August 2026. Its 17 Research Paper records resolve to 15 unique works. No outside paper has been added to the scholarly corpus.

Sources are used according to four roles:

1. **Scholarly papers:** evidence for scientific claims, qualified by peer-review status, method, setting, assumptions, and limitations.
2. **Reference implementations:** evidence about code and engineering choices, not scientific effectiveness by themselves.
3. **Official documentation:** evidence about documented system semantics, not comparative reliability.
4. **Products, blogs, wikis, videos, and other secondary sources:** context, terminology, implementation ideas, and question generation only.

The Notion corpus is a starting knowledge base, not proof that the field has been exhaustively searched. See the [source inventory](provenance/source-inventory.md) and [access log](provenance/access-log.md). Copyrighted paper PDFs are not stored here.

## Technical alignment relevance

This project did not begin by assuming that operational reliability solves alignment. The intersection arises because persistent state and execution mechanisms affect whether an agent:

- acts on beliefs that match available external evidence;
- preserves or corrupts goals over many dependent steps;
- grants stored information behavioral authority;
- remains interruptible and correctable;
- distinguishes task success from policy compliance;
- exposes enough evidence for meaningful oversight;
- limits action through scoped capabilities and independent control.

Reliable execution can make a misdirected system more effective, so state integrity must be paired with goal fidelity, policy, authority, and oversight. The [alignment section](alignment/README.md) develops these connections without claiming a general alignment solution.

## Proposed evaluation

The initial experiments would compare transcript-only, untyped-checkpoint, provenance-aware, typed-state, and dependency-aware runtimes under controlled faults such as:

- stale or contradictory observations;
- timeouts before versus after side effects;
- false-success tool responses;
- concurrent environmental changes;
- corrupted memory;
- tool-version changes;
- policy rejection and authorized goal revision.

Primary outcomes include task success, state correctness, silent divergence, invalidation precision/recall, repeated side effects, recovery work, policy compliance, and goal fidelity. The full design is in [Proposed Experiments](experiments/README.md).

## Epistemic commitments

- Never describe proposed experiments as completed.
- Separate author-reported findings from interpretation.
- Distinguish peer-reviewed evidence, preprints, surveys, implementations, documentation, and practitioner material.
- Preserve uncertainty and disagreement.
- Report verification cost and false blocks alongside prevented failures.
- Do not use *novel*, *first*, *solves*, *guarantees*, or *state of the art* without explicit, scoped evidence.
- Revise the working position when experiments or stronger literature contradict it.
