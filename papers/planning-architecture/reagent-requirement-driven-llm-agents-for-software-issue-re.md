# REAgent: Requirement-Driven LLM Agents for Software Issue Resolution

- **Status:** Located — arXiv preprint ([arXiv:2604.06861](https://arxiv.org/abs/2604.06861))
- **Area:** planning-architecture
- **Authors / venue / date:** Shiqi Kuang, Zhao Tian, Kaiwei Lin (Tianjin University); Chaofan Tao, Shaowei Wang, Haoli Bai, Lifeng Shang (Huawei); Junjie Chen (Tianjin University). arXiv preprint, April 8, 2026.

## Problem
SWE agents treat the raw GitHub issue text as the task spec, but issue quality is terrible — the authors note ~70% of issues lack reproduction steps, and many contain ambiguous or missing context. Existing frameworks (Agentless, Trae-agent, etc.) keep improving tools and workflows while feeding the agent the same underspecified input, so patches fail for reasons upstream of the coding step.

## Approach
REAgent inserts a requirements-engineering stage before patching, run by three agents:
1. **Requirement generation agent** explores the codebase (file retrieval + code analysis tools) and rewrites the issue into a structured "issue-oriented requirement" with 9 primary attributes (Background, Problem Overview, Steps to Reproduce, Actual/Expected Behavior, Environment, Root Cause Analysis, Solution, Additional Notes) and 17 sub-attributes.
2. **Requirement assessment agent** generates a patch from the requirement plus reproduction/regression tests, and scores requirement quality via RAS — the fraction of test scripts the patch passes.
3. **Requirement analysis agent** diagnoses low-RAS requirements into three deficiency types — Conflict, Omission, Ambiguity — and emits tailored refinement feedback. A greedy loop keeps the highest-RAS requirement each iteration.

## Key findings
- On 100 sampled instances each (DeepSeek-V3.2): 37% resolved on SWE-bench Lite vs Trae-agent 28% / Agentless 24%; 46% on SWE-bench Verified vs 35% for both; 21% on SWE-bench Pro vs 11% / 6%.
- Overall +9.17–24.83% absolute in % Resolved and +22.17–49.50% in % Applied over baselines; Wilcoxon p < 2.5×10⁻⁴.
- Even at N=1 iteration REAgent hits 25.67%, beating Agentless at N=10 (24%).
- Ablations: removing requirement modeling costs -9.50% resolved; removing assessment -7.67%; structured attributes -3.33%; refinement loop -2.33%. The requirement construction itself carries most of the gain.
- Cost: 5.13M input tokens / $1.474 per resolved issue on DeepSeek ($0.386 on Qwen-Plus) — pricier than most baselines.

## Limitations & open questions
Authors concede self-generated tests are unreliable (only ~23–46% test correctness), so RAS is a noisy quality signal; costs are high; only 100 instances per benchmark, two mid-tier models, mostly Python. A skeptic asks: do gains hold with frontier models that already do implicit issue clarification, and does the RAS loop just overfit patches to hallucinated tests?

## Why builders should care
The biggest ablation win comes from restructuring the task spec, not fancier tooling — a cheap, transferable idea. If your agent takes messy human requests (issues, tickets, job packets), add an explicit spec-construction step with a fixed attribute schema and a machine-checkable quality score before execution, and route low-scoring specs back for clarification instead of executing them.

## Related companies in this landscape
- **Tessl** — spec-driven development is literally this thesis productized; REAgent gives it benchmark evidence.
- **Qodo** — quality-first coding agents; requirement + test-based RAS scoring mirrors its test-generation-as-verification stance.
- **Factory** — requirements-to-code enterprise SWE agents; validates their upstream-spec emphasis.
- **Cognition / OpenHands / Cline** — autonomous issue-resolution agents that ingest raw issues; challenged to add a requirement-refinement stage.
- **Greptile / Sourcegraph** — codebase-context retrieval is exactly what the requirement generation agent depends on.
- **Braintrust / Arize** — RAS-style machine-scored intermediate artifacts are an evals pattern their platforms could operationalize.
- **Atlassian** — issue quality at the source (Jira) is the upstream lever this paper quantifies.

## Sources
- https://arxiv.org/abs/2604.06861
- https://arxiv.org/html/2604.06861v1
- https://arxiv.org/pdf/2604.06861
