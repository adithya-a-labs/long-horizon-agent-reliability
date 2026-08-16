# Falsifiable Hypotheses

All hypotheses are **proposed**. No experiment has been run.

## H1. Typed-state recovery

Under injected stale, contradictory, and false-success observations, a typed epistemic-state runtime will reduce silent state errors relative to a transcript-only agent at a matched model and tool-call budget.

**Disconfirmation:** no meaningful reduction in silent error, or gains disappear after accounting for additional verifier calls and tokens.

## H2. Selective invalidation

When a failed premise has sparse downstream dependencies, dependency-aware invalidation will use fewer recomputed steps than full replanning while achieving comparable or better final state correctness.

**Disconfirmation:** dependency tracking misses contamination, over-invalidates most of the graph, or costs as much as full replanning.

## H3. Dense-dependency limit

The advantage of selective invalidation will decrease as dependency density and hidden coupling increase.

**Disconfirmation:** recovery advantage remains constant across sparse and dense graphs, suggesting that the proposed dependency measure is not explanatory.

## H4. Verification promotion

Risk-weighted promotion—requiring stronger evidence for higher-impact state—will reduce severe false-authority events more efficiently than verifying every observation or automatically trusting every observation.

**Disconfirmation:** risk weighting is poorly calibrated, misses severe cases, or creates similar cost to universal verification.

## H5. Retry typing

Restricting blind retry to classified transient failures will reduce repeated side effects and retry loops without materially reducing recoverable task completion.

**Disconfirmation:** failure classification is too inaccurate to improve over standard bounded retries.

## H6. Recorded-decision replay

Replaying persisted model decisions will reproduce a prior control trajectory more reliably than reissuing model calls from the same checkpoint.

**Disconfirmation:** external nondeterminism dominates so strongly that recorded decisions provide little reproducibility, or reusing them creates more stale-state errors than controlled re-sampling.

## H7. Authority separation

A proposal–execution control plane will reduce policy-violating side effects relative to direct model tool execution, with a measurable false-block tradeoff.

**Disconfirmation:** unsafe actions bypass policy checks, policy gaps dominate, or legitimate completion collapses under control-plane restrictions.

## H8. Verifier independence

Verification using an independent evidence channel will have lower correlated false acceptance than actor self-verification under semantic tool faults.

**Disconfirmation:** independence does not reduce false acceptance or creates equivalent errors through a different channel.

## H9. Dependency-centrality oversight

Prioritizing human review by action irreversibility and dependency centrality will detect more consequential errors per review than uniform or uncertainty-only sampling.

**Disconfirmation:** centrality does not predict downstream harm or reviewers cannot use the additional state information effectively.

## H10. Multi-objective divergence

Across long-horizon fault scenarios, task success, state correctness, policy compliance, and goal fidelity will diverge often enough that reporting task success alone changes system rankings.

**Disconfirmation:** the metrics remain nearly collinear across representative scenarios, making separate evaluation unnecessary for that domain.

## Experimental discipline

- Predefine primary and secondary outcomes.
- Match model, tool, and recovery budgets where possible.
- Report absolute counts and uncertainty, not only percentages.
- Separate deterministic fault templates from model-in-the-loop results.
- Preserve failed traces and negative results.
- Treat evaluator changes as experimental interventions.
- Do not promote benchmark-specific improvements into general reliability claims.
