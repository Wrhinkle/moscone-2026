# dbt Labs

> The company behind dbt, the de facto standard for SQL-based data transformation in warehouses — now merged with Fivetran and repositioned as the "trusted context" layer that AI agents reason from.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** supporting
- **Founded:** 2016, Philadelphia (as Fishtown Analytics; renamed dbt Labs 2021) — Verified
- **Website / GitHub:** https://www.getdbt.com · https://github.com/dbt-labs/dbt-core

## What they do
dbt ("data build tool") lets analysts build data pipelines the way engineers build software: transformations are SQL `SELECT` statements plus Jinja templating, organized as a DAG of models with version control, tests, documentation, and lineage generated from the project itself. It runs *inside* your warehouse (Snowflake, BigQuery, Databricks, Redshift, etc.) — dbt compiles and orchestrates SQL, it doesn't move data. **dbt Core** is the open-source engine (Apache 2.0, 13.4k GitHub stars); the **dbt Platform** (formerly dbt Cloud) adds scheduling, CI, a hosted IDE, and the commercial features.

Two 2025–26 shifts matter. First, the **dbt Fusion engine**: a ground-up Rust rewrite of the runtime (shipping as dbt Core v2.0, Apache 2.0, currently alpha on `main`) with much faster parse/compile, a self-contained binary, and stricter SQL understanding. Second, an explicit AI-agent stack: the **dbt Semantic Layer** (MetricFlow) defines governed metrics/dimensions once; the **dbt MCP server** (`dbt-labs/dbt-mcp`, local via `uvx` or remote over HTTP) exposes models, metrics, lineage, freshness, and dbt CLI commands to agents like Claude and Cursor; and **dbt-agent-skills** packages curated Agent Skills for dbt workflows. At the June 2026 merger close they also announced **dbt Wizard** (an autonomous agent for model authoring/refactoring/debugging grounded in project context) and **dbt State** (incremental caching that only rebuilds what changed; claimed 30%+ infra savings — Reported, vendor-stated).

In October 2025 dbt Labs agreed to an all-stock **merger with Fivetran**, completed June 1, 2026. George Fraser (Fivetran) is CEO; Tristan Handy is President. The combined pitch: ingestion (Fivetran) + transformation/semantics (dbt) as "open data infrastructure for trusted AI agents." dbt remains a distinct product line and brand.

## Founders & origins
**Tristan Handy** (CEO), **Connor McArthur**, and **Drew Banin** — Verified. All three were colleagues at RJMetrics (Philadelphia analytics startup). They founded Fishtown Analytics in 2016 as a consultancy — named for Handy's Philadelphia neighborhood — and built dbt as an open-source tool for their client work. It grew by word of mouth to 1,000+ companies before they raised venture money, coining "analytics engineering" as the discipline along the way. Renamed dbt Labs in 2021.

## Funding
- Seed: $1.5M, 2019 (Amplify Partners) — Reported
- Series A: $12.9M, April 2020, Andreessen Horowitz — Verified
- Series B: $29.5M, November 2020 (Sequoia/a16z participating) — Reported
- Series C: $150M, June 2021, Altimeter/Sequoia/a16z — Verified
- Series D: $222M, February 2022, at **$4.2B valuation**, led by Altimeter; new investors Coatue, Tiger Global, ICONIQ, GV, GIC, plus strategics **Databricks, Snowflake, and Salesforce Ventures** — Verified
- Total raised: ~$416M (Tracxn) — Reported. Forbes noted the Series D closed ~$2B below the initially floated valuation. Now part of Fivetran via all-stock merger (no cash value disclosed; press reports pegged the combined entity around $6B — Reported).

## Evidence of real-world use
Very strong — dbt is arguably the most-adopted tool in the "modern data stack." Surpassed **5,000 dbt Platform customers** (Feb 2025, 30% YoY) and **$100M+ ARR** with 85% YoY growth in Fortune 500 adoption — Verified (company press, multiple outlets). Named customers include Condé Nast, Siemens, and SpotOn (published case study: 6x faster insights); getdbt.com hosts 40+ case studies. The open-source footprint is bigger than the paying base: dbt-core has 13.4k stars/2.5k forks, a huge community Slack, and an ecosystem of adapters, packages, and consultancies built around it. "Knows dbt" is a standard line item in analytics-engineer job postings — the hiring market itself is adoption evidence.

## Relevance to agentic AI engineering
dbt's bet is that agents fail on enterprise data not from weak models but from missing governed context — exactly the question in *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*. The Semantic Layer + MCP server turns "text-to-SQL and hope" into tool calls against defined metrics with lineage and freshness — the governed-surface pattern argued for in *Governance by Construction for Generalist Agents*, delivered through the multi-tool orchestration lens of *The Evolution of Tool Use in LLM Agents*. dbt Wizard, meanwhile, is an agentic-SWE play on a specific brownfield codebase type (large Jinja-SQL DAGs) — long-horizon repo evolution of the kind *SWE-EVO* and *SlopCodeBench* benchmark.

## Use cases & considerations
1. Point the dbt MCP server at your project so Claude/Cursor agents can discover models, query governed metrics, and run dbt commands instead of writing raw SQL.
2. Standard warehouse transformation with tests + lineage as the foundation under any RAG/analytics-agent stack.
3. Define metrics once in the Semantic Layer so agent, BI, and notebook answers agree.
4. dbt Core self-hosted for zero-cost, no-lock-in pipelines.

Considerations: Fusion/v2.0 is alpha — APIs and artifacts may change; the Fivetran merger raises pricing and open-source-stewardship questions the community is actively debating (Fusion's runtime is Apache 2.0, but parts of Fusion tooling are not); Platform pricing is seat/usage-based and climbs at enterprise scale. Competitors: SQLMesh/Tobiko (most direct), Coalesce, Dataform (Google), and warehouse-native transformation features. Open question: whether the MCP/Semantic Layer becomes the default agent-to-warehouse interface or gets bypassed by warehouse vendors' own agents (Snowflake Intelligence, Databricks Genie).

## Sources
- https://www.getdbt.com/about-us and https://www.getdbt.com/case-studies
- https://review.firstround.com/dbt-labs-path-to-product-market-fit/
- https://www.inquirer.com/business/dbt-labs-fishtown-analytics-tristan-handy-fivetran-acquisition-20251218.html
- https://www.getdbt.com/blog/dbt-labs-raises-222m-in-series-d-funding-at-4-2b-valuation-led-by-altimeter-with-participation-from-databricks-and-snowflake
- https://www.forbes.com/sites/kenrickcai/2022/02/24/dbt-labs-series-d-4-billion-less-than-planned/
- https://tracxn.com/d/companies/dbt-labs/__uetvGc5wXa2wwZOwATP8qaOeg7oS0Dcnlxf8-bQRXS4
- https://www.fivetran.com/press/fivetran-dbt-labs-complete-merger-to-create-the-data-infrastructure-for-trusted-ai-agents
- https://www.getdbt.com/blog/dbt-labs-and-fivetran-merge-announcement
- https://github.com/dbt-labs/dbt-core · https://github.com/dbt-labs/dbt-mcp · https://github.com/dbt-labs/dbt-agent-skills
- https://docs.getdbt.com/docs/dbt-ai/about-mcp
- https://www.getdbt.com/blog/ai-ready-data-in-practice-what-dbt-semantic-layer-and-dbt-s-mcp-server-and-agent-skills-do-for
- https://finance.yahoo.com/news/dbt-labs-surges-past-100-140000082.html
- https://www.getdbt.com/case-studies/spoton
