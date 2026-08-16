# Voyager: An Open-Ended Embodied Agent with Large Language Models

- **Original source:** [arXiv](https://arxiv.org/abs/2305.16291) · [implementation](https://github.com/MineDojo/Voyager)
- **Authors:** Guanzhi Wang, Yuqi Xie, Yunfan Jiang, Ajay Mandlekar, Chaowei Xiao, Yuke Zhu, Linxi Fan, Anima Anandkumar
- **Status:** Peer-reviewed primary research, Transactions on Machine Learning Research

## Research question and central hypothesis

Voyager asks how an LLM-driven embodied agent can continually explore, acquire reusable skills, and transfer them to new tasks without model fine-tuning. Its central hypothesis is that an automatic curriculum, executable skill library, and environment-grounded iterative improvement can produce open-ended in-context learning.

## Technical method and architecture

Voyager contains three main components:

1. **Automatic curriculum:** proposes exploration tasks based on progress and current state.
2. **Skill library:** stores successful, temporally extended JavaScript programs indexed by natural-language descriptions and embeddings.
3. **Iterative prompting:** uses execution errors, environment feedback, and a self-verification process to revise code until a skill succeeds or the attempt terminates.

The LLM produces executable programs rather than low-level keyboard actions. Mineflayer mediates access to Minecraft. Successful skills can call previously learned skills, creating a compositional procedural memory. The repository supports checkpoint resume and loading a learned skill library separately from a new run.

## Experiments

The environment is Minecraft. Evaluation examines exploration, item acquisition, map traversal, technology-tree progression, and transfer to unseen tasks or worlds. Baselines include prior embodied agents and prompting/ablation variants without major Voyager components.

The authors report that Voyager obtains 3.3 times more unique items, travels 2.3 times longer distances, and unlocks key technology-tree milestones up to 15.3 times faster than prior baselines in their setup. It also reuses the acquired skill library on new tasks and worlds. These are bounded Minecraft results, not general reliability guarantees.

## Important assumptions

- Minecraft exposes sufficiently informative state through APIs and textual descriptions.
- Generated code is a useful and interpretable representation of procedural knowledge.
- Success checks accurately capture whether a skill works.
- Skills remain valid as the environment, game version, and dependencies change.
- The cost and latency of repeated LLM calls are acceptable.

## Limitations

The paper and implementation reveal several constraints: high model-call cost, dependence on Minecraft-specific APIs and setup, occasional hallucinated tasks or functions, imperfect self-verification, and flawed task decomposition that may need rerunning. Results come from a narrow embodied environment and a small number of experimental runs.

## My interpretation and critique

Voyager is one of the clearest examples in this corpus of memory as executable capability rather than text history. That strength also raises a larger integrity risk. A retrieved skill carries authority to act. If its preconditions are no longer true, or if a dependency has changed, retrieval can convert stale knowledge directly into external side effects.

The library stores successful behavior, but “worked once” is weaker than “valid under current preconditions.” The architecture would benefit from explicit skill contracts: assumptions, required observations, effects, version information, confidence, and revocation conditions.

## What changed in my thinking

Voyager made procedural memory central to this project. It also shifted my focus from forgetting individual facts to invalidating dependent capabilities. A stale fact can mislead a plan; a stale executable skill can immediately perform the wrong action.

## Connection to this research

The proposed state model extends a Voyager-style skill entry with:

- provenance and creation evidence;
- explicit preconditions and postconditions;
- dependencies on environment facts and tool versions;
- last verification time;
- authority scope;
- invalidation and re-verification rules.

## Technical alignment relevance

- **Execution authority:** procedural memory bridges cognition and action and therefore deserves stricter controls than descriptive memory.
- **Least privilege:** a skill should receive only the tools and credentials its contract requires.
- **Memory integrity:** corrupted or poisoned skills can persist and compose into larger behaviors.
- **Goal fidelity:** an automatic curriculum may optimize exploration objectives that only approximate the user's current goal.
- **Oversight:** executable, named skills improve inspectability, but composition can obscure downstream effects.

## Open questions

1. How should an agent verify skill preconditions before reuse?
2. What dependency changes should invalidate a stored skill?
3. Can a skill be replayed safely in a sandbox before receiving real authority?
4. How should confidence decay with time, environment change, or tool-version change?
5. Can procedural memories be evaluated for policy compliance independently of task success?
