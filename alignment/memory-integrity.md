# Memory Integrity

## Technical problem

Persistent memory changes future policy. Its risk is therefore not limited to retrieval quality or data confidentiality. Memory can be false when written, become stale, be corrupted, be retrieved outside its original scope, or preserve an unsafe behavioral rule after its justification disappears.

The [long-term-memory security survey](../literature/core-papers/long-term-memory-security.md) organizes risk across write, store, retrieve, execute, share, and forget/rollback. [Reflexion](../literature/core-papers/reflexion.md) shows that model-generated lessons can improve later attempts but depend on evaluator quality. [Voyager](../literature/core-papers/voyager.md) makes the stakes clearer: memory can be executable code.

## Integrity dimensions

| Dimension | Question |
|---|---|
| Source integrity | Who or what produced the memory, and can that provenance be trusted? |
| Semantic integrity | Is the content accurate and justified by its cited evidence? |
| Temporal integrity | Is it still current enough for the intended action? |
| Contextual integrity | Does it apply to this user, environment, tool version, and goal? |
| Dependency integrity | Which beliefs, plans, and skills rely on it? |
| Authority integrity | What actions may rely on it without additional verification? |
| Revocation integrity | Can it and its downstream effects be invalidated or rolled back? |

## Alignment relevance

- **Persistent influence:** a poisoned or erroneous memory can redirect behavior across sessions.
- **Goal drift:** accumulated summaries and lessons can gradually replace the original objective with a proxy.
- **Corrigibility:** durable memories must remain revisable when new evidence arrives.
- **Least authority:** retrieval should not automatically grant permission to execute a stored instruction or skill.
- **Auditability:** a reviewer should be able to trace a current behavioral premise to its originating evidence.

## Proposed write path

1. accept a candidate memory with provenance;
2. store it as observed or inferred, not automatically verified;
3. evaluate source, scope, and conflicts;
4. assign an authority level and expiration/freshness policy;
5. record dependencies created when the memory is used;
6. re-verify or invalidate it when triggering conditions occur.

## Security–epistemic distinction

A memory can be cryptographically unmodified yet epistemically wrong. Conversely, an accurate memory can be accessed by an unauthorized component. A trustworthy runtime needs both conventional security properties and epistemic-state controls.

## Open questions

- Can memory promotion be calibrated to task risk?
- How can procedural memory be sandbox-tested before reuse?
- What is the right granularity for dependency tracking?
- How should the system handle multiple individually credible but contradictory memories?
- Can forgetting be complete when a memory has already shaped downstream summaries and skills?
