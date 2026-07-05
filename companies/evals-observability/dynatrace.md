# Dynatrace

> The 20-year-old APM heavyweight ($2B+ ARR, NYSE: DT) betting that agent observability is just distributed tracing with new span types — and rebuilding itself as an "agentic operations" platform in the process.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2005, Linz, Austria (Verified — Wikipedia, company history pages)
- **Website / GitHub:** https://www.dynatrace.com · https://github.com/dynatrace-oss · https://github.com/Dynatrace

## What they do

Core platform: **OneAgent** auto-instruments hosts/containers/processes with near-zero manual config; **PurePath** distributed tracing (the founding technology) captures every transaction end-to-end; everything lands in **Grail**, a schema-on-read data lakehouse queried via DQL; and **Davis AI**, a causal (not statistical) AI engine, does automated anomaly detection and root-cause analysis. This is a large, real business: FY2026 ARR surpassed **$2B** (16% CC growth), Q3 FY26 revenue was $515M (+18% YoY), and the log-management line alone crossed $100M annualized consumption growing >100% YoY (Verified — SEC 8-K earnings releases, Feb/May 2026).

The AIEWF-relevant layer is **AI Observability** (GA app, with agentic-framework support announced Nov 2025): traces of model/provider calls, tool invocations, RAG/vector-DB steps, agent topology and inter-agent communication, ingested via OpenTelemetry `gen_ai.*` semantic conventions plus OpenLLMetry/OpenInference, correlated with the underlying infra Dynatrace already watches (Verified — docs, blog). Two pieces stand out for builders: **dt-evals**, an Apache-2.0 OSS toolkit (TypeScript/Python, ~38 stars — young) that samples live `gen_ai.*` spans, scores them with a bring-your-own LLM judge (13 built-in metrics: hallucination, grounding, safety, retrieval quality, etc.), can fail CI pipelines on threshold breach, and writes results back to Dynatrace as queryable business events (Verified — GitHub repo, company blog); and a hosted **remote MCP Server** that lets external agents (Claude, GitHub Copilot, Atlassian Rovo, Bedrock AgentCore, Azure AI Foundry) query production telemetry with governance — no server to self-host (Verified — company blog, Perform 2026 press).

