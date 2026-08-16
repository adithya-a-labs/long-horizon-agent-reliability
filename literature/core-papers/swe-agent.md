# SWE-agent: Agent–Computer Interfaces Enable Automated Software Engineering

- **Original source:** [arXiv](https://arxiv.org/abs/2405.15793) · [NeurIPS proceedings](https://proceedings.neurips.cc/paper_files/paper/2024/hash/5a7c947568c1b1328ccc5230172e1e7c-Abstract-Conference.html) · [implementation](https://github.com/SWE-agent/SWE-agent)
- **Authors:** John Yang, Carlos E. Jimenez, Alexander Wettig, Kilian Lieret, Shunyu Yao, Karthik R. Narasimhan, Ofir Press
- **Status:** Peer-reviewed primary research, NeurIPS 2024

## Research question and central hypothesis

SWE-agent asks how the interface between a language model and a computer affects autonomous software-engineering performance. Its hypothesis is that an Agent–Computer Interface designed for model capabilities and limitations can materially improve problem solving without changing the underlying model.

## Technical method and architecture

The system gives an LM a constrained set of commands for repository navigation, file inspection, editing, and test execution. The interface is designed to keep outputs concise, make locations legible, reduce context waste, and recover from malformed commands. The model iteratively inspects a repository, edits files, and executes tests.

Important design choices include:

- compact search and file-viewing commands;
- guarded editing operations with explicit line ranges;
- informative command outputs and error messages;
- history and context management;
- automatic handling or retry of some malformed actions.

## Experiments

The primary evaluation uses SWE-bench, which contains real GitHub issues and repository snapshots. HumanEvalFix is used as an additional code-repair setting. The paper compares interface variants and prior agents/models using task-resolution rates.

At publication, the authors report 12.5% pass@1 on SWE-bench and 87.7% on HumanEvalFix in their evaluated configurations. These figures are historical and model/configuration-specific; they should not be presented as current state of the art.

## Important assumptions

- Repository snapshots, tests, and issue descriptions provide enough information to judge a repair.
- Test outcomes are useful proxies for correctness.
- A single-agent edit/test loop captures the relevant software-engineering task.
- The sandbox and command interface mediate consequential actions.
- Context selection can omit detail without hiding decisive evidence.

## Limitations

Passing available tests does not establish complete semantic correctness. Long trajectories still suffer from context pressure, repeated exploration, and incorrect localization. The benchmark emphasizes issue resolution in repository snapshots rather than long-lived execution under changing external state. The current repository also warns that development has shifted to mini-SWE-agent, so implementation observations must be versioned.

## My interpretation and critique

SWE-agent provides strong evidence that reliability is partly an interface and harness problem. The action language changes what errors are possible, how detectable they are, and how easily the model can recover. However, the interface mostly constrains syntax and information flow; it does not represent epistemic status for hypotheses such as “this test failure has been fixed” or “this file is the root cause.”

The benchmark's final success signal can conceal trajectory-level hazards: unnecessary edits, policy violations, fragile fixes, or reliance on stale repository assumptions.

## What changed in my thinking

The paper weakened a purely model-centric view of agent progress. Better tools are not neutral conveniences: they restructure the agent's decision problem and failure surface. This suggests that persistent-state semantics can similarly be designed into the interface rather than left to prompting.

## Connection to this research

The proposed runtime borrows the idea of an explicit Agent–Computer Interface but adds state operations such as:

- assert an observation with provenance;
- mark a belief as provisional;
- verify or reject a claim;
- invalidate downstream assumptions;
- request scoped action authority;
- record expected and observed effects.

## Technical alignment relevance

- **Constrained execution:** a narrow command interface reduces the action space and supports mediation.
- **Least privilege:** repository and shell access can be scoped by task and operation.
- **Oversight:** concise, structured action outputs improve reviewability.
- **Policy compliance:** tests measure task success, not whether the trajectory obeyed operational policy.
- **Corrigibility:** explicit errors and reversible edits improve local correction, but only within the interface's representation.

## Open questions

1. Can interface design force explicit preconditions and expected effects for consequential edits?
2. How should repository changes invalidate prior search results and diagnoses?
3. Which trajectory properties should be evaluated in addition to final test success?
4. How much context pruning is possible before the agent loses provenance needed for recovery?
5. Can the ACI expose uncertainty without making interaction prohibitively verbose?
