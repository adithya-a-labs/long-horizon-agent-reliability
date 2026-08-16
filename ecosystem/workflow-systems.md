# What Deterministic Workflow Systems Can—and Cannot—Teach LLM Agents

This comparison focuses on [Temporal](https://docs.temporal.io/), [Apache Airflow](https://airflow.apache.org/docs/), [Trigger.dev](https://github.com/triggerdotdev/trigger.dev), and [LangGraph](https://docs.langchain.com/oss/python/langgraph/overview). “Deterministic” here describes the orchestration/control model, not every external activity or LLM call.

## Mechanism comparison

| Dimension | Temporal | Airflow | Trigger.dev | LangGraph |
|---|---|---|---|---|
| Primary abstraction | Code-defined durable Workflow plus Activities | Scheduled DAG of tasks | TypeScript long-running task/run | Stateful graph of nodes and edges |
| Persistent identity | Workflow ID and Run ID | DAG run and task-instance identity | Run and task identity | Thread ID plus checkpoint lineage |
| Persisted state | Event history; Workflow state reconstructed by replay | Metadata database stores DAG/task-run state; XCom stores bounded inter-task data | Run state, waits, queues, checkpoints, logs | User-defined graph state and checkpoints |
| Resume model | Replay event history, then continue from latest durable point | Re-schedule or clear/re-run failed task instances | Resume durable task around checkpoints/waits | Resume from saved checkpoint; replay selected work |
| Retry semantics | Configurable Activity retries, timeouts, backoff | Task-level retries and retry delay | Automatic retries, backoff, queues, fine-grained retry helpers | Node/task retry policies can be configured |
| Side-effect boundary | Workflow code should be deterministic; side effects belong in Activities | Operators/tasks perform external effects | Task code performs effects within managed runs | Nodes/tools may perform effects; durable-execution guidance requires care |
| Idempotency | Application responsibility for Activities; stable IDs support deduplication | Task/operator responsibility | Idempotency keys and run controls available | Application/node responsibility; checkpoint replay can repeat unsafe effects if unguarded |
| Version change | Worker/workflow versioning and patching patterns | DAG code changes affect future scheduling and can complicate historical runs | Atomic task versioning isolates running tasks from new deployments | Graph and state-schema changes require migration discipline |
| Human intervention | Signals, Updates, workflow pause patterns, operator tooling | UI/API can inspect, mark, clear, retry, or pause | Waitpoints and human approval can pause live runs | Interrupts support human review and state modification |
| Observability | Event histories, visibility, logs, metrics | Graph/grid views, task logs, metadata state | Full run logs, traces, tags, filters, alerts | State history, checkpoints, traces through ecosystem tooling |
| Native epistemic status | None beyond application-defined state | None beyond task/run status | None beyond application-defined payloads | User can define it, but no universal observed/verified semantics |
| Native LLM role | None required | None required | Optional task logic/agent | First-class support for deterministic and agentic nodes |

## Mechanisms that transfer directly

These are useful without assuming that LLM decisions are deterministic:

- **Stable run and step identity:** every action, retry, observation, and verification should have durable identifiers.
- **Explicit task states:** pending, running, succeeded, failed, timed out, cancelled, and awaiting approval should not live only in natural-language context.
- **Append-only event history:** preserve what was proposed, executed, returned, and verified.
- **Bounded retries with backoff and deadlines:** prevent unbounded loops and make recovery cost visible.
- **Idempotency and deduplication:** attach stable action IDs to side effects.
- **Separation of orchestration from side effects:** keep control logic replayable and isolate external mutations in mediated operations.
- **Pause/resume and human gates:** allow execution to stop without losing state.
- **Version pinning:** record the model, prompt, tool schema, workflow definition, and verifier version used for a run.
- **Compensation hooks:** represent how to mitigate completed actions when literal rollback is impossible.
- **Operational observability:** expose timelines, dependencies, retries, exceptions, and intervention history.

## Mechanisms that require adaptation

### Replay

Temporal replay assumes deterministic Workflow decisions given recorded events. Re-running an LLM call can produce a different decision. An agent runtime should therefore persist the chosen model output as an event and replay the recorded decision, not silently sample a new one. Deliberate re-sampling should create a new branch with explicit provenance.

### Checkpoints

A workflow checkpoint says where execution can resume. It does not say whether the checkpoint's beliefs are still true. Agent checkpoints need freshness, provenance, and verification metadata, plus rules for revalidating external preconditions after time passes.

### Retry

Retry is appropriate for transient operational failure. It is inappropriate when arguments were generated from a false belief, the action is non-idempotent, or the environment rejected the underlying plan. Agent retries need a failure taxonomy and a decision about whether to retry, repair state, locally replan, escalate, or compensate.

### Success states

Deterministic systems usually accept task completion or a return value as success. Agent steps may return plausible but semantically wrong outputs. Success should be split into execution completion, postcondition observation, verification, policy compliance, and contribution to the current goal.

### Versioning

Workflow code versioning is necessary but insufficient. Agent runs also depend on model weights, sampling settings, system prompts, retrieved memory, tool descriptions, and verifier policies. All affect replay and comparison.

## Mechanisms that do not solve the epistemic problem

- Durable storage preserves false state as effectively as true state.
- Exactly-once or deduplicated execution does not show that the action was correct.
- A green DAG does not establish that the external environment matches the agent's belief.
- Retry cannot repair a corrupted premise.
- Logs provide evidence for later audit but do not automatically verify their own semantics.
- Human approval is weak if the reviewer sees only the model's summary rather than source evidence and expected effects.

## Proposed hybrid runtime lesson

The transferable architecture is not “put an LLM inside a workflow engine.” It is:

1. use deterministic orchestration for identity, budgets, event history, authority, and control flow;
2. treat model calls as stochastic proposal-producing activities;
3. persist proposals and observations as evidence-bearing events;
4. promote state only through explicit verification transitions;
5. invalidate dependent state before retry or replanning;
6. isolate side effects behind scoped, idempotent execution adapters;
7. branch rather than overwrite when deliberate re-sampling changes a decision.

This is a working synthesis. Its reliability advantage remains to be tested.
