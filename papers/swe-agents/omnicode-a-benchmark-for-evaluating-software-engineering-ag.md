# OmniCode: A Benchmark for Evaluating Software Engineering Agents

- **Status:** Located — [arXiv:2602.02262](https://arxiv.org/abs/2602.02262) (v1 Feb 2, 2026; v3 May 18, 2026); code/data at [github.com/seal-research/OmniCode](https://github.com/seal-research/OmniCode); also on [OpenReview](https://openreview.net/forum?id=VP204Aa0gH) under the title "OmniCode: A Benchmark for Evaluating Software Development Agents"
- **Area:** swe-agents
- **Authors / venue / date:** Atharv Sonwane, Eng-Shen Tu, Wei-Chung Lu, Claas Beger, Carter Larsen, Debjit Dhar, Simon Alford, Rachel Chen, Ronit Pattanayak, Tuan Anh Dang, Guohao Chen, Gloria Geng, Kevin Ellis, Saikat Dutta (Cornell-affiliated SEAL group, per repo org). arXiv preprint, cs.SE.

## Problem
Popular coding benchmarks (HumanEval, SWE-Bench) measure a narrow slice of software engineering — mostly Python bug fixing — while real SWE work includes writing tests, responding to review comments, and keeping style clean, in more languages than Python. They also suffer data leakage (tasks in training sets) and ill-defined instances.

## Approach
A benchmark of **1,794 tasks** derived from **494 base instances across 27 open-source GitHub repos**, spanning **Python, Java, and C++** and **four task categories**: bug fixing, test generation, code review fixing, and style fixing. Tasks are manually validated, and synthetically crafted or recently curated to dodge leakage; the paper contributes a framework for synthetically generating diverse tasks from limited real-world data (e.g., LLM-generated "bad patches" via perturbation with Gemma 2, Qwen2.5, Llama 3, GPT-4.1-nano, Gemini-2.5-Flash). Scoring: bug fixes must pass new tests without regressions; generated tests must pass the correct fix and fail multiple bad patches; style fixing scores `max((resolved − new)/original, 0)` using pylint/clang-tidy/PMD, zeroed if tests break.

## Key findings
- SWE-Agent-style frameworks that do well on Python bug fixing fall sharply on other categories/languages: max **25.0%** (with DeepSeek-V3.1) on C++ test generation.
- Agents perform significantly worse on C++ and Java than Python across the board; C++ tasks are the most structurally complex (file changes, edit fragmentation, lines modified).
- Style-only edits are surprisingly fragile — agents introduce new lint errors or break tests while "cleaning" code.
- Base-instance mix: 273 Python / 109 Java / 112 C++, plus category-specific expansions (e.g., 164 Python test-gen instances). *(Counts from repo README.)*

## Limitations & open questions
Synthetic bad patches and LLM-generated review feedback may not match the texture of human review; only three languages and 27 repos; no public leaderboard yet (you run your own evals). A skeptic would ask whether "fail the bad patches" test-gen scoring rewards adversarial overfitting rather than genuinely useful test suites.

## Why builders should care
If your agent product claims "software engineering," benchmark it beyond Python bug fixing — test generation and review response are where current agents crater (≤25%). Multi-language support (Java/C++) is a real differentiator, not a checkbox, and style/refactor passes need regression gates because agents break code while tidying it.

## Related companies in this landscape
- **Qodo** — test-generation-focused agent; OmniCode says test gen is the weakest agent skill, validating the niche and setting a bar.
- **Greptile / Baz / Sonar** — code-review agents; the review-fixing category is a direct eval for their loop (and Sonar-style linters power OmniCode's style scoring).
- **Cognition / Factory / OpenHands / Cline / Sourcegraph** — general SWE agents whose Python-bug-fix marketing numbers this benchmark challenges on Java/C++ and non-fix tasks.
- **Meticulous** — regression-safety testing; aligns with OmniCode's "no regressions" pass criterion.
- **Braintrust / Arize / Weights & Biases** — eval infrastructure that could host OmniCode-style multi-category agent evals.
- **poolside / Datacurve** — training-data players for whom leakage-resistant, synthetically expanded task generation is directly relevant.

## Sources
- https://arxiv.org/abs/2602.02262
- https://github.com/seal-research/OmniCode
- https://openreview.net/forum?id=VP204Aa0gH
- https://www.themoonlight.io/en/review/omnicode-a-benchmark-for-evaluating-software-engineering-agents
