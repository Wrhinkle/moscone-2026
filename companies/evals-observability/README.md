# Evals & Observability

LLM/agent evals, experiment tracking, tracing, APM/monitoring, telemetry, product analytics, and data labeling / human feedback.

This is the layer that answers the question every agent deployment eventually hits: **"is it actually working, and how would we know?"** Agents fail non-deterministically, degrade over long horizons, and burn money per token — so teams need trace capture (what did the agent do, span by span), evaluation (was it right, judged by code, LLM judges, or human experts), production monitoring (is it still right, and what does it cost), and the human-generated data that defines "right" in the first place. This folder holds 26 profiles spanning all of those, from $3.4B-revenue incumbents to seed-stage labs that eval agents by having them run vending machines.

## How to read this category

Three profiles carry the most weight. **[Arize](arize.md)** and **[Braintrust](braintrust.md)** are the two platinum-tier eval-native platforms and the cleanest statement of the category's core loop — instrument, trace, promote traces to datasets, score, gate releases — differing mainly on open-source posture (Arize's Phoenix is OTel-native and self-hostable; Braintrust is proprietary-core with an "evals as unit tests in CI" pitch). **[Datadog](datadog.md)** is the incumbent counterweight: if agents run where it already watches infra, agent observability is just more distributed tracing.

The axis that differentiates everything else is **what part of the loop they own**:

1. **Eval-and-trace platforms** (Arize, Braintrust, Comet/Opik, W&B Weave, Relai) — SDK-instrumented tracing plus offline/online evaluation.
2. **Incumbent observability & product telemetry extending to AI** (Datadog, Dynatrace, Sentry, PostHog, GrowthBook, Dash0, Mezmo) — you already run them; AI spans are a new workload.
3. **AI SREs — agents as the product** (Resolve.ai, Cleric, Traversal, Foam, Firetiger) — not tools for watching agents, but agents that do the watching, investigating production incidents autonomously.
4. **Human data & expert feedback** (Surge AI, Snorkel, Prolific, G2i, Taste Labs) — the supply side: the labels, rubrics, RL environments, and preference data that evals and post-training are made of.
5. **Specialist evaluators** (Hamming AI for voice, Safe Intelligence for formal/spec-driven verification, Fiddler for guardrails in regulated industries, Andon Labs for real-world long-horizon benchmarks).

A recurring pattern worth noticing: the money is converging from both directions. Datadog invested in both Arize and Braintrust; observability incumbents are building eval features while eval startups add monitoring; and the AI-SRE startups are effectively observability *consumers* competing with their own data sources' native agents (Datadog Bits AI, Dynatrace Intelligence Agents).

## Start here

- **[Braintrust](braintrust.md)** — the purest expression of eval-first engineering culture ("evals as unit tests"); $800M valuation, customer list (Notion, Stripe, Vercel, Zapier) that doubles as a who's-who of AI product teams.
- **[Arize](arize.md)** — the open-infrastructure counterpoint: Phoenix (10k+ GitHub stars) and the OpenInference tracing conventions keep the tracing layer vendor-neutral.
- **[Resolve.ai](resolve-ai.md)** — the "agent as the product" pole of the category, founded by an OpenTelemetry co-creator, $1.5B valuation in ~18 months; read alongside [Cleric](cleric.md) and [Traversal](traversal.md) for three competing theses on agent memory for incident response.
- **[Surge AI](surge-ai.md)** — the biggest business in the folder most people have never used directly: bootstrapped to a reported $1.2B revenue supplying RLHF/eval data to frontier labs.
- **[Andon Labs](andon-labs.md)** — smallest company, most cited findings: Vending-Bench and Project Vend are the best public evidence of how agents derail on long-horizon, money-touching work.

## All profiles

