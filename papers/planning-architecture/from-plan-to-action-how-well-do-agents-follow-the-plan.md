# From Plan to Action: How Well Do Agents Follow the Plan?

- **Status:** Located — [arXiv:2604.12147](https://arxiv.org/html/2604.12147v1)
- **Area:** planning-architecture
- **Authors / venue / date:** Shuyang Liu, Saman Dehghan, Jatin Ganhotra, Martin Hirzel, Reyhaneh Jabbarvand — arXiv (cs.SE), April 13, 2026

## Problem
Coding agents are routinely handed a plan in the system prompt (reproduce → fix → validate, etc.), but nothing in the scaffold enforces it — the plan is advisory. As trajectories grow, the plan competes with an ever-longer history of tool calls and error output, and each next action is chosen from local context, not the global workflow. Nobody had measured whether agents actually follow the plan, or whether success comes from somewhere else (e.g., benchmark contamination).

## Approach
Large-scale trajectory analysis using SWE-agent: 4 models (GPT-5 mini, DeepSeek-V3, DeepSeek-R1, Devstral-small) × 8 plan variants × SWE-bench Verified (500 instances) and SWE-bench Pro (31 Python instances) = 16,991 trajectories. Plan variants: standard NRPV plan, no plan, minus reproduction, minus validation, plus regression testing, plus change summary, reordered phases, and periodic plan reminders. Adherence is scored with three phase-level metrics — Plan Phase Compliance (required phases present), Plan Order Compliance (correct sequence, via longest increasing subsequence), and Plan Phase Fidelity (no extraneous phases) — combined into an overall score by geometric mean.

## Key findings
- High-quality canonical plans substantially improve resolve rates; removing the plan reduces resolution across models (DeepSeek-R1 drops most despite having the lowest compliance scores).
- Bad plans are worse than no plan: incomplete plans (e.g., dropping the reproduction phase) hurt more than omitting the plan entirely, and prematurely adding mismatched extra phases also degrades performance.
- Periodic reminders work: re-injecting the plan every 5 steps consistently improves resolution and reduces plan violations across all models.
- Contamination signal: plan compliance drops ~13% on the less-contaminated SWE-bench Pro, with different phase patterns — suggesting some "plan following" on Verified is memorized behavior.
- 23–34 instances per model were solved *only* in the no-plan condition — plans can also suppress useful exploration (inference from the paper's overfitting discussion).
- Compliance is model-dependent: Devstral-small scores high on phase presence/order but low on fidelity (extra phases); reasoning-heavy DeepSeek-R1 is least compliant overall.

## Limitations & open questions
Authors concede phase-level abstraction misses fine-grained deviations, only 4 models / 2 benchmarks, and LLM nondeterminism (mitigated by repetition). A skeptic would ask: do results transfer to frontier models (GPT-5 mini is the largest tested), to non-SWE domains, and does the 5-step reminder cadence generalize or need tuning per context length?

## Why builders should care
If your agent architecture is "planner writes a plan, executor follows it," assume drift by default and re-inject the plan periodically rather than trusting the system prompt — it's a cheap, consistent win. And audit your plans: a wrong or incomplete plan is actively worse than none, so plan-quality evals matter as much as executor evals.

## Related companies in this landscape
- **Qodo / Factory / Cognition / OpenHands / Cline** — plan-then-execute coding agents; this paper says their enforcement (or lack) of plan adherence directly moves resolve rates.
- **Braintrust / Arize / Weights & Biases** — eval and tracing platforms; PPC/POC/PPF-style plan-adherence metrics are an obvious addition to trajectory evals they host.
- **LangChain / Mastra** — agent frameworks where periodic plan re-injection is a one-line scaffold change validated here.
- **Temporal / Inngest / Orkes** — durable workflow engines; the paper's "plans are advisory" finding is the argument for enforcing workflow structure at the orchestration layer instead of the prompt.
- **Greptile / Sourcegraph** — code-review/context tools that could check whether an agent's diff actually followed the mandated phases (e.g., reproduction and validation evidence).

## Sources
- https://arxiv.org/html/2604.12147v1
- https://www.newx.sg/paper/detail/9b8be58f-3cd1-11f1-b84c-00163e10baa7
