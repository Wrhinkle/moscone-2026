# ClickHouse

> Open-source columnar OLAP database (and its managed cloud) that has become the default analytics/observability engine behind AI labs and agent products — now selling "the data platform for agents."

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** company incorporated summer 2021, Bay Area (Verified); the database itself dates to 2009 inside Yandex, open-sourced 2016 — Verified
- **Website / GitHub:** https://clickhouse.com · https://github.com/ClickHouse/ClickHouse

## What they do
The core is ClickHouse OSS: a column-oriented, C++ OLAP database built for sub-second aggregations over billions-to-trillions of rows of append-heavy data (events, logs, traces, metrics, clickstreams). Apache 2.0, SQL interface, MergeTree storage engine, aggressive compression and vectorized execution. It is not a transactional database — inserts are cheap in batches, point updates/deletes are not — and that trade-off is exactly why it wins at telemetry-scale analytics where Postgres and Elasticsearch fall over.

Commercially you buy **ClickHouse Cloud**, a managed service with separated storage/compute (proprietary SharedMergeTree) plus **ClickPipes** managed ingestion (Postgres CDC via the PeerDB acquisition; Kafka, S3, etc.). In 2025–26 the company assembled an opinionated AI/observability stack on top: **ClickStack** (OpenTelemetry-native logs/metrics/traces/session-replay UI, from the HyperDX acquisition), an official **ClickHouse MCP server** so LLM agents can query the database directly, **Langfuse** (acquired Jan 2026 — the widely used open-source LLM observability/tracing/evals platform), and an open-source "**Agentic Data Stack**" reference deployment (LibreChat chat UI + ClickHouse MCP + Langfuse). A managed Postgres offering was announced alongside the Series D, pushing toward "one platform for transactional + analytical + agent workloads." At Open House 2026 they claimed $250M ARR and launched Claude-powered agentic analytics features (Reported — company blog; ARR figure corroborated by TechCrunch).

## Founders & origins
- **Alexey Milovidov (CTO)** — created ClickHouse at Yandex starting 2009 to power Yandex.Metrica (Russia's largest web-analytics system); led its 2016 open-sourcing — Verified.
- **Aaron Katz (CEO)** — ex-CRO of Elastic (scaled sales ~$15M → $500M+); proposed spinning ClickHouse out as a standalone US company — Verified.
- **Yury Izrailevsky (President, Product & Technology)** — previously built Netflix's cloud infrastructure and led developer products at Google Cloud — Verified.

ClickHouse, Inc. incorporated in summer 2021, spinning the project out of Yandex; the company is US-based and the OSS project's governance moved with it — Verified.

## Funding
- Series A: $50M, 2021, led by Index Ventures and Benchmark — Verified
- Series B: $250M, Oct 2021, at $2B valuation (Coatue, Altimeter among leads) — Verified
- Series C: $350M, May 29, 2025, led by Khosla Ventures; BOND, IVP, Battery, Bessemer new; plus a $100M credit facility (Stifel, Goldman Sachs). Valuation not company-stated; press reported ~$6B+ — Reported
- Series C extension: Oct 2025, amount undisclosed (Citi Ventures, Insight Partners, Peak XV, D. E. Shaw Ventures, others) — Verified as event, amount Not found in public sources
- Series D: $400M, Jan 16, 2026, led by Dragoneer, at ~$15B valuation (Bloomberg) — Verified
- Total disclosed: ~$1.05B+ equity as of 2026-07-02 — Verified (sum of disclosed rounds)

## Evidence of real-world use
Unusually strong, with documented engineering case studies rather than logo walls: **Anthropic** uses ClickHouse for observability at the scale of Claude 4 development and connects Claude/Claude Code to it via the MCP server; **Tesla** monitors Gigafactories and its vehicle fleet on it and publicly stress-tested ingestion to a quadrillion rows; **OpenAI** ingests petabytes of log data per day (all Reported — ClickHouse case studies/videos, but detailed and first-person). Named customers also include Mercado Libre, Sony, Meta, Lyft, Instacart, Memorial Sloan Kettering, and agent-era companies Sierra, Poolside, Weights & Biases, and LangChain (LangSmith runs on it) — Reported. Scale metrics: 2,000+ customers (May 2025) → 4,000+ customers and $250M ARR, ~250–300% YoY growth (May 2026) — Reported. OSS: 48.5k GitHub stars, 8.6k forks, ~248k commits, active LTS releases as of July 2026 — Verified. Cloudflare, Uber, eBay, and many observability vendors (Sentry, PostHog, Highlight) have long run OSS ClickHouse — Reported.

## Relevance to agentic AI engineering
ClickHouse sits in the agent stack at two layers. First, **agent observability**: every serious agent deployment generates trace/eval/token-cost telemetry, and with Langfuse + ClickStack, ClickHouse now owns arguably the most-used open-source LLM tracing tool plus the storage engine under many others — the operational counterpart to this repo's tool-use/governance line (*The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*: you need exactly this telemetry to audit multi-tool loops). Second, **agents as query users**: the MCP server + agentic analytics bet treats the database itself as a tool an agent reasons over, which connects to *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* — ClickStack's "semantic tools for agents" is that paper's thesis productized. For agentic-SWE work (SWE-bench-style harnesses), it's the natural sink for run logs and eval matrices at scale.

## Use cases & considerations
1. Store agent traces/evals: self-host Langfuse (ClickHouse-backed) or ClickStack for OTel-instrumented agents.
2. Product analytics/event pipelines feeding agent context — billions of events, sub-second SQL.
3. Let an MCP-connected agent (Claude Code, LibreChat) query production metrics directly.
4. Log/observability consolidation off Datadog/Elasticsearch for cost (their TCO pitch).

Considerations: OLAP-only semantics (batch inserts, expensive mutations, joins weaker than Snowflake though improving); Cloud conveniences (SharedMergeTree, ClickPipes) are proprietary, so the low-lock-in story applies to core OSS only; self-hosting at scale is real ops work (Keeper, replication, schema design). Competitors: Snowflake/Databricks (warehouse side), Apache Druid/Pinot, StarRocks, DuckDB/MotherDuck (small-scale), Elasticsearch (logs). Open questions: whether Langfuse stays genuinely open under acquisition, and how hard the $15B valuation leans on the agent narrative versus classic analytics revenue.

## Sources
- https://clickhouse.com/company/our-story
- https://github.com/ClickHouse/ClickHouse
- https://clickhouse.com/blog/clickhouse-raises-350-million-series-c-to-power-analytics-for-ai-era
- https://clickhouse.com/blog/clickhouse-extends-series-c-financing-expands-leadership-team
- https://clickhouse.com/blog/clickhouse-raises-400-million-series-d-acquires-langfuse-launches-postgres
- https://www.bloomberg.com/news/articles/2026-01-16/clickhouse-lands-15-billion-valuation-in-ai-database-race
- https://techcrunch.com/2026/05/27/clickhouse-triples-annualized-revenue-to-250m-charting-a-path-toward-an-ipo/
- https://clickhouse.com/blog/how-anthropic-is-using-clickhouse-to-scale-observability-for-ai-era
- https://clickhouse.com/videos/tesla-observability
- https://clickhouse.com/blog/clickhouse-acquires-langfuse-open-source-llm-observability
- https://clickhouse.com/blog/building-a-data-platform-for-agents
- https://github.com/ClickHouse/agentic-data-stack
- https://clickhouse.com/blog/clickhouse-tops-250m-arr-and-4000-customers
- https://www.indexventures.com/perspectives/aaron-katzs-journey-from-salesforce-to-clickhouse/
- https://research.contrary.com/company/clickhouse
