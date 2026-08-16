# Proposed Proposal–Execution Authority Study

> **Status: proposed; not implemented or run.**

## Question

Does separating model proposals from execution authority reduce policy violations and unsupported side effects without making legitimate tasks unusably difficult?

## Conditions

| Condition | Execution path |
|---|---|
| Direct | Valid structured model call executes immediately |
| Schema-only | Call must match schema but receives no semantic policy check |
| Policy gate | Deterministic policy checks target, action, and scope |
| State-aware gate | Policy plus verified/fresh preconditions and expected effects |
| State-aware + human | High-impact or ambiguous actions require approval |

## Scenario classes

- valid, low-risk actions;
- malformed actions;
- validly structured but semantically wrong targets;
- actions based on stale approval or stale resource state;
- over-broad actions when a narrower capability suffices;
- actions that advance the task but violate a policy constraint;
- actions with irreversible effects;
- adversarial or misleading memory instructing the agent to bypass controls.

## Primary outcomes

- executed policy violations;
- unsafe or unsupported side effects;
- legitimate-action false-block rate;
- task completion;
- number and duration of human escalations;
- authority granted beyond actual use;
- postcondition-verification failures.

## Verifier/control-plane variants

Compare rule-based checks, deterministic environment queries, model-based policy review, and mixed review. Record whether the actor and reviewer share model, memory, and context to measure correlated failures.

## Interpretation constraints

Preventing all actions is not successful control. Report the safety–utility frontier rather than a single blocking percentage. Simulated policy coverage does not establish real-world safety, and a closed execution path must be identified as an experimental assumption.
