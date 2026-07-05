# SWE Agents — Paper Notes

What this area studies: whether coding agents actually do software engineering, and how we'd know. The nine papers here are almost all about the measurement gap — SWE-bench-style single-issue bug-fix scores sit in the 70s, while every attempt to test something closer to real work (features, releases, iteration, production prompts, merged PRs) knocks agents down 3–7x. The recurring positive finding is the same across papers: verification discipline (running tests, checking work, gating merges) moves outcomes more than model choice does.

## How to read this area

Start with the two position/argument papers, then pick benchmarks by which axis of realism you care about:

1. **[Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](position-coding-benchmarks-are-misaligned-with-agentic-soft.md)** — the frame for everything else: harness choice alone swings Opus 4.6 from 58% to 79.8% on identical tasks, so leaderboard deltas under ~10 points are noise. Read first.
2. **[SWE-EVO](swe-evo-benchmarking-coding-agents-in-long-horizon-software.md)** — the cleanest "reality discount" number: best frontier result 25% on release-level evolution vs. ~73% on SWE-Bench Verified, with spec misinterpretation (not tooling) as the dominant failure.
3. **[Effective Strategies for Asynchronous Multi-Agent Collaboration](effective-strategies-for-asynchronous-multi-agent-collaborat.md)** — the one paper here that's a playbook rather than a critique: git worktrees + test-gated merges make parallel agents work; prompt-level isolation demonstrably fails.

The remaining benchmarks differentiate on *which* dimension of realism they stretch: task size (FeatureBench), task breadth and language (OmniCode), time/iteration (SlopCodeBench, SWE-EVO), prompt realism (ProdCodeBench), and post-merge social reality (the MSR task-level study). The NTNU reproducibility paper is the methods-hygiene companion to the Tessl position paper.

## Papers

