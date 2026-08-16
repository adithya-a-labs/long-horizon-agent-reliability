# Source Inventory

Audit date: **2026-08-16**
Starting database: [Notion Document Hub](https://www.notion.so/3edf975653bf833b9c490161834cfa41?v=171f975653bf8387a73d887d21231b86&source=copy_link)

## Inventory summary

- 51 Notion records inspected.
- 17 records tagged `Research Paper`, representing 15 unique works.
- 11 GitHub records, 6 Documentation records, 5 App records, 3 Wiki records, 1 YouTube record, and 8 uncategorized records.
- Two duplicated scholarly works: the long-term-memory security survey appears twice; ReAct appears once as an arXiv page and once as its project page.
- Two records tagged `Research Paper` are practitioner publications rather than scholarly papers: *Designing Agentic Memory* and Zylos's *Long-Horizon Planning and Goal Decomposition*.

## Evidence tiers

| Tier | Source type | Permitted use |
|---|---|---|
| 1 | Scholarly papers | Evidence for scientific claims, qualified by venue, method, assumptions, and limitations. Preprints and surveys are labelled separately. |
| 2 | GitHub/reference implementations | Evidence about implementation structure and engineering choices, not scientific effectiveness unless backed by a study. |
| 3 | Official documentation | Evidence about documented semantics such as retry, replay, checkpointing, tool contracts, and persistence. |
| 4 | Products, apps, blogs, wikis, videos, uncategorized material | Ecosystem context, terminology, demonstrations, and question generation only. |

## Complete Notion inventory

| # | Notion record | Notion category | Resolved role | Source |
|---:|---|---|---|---|
| 1 | A Survey on the Security of Long-Term Memory in LLM Agents | Research Paper | Tier 1, survey preprint; duplicate of #37 | [arXiv](https://arxiv.org/html/2604.16548v1) |
| 2 | Apache Airflow | Uncategorized | Tier 4 product/project overview; paired with #3 | [Site](https://airflow.apache.org/) |
| 3 | Apache Airflow (1) | Documentation | Tier 3 deterministic workflow documentation | [Docs](https://airflow.apache.org/docs/) |
| 4 | AutoGPT | Wiki | Tier 4 historical context; page carries a sourcing warning | [Wikipedia](https://en.wikipedia.org/wiki/AutoGPT) |
| 5 | AutoGPT | GitHub | Tier 2 current platform and historical `classic/` implementation | [GitHub](https://github.com/Significant-Gravitas/AutoGPT) |
| 6 | BabyAGI | GitHub | Tier 2 experimental implementation; original archived | [GitHub](https://github.com/yoheinakajima/babyagi) |
| 7 | Ceiling in long-horizon planning | Wiki | Tier 4 practitioner analysis | [Adaline](https://labs.adaline.ai/p/long-horizon-ai-agents-planning-ceiling) |
| 8 | Decoupling AI-Execution from reasoning in Real World Systems? | Research Paper | Tier 1, primary preprint; resolved title: *Sovereign Agentic Loops* | [arXiv PDF](https://arxiv.org/pdf/2604.22136) |
| 9 | Designing Agentic Memory | Research Paper, Wiki | Tier 4 practitioner essay despite tag | [Substack](https://thenuancedperspective.substack.com/p/designing-agentic-memory-in-2026) |
| 10 | Examples of Long Horizon Tasks | Uncategorized | Tier 4 private Notion attachment; not extractable during audit | Notion attachment |
| 11 | Hermes Agent | App | Tier 4 product description; paired with #12 | [Site](https://hermes-agent.org/) |
| 12 | Hermes Agent Github | GitHub | Tier 2 agent implementation | [GitHub](https://github.com/NousResearch/hermes-agent) |
| 13 | Krishna's RepoLens AI | App | Tier 4 interactive architecture/repository-analysis UI | [App](https://repolens-ai-sepia.vercel.app/) |
| 14 | LangChain | GitHub | Tier 2 framework implementation | [GitHub](https://github.com/langchain-ai/langchain) |
| 15 | LangChain | Uncategorized | Tier 4 project overview; paired with #14 | [Site](https://www.langchain.com/) |
| 16 | LangGraph | GitHub | Tier 2 stateful orchestration implementation | [GitHub](https://github.com/langchain-ai/langgraph) |
| 17 | LangGraph (1) | Documentation | Tier 3 stateful-agent runtime documentation | [Docs](https://docs.langchain.com/oss/python/langgraph/overview) |
| 18 | Long Horizon Agent Planning-Memory | Wiki | Tier 4 aggregator/synthesis | [Emergent Mind](https://www.emergentmind.com/topics/long-horizon-agent-planning) |
| 19 | Long horizon planning and goal decomposition | Research Paper | Tier 4 practitioner article despite tag | [Zylos](https://zylos.ai/research/2026-05-14-long-horizon-planning-goal-decomposition-ai-agents/) |
| 20 | Memory for Autonomous LLM Agents | Research Paper | Tier 1, survey preprint | [arXiv](https://arxiv.org/abs/2603.07670) |
| 21 | Microsoft Power Automate | Uncategorized | Tier 4 commercial workflow platform | [Site](https://www.microsoft.com/en-us/power-platform/products/power-automate) |
| 22 | n8n | Uncategorized | Tier 4 product overview; paired with #23 | [Site](https://n8n.io/) |
| 23 | n8n (1) | GitHub | Tier 2 source-available workflow platform | [GitHub](https://github.com/n8n-io/n8n) |
| 24 | Open Notebook | App | Tier 4 research/note-taking product | [Site](https://www.open-notebook.ai/) |
| 25 | OpenAI Structured Outputs & Function Calling | Documentation | Tier 3 official function-calling semantics | [Docs](https://developers.openai.com/api/docs/guides/function-calling) |
| 26 | OpenAI Structured Outputs & Function Calling | Documentation | Tier 3 official structured-output semantics | [Docs](https://developers.openai.com/api/docs/guides/structured-outputs) |
| 27 | Pi Coding Agent | App | Tier 4 project description; paired with #28 | [Site](https://pi.dev/) |
| 28 | Pi Coding Agent Harness Github | GitHub | Tier 2 minimal, extensible agent harness | [GitHub](https://github.com/earendil-works/pi) |
| 29 | React Flow | GitHub | Tier 2 UI implementation, not an agent runtime | [GitHub](https://github.com/xyflow/xyflow) |
| 30 | React Flow | App | Tier 4 visualization documentation/site | [Site](https://reactflow.dev/) |
| 31 | ReAct | Research Paper | Tier 1, peer-reviewed primary study; duplicate work with #32 | [arXiv](https://arxiv.org/abs/2210.03629) |
| 32 | ReAct (1) | Research Paper | Project page for #31, not a second paper | [Project](https://react-lm.github.io/) |
| 33 | Reflexion | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2303.11366) |
| 34 | Replit Agents | YT | Tier 4 short secondary video; no transcript/captions | [YouTube](https://www.youtube.com/watch?v=c8QiXuUMZCI) |
| 35 | Self-healing agentic orchestrators | Research Paper | Tier 1, primary preprint | [arXiv](https://arxiv.org/html/2606.01416v1) |
| 36 | Survey on long-horizon agents | Research Paper | Tier 1, survey preprint; resolved title: *Towards Long-Horizon Agents: A Survey* | [Preprints.org](https://www.preprints.org/manuscript/202607.1328) |
| 37 | Survey on the security of long-term memory in agents | Research Paper | Duplicate of #1 | [arXiv](https://arxiv.org/html/2604.16548v1) |
| 38 | SWE Agent | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2405.15793) |
| 39 | SWE Agent | GitHub | Tier 2 implementation; now superseded by mini-SWE-agent | [GitHub](https://github.com/SWE-agent/SWE-agent) |
| 40 | Temporal | Uncategorized | Tier 4 product/project overview; paired with #41 | [Site](https://temporal.io/) |
| 41 | Temporal (1) | Documentation | Tier 3 durable-execution documentation | [Docs](https://docs.temporal.io/) |
| 42 | The New SDLC With Vibe Coding | Documentation | Tier 4 practitioner whitepaper, 51 pages | [Drive](https://drive.google.com/file/d/1wNEl8FMpTso8aXlb_joxgzparxi-0ciM/view?usp=sharing) |
| 43 | Toolformer | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2302.04761) |
| 44 | Tree of Thoughts | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2305.10601) |
| 45 | Trigger.dev | Uncategorized | Tier 4 product overview; paired with #46 | [Site](https://trigger.dev/) |
| 46 | Trigger.dev (1) | GitHub | Tier 2 durable-task implementation | [GitHub](https://github.com/triggerdotdev/trigger.dev) |
| 47 | Voyager | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2305.16291) |
| 48 | Voyager | GitHub | Tier 2 reference implementation | [GitHub](https://github.com/MineDojo/Voyager) |
| 49 | Why do multi-agent AI systems fail? | Research Paper | Tier 1, peer-reviewed dataset/analysis paper | [arXiv PDF](https://arxiv.org/pdf/2503.13657) |
| 50 | WorkflowLLM | Research Paper | Tier 1, peer-reviewed primary study | [arXiv](https://arxiv.org/abs/2411.05451) |
| 51 | Zapier | Uncategorized | Tier 4 commercial automation platform | [Site](https://zapier.com/) |

## Deduplicated scholarly corpus

The 17 Research Paper rows resolve to 15 unique works: eight peer-reviewed primary studies or datasets, two primary preprints, three survey preprints, and two practitioner articles misclassified as research papers. See [literature/evidence-ledger.md](../literature/evidence-ledger.md) for study-level treatment.
