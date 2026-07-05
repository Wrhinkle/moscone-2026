# Datadog

> The incumbent cloud observability platform (infra, APM, logs) now extending the same distributed-tracing model to LLM apps and AI agents — plus its own fleet of ops agents.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2010, New York City (Verified — Wikipedia, company site, press)
- **Website / GitHub:** https://www.datadoghq.com · https://github.com/DataDog

## What they do

Datadog's core business is a SaaS observability platform: an agent you install on hosts/containers ships metrics, traces, and logs into a unified backend with dashboards, alerting, APM, RUM, and a growing security suite. It's one of the largest pure-play observability vendors — FY2025 revenue was **$3.43B, up 28% YoY**, with ~32,700 customers, 4,310 of them at $100k+ ARR and 603 at $1M+ ARR (Verified — Q4/FY2025 earnings release, Feb 2026).

The AIEWF-relevant piece is **LLM Observability / Agent Observability** (GA since mid-2024, agentic expansion announced at DASH, June 2025). It treats each agent request as a distributed trace: spans for LLM calls, tool invocations, retrieval steps, and agent decisions, correlated with the rest of your APM traces. Around that: **LLM Experiments** (versioned datasets from production traces, side-by-side config comparisons, regression testing), a prompt **Playground**, out-of-the-box online evaluators (hallucination, drift, quality/cost/latency), sensitive-data scanning and prompt-injection detection, and an **AI Agents Console** for inventorying agents running across an org. Auto-instrumentation covers major frameworks; Google's Agent Development Kit was added ~Feb 2026 (Reported — InfoQ). OpenTelemetry ingestion is supported. Pricing: free tier ~40K LLM spans/month, Pro from ~$160/month for 100K spans (Reported — third-party comparison; confirm on pricing page).

Datadog also ships agents of its own — **Bits AI SRE** (autonomous incident investigation that reads telemetry and follows runbooks), Bits AI Dev Agent, and Bits AI Security Analyst — and publishes AI research: **Toto**, an open-weights time-series foundation model trained on Datadog's internal telemetry, with an accompanying observability benchmark (BOOM) (Verified — company press release and blog).

## Founders & origins

**Olivier Pomel** (CEO) and **Alexis Lê-Quôc** (CTO) — met as undergraduates at École Centrale Paris, then worked together ~9 years at Wireless Generation (acquired by NewsCorp). They founded Datadog in 2010 explicitly to reduce dev-vs-ops friction they'd lived through — "monitoring as the shared source of truth." (Verified — Wikipedia, Forbes, company leadership page.) Both became billionaires post-IPO (Reported — Forbes).

## Funding

Public company — funding history is settled record:

- **Series A, 2012:** $6.2M, Index Ventures and RTP Ventures (Verified)
- **Series C, 2015:** $31M; **Series D, early 2016:** $94M (Verified — press, Wikipedia)
- **IPO:** Nasdaq (DDOG), September 19, 2019 — raised $648M at an $8.7B valuation, after rejecting a $7B+ acquisition offer from Cisco (Verified)
- Market cap as of 2026-07-02: not checked in real time; a multi-tens-of-billions large-cap (Unverified for exact figure)

## Evidence of real-world use

Overwhelming for the core platform (32,700 paying customers, Verified via SEC filings). For the AI-specific products, named case studies exist and include metrics, not just logos:

- **AppFolio** — used Agent Observability on its Realm-X LLM inbox; reports 80–90% latency reduction and ~300% adoption increase (Reported — Datadog case study)
- **Baz** (coding agents) — end-to-end visibility into agent decisions; ~80% faster evaluation of product changes (Reported — Datadog case study)
- **Dust** (enterprise agent platform, 1,000+ customers incl. Clay, Doctolib, Photoroom) — monitors agent reliability with LLM Observability (Reported — Datadog case study)

Vendor-published case studies, so treat numbers as directional. Notable strategic signal: Datadog invested in Braintrust's Series A — hedging/participating in the eval-native segment it now competes in (Verified — Braintrust funding press).

## Relevance to agentic AI engineering

Datadog is the "agents in production" counterweight to eval-first startups: if your agent already runs where Datadog watches infra, its trace-per-agent-request model gives you tool-call and decision spans alongside normal APM. That trace-level scoring is the operational side of this repo's agentic-SWE evaluation papers (*SWE-EVO*, *ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*), and multi-step tool-span capture maps directly to *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. The AI Agents Console, prompt-injection scanning, and audit-grade traces are a production expression of the control-plane concerns in *Governance by Construction for Generalist Agents*. Bits AI SRE is itself a long-horizon investigation agent worth studying as a deployed artifact.

## Use cases & considerations

Use cases: (1) production monitoring of a back-office agent (e.g., a job-packet auditor) with cost/latency/token dashboards next to existing infra alerts; (2) hallucination and drift evaluators running online against live traffic; (3) dataset-from-traces regression testing via LLM Experiments before model swaps; (4) org-wide agent inventory/governance via AI Agents Console.

Considerations: Datadog's pricing reputation is "powerful but expensive, watch the bill" — LLM span volume from chatty agents can compound the classic Datadog cost problem. Its eval workflow is younger than eval-native rivals (**Braintrust, LangSmith, Arize, Langfuse, W&B Weave**; infra-side, **Grafana, New Relic, Honeycomb**). Strongest when you're already a Datadog shop; weakest as a standalone eval harness for pre-production experimentation. Open question: how deep the Experiments/CI-gating story gets versus staying production-monitoring-first.

## Sources

- https://en.wikipedia.org/wiki/Datadog
- https://investors.datadoghq.com/news-releases/news-release-details/datadog-announces-fourth-quarter-and-fiscal-year-2025-financial
- https://www.datadoghq.com/products/ai/agent-observability/ · https://docs.datadoghq.com/llm_observability/
- https://www.datadoghq.com/about/latest-news/press-releases/datadog-expands-llm-observability-with-new-capabilities-to-monitor-agentic-ai-accelerate-development-and-improve-model-performance/
- https://investors.datadoghq.com/news-releases/news-release-details/datadog-llm-observability-now-generally-available-help
- https://www.datadoghq.com/blog/bits-ai-sre/ · https://www.datadoghq.com/blog/datadog-ai-innovation/
- https://www.datadoghq.com/about/latest-news/press-releases/datadog-ai-research-launches-new-open-weights-ai-foundation-model-and-observability-benchmark/
- https://www.datadoghq.com/case-studies/appfolio/ · https://www.datadoghq.com/case-studies/baz/ · https://www.datadoghq.com/case-studies/dust/
- https://www.infoq.com/news/2026/02/datadog-google-llm-observability/
- https://www.forbes.com/profile/olivier-pomel/ · https://www.datadoghq.com/about/leadership/
- https://www.confident-ai.com/knowledge-base/compare/10-llm-observability-tools-to-evaluate-and-monitor-ai-2026
