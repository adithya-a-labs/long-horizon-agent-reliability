# A Survey on the Security of Long-Term Memory in LLM Agents

- **Original source:** [arXiv HTML](https://arxiv.org/html/2604.16548v1)
- **Authors:** Zehao Lin, Chunyu Li, Kai Chen
- **Status:** Survey preprint, April 2026; not peer reviewed at the time of this audit

## Research question and central thesis

The survey asks how long-term-memory security should be organized across the full lifecycle of an LLM agent. Its central thesis is that memory security is broader than prompt injection or retrieval poisoning: confidentiality, integrity, availability, and governance risks appear at every phase from writing to forgetting and rollback.

## Survey method and taxonomy

The authors report reviewing roughly 70 works published from January 2023 through April 2026. The corpus is described as approximately 30% peer-reviewed work, 55% preprints, and 15% grey literature.

The survey uses a six-phase lifecycle:

1. Write
2. Store
3. Retrieve
4. Execute
5. Share
6. Forget/Rollback

Each phase is examined across four security properties:

- integrity;
- confidentiality;
- availability;
- governance.

This produces a matrix for locating attacks, defences, and underexplored regions. The paper also discusses “mnemonic sovereignty”: maintaining control over what an agent remembers, trusts, shares, and can remove.

## Findings

The survey's synthesis identifies a concentration of work on memory writing, retrieval, and integrity attacks, with less coverage of storage-layer security, availability, and reliable forgetting/rollback. It argues that existing defences are fragmented and that there is no demonstrated full-lifecycle architecture or benchmark covering the entire matrix.

These are survey conclusions. Quantitative claims about individual attacks or defences require reading the cited primary work rather than relying on this note.

## Important assumptions

- The lifecycle phases are sufficiently distinct to organize real systems.
- Security properties borrowed from conventional systems transfer meaningfully to LLM memory.
- The reviewed corpus is representative despite rapid publication and substantial grey literature.
- A lifecycle matrix exposes gaps that topic- or attack-based taxonomies miss.

## Limitations

The paper is a recent preprint covering a fast-moving field. Much of its underlying corpus is itself preprint or grey literature. The taxonomy is broad, so sources grouped in one cell can study materially different memory architectures and threat models. Survey coverage does not establish field exhaustiveness.

## My interpretation and critique

This is the strongest conceptual source in the starting corpus for memory integrity and rollback. Its lifecycle view is more useful than treating “memory” as a single store. However, security properties alone do not capture epistemic correctness. A memory can be uncorrupted, confidential, and available while still being false, stale, or unjustifiably authoritative.

I therefore add an epistemic dimension: provenance, observation status, verification, freshness, dependency, and invalidation. This complements rather than replaces the security lifecycle.

## What changed in my thinking

The survey broadened my focus from retrieval accuracy to lifecycle control. In particular, forgetting and rollback became first-class reliability mechanisms rather than cleanup features. It also made governance relevant: an agent needs rules for who may write, verify, promote, share, or revoke memory.

## Connection to this research

The repository combines the survey's lifecycle with the proposed epistemic-state machine. For example:

- **Write:** store an observation and provenance without automatically promoting it to verified belief.
- **Retrieve:** expose freshness and authority metadata.
- **Execute:** require current verified preconditions for consequential actions.
- **Forget/Rollback:** invalidate dependent beliefs, plans, and skills rather than deleting one isolated record.

## Technical alignment relevance

- **Memory integrity:** persistent false or adversarial memories can redirect future behavior.
- **Corrigibility:** reliable removal and rollback make durable behavior revisable.
- **Least authority:** memory writers and memory consumers should have separate permissions.
- **Goal fidelity:** corrupted long-term state can gradually shift the operational objective.
- **Oversight:** provenance and governance make memory updates auditable.

## Open questions

1. How should epistemic status interact with confidentiality and access control?
2. Can rollback remove all downstream effects of a corrupted memory?
3. How should availability be measured when safe refusal is preferable to using stale memory?
4. What benchmark can cover both adversarial corruption and ordinary state drift?
5. Who or what is authorized to promote a memory from observed to verified?
