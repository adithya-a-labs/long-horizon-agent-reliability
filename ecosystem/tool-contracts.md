# Tool Contracts: Structure Is Not Truth

The official [function-calling guide](https://developers.openai.com/api/docs/guides/function-calling) describes a loop in which a model proposes a structured function call, the application executes it, and the result is returned to the model. [Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs) can constrain generated data to a supported JSON schema when strict mode is used.

## What structure provides

- machine-parseable action proposals;
- explicit argument types and required fields;
- rejection of many malformed outputs;
- a stable boundary between model generation and application execution;
- a place for deterministic policy and authorization checks.

## What structure does not provide

- semantic correctness of arguments;
- evidence that an identifier refers to the intended real object;
- authorization to perform the action;
- freshness of model-supplied state;
- successful execution or expected side effects;
- policy compliance;
- truth of the tool's returned data.

## Proposed intent envelope

The repository's working design adds fields beyond a tool's ordinary input schema:

```json
{
  "intent_id": "stable-run-scoped-id",
  "goal_reference": "goal-or-subgoal-id",
  "proposed_action": "tool_name",
  "arguments": {},
  "precondition_claims": ["state-id"],
  "expected_effects": ["effect-schema-id"],
  "evidence_references": ["event-id"],
  "requested_authority_scope": ["capability-id"],
  "verification_plan": "verifier-id",
  "compensation_plan": "optional-operation-id"
}
```

This envelope is a proposed research artifact, not a validated standard. Its purpose is to make authority, evidence, and expected effects explicit before execution.