### Eval-and-trace platforms

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Arize](arize.md) | OTel-native tracing (OpenInference) + evals, OSS Phoenix core and enterprise AX platform | Platinum | ~$131M; Series C $70M (2025) incl. Datadog & PagerDuty | Phoenix crossed 10k GitHub stars / 2M+ monthly downloads; Booking.com, Duolingo, Uber as customers |
| [Braintrust](braintrust.md) | Eval-first platform: traces → datasets → scorers → CI gates that block regressions | Platinum | ~$121M; $800M post-money Series B (Feb 2026, ICONIQ) | Loop, an agent that writes your evals from production traces; Datadog invested in a direct future competitor |
| [Comet](comet.md) | MLOps veteran whose center of gravity is now Opik, Apache-2.0 OSS LLM/agent evals + tracing | Silver | ~$70M, nothing raised since 2021 | Opik at ~20.3k GitHub stars — biggest OSS footprint in the category; Cost Intelligence tracks Claude Code/Codex spend |
| [Weights & Biases by CoreWeave](weights-and-biases-by-coreweave.md) | The experiment-tracking default, with Weave competing in agent tracing/evals — now fused to CoreWeave GPUs | Gold | ~$250M raised, acquired ~$1.4B (May 2025) | OpenAI trained GPT-4 on W&B; unique closed loop from production traces into Serverless RL post-training |
| [Relai](relai.md) | Verifiable continual learning: turns agent failures/traces/feedback into regression-validated prompt & tool improvements | Silver | $6.9M pre-seed (.406 Ventures, June 2026) | Founded by a UMD professor (Soheil Feizi); claims 39%→80% validation-score lift at a financial-services deployment |

### Incumbent observability & product telemetry extending to AI

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Datadog](datadog.md) | Cloud-observability incumbent extending distributed tracing to LLM apps and agents, plus its own Bits AI ops agents | Gold | Public (DDOG); FY2025 revenue $3.43B | Invested in both Braintrust and Arize — hedging the segment it competes in; ships Toto, an open-weights time-series foundation model |
| [Dynatrace](dynatrace.md) | APM heavyweight betting agent observability is tracing with new span types; OSS dt-evals judges live `gen_ai.*` spans | Gold | Public (DT); $2B+ ARR | Hosted remote MCP server lets Claude/Copilot query production telemetry with governance — no self-hosting |
| [Sentry](sentry.md) | Developer-default error tracking extended to agent monitoring, plus Seer, an AI debugging agent | Gold | ~$217M; >$3B valuation (2022) | 44k+ GitHub stars; its MCP server feeds real stack traces *to* coding agents — observability flowing both directions |
| [PostHog](posthog.md) | All-in-one product analytics (events, replay, flags, experiments) with LLM tracing tied to the same user data | Silver | ~$182–194M; ~$1.4B (Series E, Sept 2025, Stripe led the D) | The only tool here that can answer "did the slow, expensive generation hurt retention?" in one query |
| [GrowthBook](growthbook.md) | Open-source, warehouse-native feature flags + A/B testing — experiment stats computed in your own warehouse | Silver | ~$23.1M (Series A, June 2025) | Online eval infrastructure in disguise: A/B test prompts, models, or agent policies without a new data pipeline |
| [Dash0](dash0.md) | OpenTelemetry-native observability with Agent0, an autonomous production engineer that ships fix PRs | Silver | $155M; $1B valuation ~1 year after founding | Founder previously built and sold Instana to IBM; fastest unicorn in the folder |
| [Mezmo](mezmo.md) | Telemetry pipeline (ex-LogDNA) that filters/enriches observability data before it hits your tools — or your agents | Silver | ~$109M across 6 rounds | MCP server serves agents pre-filtered, context-engineered telemetry instead of a raw firehose |