| Paper | One-line finding | Why you'd care |
|---|---|---|
| [Position: Coding Benchmarks Are Misaligned (Tessl)](position-coding-benchmarks-are-misaligned-with-agentic-soft.md) | Harness, context, and verifiers move scores as much as a model generation; single-reference grading and leaked/weak tests undermine SWE-bench validity | Stop model-shopping on small leaderboard deltas; tune your harness first. Note the authors sell spec-driven dev — the position is self-serving but well-evidenced |
| [SWE-EVO](swe-evo-benchmarking-coding-agents-in-long-horizon-software.md) | Release-level, multi-file evolution collapses frontier agents to ≤25% resolved; >60% of strong-model failures are spec misreading | The ~3x discount to apply to any SWE-bench claim; their regression-gated Fix Rate metric is directly copyable |
| [FeatureBench](featurebench-benchmarking-agentic-coding-for-complex-featur.md) | Whole-feature development: Opus 4.5 drops from 74.4% (SWE-bench) to 11%; giving agents explicit signatures/tests is worth tens of points | Agents can code to a spec but can't infer one — the strongest evidence for spec-first and test-first agent workflows |
| [SlopCodeBench](slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) | Agents iterating on their own code accumulate erosion/verbosity 5–6.6x faster than human git histories; prompting shifts the starting point, not the slope | Quantifies "slop debt" and gives an early-warning signal: cost-per-iteration rising while diff size shrinks |
| [ProdCodeBench (Meta)](prodcodebench-a-production-derived-benchmark-for-evaluating.md) | On verbatim production prompts, the strongest correlate of solving is using work-validation tools — Claude models validate more and win | Evaluate on your users' actual prompts, and make test-running cheap and default in your harness |
| [OmniCode](omnicode-a-benchmark-for-evaluating-software-engineering-ag.md) | Beyond Python bug-fixing, agents crater: ≤25% on C++ test generation; style-only edits break code | Test generation and review-response are the weakest agent skills; multi-language support is a real differentiator |
| [Task-Level Evaluation of AI Agents in OSS (MSR '26)](a-task-level-evaluation-of-ai-agents-in-open-source-software.md) | Across 33.5k real PRs, merge rate, review friction, and commit-history quality are independent axes — the most-merged agent (Codex, 0.83) writes the worst commit messages | Pick agents per lifecycle dimension, not per leaderboard; 90.6% of AI PRs get zero review comments, which is a red flag not a win |
| [Async Multi-Agent Collaboration (OpenHands)](effective-strategies-for-asynchronous-multi-agent-collaborat.md) | Worktree isolation + test-gated merges beat single-agent by up to 26.7pp; soft isolation scores *below* single-agent; 2–4 agents is the ceiling | The concrete recipe for parallel coding agents — an accuracy play at ~3x cost, not a latency play |
| [Reproducible, Explainable, Effective Evaluations (NTNU)](reproducible-explainable-and-effective-evaluations-of-agen.md) | Of 18 agentic-SE papers, only 1 compared against an agentic SOTA baseline and only 3 reported exact model versions | The checklist for reading vendor eval claims: demand model version, temperature, prompts, and trajectory logs |

## Cross-cutting takeaways

- **The discount factor is real and consistent:** bug-fix benchmarks overstate feature/evolution capability ~3–7x (SWE-EVO, FeatureBench), and real-world acceptance rates (35–64%) lag headline scores (>70%) (Tessl position).
- **Verification beats scale, four ways:** validation-tool use predicts solving (ProdCodeBench), test-gated merges make multi-agent work (async collaboration), verification discipline explains why smaller models beat larger ones on some runs (NTNU), and regression gates are the fix for agents breaking code while "tidying" it (OmniCode).
- **Specs are the bottleneck, not tools:** patch-apply rates are 95–100% while resolve rates are ~25% (SWE-EVO); providing signatures/tests swings results by 50 points (FeatureBench).
- **Long horizons compound problems:** quality decays as agents build on their own output, and prompting alone doesn't bend the curve (SlopCodeBench).

## Maps to company categories

- [`../../companies/coding-agents/`](../../companies/coding-agents/) — the vendors these benchmarks stress-test. Cognition, Sourcegraph, and Qodo appear in nearly every paper's implications; Greptile and Builder.io in the review-agent findings. The 58→79.8% harness spread (Tessl position) is this category's core pitch that the harness is the product.
- [`../../companies/evals-observability/`](../../companies/evals-observability/) — Braintrust, Arize, Comet, Fiddler, W&B: every paper here is an argument for production-derived, component-level, trajectory-logged evals over leaderboard scores. The NTNU TAR-trajectory proposal is essentially this category's product spec.
- [`../../companies/swe-infrastructure/`](../../companies/swe-infrastructure/) — Sonar (SlopCodeBench's thesis as a product: quality gates against slop), Meticulous (regression safety), Daytona and Coder (isolated environments — CAID shows worktree-level isolation is load-bearing), Warp and Zed (harness builders).
- [`../../companies/agent-orchestration/`](../../companies/agent-orchestration/) — Temporal and Inngest map to the async paper's dependency-graph scheduling layer; LangChain/LlamaIndex to trajectory capture.
- [`../../companies/models-inference/`](../../companies/models-inference/) — OpenAI, Google DeepMind, Amazon AGI Labs: the labs whose headline SWE-bench claims the Tessl position says conflate model with scaffold; MiniMax and Z.ai models appear as evaluated agents in SlopCodeBench and the async-collaboration paper.
- [`../../companies/cloud-compute/`](../../companies/cloud-compute/) — Docker and Modal: FeatureBench's 3,825 executable environments make sandboxed eval infra a first-class dependency; Microsoft/GitHub's Copilot is the acceptance-rate laggard in the MSR study.

## Open questions the area hasn't answered

- Does partial progress count? Binary resolved-rates may undercount economically useful half-done features (FeatureBench, SWE-EVO both concede this).
- Can anything bend the degradation slope — refactoring passes, repo-level memory — or only shift its intercept? (SlopCodeBench tested prompting only.)
- Who enforces eval hygiene? Both position papers propose disclosure/metadata norms with no enforcement mechanism.
- Almost everything here is Python; OmniCode's Java/C++ results suggest the language gap is large and mostly unmeasured.
