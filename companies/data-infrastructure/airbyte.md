# Airbyte

> Open-source data-movement platform (600+ ELT connectors) that repositioned in 2026 as a "context layer" feeding pre-indexed enterprise data to AI agents via MCP and SDK.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** 2020, San Francisco (Y Combinator W20) — Verified
- **Website / GitHub:** https://airbyte.com · https://github.com/airbytehq/airbyte

## What they do
Airbyte's core product is open-source ELT: a platform that syncs data from ~600+ sources (SaaS APIs, databases, files) into warehouses, lakes, and vector stores. You run it self-hosted (Airbyte Core, dual-licensed MIT/ELv2) or on Airbyte Cloud; connectors are built with a Python CDK plus a low-code/no-code builder, which is how the catalog got so large. PyAirbyte lets you run connectors directly in Python without the platform, and also powers their Cloud Replication MCP server. This is the classic "modern data stack" ingestion layer — the open-source counterweight to Fivetran.

In May 2026 they launched **Airbyte Agents** with a managed **Context Store**: instead of an agent hammering source APIs at query time, Airbyte continuously replicates and pre-indexes a curated subset of entities from connected systems, matching records about the same entity across sources (the Salesforce customer, their Zendesk tickets, their billing contract). Agents hit this store via MCP (works in Claude, ChatGPT, Cursor) or a native SDK. Launch claims: ~40% fewer tool calls and up to 80% fewer tokens in some workflows (Reported — vendor-stated, not independently benchmarked). It shipped with 50 connectors populating the store, with the full catalog on the roadmap. Pricing for Agents is metered in "Agent Operations" (free 1,000/mo; $29 individual; $299 team; custom enterprise), alongside volume/capacity-based replication plans — a real public pricing page across both product lines.

## Founders & origins
**Michel Tricot** (CEO) and **John Lafleur** (COO) — Verified. Tricot ran data-integration engineering at LiveRamp (hundreds of TB/day) and was a founding member of rideOS; Lafleur is a serial founder (StreamNation → SmugMug acquisition, CodinGame, Anaxi). They met in San Francisco in 2013, did YC W20, and released the first open-source version in late 2020 with the explicit thesis of commoditizing data-integration pipelines. ~600 companies were syncing data within six months of launch (Reported — company blog).

## Funding
- Seed: $5.2M, March 2021, led by Accel — Verified
- Series A: $26M, May 2021, led by Benchmark — Verified
- Series B: $150M, Dec 2021, at $1.5B valuation; Altimeter and Coatue leading, with Thrive, Salesforce Ventures, Benchmark, Accel, SV Angel — Verified
- Total raised: ~$181M — Verified (Tracxn). No publicly confirmed rounds since 2021 as of 2026-07-05; one estimate pegs ARR ~$20M (2024, Getlatka — Unverified).

## Evidence of real-world use
Strong. Main repo: 21.6k stars, 5.2k forks (Verified, July 2026). Named customers with actual case studies (not just logos): Peloton (financial-data infrastructure on 600+ connectors), Graniterock (claims 50% engineering-cost reduction), KORTX and CodeSandbox ("Powered by Airbyte" embedded use), PensionBee, Petvisor, Symend. Landing-page logos additionally include Siemens, Unity, Perplexity, Monday.com, Calendly (Reported). Enlyft counts ~4,300 companies using it (Reported). The connector-builder community and PyPI-published per-connector packages are further adoption signals. The Context Store itself is too new (May 2026) to have documented production users — watch for case studies.

## Relevance to agentic AI engineering
Airbyte is a direct bet on the agent-context problem: it sits between raw enterprise systems and the agent's tool-calling loop, converting many brittle API tools into one pre-indexed search surface. That maps onto this repo's memory line of work — *Are We Ready For An Agent-Native Memory System?*, *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*, and especially *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* (the Context Store's entity-linking is essentially pre-computed semantic metadata). Its "fewer tool calls" pitch is the practical counterpart of *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*; and pre-indexing to cut retrieval latency is the same bottleneck *VoiceAgentRAG* attacks for voice agents.

## Use cases & considerations
1. Feed a warehouse/vector store for RAG from SaaS + DB sources without writing extractors.
2. Give an MCP-connected agent (Claude, Cursor) cross-system entity context without building N integrations.
3. Embed "Powered by Airbyte" ingestion inside your own product (KORTX pattern).
4. PyAirbyte for lightweight, in-Python extraction in agent pipelines.

Considerations: self-hosting the platform is operationally heavy (Kubernetes, connector version churn); ELv2 restricts offering it as a competing service; the Context Store is v1 (50 connectors) and creates data-residency/freshness questions since it copies your data into a managed store. Competitors: Fivetran, Meltano, Estuary, dltHub on ELT; on agent context, it converges with MCP gateways (Composio, Arcade) and memory layers (Mem0, Zep). Open question: no funding since 2021 at a $1.5B valuation — the Agents pivot reads partly as a growth-story reset.

## Sources
- https://airbyte.com/ and https://airbyte.com/company/about-us
- https://www.ycombinator.com/companies/airbyte
- https://moneyinc.com/michel-tricot/ and https://moneyinc.com/airbyte/
- https://research.contrary.com/company/airbyte
- https://airbyte.com/blog/a-150m-series-b-to-power-the-movement-of-data
- https://tracxn.com/d/companies/airbyte/__msyjFhyA1oYCHhgK3YkbjM6Jfs3I4ehkOtBsvWydrDU
- https://www.businesswire.com/news/home/20260505801702/en/Airbyte-Agents-Launched-to-Fix-the-Data-Problem-Breaking-AI-Agents
- https://thenewstack.io/airbyte-agents-context-store/
- https://airbyte.com/pricing
- https://github.com/airbytehq/airbyte and https://github.com/airbytehq/PyAirbyte
- https://airbyte.com/success-stories (Peloton, Graniterock, KORTX, CodeSandbox, PensionBee, Petvisor, Symend)
- https://enlyft.com/tech/products/airbyte
- https://getlatka.com/companies/airbyte.com
