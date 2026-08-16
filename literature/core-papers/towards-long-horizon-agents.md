# Towards Long-Horizon Agents: A Survey

- **Original source:** [Preprints.org](https://www.preprints.org/manuscript/202607.1328)
- **Authors:** Guanting Dong, Xiaoshuai Song, Yuyang Hu, Jiajie Jin, Chenghao Zhang, Yifei Chen, Xiaoxi Li, Huaying Yuan, Xinyu Yang, Tongyu Wen, Jiejun Tan, Hongjin Qian, Shijue Huang, Junting Lu, Zhenyu Li, Wanjun Zhong, Yutao Zhu, Tat-Seng Chua, Zhicheng Dou, Ji-Rong Wen
- **Status:** Survey preprint, posted July 2026; explicitly not peer reviewed at the time of this audit

## Research question and central thesis

The survey asks how long-horizon agency should be defined and how progress should be attributed between the foundation model and its surrounding runtime. Its central thesis is that long-horizon competence belongs to a coupled model–harness system rather than to the model alone.

## Technical framing

The survey formalizes an agent as a base policy coupled to a harness:

`Agent = πθ ⊕ H`

The harness assembles context, mediates tools, retains memory, orchestrates control flow, and applies verification. The environment is treated as partially observable, and the long-horizon trajectory is characterized by interdependent decisions rather than duration alone.

The paper organizes the field through six perspectives:

- Foundation
- Evolution
- Harness
- Optimization
- Application
- Frontier

It also distinguishes three nested horizon/capability levels: intra-context reasoning, cross-context memory, and cross-task experience. The historical narrative moves from prompt-level control to context engineering and then runtime systems.

## Evidence and synthesis

This is a broad survey, not an intervention study. It synthesizes papers, official documentation, open-source implementations, and specifications. The paper highlights goal drift and compounding error, context pressure, sparse delayed reward, and irreversible actions as recurring long-horizon difficulties. It maps harness components—workflows, memory, tools, orchestration, hooks, and verification—against model optimization and application areas.

## Important assumptions

- Logical dependency length is a better defining property of horizon than elapsed time alone.
- Model and harness contributions can be meaningfully separated even though they interact.
- Engineering documentation and implementations can inform a field taxonomy alongside scholarly papers.
- The proposed H1–H3/C1–C3 levels cover the most important forms of horizon extension.

## Limitations

The survey is extremely recent and not peer reviewed. It combines sources with different evidence strength and does not report a systematic-review protocol comparable to a formal meta-analysis. Its breadth limits close scrutiny of every cited result. Frontier scaling and product capability statements can become outdated quickly.

## My interpretation and critique

The model-plus-harness formalization gives this repository a clearer unit of analysis. It supports studying state, authority, and recovery as runtime properties. However, “harness” is broad enough to become explanatory shorthand. A useful research program must identify which harness mechanisms cause which improvements under controlled conditions.

The survey treats verification as one component among many. I place epistemic transitions and verification closer to the center because every other mechanism—planning, memory, tools, and recovery—depends on what the runtime treats as true.

## What changed in my thinking

This survey made me state the research object more precisely: not “the reliability of an LLM,” but the reliability of a coupled policy, harness, tool environment, and persisted state. It also reduced my confidence in claims that longer context alone addresses long-horizon reliability.

## Connection to this research

The repository narrows the survey's broad landscape to a specific systems question: how the harness should represent, verify, invalidate, and recover execution state when observations are partial and actions have side effects.

## Technical alignment relevance

- **Goal fidelity:** long dependency chains create opportunities for gradual objective drift.
- **Controllability:** externalized harness mechanisms can pause, constrain, or redirect execution.
- **Oversight:** runtime traces and checkpoints create intervention surfaces unavailable inside model weights.
- **Irreversibility:** growing horizons increase the importance of authority gates and recoverable operations.
- **Attribution:** separating model and harness changes is necessary to know which safety mechanism produced an improvement.

## Open questions

1. Which harness mechanisms transfer across domains and model families?
2. How should reliability scale with logical dependency depth rather than elapsed time?
3. Can harness interventions be evaluated independently from stronger base models?
4. When should a capability remain externalized for controllability rather than be internalized into policy?
5. What state representation best supports verification and recovery across context and session boundaries?
