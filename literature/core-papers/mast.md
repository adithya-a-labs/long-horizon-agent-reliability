# Why Do Multi-Agent LLM Systems Fail?

- **Original source:** [arXiv PDF](https://arxiv.org/pdf/2503.13657) · [NeurIPS proceedings](https://proceedings.neurips.cc/paper_files/paper/2025/hash/b1041e52d3be19f0a9bc491657488e4a-Abstract-Datasets_and_Benchmarks_Track.html)
- **Authors:** Mert Cemri, Melissa Z. Pan, Shuyi Yang, Lakshya A. Agrawal, Bhavya Chopra, Rishabh Tiwari, Kurt Keutzer, Aditya Parameswaran, Dan Klein, Kannan Ramchandran, Matei A. Zaharia, Joseph E. Gonzalez, Ion Stoica
- **Status:** Peer-reviewed dataset and analysis paper, NeurIPS 2025 Datasets and Benchmarks Track

## Research question and central hypothesis

The paper asks why multi-agent LLM systems fail across tasks and frameworks, and whether failures can be described using a reusable taxonomy rather than framework-specific anecdotes. The motivating hypothesis is that system-level traces reveal recurring coordination and verification failures that final-answer accuracy alone obscures.

## Technical method

The authors construct MAST-Data from 1,642 execution traces spanning seven multi-agent frameworks. Human annotators examine failed trajectories and develop a taxonomy of 14 failure modes grouped into three broad categories:

- system-design failures;
- inter-agent misalignment or coordination failures;
- task-verification and termination failures.

The study uses a structured annotation protocol and reports inter-annotator agreement of approximately κ = 0.88. It analyzes how failure modes distribute across frameworks and tasks and whether multiple failures co-occur in a trace.

## Experiments and findings

This is primarily a diagnostic dataset/analysis rather than an intervention study. The authors show that:

- many failures are trace-level and cannot be explained solely by the final answer;
- coordination, role specification, information sharing, and verification contribute distinct failure modes;
- failures can compound, with an earlier coordination or reasoning problem producing later verification or termination errors;
- no single framework eliminates the observed categories.

The paper's value is taxonomic and empirical: it organizes observed failures across heterogeneous systems. It does not establish the effectiveness of a specific recovery architecture.

## Important assumptions

- The sampled tasks and seven frameworks adequately expose representative multi-agent failures.
- Annotators can infer failure modes from available traces.
- The taxonomy granularity is stable enough for cross-framework use.
- Recorded traces include the information required to identify causal failures rather than only their symptoms.

## Limitations

The dataset is conditioned on selected frameworks, tasks, trace formats, and model versions. Human labels can identify plausible failure modes without proving causal attribution. Multi-agent communication failures do not map perfectly onto single-agent persistent-state failures. The taxonomy may need revision as architectures and tools change.

## My interpretation and critique

MAST is important because it treats reliability as a trajectory and system property. Its categories support the idea that final task success is too coarse. However, taxonomic labels should not be mistaken for mechanistic explanations. “Failure to verify” names a failure class; it does not tell us what state representation or verifier architecture would have prevented it.

The same trace may support multiple causal stories. A verifier may fail because it received incomplete state, because the evidence was stale, because it shared the actor's misconception, or because termination rules rewarded speed over certainty.

## What changed in my thinking

The paper made failure composition more central to my research. I previously framed state divergence mainly as a memory problem. MAST suggests that divergence is also produced by role boundaries, communication protocols, termination conditions, and verification design.

## Connection to this research

This repository adapts the taxonomy into a state-centric diagnostic sequence:

1. Where did an unsupported or stale state enter?
2. Which agents, plans, or actions depended on it?
3. What verification opportunity was missed?
4. Why did termination or escalation rules permit continuation?
5. What is the smallest safe recovery boundary?

## Technical alignment relevance

- **Oversight:** trace-level failures show why outcome-only evaluation misses unsafe intermediate behavior.
- **Verifier reliability:** verification can fail independently from planning and action.
- **Goal fidelity:** role and communication failures can transform or lose the original objective.
- **Policy compliance:** a system may produce a correct answer through an impermissible trajectory.
- **Error propagation:** one agent's unsupported claim can become another agent's accepted premise.

## Open questions

1. Can the MAST taxonomy be operationalized as automatic state-transition checks?
2. Which failure modes are detectable before task failure?
3. How often do apparently independent agents share correlated model errors?
4. Can provenance links distinguish causal failure propagation from coincidental co-occurrence?
5. What recovery policies correspond to each failure category?
