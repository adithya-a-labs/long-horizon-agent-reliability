# Working Failure Taxonomy

> **Status: synthesis for experiment design; not a validated taxonomy.**

| Class | Example | Detection signal | Candidate response |
|---|---|---|---|
| Operational | Timeout, crash, rate limit | Exception, deadline, missing response | bounded retry, backoff, alternate tool |
| Ambiguous effect | Timeout after side effect | Lost response, duplicate detector, postcondition query | observe effect before retry; deduplicate or compensate |
| Epistemic | Stale or false belief | contradiction, freshness expiry, failed check | re-observe, invalidate dependants, replan |
| Memory integrity | Poisoned, corrupted, or out-of-scope memory | provenance failure, conflict, policy scan | quarantine, revoke authority, trace consumers |
| Planning | Invalid decomposition or missing dependency | unsatisfied precondition, cyclic plan, verifier failure | repair graph or replan affected subgraph |
| Verification | False acceptance or false rejection | independent disagreement, hidden check, audit | change verifier/evidence; escalate |
| Authority/policy | Action exceeds scope or violates constraint | policy engine, capability mismatch | deny, narrow capability, request approval |
| Goal fidelity | Subgoal or termination drifts from intent | constraint loss, goal-diff check, human review | restore goal version, invalidate derived plans |
| Recovery | Retry loop, incomplete rollback, contaminated branch | budget exhaustion, repeated signature, residual state error | escalate, full replan, safe stop |
| Observability | Missing provenance or untraceable side effect | event gap, unmatched action/result | stop protected execution; reconstruct if possible |

The categories overlap. Classification should permit multiple labels and record uncertainty rather than forcing one cause prematurely.
