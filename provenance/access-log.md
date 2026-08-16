# Source Access Log

Audit date: **2026-08-16**

## Access labels

- **Full**: the relevant full text or repository documentation was reviewed.
- **Substantive**: enough primary material was reviewed to characterize the source, but not every file or linked appendix.
- **Metadata only**: title/description or other limited metadata was available.
- **Unavailable**: the source could not be extracted or reviewed.

## Scholarly sources

| Source | Access | Notes |
|---|---|---|
| Long-term-memory security survey | Full | arXiv HTML reviewed, including taxonomy, survey construction, gaps, and conclusions. |
| Sovereign Agentic Loops | Full | 15-page PDF reviewed. |
| Memory for Autonomous LLM Agents | Full | arXiv HTML reviewed; survey-method reporting was limited. |
| ReAct | Full | Full paper reviewed. |
| Reflexion | Full | Full paper and official venue record reviewed. |
| Self-Healing Agentic Orchestrators | Full | arXiv HTML reviewed, including limitations. |
| Towards Long-Horizon Agents | Full | Preprints.org full text reviewed. |
| SWE-agent | Full | Paper and current repository overview reviewed. |
| Toolformer | Full | Full paper and venue record reviewed. |
| Tree of Thoughts | Full | Full paper and venue record reviewed. |
| Voyager | Full | Paper, venue status, and repository reviewed. |
| Multi-Agent Systems Failure Taxonomy (MAST) | Full | Paper and official NeurIPS record reviewed. |
| WorkflowLLM | Full | Paper and ICLR record reviewed. |
| Designing Agentic Memory | Full | Practitioner article reviewed; excluded from scholarly evidence. |
| Zylos long-horizon planning article | Full | Practitioner article reviewed; excluded from scholarly evidence. |

## Implementation and documentation sources

| Source group | Access | Notes |
|---|---|---|
| Airflow site and documentation | Substantive | DAG/task semantics, scheduling, monitoring, logs, and runtime isolation reviewed. |
| AutoGPT wiki and repository | Substantive | Current platform and historical `classic/` distinction reviewed; wiki treated cautiously. |
| BabyAGI repository | Substantive | Archive notice, experimental status, dependency graph, logging, and self-building claims reviewed. |
| Hermes site and repository | Substantive | Persistent memory, skills, execution backends, sessions, approvals, and documentation map reviewed. |
| RepoLens | Substantive | Interactive UI inspected; architecture/dependency visualization claims reviewed. |
| LangChain site and repository | Substantive | Framework role reviewed; detailed reliability semantics deferred to LangGraph. |
| LangGraph repository and docs | Substantive | Persistence, durable execution, stateful graphs, memory, human intervention, and tracing reviewed. |
| Power Automate | Substantive | Product-level workflow and governance material reviewed. |
| n8n site and repository | Substantive | Workflow graphs, human approvals, observability, integrations, and licensing reviewed. |
| Open Notebook | Substantive | Product role, source ingestion, privacy, and research-workflow features reviewed. |
| OpenAI function calling and Structured Outputs | Full | Official semantics and stated edge cases reviewed. |
| Pi site and repository | Substantive | Session trees, compaction, dynamic context, extensions, and harness scope reviewed. |
| React Flow site and repository | Substantive | UI/graph visualization role reviewed; not treated as a runtime. |
| SWE-agent repository | Substantive | Current README and supersession notice reviewed. |
| Temporal site and docs | Substantive | Event-history durability, replay, Activities, retries, pause/resume, and observability reviewed. |
| Trigger.dev site and repository | Substantive | Long-running tasks, retries, queues, checkpointing, idempotency, versioning, and HITL reviewed. |
| Voyager repository | Substantive | Checkpoint resume, skill libraries, and task decomposition warnings reviewed. |
| Zapier | Substantive | Workflow governance, role-based authority, auditability, and guardrails reviewed at product level. |

## Limited or inaccessible sources

| Source | Access | Consequence |
|---|---|---|
| Examples of Long Horizon Tasks | Unavailable | The Notion page contains a private PDF attachment that the available connector did not materialize. No claims are taken from it. |
| Replit Agents video | Metadata only | Title, creator, description, and page metadata were available. The short video had no captions or transcript; it is not used as evidence. |
| The New SDLC With Vibe Coding | Full | Initially inaccessible through ordinary web retrieval, then fetched through authenticated Google Drive. It remains Tier 4 practitioner material. |

## Re-audit triggers

Revisit this log when a source changes version, a preprint gains peer review, an unavailable artifact becomes accessible, or a repository's current implementation materially diverges from the recorded description.
