# Verification and Oversight

## Technical problem

Verification is often treated as a final check: did the task succeed? Long-horizon agents require verification throughout the trajectory because a plausible intermediate output can contaminate many downstream steps before final evaluation.

[Reflexion](../literature/core-papers/reflexion.md) depends on the evaluator that generates feedback. [MAST](../literature/core-papers/mast.md) identifies task-verification failures across multi-agent systems. [Self-Healing Agentic Orchestrators](../literature/core-papers/self-healing-orchestrators.md) reports controlled benefits from verifier-guided recovery. These sources suggest verification matters; they do not establish a universally reliable verifier.

## Verification targets

| Target | Example question |
|---|---|
| Structural validity | Did the output match the required schema? |
| Execution validity | Did the tool call complete without operational error? |
| Postcondition validity | Did the external state change as expected? |
| Epistemic validity | Does the evidence justify the state claim? |
| Policy validity | Was the action permitted? |
| Goal validity | Does this step still advance the intended objective? |
| Recovery validity | Did repair remove downstream effects of the original error? |

A check at one layer should not be reported as validation of all layers.

## Correlated verifier failure

Actor and verifier can fail together when they:

- use the same base model and context;
- share an incorrect memory or summary;
- optimize the same proxy;
- see only model-generated evidence;
- inherit the same ambiguous task interpretation.

Useful independence can come from deterministic tests, separate data sources, hidden checks, different models, policy engines, or human review. Independence is not binary; each mechanism has its own failure modes.

## Oversight design

Operational oversight should expose:

- raw observations and their provenance;
- the claims inferred from those observations;
- unresolved contradictions;
- planned and completed side effects;
- authority grants and denials;
- verifier identity, method, and result;
- the dependency impact of accepting or rejecting a claim.

More information is not automatically better. The interface should foreground decisions with high impact, uncertainty, irreversibility, or dependency centrality.

## Alignment relevance

- **Scalable oversight:** long traces require selective attention without losing decisive evidence.
- **Policy–outcome separation:** a correct result does not excuse a prohibited trajectory.
- **Corrigibility:** verification supplies triggers for pause, rollback, and replanning.
- **Robustness:** independent evidence can interrupt self-consistent but false internal narratives.

## Open questions

- How can verifier correlation be measured?
- Which intermediate states deserve mandatory verification?
- Can dependency centrality prioritize oversight better than model uncertainty alone?
- When should disagreement trigger re-observation versus human escalation?
- How should false-positive verification cost be compared with silent failure cost?
