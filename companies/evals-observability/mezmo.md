# Mezmo

> A telemetry/observability pipeline (formerly LogDNA) that sits between log/metric/trace sources and your observability stack, cutting volume and adding AI-driven context — including an MCP server for feeding agents structured telemetry instead of raw noise.

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** 2015 as LogDNA, San Francisco; rebranded to Mezmo May 2022 (Verified — Crunchbase, Mezmo blog)
- **Website / GitHub:** https://www.mezmo.com

## What they do
Mezmo's Telemetry Pipeline ingests logs, metrics, and traces from across a company's stack, applies real-time filtering/enrichment/routing, and controls what actually reaches (and gets billed by) downstream tools like Datadog or Splunk. Its newer "Active Telemetry" layer adds AI-driven root-cause detection, and an MCP Server exposes this data to AI coding/ops tools as pre-filtered, context-engineered datasets rather than a raw firehose — explicitly positioned against competitors that "just stream raw observability data to LLMs."

## Founders & origins / Funding
Founded by Chris Nguyen (CEO) and Lee Liu (CTO), both from prior startups TeamSave/JobLoft; went through YC Winter 2015. Raised $109.3M total across 6 rounds: seed (~$1.3M, 2016, Initialized Capital/Jaan Tallinn), Series A ($6.7M, 2017), Series B ($25M, 2018), Series D ($50M, Dec 2021) (Verified — Crunchbase, Dealroom).

## Evidence of real-world use
Company reports customers using Active Telemetry see 52% lower Datadog costs, 40% faster incident resolution, and 90% fewer noisy alerts (Reported — vendor claim, no independently named customer case study found).

## Relevance to agentic AI engineering
Sits squarely in the observability layer of an agent stack — pre-processing telemetry so agentic ops/SRE tools get signal, not noise, and it's one of the few sponsors explicitly building for "agentic ops" via MCP.

## Sources
- https://www.mezmo.com/
- https://www.mezmo.com/telemetry-pipeline
- https://www.mezmo.com/ai-agents
- https://www.mezmo.com/blog/logdna-is-now-mezmo
- https://www.crunchbase.com/organization/logdna
