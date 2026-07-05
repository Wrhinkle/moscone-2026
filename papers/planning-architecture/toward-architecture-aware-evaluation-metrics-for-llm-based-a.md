# Toward Architecture-Aware Evaluation Metrics for LLM-Based Agents

- **Status:** Located — [arXiv:2601.19583](https://arxiv.org/abs/2601.19583) (listed on arXiv as "Toward Architecture-Aware Evaluation Metrics for LLM Agents")
- **Area:** planning-architecture
- **Authors / venue / date:** Débora Souza, Patrícia Machado (Federal University of Campina Grande, Brazil); accepted at CAIN 2026 (IEEE/ACM 5th Intl. Conf. on AI Engineering — Software Engineering for AI); arXiv submitted 2026-01-27

## Problem
Agent evaluation today is model-centric and fragmented: the paper reports that over 66% of surveyed studies use only accuracy or success-rate measures. A single end-to-end pass/fail number cannot tell you *which* component failed — the planner, the memory module, the tool router, or the reflection loop — so debugging an agent regression means guessing. Tooling like DeepEval and LangSmith ships metrics but no guidance on mapping them to architectural components.

## Approach
A lightweight three-layer mapping framework: (1) identify observable behaviors (planning consistency, tool-use decisions, memory retrieval); (2) map each behavior to the architectural component responsible for it (planner, tool router, memory, persona, reflection, MCP integrations); (3) select metrics that meaningfully assess that behavior. Agents are instrumented to capture planning traces, tool-use events, memory retrievals, and reflection steps. Framed around three research questions: how components relate to behaviors (RQ1), how to systematically map both to existing metrics (RQ2), and whether this improves structure, reproducibility, and diagnostic power (RQ3). Applicability is illustrated on real open-source agents: SWE-Agent, MetaGPT, and HuggingGPT. Validation is a planned comparative case study — ad hoc vs. architecture-informed evaluation — measuring diagnostic accuracy, failure-attribution clarity, and reproducibility.

## Key findings
- >66% of existing agent-evaluation studies rely solely on accuracy/success-rate metrics (the paper's motivating survey figure).
- The component→behavior→metric mapping is the contribution itself; the authors claim it yields "more organized and precise diagnosis" and reduces misinterpretation from system-level scores alone.
- This is a short, early-stage position/vision paper (CAIN track): the comparative case study is proposed, not yet reported — no benchmark deltas or quantitative validation numbers exist yet (inferred from the paper's evaluation-plan framing and brief length).

## Limitations & open questions
Authors concede that agent-architecture heterogeneity may limit generality, and that results depend on logging/instrumentation quality, which varies widely across agent frameworks. A skeptical builder would add: without the case-study results, there is no evidence yet that component-level attribution beats a good trace-review workflow; and the mapping may drift as architectures evolve (e.g., planner and router collapsing into one model call).

## Why builders should care
Stop treating agent evals as one end-to-end success rate. Instrument each architectural component (plan traces, tool-route decisions, memory hits) and attach a metric per behavior, so a regression tells you *what* broke, not just *that* something broke. If you already emit OpenTelemetry-style traces, you are one mapping table away from this approach.

## Related companies in this landscape
- **Arize** — component-level tracing and eval attribution is exactly its AI-observability pitch; this paper is the academic case for it.
- **Braintrust** — eval platform; the paper challenges "metrics without mapping guidance," which Braintrust's experiment-centric workflow partially addresses.
- **LangChain** — LangSmith is named in the paper as a metrics tool lacking component-mapping guidance — both a challenge and a roadmap hint.
- **Weights & Biases (CoreWeave)** — Weave agent tracing benefits from a principled component→metric taxonomy.
- **Datadog / Dynatrace / Sentry** — agent telemetry pipelines are the prerequisite the paper says evaluation quality depends on.
- **Hamming AI / Fiddler / Comet** — agent-eval and monitoring vendors whose diagnostic claims this framework would systematize.
- **LlamaIndex / Composio** — memory/retrieval and tool-router components are the exact modules the paper argues need dedicated metrics.

## Sources
- https://arxiv.org/abs/2601.19583
- https://arxiv.org/html/2601.19583v1
