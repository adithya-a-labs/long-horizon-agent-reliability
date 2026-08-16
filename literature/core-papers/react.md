# ReAct: Synergizing Reasoning and Acting in Language Models

- **Original source:** [arXiv](https://arxiv.org/abs/2210.03629) · [project page](https://react-lm.github.io/)
- **Authors:** Shunyu Yao, Jeffrey Zhao, Dian Yu, Nan Du, Izhak Shafran, Karthik Narasimhan, Yuan Cao
- **Status:** Peer-reviewed primary research, ICLR 2023

## Research question and central hypothesis

The paper asks whether language-model reasoning traces and environment actions should be generated in one interleaved trajectory. Its central hypothesis is that reasoning helps an agent plan, track, and revise, while actions ground that reasoning in external observations; each compensates for weaknesses in the other.

## Technical method

ReAct prompts a language model to emit a sequence containing free-form reasoning traces, actions from an environment-specific action space, and observations returned by the environment. The model is not given a separately trained controller. Few-shot demonstrations teach both the trajectory format and the available action vocabulary.

Two task families are used:

- **Knowledge-intensive question answering and fact verification:** the agent searches and reads Wikipedia through a small action interface.
- **Interactive decision-making:** the agent operates in ALFWorld text environments and WebShop's simulated shopping environment.

The architecture remains deliberately minimal: the language model produces both cognitive traces and actions; a deterministic wrapper parses actions, invokes the environment, and appends observations to context.

## Experiments

The paper evaluates HotpotQA, FEVER, ALFWorld, and WebShop. It compares ReAct with standard prompting, chain-of-thought variants, action-only agents, and task-specific methods. PaLM-540B is used for the knowledge tasks; GPT-3-family code models are used for interactive tasks.

Author-reported findings include:

- On interactive tasks, interleaving reasoning with actions substantially improves success over action-only prompting.
- On knowledge tasks, ReAct makes its information-gathering trajectory inspectable and reduces some hallucination and error-propagation patterns, but pure chain-of-thought can outperform ReAct in some settings.
- Combining ReAct with chain-of-thought self-consistency performs better than either alone on the knowledge tasks tested.

The paper also provides qualitative trajectory analysis: reasoning helps determine what to retrieve and how to update a plan, while observations can correct unsupported internal reasoning.

## Important assumptions

- The environment exposes a small, legible, synchronous action space.
- Tool results are appended faithfully and fit within the context window.
- Few-shot trajectories are representative enough to teach control behavior.
- The model can distinguish its own reasoning from external observations because the prompt format labels them.
- Tool invocation is mediated by a wrapper; the model does not directly mutate external state.

## Limitations

The paper notes that prompting is sensitive to demonstrations and that more complex action spaces require longer examples, consuming context. ReAct can still produce invalid actions, repeat unproductive steps, or reason incorrectly. The environments do not require durable execution across process restarts, long delays, concurrent actors, or changing external state.

## My interpretation and critique

ReAct is best understood as an interface pattern for coupling reasoning to evidence, not as a solution to long-horizon state integrity. Its transcript is an append-only conversational record. It does not assign typed epistemic status to observations, model inferences, plans, or verified facts. An observation can become stale while remaining indistinguishable from a current fact in the prompt.

The model also generates the next action and the rationale for that action in the same channel. This aids interpretability, but it does not create independent execution authority or verification. The wrapper checks syntax, not whether the action is justified by current external state.

## What changed in my thinking

This paper moved my starting point away from viewing tool use as a sequence of isolated API calls. Reliability depends on the closed loop between internal reasoning and returned evidence. It also clarified that a visible trajectory is not the same as a trustworthy state representation: the trajectory records what was said and observed, but not which claims remain valid.

## Connection to this research

ReAct supplies the foundational loop for the proposed runtime:

`reason → propose action → execute → observe → update`

This repository extends the loop by asking what must happen between observation and update: provenance capture, verification, freshness checks, authority checks, dependency tracking, and invalidation.

## Technical alignment relevance

- **Belief versus reality:** observations can correct reasoning, but the architecture does not formally separate believed from verified state.
- **Action authority:** the model proposes actions through a bounded interface, an early form of constrained execution.
- **Oversight:** explicit trajectories expose intermediate steps, but oversight quality depends on whether traces are faithful and sufficiently complete.
- **Goal fidelity:** long trajectories can drift even when each local action is syntactically valid.

## Open questions

1. Should an observation enter memory as evidence, as a belief update, or both?
2. How should a ReAct-style agent represent that an old observation is stale?
3. Can action proposals be evaluated against a typed state graph before execution?
4. When an observation contradicts memory, which dependent plans and actions should be invalidated?
5. What parts of the reasoning trace are necessary for audit, and what parts are unreliable rationalization?
