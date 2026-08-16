# Epistemic Execution State

> **Status: proposed conceptual model; not experimentally validated.**

## Motivation

An ordinary workflow engine records whether a task is pending, running, completed, or failed. A long-horizon agent also needs to represent what it plans, believes, has observed, has verified, no longer considers fresh, and has rejected.

Collapsing these into one memory field creates avoidable ambiguity:

- a planned future state can be mistaken for an accomplished state;
- a model inference can be stored as if it came from a tool;
- an old verified fact can remain authoritative after the environment changes;
- an invalidated premise can survive in downstream summaries or plans.

## Two-axis representation

The most precise design separates a record's **role** from its **epistemic status**.

### State role

| Role | Meaning | Example |
|---|---|---|
| Planned | Desired or predicted future state | “Service B will be restarted after configuration update.” |
| Believed | Working model claim or hypothesis | “Configuration drift is probably the root cause.” |
| Observed | Evidence returned by a tool, environment, or human | “Health endpoint returned HTTP 200 at 10:31.” |

### Epistemic status

| Status | Meaning | Behavioral authority |
|---|---|---|
| Unverified | Recorded but not checked by an appropriate procedure | May guide low-risk inquiry; should not alone authorize consequential action |
| Verified | Passed a recorded verification procedure within a defined scope and time | May satisfy matching action preconditions, subject to policy |
| Stale | Was usable, but freshness or dependency conditions no longer hold | Must be re-observed or re-verified before protected use |
| Invalidated | Contradicted, revoked, superseded, or shown inapplicable | Must not authorize action; dependants require review |

“Observed” and “verified” are not synonyms. Observation identifies the source of evidence; verification records that a procedure supports a claim. A direct deterministic observation can be verified immediately, but that is an explicit transition rather than an implicit assumption.

## Six requested distinctions

### Planned state

A plan expresses an intended or expected transition. It is evaluated by whether its preconditions are satisfied and whether its predicted effects occur. It must never be presented as evidence that the effect already happened.

### Believed state

A belief is the runtime's current working claim. It may be inferred from several observations or supplied by a model. A belief can be useful while unverified, but its uncertainty, basis, and scope should remain visible.

### Observed state

An observation is an event from a named source at a particular time. It can be incomplete, delayed, deceptive, or semantically wrong. Store the raw response or a content-addressed reference alongside any interpretation.

### Verified state

A verified claim passed a declared method: deterministic postcondition check, independent observation, consistency rule, trusted human approval, or another scoped verifier. Verification is always relative to a claim, method, scope, and time.

### Stale state

A stale claim is not necessarily false. Its age, changed dependency, version mismatch, or environmental mutation makes it insufficiently current for a particular use. Staleness is reversible through re-observation and re-verification.

### Invalidated state

An invalidated claim has affirmative reason not to be used: contradiction, failed verification, revoked approval, superseding version, or discovered provenance failure. It remains in history for audit but loses behavioral authority.

## Core record

Each state record should minimally contain:

- stable identifier and version;
- subject, predicate, and value or structured payload;
- state role and epistemic status;
- originating event and raw-evidence reference;
- source identity and source type;
- observation, verification, and expiry times;
- scope: environment, user, resource, tool/model version, and goal;
- verifier identity, method, and result;
- confidence or uncertainty representation where meaningful;
- authority level and permitted uses;
- dependencies and known consumers;
- supersession, staleness, and invalidation reason;
- immutable transition history.

A candidate JSON schema is provided in [schemas/epistemic-state.schema.json](../schemas/epistemic-state.schema.json).

## Transition rules

| From | Trigger | To | Required action |
|---|---|---|---|
| Unverified belief | supporting source event | Observed/unverified | attach evidence and preserve inference separately |
| Observed/unverified | successful scoped check | Verified | record verifier, method, time, and scope |
| Verified | expiry or relevant dependency change | Stale | block protected use and enqueue revalidation if needed |
| Any non-invalid state | contradiction, revocation, or provenance failure | Invalidated | traverse dependants and remove authority |
| Stale | successful re-observation and verification | Verified | create a new version; do not erase stale history |
| Invalidated | new contrary evidence | New record | create a new version or replacement; do not resurrect silently |

## Contradiction handling

Conflicting observations should be stored as separate evidence records. The runtime may create a belief describing the conflict, but should not force an early merge. Resolution can use source authority, recency, independent checks, or human review. A contradiction involving a high-impact precondition should pause execution.

## Freshness

Freshness is use-specific. A repository commit hash may remain valid indefinitely for one archived artifact, while an inventory count may expire in seconds. Each protected action should declare acceptable observation age or version constraints for its preconditions.

## Relationship to action authority

Verified state is still not an authorization decision. An action may have true preconditions but violate policy, exceed scope, or be unnecessarily irreversible. The authority controller consumes epistemic state; it does not collapse into it.

## Dependency semantics

Dependencies should record why one object relies on another:

- `derived_from`: belief B was inferred from observations O1 and O2;
- `planned_from`: action A was selected because of belief B;
- `parameterized_by`: tool argument X used state S;
- `authorized_by`: execution relied on approval P;
- `verified_by`: claim C was promoted by verifier result V;
- `implements`: subgoal G2 contributes to goal G1;
- `requires_version`: skill K assumes tool version T.

When a record becomes stale or invalid, the recovery engine follows these typed edges rather than invalidating every later event by timestamp.

## Risks of this model

- annotation and storage overhead;
- model confusion if all metadata is placed in context;
- false confidence in an incorrect verifier;
- hidden dependencies not represented in the graph;
- over-invalidation and unnecessary recomputation;
- inconsistent state transitions under concurrent execution;
- governance complexity around who may verify or revoke.

These risks are part of the proposed evaluation, not implementation details to be assumed away.
