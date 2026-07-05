# Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering

- **Status:** Located — [arXiv:2606.17799](https://arxiv.org/abs/2606.17799)
- **Area:** swe-agents
- **Authors / venue / date:** Maria I. Gorinova, Macey Baker, Amy Heineike, Maksim Shaposhnikov, Rob Willoughby, Dru Knox (Tessl) — arXiv cs.SE, submitted 2026-06-16

## Problem

Coding-agent leaderboards were designed in a pre-agent era: they collapse model, harness, context, environment, and feedback signals into one end-to-end score graded against a single reference solution. But a coding agent in practice is a *system*, and any non-model component can move the score by as much as a model-generation jump — so leaderboard deltas tell you little about what to buy, tune, or fix.

## Approach

A position paper, not a benchmark. It documents three symptoms — (i) scores conflate model with harness, (ii) single-reference grading penalises equally valid alternative implementations, (iii) no component-level signal means end-to-end scores are hard to iterate on — then proposes three structural fixes:

1. **Harness-aware metadata:** submissions must declare model version, harness version, environment hash, dataset version, plus at least one ablation across a non-model axis.
2. **Multi-shape verifiers:** replace single reference tests with property tests, reference oracles, or differential tests that accept multiple correct implementations.
3. **Component-level evaluation:** score context quality, verifier effectiveness, and invariant adherence alongside the end-to-end number.

## Key findings

- Claude Opus 4.6 varies from **58% to 79.8%** success on identical tasks depending only on the agent harness — comparable to inter-generation model gaps (paper's Table 1).
- Practitioners report **4–10 point swings** for Opus 4.5 on SWE-bench Verified between standardized and custom scaffolds; Fan et al. (2025) found **2–3×** effectiveness variance across model–scaffold combinations; AI21's 200,000+ SWE-bench runs show orchestration choices materially move pass rates.
- SWE-bench validity: **32.67%** of instances have solution leakage in issue text; **31.08%** pass under insufficient tests (SWE-Bench+); **7.8%** of "resolved" patches fail developer-written tests and **29.6%** diverge from reference behavior under differential testing.
- Real-world acceptance rates for agent-written code (**35–64%**) lag headline benchmark figures (**>70%**).

## Limitations & open questions

Authors concede end-to-end scores do reflect real usage (they oppose using *only* them), decomposed evaluation adds cost, and the hardest open problem is operationalisation — specifying behavior without encoding one implementation. A skeptic asks: who enforces metadata/ablation requirements on leaderboards, will multi-shape verifiers scale beyond well-specified tasks, and note the authors (Tessl) sell spec-driven development, which this position conveniently supports.

## Why builders should care

Stop model-shopping off leaderboard deltas smaller than ~10 points — your harness, context assembly, and verifiers are a cheaper, larger lever than switching models. When building internal evals, grade against properties/behaviors rather than one golden output, and log harness + environment versions so scores are comparable over time.

## Related companies in this landscape

- **Tessl** (Gold) — authors; spec-driven development is their answer to "specify behavior without encoding implementation."
- **Braintrust / Arize / Weights & Biases / Hamming AI** — eval and tracing platforms positioned to deliver the component-level signal the paper says leaderboards lack.
- **Qodo / Sonar / Greptile / Snyk / Meticulous** — verification-layer vendors; multi-shape verifiers (property/differential testing, review agents) are their product surface.
- **Cognition / Factory / OpenHands / Sourcegraph / Cline / Warp / Zed** — harness builders; the 58→79.8% harness spread is their pitch that the harness, not just the model, is the product.
- **OpenAI / Google DeepMind / Amazon AGI Labs** — labs whose headline SWE-bench claims this paper says conflate model with scaffold.

## Sources

- https://arxiv.org/abs/2606.17799
- https://arxiv.org/html/2606.17799
