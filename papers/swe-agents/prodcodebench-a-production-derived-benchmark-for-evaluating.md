# ProdCodeBench: A Production-Derived Benchmark for Evaluating AI Coding Agents

- **Status:** Located — [arXiv:2604.01527](https://arxiv.org/abs/2604.01527)
- **Area:** swe-agents
- **Authors / venue / date:** Smriti Jha, Matteo Paltenghi, Chandra Maddila, Vijayaraghavan Murali, Shubham Ugare, Satish Chandra (Meta). arXiv, submitted April 2, 2026 (v3 May 10, 2026).

## Problem
Benchmarks like SWE-bench are built from GitHub issue descriptions — text written for humans — while real coding-agent usage consists of terse, verbatim prompts developers type into an assistant, against monorepo codebases and language mixes that public benchmarks don't reflect. Scores on issue-derived benchmarks therefore may not predict how an agent performs on actual production traffic.

## Approach
The team mines real developer–agent sessions from a production coding assistant at Meta. Each retained sample is a verbatim developer prompt, the committed code change (with AI-provenance tracking), and fail-to-pass tests. The curation pipeline: filter to single-turn interactions → map prompts to committed diffs → remove the solution diff from the repo to prevent leakage → LLM classifiers for testability → agentic test-relevance validation → multi-run stability checks to exclude flaky tests → classify tests as fail-to-pass (F2P) vs. pass-to-pass (P2P). Result: a few hundred instances across seven programming languages; ~75% of tasks have at least one F2P test, the rest rely on P2P only.

## Key findings
- Solve rates across four frontier models range from **53.2% to 72.2%**; Claude Opus tops at 72.2% (per the HTML version; exact per-model breakdown for the other models is not fully enumerated in what I could fetch — treat mid-table ordering as inferred).
- The strongest behavioral correlate of success: **use of work-validation tools** (running tests, checking for errors). Claude-family models validated their work at higher rates than GPT Codex and solved more tasks.
- ~65% of retained diffs are 100% AI-authored, which the authors flag as a self-consistency risk: the benchmark partly measures whether an agent can reproduce a solution its own model family already produced.

## Limitations & open questions
Authors concede: a few hundred instances is too small for RL training; single-turn filtering excludes iterative-refinement work; the ~70% ceiling limits discrimination between frontier models; and the rolling design (re-curated against a moving monorepo) breaks longitudinal comparability. A skeptic adds: it's Meta-internal data (Hack-heavy monorepo), so external replication is impossible, and the AI-provenance contamination cuts against the "production-realistic" claim.

## Why builders should care
If you ship a coding agent, evaluate it on your users' actual prompts, not proxy benchmarks — prompt style and language mix materially change difficulty. And bias your agent harness toward verification: agents that run tests and check errors before finishing solve measurably more tasks, so make validation tools cheap and default.

## Related companies in this landscape
- **Qodo, Sonar, Meticulous** — the "validation tools drive solve rates" finding directly validates test-generation/quality-gate products in the agent loop.
- **Cognition, Factory, OpenHands, Cline, poolside** — coding-agent vendors whose real gap between benchmark and production traffic this paper quantifies.
- **Braintrust, Arize, Weights & Biases** — eval platforms; the curation pipeline (LLM testability classifiers, flake-stability checks) is a template for customer-derived evals.
- **Sourcegraph, Greptile** — monorepo-scale code context is exactly the setting the paper says public benchmarks miss.
- **Datacurve, Surge AI** — production-derived task curation as a data product.

## Sources
- https://arxiv.org/abs/2604.01527
- https://arxiv.org/html/2604.01527v1
