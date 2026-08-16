# Study Comparison

| Work | Environment/data | Intervention or object studied | Outcome type | Main evidential boundary |
|---|---|---|---|---|
| ReAct | HotpotQA, FEVER, ALFWorld, WebShop | Interleaved reasoning and action prompting | Answer accuracy and interactive success | No durable cross-session state or changing concurrent environment |
| Reflexion | ALFWorld, programming tests, reasoning tasks | Stored verbal reflections across attempts | Success, pass@1, correctness | Feedback and self-evaluation may be wrong; small context-bound memory |
| Toolformer | Text corpora plus five simple tools | Self-supervised API-call training | Language-model task performance | No chained interactive recovery or durable execution |
| Tree of Thoughts | Game of 24, creative writing, crosswords | Search over model-generated thought states | Task-specific success/quality | Small tasks; higher inference cost; no external state mutation |
| Voyager | Minecraft | Curriculum + executable skill memory + iterative repair | Exploration, item, distance, progression, transfer | Narrow environment, few runs, API-specific skills |
| SWE-agent | SWE-bench, HumanEvalFix | Agent–Computer Interface | Resolved issues/pass@1 | Test success is incomplete correctness; snapshot tasks |
| WorkflowLLM | 106,763 workflows, 1,503 APIs, 83 apps | Data synthesis and fine-tuning | Code/reference and model-judge metrics | Correct APIs supplied; workflows not executed |
| MAST | 1,642 traces, seven MAS frameworks | Human/LLM failure annotation taxonomy | Failure prevalence and agreement | Diagnostic labels do not establish causal repair mechanisms |
| Sovereign Agentic Loops | 10,000 simulated cloud traces | Control-plane validation and evidence chain | Unsafe-intent blocking, replay, latency | Closed execution, complete state, deterministic validator assumptions |
| Self-Healing Orchestrators | 100 controlled fault-injection tasks | Failure-aware bounded recovery | Success, silent failure, cost/latency proxies | Fault ontology and local tools are constructed; limited live-model validation |

## Cross-study synthesis

The corpus supports three bounded conclusions:

1. **Harness and interface choices change observed performance and failure modes.** ReAct, SWE-agent, Voyager, and MAST support this across different settings.
2. **Feedback and persistence can improve repeated behavior, but their value depends on evaluator quality and memory validity.** Reflexion and Voyager provide bounded evidence; the memory surveys describe broader risks.
3. **Verification and recovery are separable from plan generation.** WorkflowLLM evaluates generation without execution, while the two 2026 preprints test controlled validation or recovery mechanisms.

It does **not** follow that the proposed epistemic-state model is validated, that deterministic workflow mechanisms automatically transfer, or that any reviewed system solves general long-horizon reliability.
