# Ecosystem Comparison Matrix

| Source group | Primary lesson | Relevance | Evidence boundary |
|---|---|---|---|
| Temporal + docs | Event-history durability, replay, Activities, retries, signals, versioning | High | Documented workflow semantics, not agent evidence |
| Airflow + docs | DAG/task state, scheduling, retries, operational views | High | Batch workflow model; no native epistemic semantics |
| Trigger.dev + repo | Durable tasks, queues, checkpointing, idempotency, HITL, observability | High | Product/implementation claims, not controlled research |
| LangGraph + repo | Typed state graphs, checkpoints, interrupts, durable agent execution | High | Application must define truth, authority, and verification |
| Hermes | Persistent memory, skills, approvals, multiple execution backends | High implementation relevance | Product and repository claims only |
| Pi | Branching session trees, configurable compaction, extensions | High implementation relevance | Minimal harness; reliability properties depend on extensions |
| SWE-agent + Voyager repos | Constrained ACI and procedural-memory implementation | High | Paper results remain environment/version-specific |
| AutoGPT + BabyAGI | Historical autonomous loops and current experimental/platform designs | Medium | Rapidly changed; BabyAGI warns against production use |
| LangChain | Broad tool/model integration abstractions | Medium | Too general for reliability claims without a concrete runtime |
| n8n, Zapier, Power Automate | Visual workflows, permissions, approvals, audit and integrations | Medium | Product-level material; closed components limit inspection |
| OpenAI tool documentation | Schema-constrained proposals and application-mediated execution | High | Structure does not establish semantic truth or safety |
| Open Notebook | Source-backed research workspace and privacy controls | Low/medium | Research tooling, not execution reliability |
| React Flow + RepoLens | Graph/dependency visualization patterns | Low/medium | Interface inspiration, not runtime evidence |
| Adaline, Emergent Mind, SDLC whitepaper, Replit video, Wikipedia | Terminology and ecosystem context | Low | Tier 4; no substantive scientific claims |

The private “Examples of Long Horizon Tasks” attachment remains unavailable and is not used.
