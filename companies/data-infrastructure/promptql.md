# PromptQL

> Hasura's AI-native successor to GraphQL: instead of generating an API to your data, it generates and executes a program in natural language to answer a question accurately over your business data.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** silver
- **Founded:** Built by Hasura (founded 2017); PromptQL launched as a distinct product/rebrand line in 2024-2025 (Reported)
- **Website / GitHub:** https://promptql.io · https://github.com/hasura/promptql-mcp

## What they do
PromptQL is a data-access layer for LLMs/agents: given a natural-language query, it plans an approach, writes and executes code against your connected data sources (databases, warehouses, SaaS tools, docs, Slack, tickets), fixes errors from the results, and returns an answer while showing its work (sources pulled, assumptions made). It's positioned as the AI-era successor to Hasura's GraphQL engine — instead of exposing CRUD endpoints, it exposes a natural-language interface that composes arbitrary business logic on the fly. Ships an MCP server (hasura/promptql-mcp) so it can be wired directly into agent tool-calling stacks, and a connector pattern (e.g. importing a Hugging Face dataset into DuckDB for NL querying) for extending it to new sources.

## Founders & origins
Built by the Hasura team; Hasura was co-founded by Tanmai Gopal (CEO) and Rajoshi Ghosh (Verified — Crunchbase, ForbesIndia).

## Funding
No PromptQL-specific round found; it is a product of Hasura, which has raised ~$239M total including a $100M Series C in Feb 2022 at a ~$1B valuation (Verified for Hasura; PromptQL itself has no separately disclosed funding).

## Evidence of real-world use
Client roster cited on PromptQL's own site includes OpenAI, Siemens, Airbus, NASA, and Atlassian (company-stated, treat as Reported rather than independently verified). VentureBeat reported PromptQL has signed seven-figure enterprise deals and offers $900/hour "AI engineer" access aimed at the ~95% enterprise-AI-failure-rate problem.

## Relevance to agentic AI engineering
Directly addresses the tool-calling/data-access layer of an agent stack: how an agent reliably queries heterogeneous enterprise data sources with accuracy guarantees and auditability, an alternative to hand-rolled RAG or ad hoc SQL-generation agents.

## Use cases & considerations
Use cases: natural-language BI/analyst agents over warehouse data, customer-support assistants that pull live account data, "AI engineer" style deep investigations billed by usage (OLUs, ~$0.20 each). Considerations: pricing is usage-metered and can get expensive for heavy workloads; competitors include text-to-SQL tools, general RAG frameworks, and other enterprise data-agent platforms (e.g. Glean, Sourcegraph-style code/data agents); depends on Hasura's broader GraphQL/DDN ecosystem for connectors.

## Sources
- https://promptql.io/about
- https://promptql.io/pricing
- https://hasura.io/blog/from-graphql-to-promptql-a-new-chapter-begins
- https://github.com/hasura/promptql-mcp
- https://venturebeat.com/technology/promptqls-usd900-hour-ai-engineers-are-coming-for-mckinseys-ai-business
- https://techcrunch.com/2022/02/22/graphql-developer-platform-hasura-raises-100m-series-c/
- AI Engineer World's Fair 2026 sponsor list (silver tier), https://www.ai.engineer/worldsfair/2026