### AI SREs — agents as the product

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Resolve.ai](resolve-ai.md) | Multi-agent "AI for prod": triages alerts, root-causes incidents, remediates within guardrails across 60+ integrations | Gold | ~$200M in 18 months; $1.5B valuation (Apr 2026) | CEO co-created OpenTelemetry; DoorDash reports 87% faster time-to-root-cause |
| [Cleric](cleric.md) | AI SRE with per-tenant "operational memory" — every investigation distills into reusable institutional knowledge | Gold | $9.8M (seed + extension) | Read-only by default, enforced via cloud/K8s RBAC inside the customer VPC — the cleanest governance posture in the group |
| [Traversal](traversal.md) | Causal-ML academics turned RCA into graph search: a 1.7M-node Production World Model + Causal Search Engine | Gold | ~$53M (Sequoia seed, Kleiner A, Amex strategic) | American Express reports 82% root-cause accuracy, then invested; three of four founders are causal-inference researchers |
| [Foam](foam.md) | Agent that reads logs/traces/metrics, investigates anomalies, and Slacks the responsible engineer a diagnosis + fix | Bronze | $10M seed (Khosla, Max Levchin) | Customer testimonials from Perplexity, Together AI — and Braintrust, an evals vendor in this same folder |
| [Firetiger](firetiger.md) | Change Monitors that verify a PR's intended change actually worked in prod — closing the loop on AI-generated code | Bronze | $7.6M seed (Sequoia) | Customers report it running "on the majority of PRs"; hands fixes to Cursor/Codex/Claude Code via MCP and re-verifies |

### Human data & expert feedback

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Surge AI](surge-ai.md) | Expert-annotator marketplace for RLHF, rubrics, and RL environments — the labor market training frontier models | Supporting | Bootstrapped and profitable; 2025 raise reported at up to $1B at $15–25B+ | Reported $1.2B revenue in 2024 from ~12 frontier labs, with zero outside capital through 2024 |
| [Snorkel](snorkel.md) | Stanford weak-supervision spinout: programmatic labeling → expert-calibrated evaluators and benchmark construction | Gold | ~$237M; $1.3B (Series D, May 2025) | Five of the top 10 US banks are customers; design partner improved evaluator accuracy from 75% (LLM-judge) to 99%+ |
| [Prolific](prolific.md) | Marketplace of 200k+ vetted, demographically profiled human participants for preference data, evals, red-teaming | Silver | ~$33–34M (Series A 2023) | Sacra estimated ~$350M annualized revenue (Apr 2026) on a fraction of competitors' funding |
| [G2i](g2i.md) | Vetted-engineer network repositioned as human-data vendor: staff-level engineers authoring evals and RL environments for labs | Gold | Largely bootstrapped; no public rounds | Publicly recruiting ~50 engineers at $100–200/hr to critique AI-generated code — the human side of SWE-bench-style evals |
| [Taste Labs](taste-labs.md) | Preference data, rubrics, and eval environments for subjective quality — the anti-"AI slop" eval layer | Supporting | $18.5M seed (Amplify, CRV) | Sells judgment on "does this look/sound right," the eval dimension correctness-only pipelines skip |

### Specialist evaluators

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Fiddler](fiddler.md) | Enterprise AI observability + guardrails ("AI control plane") for banks, insurers, healthcare, defense | Silver | ~$100M; Series C $30M (Jan 2026) | In-house Trust Models run guardrails in your VPC at claimed <100ms — no per-call judge-LLM fees or data exfiltration |
| [Hamming AI](hamming-ai.md) | Automated QA for voice agents: thousands of simulated phone calls, audio-native scoring, prod-call-to-regression-test loop | Supporting | ~$4.3M seed (Mischief, YC S24) | Its synthetic callers do accents, interruptions, background noise, and IVR — claims 50k+ concurrent test calls |
| [Safe Intelligence](safe-intelligence.md) | Imperial College spinout: formal verification of ML models plus Spec27, spec-driven black-box testing for agents | Bronze | £4.15M seed (Amadeus, Feb 2025) | Spec27 tests outside-in through your deployed endpoint — guardrails and filters included — with no SDK or model access |
| [Andon Labs](andon-labs.md) | Eval lab, not eval platform: benchmarks agents by making them run real businesses (Vending-Bench, Project Vend) | Supporting | ~$500K reported (YC W24) | Anthropic co-published Project Vend, in which Claude ran a real office store, lost $200, and promised deliveries "in person wearing a blue blazer" |

## Related papers

The `papers/` folders and this category are two views of the same problem: the benchmarks define what to measure, the vendors above are where teams operationalize the measurement.

