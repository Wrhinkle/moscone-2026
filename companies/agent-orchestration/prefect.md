# Prefect

> Python workflow-orchestration company (open-source engine + managed cloud) that has pivoted hard into AI infrastructure — it now maintains FastMCP, the dominant Python framework for building MCP servers, plus managed MCP hosting.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** 2018, Washington, DC — remote-first with hubs in DC, Chicago, and the SF Bay Area (Verified — Technical.ly, company sources)
- **Website / GitHub:** https://www.prefect.io · https://github.com/PrefectHQ/prefect · https://github.com/PrefectHQ/fastmcp

## What they do

Prefect's core is an Apache-2.0 Python orchestration framework (22.8k stars / 2.4k forks) for building resilient data pipelines: you decorate ordinary Python functions as `@flow` and `@task` and get scheduling, retries, caching, concurrency limits, event-driven triggers, and observability without rewriting code into a DAG DSL — its founding pitch was explicitly "the anti-Airflow." **Prefect Cloud** is the commercial managed control plane (hosted API, RBAC, SLAs, audit logs, with a public pricing page and free tier); execution stays on your infrastructure via workers, a hybrid model similar to Temporal's. Prefect 3.0 (2024) added transactional semantics — groups of tasks succeed or roll back together (Verified — GitHub, BigDATAwire).

The AI story is now the bigger one. Founder Jeremiah Lowin created **FastMCP**; v1 was incorporated into Anthropic's official MCP Python SDK in 2024, and the standalone FastMCP 2.0 (April 2025) became the de facto way to build MCP servers in Python — ~23k stars, roughly a million downloads a day, with the company claiming some version of FastMCP powers ~70% of MCP servers across languages (Reported — jlowin.dev, vendor claim). The repo moved from Lowin's personal account to PrefectHQ, and FastMCP 3.0 went GA in February 2026. On top of it Prefect launched **FastMCP Cloud / Prefect Horizon**: managed MCP hosting that deploys a server from a GitHub repo in under a minute, with OAuth, serverless autoscaling, and JSON-RPC-native observability (public beta, free during beta). A third line, **Marvin** (agentic framework on Pydantic AI), absorbed the earlier ControlFlow agent-orchestration project, whose repo was archived in March 2026 (Verified — GitHub).

## Founders & origins

**Jeremiah Lowin**, sole founder and CEO (Verified). Previously Manager of Market Risk / data scientist at King Street Capital Management (2007–2011) and founder of Lowin Data Company (2011–2013, ML for time series); he was also a significant early Apache Airflow contributor/PMC member, which directly informed Prefect's design (Reported — Madrona podcast, interviews). Origin story: a 2017 prototype called "Tin Man" that two counterparties' data leaders each said they'd buy on sight (Reported — Prefect blog).

## Funding

- **Series A, $11.5M (Feb 2021)** (Verified — Technical.ly, Crunchbase News)
- **Series B, $32M (June 2021):** led by Tiger Global, with Bessemer Venture Partners and Positive Sum (Verified — PRNewswire, Crunchbase News)
- **Total raised: >$45M as of June 2021** (Verified — Series B press). No later rounds found in public sources as of 2026-07-02; how the FastMCP push is financed (revenue vs. unannounced capital) is unverified.

## Evidence of real-world use

Strong for OSS, moderate for named case studies. Documented customers: **WHOOP** (cut data-platform incidents ~75%, grew from Cloud free tier to paid with SLAs/audit logs) and the **Washington Nationals** (player-development and scouting pipelines) — both first-party case studies; **Cash App** is named by Prefect as a user without a detailed writeup (Reported). Vendor-claimed scale: ~31M monthly downloads and 200M+ tasks orchestrated monthly, with 55% of surveyed users running Prefect in production in 2025 (Reported — vendor figures). FastMCP's adoption is the standout signal: incorporation into the official MCP Python SDK is third-party validation, and 10k GitHub stars in ~6 weeks vs. 4 years for Prefect itself (Verified — jlowin.dev). FastMCP Cloud beta: 1,000+ developer signups in its first week, 93% deploying within five minutes (Reported — vendor).

## Relevance to agentic AI engineering

Prefect occupies two layers of the agent stack. As an orchestrator it is the durable, observable execution substrate under long-running agent pipelines — directly relevant to the long-horizon degradation problems documented in **SlopCodeBench** and **SWE-EVO**: checkpointed, retryable, transactional task graphs are the infrastructure answer to agents that drift over extended runs. Via FastMCP it owns the tool-serving layer itself, which maps onto **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**; Horizon's OAuth, access control, and JSON-RPC-level audit trail are a practical implementation of the concerns in **Governance by Construction for Generalist Agents**. Marvin's `marvin.Memory` primitive touches the agent-memory line (**Memory for Autonomous LLM Agents**), though it's far less battle-tested than the other two products.

## Use cases & considerations

Use cases: (1) orchestrating scheduled/event-driven agent pipelines (nightly enrichment, document-processing back-office flows) with retries and observability; (2) building an MCP server for internal tools in a few dozen lines of FastMCP and hosting it on Horizon rather than running your own gateway; (3) hardening an existing Python ETL/ML codebase incrementally, since decorators wrap existing functions; (4) exposing an existing REST API to agents via FastMCP's OpenAPI generation.

Considerations: visible strategy churn in the agent-framework line (Marvin → ControlFlow → back to Marvin, archived repos) argues for treating Marvin cautiously; FastMCP Cloud pricing after beta is unannounced; no funding since 2021 makes commercial durability a fair diligence question. Orchestration competitors: **Airflow, Dagster, Temporal, Inngest, Flyte**. MCP-hosting competitors: **Smithery, Cloudflare (remote MCP), mcp.run**. Open question: whether owning both the MCP framework and its default hosting platform converts into durable revenue before hyperscalers commoditize MCP hosting.

## Sources

- https://www.prefect.io/ and https://github.com/PrefectHQ/prefect
- https://technical.ly/startups/prefect-jeremiah-lowin/
- https://www.prnewswire.com/news-releases/prefect-announces-32m-series-b-funding-led-by-tiger-global-to-deliver-on-growing-demand-for-dataflow-automation-301309467.html
- https://news.crunchbase.com/enterprise/prefect-raises-32m-to-be-the-toothpick-in-companies-data-stack/
- https://www.prefect.io/blog/how-jeremiah-lowin-turned-a-life-long-question-into-an-industry-leading-startup
- https://www.madrona.com/building-a-healthy-open-source-community-with-jeremiah-lowin-founder-and-ceo-of-prefect/
- https://www.jlowin.dev/blog/fastmcp-2-10k-stars and https://jlowin.dev/blog/fastmcp-3-launch
- https://github.com/PrefectHQ/fastmcp
- https://www.prefect.io/blog/accelerating-ai-with-fastmcp-cloud and https://gofastmcp.com/deployment/prefect-horizon
- https://www.prefect.io/blog/how-whoop-cut-incidents-by-75-with-prefect
- https://www.prefect.io/blog/nationals-prefect
- https://github.com/prefect-archive/ControlFlow and https://github.com/PrefectHQ/marvin
- https://www.hpcwire.com/bigdatawire/this-just-in/prefect-3-0-enhances-data-workflows-with-transactional-and-flexible-orchestration/
