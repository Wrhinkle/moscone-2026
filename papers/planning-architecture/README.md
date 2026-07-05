# Planning & Architecture

Papers on the step *before* the code gets written: how requirements turn into specs, plans, and architecture, and whether agents actually honor any of it once they start executing. The through-line across all six notes is that the binding constraint on agentic software work is upstream of codegen. Issue text is underspecified, plans are advisory and drift, prompts silently make architectural decisions nobody reviews, and end-to-end pass/fail evals can't tell you which stage failed. Every paper here is some version of "invest in the spec/plan/architecture layer and the ability to audit it."

## How to read this area

Start with **From Plan to Action**. It is the largest empirical study (16,991 trajectories) and establishes the area's core fact: agents drift from plans by default, and a bad plan is worse than none. Pair it with **REAgent**, which shows the single biggest resolve-rate lever is restructuring the task spec itself; better tooling moves the needle less. Then read **One Developer Is All You Need** for the production-scale existence proof that spec-driven, role-partitioned agent teams work in a regulated brownfield enterprise.

The remaining three differentiate on altitude: **Architecture Without Architects** and **MAAD** sit above the plan at the system-design layer (the first diagnoses the problem, "vibe architecting"; the second proposes the agentic fix), while **Architecture-Aware Evaluation Metrics** is the measurement companion, a position paper on scoring agents per-component instead of end-to-end. Note the evidence spread: two large empirical studies, one production case study, one demo-backed analytical paper, one system paper with soft baselines, and one early-stage vision paper with no results yet.

## Papers

| Paper | Core finding | Evidence strength |
|---|---|---|
| [From Plan to Action: How Well Do Agents Follow the Plan?](from-plan-to-action-how-well-do-agents-follow-the-plan.md) | Plans are advisory and agents drift; re-injecting the plan every 5 steps consistently improves resolve rates, and incomplete plans hurt more than no plan at all. | Strong: 16,991 SWE-agent trajectories, 4 models × 8 plan variants, with a contamination check on SWE-bench Pro. |
| [REAgent: Requirement-Driven LLM Agents for Software Issue Resolution](reagent-requirement-driven-llm-agents-for-software-issue-re.md) | Rewriting messy GitHub issues into structured requirements (with a machine-checkable quality score) beats better agent tooling; requirement construction alone carries most of a +9–25pt resolve gain. | Solid but scoped: 100 instances per benchmark, two mid-tier models; self-generated tests make the quality signal noisy. |
| [One Developer Is All You Need](one-developer-is-all-you-need-a-case-study-of-an-ai-augment.md) | One senior engineer orchestrating four role-specialized agents (Devin ×2, Copilot, StackSpot) under spec-driven development delivered squad-scale regulated bank work at 5.4× throughput and >85% cost reduction; undocumented legacy contracts, rather than model capability, were the bottleneck. | Compelling but N=1: single case, subject is an author, historical baseline rather than a control. |
| [Architecture Without Architects](how-ai-coding-agents-shape-software-architecture.md) | "Vibe architecting": prompt wording alone swung an identical task from 141 to 827 LoC (5.9×) with different dependency graphs; prompts and agent configs are unreviewed architectural artifacts. | Illustrative: sharp framing and a vivid demo, but single-run, single-agent, construct unvalidated. |
| [Bridging Requirements and Architecture (MAAD)](bridging-requirements-and-architecture-multi-agent-orchestr.md) | A four-agent architecture-design pipeline (Analyst/Modeler/Designer/Evaluator) with RAG over ISO standards and working/episodic/semantic memory out-designs MetaGPT; the built-in Evaluator meaningfully cuts manual review. | Moderate: 10 case studies, six practitioner interviews, and MetaGPT is a soft baseline. |
| [Toward Architecture-Aware Evaluation Metrics for LLM-Based Agents](toward-architecture-aware-evaluation-metrics-for-llm-based-a.md) | >66% of agent evals use only end-to-end success rates; a component→behavior→metric mapping (planner, tool router, memory, reflection) would make regressions attributable. | Early: CAIN 2026 position paper; the validating case study is proposed, not yet run. |

## Builder takeaways

- **Re-inject the plan.** Don't trust the system prompt to keep an executor on-plan over a long trajectory; periodic reminders are a cheap, consistently validated scaffold change (From Plan to Action).
- **Spec-construct before executing.** Add an explicit requirement-restructuring stage with a fixed schema and a quality score; route low-scoring specs back for clarification instead of running them (REAgent, One Developer).
- **Review prompts as architecture.** One clause added 330 LoC of infrastructure in the demo. Record agent prompts/configs in ADRs and set complexity thresholds that trigger human review (Architecture Without Architects).
- **Partition agents by judgment required.** Autonomous for boilerplate/infra, human-in-the-loop for core logic: the pattern that made 90% first-pass code acceptance safe in a bank (One Developer).
- **Score components, not just outcomes.** Instrument planning traces, tool routing, and memory hits separately so a regression names its culprit (Architecture-Aware Metrics, MAAD's Evaluator agent).

## Maps to company categories

- [`companies/coding-agents/`](../../companies/coding-agents/README.md): the most direct consumers are Cognition, Factory, Qodo, OpenHands, Cline, and Tessl. Plan-adherence, requirement-refinement, and spec-driven development are these vendors' theses being stress-tested (Tessl's spec-first stance gets its strongest field evidence from *One Developer* and *REAgent*; Cognition's Devin is two of that case study's four agents).
- [`companies/agent-orchestration/`](../../companies/agent-orchestration/README.md): LangChain, Mastra, Temporal, Inngest, Orkes. The "plans are advisory" finding is the academic argument for enforcing workflow structure at the orchestration layer rather than in the prompt; MAAD's revision loop is the pattern these platforms operationalize.
- [`companies/evals-observability/`](../../companies/evals-observability/README.md): Arize, Braintrust, Weights & Biases, Datadog, Hamming. Plan-compliance metrics and component-level failure attribution are eval-product roadmaps written in paper form (*From Plan to Action*, *Architecture-Aware Metrics*).
- [`companies/memory-rag-search/`](../../companies/memory-rag-search/README.md): Zep AI, Cognee, Qdrant, Neo4j. MAAD's working/episodic/semantic memory hierarchy and RAG-over-standards knowledge layer mirror these vendors' product architectures.
- [`companies/swe-infrastructure/`](../../companies/swe-infrastructure/README.md): Sonar, Unblocked, Coder, Zed, Warp. Code-quality gates and institutional-knowledge tooling are what make high-autonomy agent output safe; the "undocumented legacy contracts cause rework" finding is Unblocked's pitch verbatim.

## Open questions

- Do plan-adherence and requirement-refinement gains hold with frontier models that already do implicit clarification, or are they artifacts of mid-tier backbones (the largest model tested in *From Plan to Action* is GPT-5 mini)?
- Nobody has run the long-horizon experiment: does spec-driven agent development stay maintainable past 3 sprints, and does accumulated agent memory (MAAD's semantic tier) compound or contaminate?
- All six papers agree prompts/plans/specs need review, but who reviews them, with what tooling, and is "more scaffolding LoC" actually worse, or just different?
- Component-level eval attribution remains unvalidated against a good trace-review workflow; the one paper proposing it hasn't run its case study.
