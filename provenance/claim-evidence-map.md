# Claim–Evidence Map

This is a living control against accidental overclaiming. It records the strongest support currently available and what the evidence does **not** establish.

| Working claim | Current support | Evidence boundary | Status |
|---|---|---|---|
| Long-horizon failures can arise from system design, coordination, and verification rather than model reasoning alone. | [MAST](https://arxiv.org/pdf/2503.13657), [SWE-agent](https://arxiv.org/abs/2405.15793), workflow-system implementations | Does not show that model capability is unimportant or that all reliability failures are systems failures. | Supported as a qualified claim |
| Persistent memory introduces integrity, confidentiality, availability, and governance risks throughout its lifecycle. | [Long-term-memory security survey](https://arxiv.org/html/2604.16548v1) | Survey synthesis; individual attack/defence claims should be traced to primary sources before quantitative use. | Supported as survey synthesis |
| Reflection can improve task performance but depends on feedback and self-evaluation quality. | [Reflexion](https://arxiv.org/abs/2303.11366) | Evidence is task- and evaluator-dependent; reflection can reinforce incorrect diagnoses. | Supported with limitations |
| Executable skill libraries can preserve reusable procedural behavior. | [Voyager](https://arxiv.org/abs/2305.16291), [Voyager code](https://github.com/MineDojo/Voyager) | Minecraft-specific evidence does not establish general long-horizon reliability. | Supported in a bounded environment |
| Deterministic workflow runtimes implement useful mechanisms such as persisted histories, retries, replay, checkpoints, and human intervention. | [Temporal docs](https://docs.temporal.io/), [Airflow docs](https://airflow.apache.org/docs/), [Trigger.dev](https://github.com/triggerdotdev/trigger.dev), [LangGraph docs](https://docs.langchain.com/oss/python/langgraph/overview) | Documentation establishes mechanisms, not that they improve stochastic-agent reliability. | Implementation fact |
| Structured tool outputs reduce representational ambiguity. | [OpenAI function calling](https://developers.openai.com/api/docs/guides/function-calling), [Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs) | Schema validity does not imply semantic truth, authorization, successful execution, or current external state. | Documentation fact |
| Separating model reasoning from execution authority may reduce unsafe or unverifiable actions. | [Sovereign Agentic Loops](https://arxiv.org/pdf/2604.22136) plus workflow-system patterns | Direct experiment is simulated and assumes closed execution, deterministic evaluation, and complete mediation. | Provisional hypothesis |
| Local recovery may outperform blind retry or full replanning in some controlled fault settings. | [Self-Healing Agentic Orchestrators](https://arxiv.org/html/2606.01416v1) | Evidence uses controlled synthetic faults and does not establish production superiority. | Bounded preprint result |
| Planned, believed, observed, and verified state should be represented separately. | Literature synthesis and documented system semantics | No reviewed paper directly validates the proposed state machine as a whole. | Working hypothesis |
| Recovery should invalidate dependent state before replanning. | Memory-integrity synthesis, workflow dependency semantics, proposed model | Empirical advantage has not yet been tested in this project. | Working hypothesis |
| Task success, state correctness, policy compliance, and goal fidelity are distinct evaluation targets. | MAST failure categories, workflow validation boundaries, alignment analysis | The repository has not yet validated a complete metric suite or independence among these targets. | Working hypothesis |

## Language rules

- Use **shows** only for a result directly supported by the cited experiment within its tested setting.
- Use **suggests** for limited, indirect, preprint, or cross-domain evidence.
- Use **documents** for official implementation semantics.
- Use **I hypothesize** or **working hypothesis** for repository positions not yet empirically tested.
- Never use *solves*, *guarantees*, *state of the art*, *first*, or *novel* without explicit, scoped evidence.
