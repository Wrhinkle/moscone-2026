# SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution

- **Status:** Located — [arXiv:2512.18470](https://arxiv.org/abs/2512.18470) (published title adds "Scenarios"; also on [OpenReview](https://openreview.net/forum?id=SCpCfeSLtn))
- **Area:** swe-agents
- **Authors / venue / date:** Tue Le, Minh V. T. Thai, Dung Nguyen Manh, Huy Phan Nhat, Nghi D. Q. Bui — arXiv, submitted 2025-12-20 (v6 revised 2026-05-22)

## Problem
SWE-Bench-style benchmarks test single-issue fixes: one bug, one small patch. Real software work is version-to-version evolution — implementing a release's worth of interdependent features across many files without breaking what already works. Existing scores wildly overstate agent readiness for that job.

## Approach
A benchmark of 48 tasks built from seven mature open-source Python repos (scikit-learn, pydantic, dask, dvc, and three others). Each task's spec is derived from official release notes between consecutive version tags, augmented with linked PR/issue content — a high-level software requirement specification rather than a single issue. Tasks average ~21 files modified and are validated against test suites averaging ~874 tests. Construction pipeline: repo selection from SWE-bench resources → filter candidates whose base commit matches a version tag → execution-based validation requiring at least one FAIL_TO_PASS test. Scoring: binary **Resolved Rate** (all FAIL_TO_PASS + PASS_TO_PASS pass), plus a novel **Fix Rate** — fraction of initially-failing tests fixed, zeroed out if any regression is introduced.

## Key findings
- Best result: GPT-5.4 with OpenHands resolves only **25.00%**, versus **72.80%** for GPT-5.2 on SWE-Bench Verified — roughly a 3x collapse when horizon lengthens.
- Frontier models cluster tightly: gpt-5.2 18.75–22.92%, deepseek-v3p2 20.83–23.40%, kimi-k2p5 22.92–25.00% (OpenHands vs. SWE-agent scaffolds); 18 models across 5 providers tested.
- Patch apply rates are 95–100%, so failures are about *what* to build, not tooling mechanics.
- For strong GPT-series models, over 60% of failures are instruction-following — misreading nuanced release notes — not tool-use errors. Weaker/open models fail more on implementation and syntax.
- Instances with more linked PRs are empirically harder; stronger models adaptively spend more turns on hard instances, weaker ones don't.

## Limitations & open questions
Authors concede: Python-only; release notes miss security/refactoring work; only 48 instances (low statistical power); public-repo contamination risk; Fix Rate weighs all tests equally. A skeptic adds: release-note-derived SRS is still tidier than real backlog specs, and scaffold defaults (OpenHands, SWE-agent) may undersell purpose-built long-horizon harnesses.

## Why builders should care
Don't extrapolate SWE-Bench Verified numbers to multi-file feature work — expect ~3x worse. Since the dominant failure mode is spec misinterpretation, invest in spec decomposition, plan review gates, and regression-aware partial-credit evals (Fix Rate is copyable) before investing in more tools.

## Related companies in this landscape
- **OpenHands** (Bronze sponsor) — its scaffold is the benchmark's primary harness; results directly measure its long-horizon ceiling.
- **Cognition** — Devin's pitch is exactly multi-file, long-horizon autonomy; SWE-EVO quantifies how hard that claim is.
- **Factory** — sells "agentic software development" for enterprise codebases; this is the benchmark for its core workload.
- **Qodo / Greptile / Sourcegraph** — code-review and codebase-context products address the multi-file coordination gap the paper exposes.
- **Braintrust / Arize** — eval platforms; Fix Rate-style partial-credit, regression-gated metrics are what customers should be running.
- **Tessl / Cline / poolside** — spec-driven and agentic coding vendors whose value hinges on closing the instruction-following failure mode.

## Sources
- https://arxiv.org/abs/2512.18470
- https://arxiv.org/html/2512.18470v5
- https://openreview.net/forum?id=SCpCfeSLtn
- https://huggingface.co/papers/2512.18470
