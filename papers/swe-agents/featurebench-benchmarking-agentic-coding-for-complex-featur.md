# FeatureBench: Benchmarking Agentic Coding for Complex Feature Development

- **Status:** Located — [arXiv:2602.10975](https://arxiv.org/abs/2602.10975), ICLR 2026
- **Area:** swe-agents
- **Authors / venue / date:** Qixing Zhou, Jiacheng Zhang, Haiyang Wang, Rui Hao, Jiahe Wang, Minghao Han, Yuxue Yang, Shuzhe Wu, Feiyang Pan, Lue Fan, Dandan Tu, Zhaoxiang Zhang. ICLR 2026; arXiv submitted 2026-02-11.

## Problem
SWE-bench-style benchmarks test small bug fixes (~33 changed lines) and are near-saturated, but real feature work spans many files, commits, and PRs. There is no execution-based benchmark for building a whole feature end-to-end in a live codebase — the thing coding-agent products actually claim to do.

## Approach
A scalable, mostly-automated pipeline derives feature-level tasks from real repos: dynamic tracing during fail-to-pass test runs builds an object dependency graph; an LLM identifies the test's target objects; BFS traversal separates "extracted" feature code from code needed by pass-to-pass tests; the feature code is removed and the agent must rebuild it. Verification confirms P2P tests still pass and the ground-truth patch restores F2P tests. v1: 200 tasks and 3,825 executable environments from 24 open-source Python repos (commits after May 2022, plus log inspection to catch agents reading installed package source). Metrics: resolved rate (all F2P tests pass), passed rate (partial credit), and token I/O.

## Key findings
- Claude Opus 4.5 + Claude Code: 11.0% resolved (full set) vs. its 74.4% on SWE-bench — a ~63-point cliff.
- GPT-5.1-Codex (medium reasoning): 12.5% full / 20.0% lite. Gemini-3-Pro + OpenHands: 4.5%. DeepSeek-V3.2 + OpenHands: 5.5%.
- Tasks average ~790 lines across 15+ files — ~24x more code than SWE-bench tasks.
- Removing explicit function signatures dropped Gemini-3-Pro from 10.0% to 3.3%; showing ground-truth unit tests boosted GPT-5.1-Codex by ~50 points — agents can code to a spec but struggle to infer one.
- Failure modes: cross-file NameErrors, "lazy" hallucination of interfaces instead of reading files, long-context breakdown; all models burned >1M input tokens per task regardless of success.
- Code length correlates strongly (negatively) with pass rate; commit recency barely matters — difficulty, not contamination, drives scores. *(Inference from their correlation analysis.)*

## Limitations & open questions
Python-only, unit-test-defined "features" (a feature is whatever the traced tests cover — not UX or design work). LLM-in-the-loop task extraction may bias task selection. A skeptic would ask whether rebuilding deleted code matches greenfield feature dev, and whether resolved-rate undercounts economically useful partial progress.

## Why builders should care
Treat SWE-bench-class numbers as bug-fix numbers, not feature-dev numbers — autonomy claims should be discounted ~7x. The interface/test ablations are actionable today: giving agents explicit signatures and acceptance tests is worth tens of points, so spec-first and test-first workflows (write the contract, then let the agent fill it) are the highest-leverage harness change.

## Related companies in this landscape
- **Cognition, Factory, OpenHands, Cline, poolside** — autonomous/feature-level coding agents this benchmark directly stress-tests (OpenHands is one of the evaluated scaffolds).
- **Qodo, Tessl, Greptile, Sourcegraph** — spec-, test-, and codebase-context tooling; the signature/test ablations validate their premise.
- **Braintrust, Arize, Weights & Biases, Hamming AI** — eval platforms; execution-based, contamination-resistant task generation is the pattern to copy.
- **Daytona, E2B, Docker, Coder, Modal** — the 3,825 executable environments show sandboxed eval infra is a first-class dependency.

## Sources
- https://arxiv.org/abs/2602.10975
- https://arxiv.org/html/2602.10975v1
- https://openreview.net/forum?id=41xrZ3uGuI
