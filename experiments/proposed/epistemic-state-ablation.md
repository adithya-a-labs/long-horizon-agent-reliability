# Proposed Epistemic-State Representation Ablation

> **Status: proposed; not implemented or run.**

## Question

Does explicitly separating planned, believed, observed, verified, stale, and invalidated state reduce silent divergence enough to justify its complexity?

## Runtime variants

| Variant | Representation |
|---|---|
| A. Transcript only | ReAct-style prompt history; no external state store |
| B. Untyped checkpoint | Key/value persistent state plus task execution status |
| C. Provenance only | Untyped state with source and timestamp |
| D. Typed epistemic state | State type, provenance, freshness, verifier, and authority |
| E. Typed + dependencies | Variant D plus downstream dependency edges and invalidation |

The same action proposals should first be replayed through every variant. A later live-model phase can test whether representation changes model behavior.

## Fault conditions

- stale successful read;
- contradictory tool observations;
- false-success response;
- model inference mistakenly stored as an observation;
- previously verified state invalidated by a concurrent change;
- corrupted durable memory.

## Promotion policies

Within variants D and E, compare:

- automatic observation-to-verification promotion;
- deterministic postcondition check;
- independent observation source;
- risk-weighted verification;
- verification on first consequential use.

## Primary hypotheses

- H1: typed state reduces silent divergence relative to A and B.
- H4: risk-weighted promotion reduces severe false-authority events more efficiently than universal or absent verification.
- H10: task success and state correctness produce different system rankings.

## Measures

- silent divergence rate;
- state correctness over time, not only at termination;
- false promotion and false invalidation;
- time from external change to stale-state detection;
- task success and policy compliance;
- model/tool/token overhead;
- trace length and operator diagnosis time.

## Failure interpretation

If typed state improves only audit readability but not automated recovery, that is still informative but weaker than H1. If it increases failures through over-complex prompts or stale metadata, the representation should be simplified or moved out of model context.

## Planned ablation discipline

Do not add dependencies, stronger verification, or more model calls to one variant without recording them as separate interventions. “Typed state” must not become a bundle of every reliability mechanism.
