# Reflexion: Language Agents with Verbal Reinforcement Learning

- **Original source:** [arXiv](https://arxiv.org/abs/2303.11366) · [NeurIPS proceedings](https://papers.neurips.cc/paper_files/paper/2023/hash/1b44b878bb782e6954cd888628510e90-Abstract-Conference.html)
- **Authors:** Noah Shinn, Federico Cassano, Ashwin Gopinath, Karthik Narasimhan, Shunyu Yao
- **Status:** Peer-reviewed primary research, NeurIPS 2023

## Research question and central hypothesis

Reflexion asks whether an agent can improve across attempts without updating model weights. The central hypothesis is that language feedback derived from task outcomes can be stored as episodic memory and used to alter subsequent behavior.

## Technical method

The framework separates three roles:

- an **Actor** generates a trajectory;
- an **Evaluator** scores the result using environment feedback, tests, heuristics, or model judgment;
- a **Self-Reflection** component converts the trajectory and feedback into a concise verbal lesson.

The reflection is placed in an episodic memory buffer and included in later attempts. This is “verbal reinforcement” because improvement occurs through context rather than parameter updates. The implementation uses variants of ReAct and chain-of-thought depending on the task.

## Experiments

The evaluation spans:

- sequential decision-making in ALFWorld;
- programming on HumanEval, using compiler/test feedback;
- reasoning and question answering, including HotpotQA-style tasks.

Baselines include non-reflective prompting and task-specific actor variants. Metrics are task success, pass@1 for code, and answer correctness. The authors report strong improvements across domains; in ALFWorld, ReAct with Reflexion solves 130 of 134 tasks in the evaluated setup. The programming experiments show that test-driven feedback and stored reflections can improve subsequent solutions without fine-tuning.

## Important assumptions

- The evaluator's feedback is informative enough to distinguish productive from misleading trajectories.
- A concise natural-language reflection preserves the causal lesson needed on the next attempt.
- Reattempting the same or a closely related task is permitted.
- The memory buffer remains small enough to fit within context and relevant enough not to distract the actor.
- Failures can be repaired through behavioral changes expressible in language.

## Limitations

The authors identify dependence on self-evaluation quality, the possibility of local minima, and finite-context memory. Programming results depend on available tests: weak tests provide weak or misleading feedback. Reflexion does not guarantee that an explanation of failure is causally correct, nor does it protect the memory buffer from inaccurate reflections.

## My interpretation and critique

Reflexion demonstrates that memory can influence policy without modifying weights, but it also creates an epistemic hazard: a reflection is a model-generated interpretation of evidence, not the evidence itself. If stored with the same authority as a verified observation, an incorrect diagnosis can persist and bias later behavior.

The most reliable version of the method appears when external feedback is discriminating and difficult for the actor to manipulate—for example, hidden tests or deterministic environment success. Model-judged feedback creates a tighter correlation between actor and verifier errors.

## What changed in my thinking

The paper changed my view of “memory quality” from a retrieval-only problem to a write-authority problem. The critical question is not merely whether an agent remembers a lesson, but whether the lesson was justified, what evidence produced it, and when it should be revised or invalidated.

## Connection to this research

Reflexion motivates separating:

1. raw trajectory and external feedback;
2. model-generated diagnosis;
3. proposed lesson;
4. verified or provisionally accepted memory update.

The proposed epistemic-state model treats these as different objects with different authority and provenance.

## Technical alignment relevance

- **Verifier reliability:** correlated actor/evaluator errors can reinforce a false lesson.
- **Memory integrity:** erroneous reflections may become durable behavioral instructions.
- **Corrigibility:** a useful memory system must make stored lessons revisable when contrary evidence arrives.
- **Policy compliance versus task success:** a reflection that improves task reward may still encourage prohibited shortcuts unless the evaluator checks policy separately.

## Open questions

1. What evidence threshold should permit a reflection to become durable memory?
2. Can reflections retain pointers to the observations and tests that justified them?
3. How should contradictory reflections be reconciled?
4. Should actor, evaluator, and memory writer use independent models or mechanisms?
5. How can a system detect that an old reflection no longer applies after the environment changes?