**Agentic-SWE evaluation** — the intellectual backbone of the eval platforms (Arize, Braintrust, Comet, W&B, Snorkel all cite this problem shape):
- [Reproducible, Explainable, and Effective Evaluations of Agentic AI for SWE](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md) — the methodology the trace-to-dataset-to-scorer loop implements.
- [SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md) and [SlopCodeBench: How Coding Agents Degrade Over Long Horizons](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) — long-horizon degradation, the same failure mode Andon Labs observes with dollar-denominated scoring.
- [ProdCodeBench: A Production-Derived Benchmark](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md) — production-derived eval data; the research cousin of Braintrust's trace-promotion and Firetiger's PR verification.
- [Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) — the case for custom, domain-specific evals, which is precisely what Snorkel, G2i, and Safe Intelligence sell.
- [FeatureBench: Benchmarking Agentic Coding for Complex Features](../../papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md) — Snorkel's UNDERWRITE benchmark is the enterprise-domain analogue.

**Tool use & governance** — tool-call spans are both the unit of tracing and the unit of control:
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — multi-tool orchestration; what Resolve.ai's 60+ integrations and every tracing SDK here capture.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — the research frame for Fiddler's control plane, Cleric's read-only RBAC posture, and Resolve's tiered action guardrails.
- [Verifiable Software Worlds for Computer-Use Agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md) — parallels Snorkel's executable simulation environments and G2i's RL-environment work.

**Agent memory** — the AI SREs are competing memory architectures in production:
- [Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) — compare Cleric's episodic operational memory vs. Traversal's structured world model vs. Resolve's incident learning.
- [GAM: Hierarchical Graph-Based Agentic Memory](../../papers/memory-research-agents/gam-hierarchical-graph-based-agentic-memory-for-llm-agents.md) — Traversal's 1.7M-node dependency graph is a deployed instance of the graph-memory thesis.

**Voice evaluation** — Hamming AI is the commercial expression of this thread:
- [From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation](../../papers/voice-realtime/from-text-to-voice-a-reproducible-and-verifiable-framework.md) — argues for exactly the audio-native, reproducible QA Hamming productizes.
- [τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains](../../papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md), [ProVoice-Bench](../../papers/voice-realtime/provoice-bench-assessing-the-proactivity-of-voice-agents.md), and [Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md) — define the interruption/turn-taking/proactivity behaviors Hamming's synthetic callers exercise.

**Plan adherence:**
- [From Plan to Action: How Well Do Agents Follow the Plan?](../../papers/planning-architecture/from-plan-to-action-how-well-do-agents-follow-the-plan.md) — Project Vend's phase-two fix (enforced procedures) is a live demonstration of why plan adherence needs measuring.

## Open questions the category hasn't answered

1. **Does eval tooling survive as an independent layer?** Model providers, agent frameworks, and hyperscalers are all absorbing evals and guardrails (AWS/Google bundle guardrails; frameworks ship eval harnesses). Braintrust's $800M and Arize's $131M say investors think yes; Datadog investing in both says the incumbents are hedging.
2. **Who evaluates the evaluators?** LLM-as-judge dominates, but Snorkel's 75%→99% evaluator-accuracy claim and Fiddler's in-house judge models both argue generic judges are miscalibrated — and nearly every accuracy number in this folder (Cleric's 92% actionable, Traversal's 82% RCA, Hamming's 95% human agreement) is vendor-reported. Incident diagnosis still has no public SWE-bench equivalent.
3. **Trace-volume economics.** Chatty agents generate enormous span volume, and most pricing here is per-GB/per-span/per-event (Datadog, W&B Weave, Braintrust, Sentry, PostHog). Mezmo's pipeline pitch and Comet's Cost Intelligence exist because nobody has solved observing agents without a bill that scales like the agents' verbosity.
4. **Does per-tenant learning become the moat — or the lock-in?** Cleric's operational memory, Traversal's world model, and Relai's continual learning all improve with tenure and don't transfer out. The better these systems get, the more expensive it becomes to leave.
5. **Human data at frontier prices.** Surge's reported $1.2B revenue from ~12 labs, G2i's $200/hr engineers, and Taste Labs' "judgment as a service" all bet expert human data stays scarce; synthetic data and self-play bet the opposite. The folder's five human-data vendors are effectively short that trade.
