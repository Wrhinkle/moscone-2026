# Stop Evaluating Models Like It's the 50s

> Applying item response theory from psychometrics to LLM benchmarks: per-item difficulty and discrimination replace raw accuracy, enabling smaller benchmarks, leak detection, and distillation fingerprinting.

- **Speaker:** Alejandro Vidal, Mindmakers
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=EfcfUB2uprc) (AI Engineer channel; ~23m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Vidal argues that benchmark accuracy carries a hidden assumption: every question weighs the same. Items can be correlated, pure noise, or far more important than others, and a single accuracy number models none of that. His remedy is item response theory (IRT), the machinery psychometrics has used to measure human intelligence for decades, applied to the full model-by-item answer matrix instead of a summed score. IRT estimates a difficulty parameter b for each item and an ability parameter theta for each model, on the same scale and normally distributed, plus a discrimination parameter a describing how steeply an item's probability-of-correct curve rises with ability. Confidence intervals come for free.

The parameters immediately expose things accuracy hides. Two models can share a benchmark score while their abilities differ: in his data, Claude Opus 4.1 and Gemini 3 Pro score identically but sit a full standard deviation apart in theta, because IRT weighs which questions each model got right. Discrimination audits the benchmark itself. Flat curves are uninformative noise, and negative discrimination, where stronger models do worse, usually flags a mislabeled item; Vidal shows two items from a real dataset whose gold answers turn out to be wrong. For teams running private benchmarks repeatedly across models, harnesses, and fine-tunes, he demonstrates benchmark shrinking in the style of the Tiny Benchmarks paper, ordering items by informativeness and reaching 0.99 correlation with full-benchmark ability estimates using a fraction of the items.

The second half builds on residuals, the gap between an answer and what the fitted curves predict. Improbable results, like Gemini 3 missing a question it should answer 86 percent of the time or DeepSeek landing questions far above its level, become measurable outliers. Aggregated per model, person-fit statistics catch unstable inference (o4-mini shows the most inconsistency in his matrix, the kind of signal that can expose a broken GPU platform). For benchmark creators worried about contamination, Vidal proposes adaptive testing with policies: serve each organization a shared anchor set for calibration plus a unique fingerprint set of difficult items, and watch whether later models improve on those specific items in statistically weird ways. In a synthetic test, he fine-tuned a model on the five fingerprint items given to one organization and the average residuals exceeded two standard deviations against controls, identifying both the leak and its source.

He then borrows differential item functioning, which psychometrics uses for test fairness, to compare Anthropic and OpenAI models: items where the two groups' curves diverge at equal ability reveal systematic capability differences, and the flagged items share properties. Finally, treating each model's residual vector as a fingerprint, he correlates them across models. Model families cluster, two DeepSeek R1 distillations share a 0.3 correlation from the same checkpoint, the same model at different effort levels correlates almost perfectly, and successor generations like Gemini 3 Pro and Gemini 2.5 Pro show shared-weights patterns. Vidal claims this residual evidence for distillation is stronger than prompt-based probing. He closes with open directions, including merging benchmarks, secondary signals like tokens and latency, and multidimensional ability, where he says LLMs and humans show strikingly similar intelligence structure, and promises to share the benchmarks, tools, and datasets.

## Notable moments

- [0:04:40](https://www.youtube.com/watch?v=EfcfUB2uprc&t=280s) Claude Opus 4.1 and Gemini 3 Pro tie on benchmark score but sit one standard deviation apart in estimated ability.
- [0:06:50](https://www.youtube.com/watch?v=EfcfUB2uprc&t=410s) Negative discrimination flags mislabeled items; two real gold answers turn out to be wrong.
- [0:14:16](https://www.youtube.com/watch?v=EfcfUB2uprc&t=856s) The fingerprint-set scheme for tracing which organization leaked benchmark items.
- [0:19:50](https://www.youtube.com/watch?v=EfcfUB2uprc&t=1190s) Residual correlation matrices cluster model families and expose distillation relationships.

## Connections

- [Position: Coding Benchmarks Are Misaligned](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) makes a complementary critique of what benchmark scores fail to measure.
- [Reproducible, Explainable, and Effective Evaluations of Agents](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md) pursues the same goal of eval methodology with statistical rigor.
- [Braintrust](../../companies/evals-observability/braintrust.md) operates the private-benchmark workflow (datasets, scoring, release gates) that Vidal's IRT auditing and shrinking techniques would slot into.
