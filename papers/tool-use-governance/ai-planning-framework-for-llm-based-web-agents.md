# AI Planning Framework for LLM-Based Web Agents

- **Status:** Located — [arXiv:2603.12710](https://arxiv.org/abs/2603.12710)
- **Area:** tool-use-governance
- **Authors / venue / date:** Orit Shahnovsky, Rotem Dror — arXiv (cs.AI, cs.CL), submitted 13 March 2026

## Problem
LLM web agents are black boxes: when one fails a booking or a CMS edit, you can't tell whether the plan was wrong, the execution drifted, or the task decomposition was incoherent. Success-rate-only evaluation hides all of this — two agents with similar pass rates can behave completely differently under the hood.

## Approach
The paper formalizes web tasks as sequential decision-making and maps modern agent architectures onto classical AI planning paradigms: Step-by-Step agents ≈ Breadth-First Search, Tree Search agents ≈ Best-First Tree Search, Full-Plan-in-Advance agents ≈ Depth-First Search. This taxonomy makes failure modes (context drift, bad decomposition) diagnosable in planning terms. They back it with a new dataset: 794 of 812 WebArena tasks (97.7%) manually completed by humans, recording action type and target element per step — gold trajectories, published at github.com/shahnovsky/WebArena-Human-Trajectory-Dataset. On top of it, five trajectory-quality metrics: Recovery Rate (returning to the gold path after deviating), Repetitiveness Rate, Step Success Rate, Partial Success Rate, and Element Accuracy Rate. Experiments ran two agents (Step-by-Step and Full-Plan-in-Advance) on GPT-4o-mini (temp 1.0, top-p 0.95).

## Key findings
- Overall success: Step-by-Step 38.41% vs Full-Plan-in-Advance 36.29% — nearly tied on the headline number.
- But Step Success Rate diverges hard: 82% vs 58% — the step-by-step agent tracks human gold trajectories far more closely.
- Full-Plan-in-Advance wins Element Accuracy (89% vs 82.45%) — when it acts, it hits the right elements.
- Recovery Rate is low for both (36% vs 31%): once off the gold path, agents mostly don't get back on.
- Repetitiveness is high for both (~79–81%): redundant actions are pervasive regardless of architecture.

## Limitations & open questions
No formal limitations section; the authors concede the Full-Plan-in-Advance agent "was not optimized for performance" and is a proof of concept. The Tree Search paradigm is in the taxonomy but not experimentally evaluated. Everything runs on one small model (GPT-4o-mini), so architecture-vs-model effects are confounded; a skeptic would ask whether the gaps hold on frontier models, and whether human gold trajectories are the right reference when agents find valid alternate paths (which the Recovery metric would penalize).

## Why builders should care
Stop evaluating web agents on pass/fail alone — near-identical success rates masked a 24-point gap in step-level fidelity here. If you need auditable, human-legible trajectories (governance, approval gates), prefer step-by-step architectures; if you need precise element targeting on well-specified flows, upfront planning helps. The low recovery rates say invest in explicit re-planning/recovery logic, not just better initial plans.

## Related companies in this landscape
- **Browserbase** — hosted browser infra where these agent trajectories actually execute; trajectory-level metrics are the natural QA layer on top.
- **Arize / Braintrust / Weights & Biases** — agent tracing and eval platforms; the five metrics are directly implementable as trajectory evals.
- **Hamming AI / Meticulous** — automated agent testing; human gold trajectories are exactly the reference data such tools need.
- **Apify / Bright Data / Oxylabs** — web automation and data-extraction stacks whose reliability this paper's diagnosis framework targets.
- **LangChain / LlamaIndex** — ship the planner abstractions (ReAct-style step-by-step vs plan-and-execute) the taxonomy formalizes; the results argue for exposing both and measuring per-step.
- **The Browser Company / Cua / Yutori** — consumer/computer-use web agents where low recovery rate is the user-facing failure mode.

## Sources
- https://arxiv.org/abs/2603.12710
- https://arxiv.org/html/2603.12710v1
- https://arxiv.org/pdf/2603.12710
