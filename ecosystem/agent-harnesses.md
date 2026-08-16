# Agent Harness and Reference-Implementation Patterns

| System | Persistent representation | LLM authority | Reliability-relevant observation | Evidential use |
|---|---|---|---|---|
| [ReAct](https://react-lm.github.io/) | Prompt trajectory | Proposes bounded actions | Visible action–observation loop, but no typed durable state | Paper-backed reference pattern |
| [Voyager](https://github.com/MineDojo/Voyager) | Checkpoints and executable skill library | Writes and invokes code through environment adapter | Procedural memory is compositional and powerful, but preconditions and revocation are weakly represented | Paper + implementation |
| [SWE-agent](https://github.com/SWE-agent/SWE-agent) | Trajectory, repository state, configuration | Uses a constrained command interface | Interface design changes error surface; current project is superseded by mini-SWE-agent | Paper + versioned implementation |
| [LangGraph](https://github.com/langchain-ai/langgraph) | Typed graph state and checkpoints | Depends on graph design | Strong substrate for durable state and human interrupts; epistemic semantics remain application-defined | Tier 2/3 implementation |
| [Hermes](https://github.com/NousResearch/hermes-agent) | Sessions, persistent memory, profiles, skills, schedules | Broad tool access through configurable backends and approvals | Useful implementation study for memory, reusable skills, isolation, and command approval | Tier 2 only |
| [Pi](https://github.com/earendil-works/pi) | Tree-structured sessions, compaction, project instructions | Minimal core; authority added through extensions | Branching history and customizable context expose useful provenance choices | Tier 2 only |
| [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | Platform runs, visual workflows; historical Classic loop | Platform-dependent | Current repository differs substantially from the original AutoGPT architecture | Tier 2, version-sensitive |
| [BabyAGI](https://github.com/yoheinakajima/babyagi) | Function database, dependency graph, logs | Experimental self-building functions | Explicitly not production-ready; useful for dependency and self-modification questions | Tier 2 exploratory only |
| [LangChain](https://github.com/langchain-ai/langchain) | Framework-dependent | Application-defined | Broad integration layer; reliability claims must be tied to a specific runtime | Tier 2 only |

## Cross-cutting questions

- Is memory descriptive text, typed state, executable code, or a mixture?
- Does retrieval grant information behavioral authority automatically?
- Are action permissions global, tool-level, or intent-specific?
- Can a run branch without overwriting its original history?
- Are tool outputs treated as observations or as verified facts?
- Can the system explain which current plans depend on a particular memory?
- Can a human inspect raw evidence rather than only model-written summaries?

No reviewed implementation answers all of these questions in a unified state model.