At Perform 2026 (Jan 2026) the company announced **Dynatrace Intelligence** and **Intelligence Agents** — its own fleet of specialized ops agents taking closed-loop remediation actions — repositioning from monitoring vendor to "agentic operations system" (Verified — press release, BusinessWire; analyst framing: Futurum's "Is Observability the New Agent OS?"). A May 2025 NVIDIA partnership put its AI/LLM observability into the NVIDIA Enterprise AI Factory validated design (Verified — press release).

## Founders & origins

Founded as dynaTrace Software GmbH by **Bernd Greifeneder**, **Sok-Kheng Taing**, and **Hubert Gerstmayr** in Linz, 2005; Greifeneder built the PurePath tracing tech and remains CTO today (Verified — Wikipedia, company leadership page). Unusual corporate arc: acquired by Compuware in 2011 for ~$256M; Thoma Bravo took Compuware private (~$2.5B, 2014) and spun Dynatrace out standalone; during that period the product was rebuilt from scratch around OneAgent/Davis. CEO since Dec 2021 is **Rick McConnell** (ex-Akamai president). HQ is Waltham, MA; the main engineering hub remains Linz (Verified — multiple sources).

## Funding

Not a venture story — public company, so the record is settled: bootstrap-era Austrian startup → Compuware acquisition (2011, ~$256M, Verified) → Thoma Bravo ownership (2014) → **IPO on NYSE (DT), August 2019** (Verified). No private funding rounds to track; financials come from SEC filings.

## Evidence of real-world use

The strongest evidence in this category short of open-source ubiquity: thousands of enterprise customers and $2B ARR under SEC-audited reporting (Verified). Named, metric-bearing cases from Perform 2026: **TELUS** cut end-to-end observability deployment from 600 minutes to 20 and new-team onboarding time by 30% after consolidating onto Dynatrace; **ADT** credits Davis AI with large MTTR reductions; **DXC Technology** and **Storio Group** presented rollout stories (Reported — vendor case studies and Investing.com/diginomica coverage of Perform 2026; treat numbers as directional). Caveat for this repo's purposes: that evidence is for the core platform — the AI Observability app and dt-evals are new (GA Nov 2025; dt-evals is early, 38 GitHub stars), so agent-specific adoption is not yet independently demonstrated.

## Relevance to agentic AI engineering

Three distinct angles. (1) **Agent tracing in production**: span-level capture of tool invocations and inter-agent messages is the operational counterpart of *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and dt-evals' trace-sampled judging + CI gating is a production analogue of the agentic-SWE evaluation papers (*SWE-EVO*, *ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*). (2) **Agents as telemetry consumers**: the MCP Server makes production observability a governed tool for coding/ops agents — squarely the access-control territory of *Governance by Construction for Generalist Agents*. (3) **Deployed ops agents to study**: Intelligence Agents are long-horizon remediation agents shipping to enterprises now.

## Use cases & considerations

Use cases: (1) tracing a back-office agent's LLM/tool spans next to the databases and queues it touches — one root-cause graph via Davis; (2) scheduled dt-evals runs judging live production traffic for hallucination/grounding, with alerts in the same platform; (3) wiring Claude Code or Copilot to the MCP Server so a coding agent can pull real production logs/traces while debugging; (4) CI gates that fail a deploy when eval scores regress.

Considerations: enterprise-priced consumption model (DPS rate card is public, but bills scale with ingestion — chatty agents are expensive); heaviest value requires adopting the whole platform (OneAgent + Grail), meaning real lock-in; the AI-native tooling trails eval-first rivals (**Arize, Braintrust, LangSmith, Langfuse**) in workflow depth and trails **Datadog** in AI-observability marketing presence. Open questions: whether dt-evals gets sustained OSS investment, and whether Intelligence Agents' "closed-loop remediation" earns trust in production.

## Sources

- https://en.wikipedia.org/wiki/Dynatrace
- https://www.sec.gov/Archives/edgar/data/0001773383/000177338326000006/q3fy26-earningsreleaseex99.htm · https://ir.dynatrace.com/news-events/press-releases/detail/425/dynatrace-reports-fourth-quarter-and-full-year-fiscal-2026-financial-results
- https://www.dynatrace.com/solutions/ai-observability/ · https://docs.dynatrace.com/docs/observe/dynatrace-for-ai-observability
- https://www.dynatrace.com/news/blog/announcing-agentic-framework-support-and-general-availability-of-the-dynatrace-ai-observability-app/
- https://www.dynatrace.com/news/blog/evaluate-llm-and-agent-quality-in-dynatrace-ai-observability/ · https://github.com/dynatrace-oss/dt-evals
- https://www.dynatrace.com/news/blog/dynatrace-mcp-server-allow-ai-interact-dynatrace-access-production-insights/
- https://www.dynatrace.com/news/press-release/perform-2026-ignites-new-era/ · https://www.businesswire.com/news/home/20260128134927/en/Dynatrace-Perform-2026-Ignites-a-New-Era-of-Autonomous-Intelligence-and-Innovation
- https://www.dynatrace.com/news/press-release/dynatrace-nvidia-ai-llm-observability/
- https://www.dynatrace.com/customers/adt/ · https://www.investing.com/news/company-news/dynatrace-showcases-customer-success-with-ai-observability-platform-93CH-4470891 · https://diginomica.com/dynatrace-perform-2026-why-do-observability-pocs-succeed-enterprise-rollouts-stall
- https://futurumgroup.com/insights/dynatrace-perform-2026-is-observability-the-new-agent-os/
