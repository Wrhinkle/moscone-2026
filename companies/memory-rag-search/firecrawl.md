# Firecrawl

> An API that turns any website into clean, LLM-ready data — scrape, crawl, search, and extract endpoints that agents call instead of writing their own scrapers and parsers.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** silver
- **Founded:** 2022, San Francisco (YC S22, originally as Mendable; Firecrawl launched as OSS April 2024) (Verified — YC, company site, GitHub)
- **Website / GitHub:** https://www.firecrawl.dev · https://github.com/firecrawl/firecrawl

## What they do

Firecrawl is web-ingestion infrastructure for AI apps. You POST a URL (or a query) and get back markdown, structured JSON, HTML, or screenshots — with JS rendering, anti-bot handling, proxies, and parsing handled by their proprietary "Fire-Engine" backend. Core endpoints (Verified — docs/GitHub):

- **Scrape** — one URL → clean markdown/JSON/screenshot; the workhorse for RAG ingestion.
- **Crawl** — whole-site traversal without a sitemap; **Map** lists a site's URLs instantly.
- **Search** — web search that returns full page content for results, not just links (2 credits/10 results).
- **Extract** — schema-driven structured extraction ("agentic scraping": describe the fields, it finds them).
- **Interact / Agent** — drive pages with natural-language actions (click, fill, scroll) before extracting, for content behind interaction.

SDKs for Python, Node, Java, Rust, Elixir; the core repo is AGPL-3.0 and self-hostable, SDKs MIT, with the cloud service carrying the extra features (Fire-Engine, higher reliability). v2 shipped August 2025 alongside the Series A, adding semantic crawling and speed improvements (Verified — company blog). Pricing is public and credit-based: free 500 credits/mo, then Hobby → Standard (~$83/mo, 100k credits) → Growth/Scale/Enterprise; roughly 1 credit = 1 page (Verified — pricing page).

## Founders & origins

**Caleb Peffer** (CEO), **Eric Ciarla** (Chief Growth Officer), **Nicolas Silberstein Camara** (CTO) (Verified — company About page, YC). They entered YC S22 as **Mendable**, an AI chat-for-docs product used by teams at Snapchat, MongoDB, and DoorDash (~$250k ARR, Reported — Ciarla's LinkedIn). Building Mendable exposed the upstream bottleneck — getting clean web data into LLMs — so they open-sourced Firecrawl in April 2024, and the tool outgrew the parent product; Mendable was shut down in 2025 (Verified — LinkedIn post, press). TechCrunch noted their recurring stunt of posting job listings to "hire AI agents as employees" (Verified — TechCrunch, Aug 2025).

## Funding

- **Seed/YC:** ~$1.7M implied (total minus Series A); details not broken out in public sources (Unverified as a discrete round).
- **Series A:** $14.5M, announced Aug 19, 2025, led by **Nexus Venture Partners**, with Y Combinator, Shopify CEO Tobi Lütke, and Postman CEO Abhinav Asthana (Verified — GlobeNewswire, TechCrunch, SiliconANGLE).
- **Total raised:** $16.2M (Verified — company/press).

Small raise relative to the category (Exa: ~$357M) — they appear to be running lean on strong self-serve revenue rather than capital.

## Evidence of real-world use

Unusually strong OSS signal: the main repo shows **~145k GitHub stars** (Verified — GitHub, July 2026; among the most-starred AI infra repos anywhere), 8.3k+ forks, and the official **MCP server ~6.5k stars** — widely cited as the most-adopted scraping MCP server. Company-reported metrics (Reported — About page): 5B+ requests served, 1.25M+ developer signups, 150k+ companies, 2.5M+ weekly npm/PyPI downloads. Named customers with published detail: **Zapier** (web-knowledge feature in Zapier Chatbots, integrated "in an afternoon"), **Replit** (Replit Agent's ingestion of live API docs — one production incident in 4+ months, per their case study), **Shopify** (usage plus the CEO investing) (Verified — customer stories, Series A press). Apple and Canva appear as landing-page logos (Reported — treat as logos, not documented usage). A public pricing page and heavy MCP-registry presence confirm a real self-serve motion.

## Relevance to agentic AI engineering

Firecrawl is the ingestion layer of the memory/RAG stack: it feeds the pipelines this repo's memory papers assume exist ("Memory for Autonomous LLM Agents", "Are We Ready For An Agent-Native Memory System?", graph-RAG work like "GAM: Hierarchical Graph-based Agentic Memory"). Its Search endpoint puts it in the trajectory patterns studied in "Agentic Search in the Wild"; its schema-driven Extract speaks directly to "Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval". The Interact/Agent endpoints overlap with web-agent research ("AI Planning Framework for LLM-Based Web Agents", "WebXSkill") and, as a hosted tool an agent calls, with "The Evolution of Tool Use in LLM Agents". Via MCP it is a default web tool for Claude Code/Cursor-class coding agents. Relevant to the Ridgeline backlog item: the planned weekly signal-intelligence tracker is explicitly "Firecrawl-style."

## Use cases & considerations

Use cases: (1) RAG ingestion of docs/help centers into a vector store; (2) agent tool for live web lookup via MCP; (3) structured extraction for lead/competitor/permit-record monitoring; (4) feeding freshness-sensitive context (API docs, pricing pages) to coding agents.

Considerations: credits don't roll over; AGPL core means self-hosting is viable but the best reliability (Fire-Engine) is cloud-only — moderate lock-in. Scraping legality/ToS exposure sits with you. Competitors: **Exa** (search-first), **Apify**, **Bright Data**, **Oxylabs** (proxy/scale incumbents, all in this repo), **Tavily**, **Jina Reader**, and **Browserbase** for browser-level control. Open question: whether a thin-ish API layer defends against both proxy giants moving up and search-native rivals moving down.

## Sources

- https://www.firecrawl.dev/about
- https://github.com/firecrawl/firecrawl
- https://www.ycombinator.com/companies/firecrawl
- https://www.globenewswire.com/news-release/2025/08/19/3135573/0/en/firecrawl-announces-14-5-million-in-series-a-funding-to-put-web-data-on-tap-for-ai-agents.html
- https://techcrunch.com/2025/08/19/ai-crawler-firecrawl-raises-14-5m-is-still-looking-to-hire-agents-as-employees/
- https://siliconangle.com/2025/08/19/firecrawl-raises-14-5m-grow-ai-ready-web-data-infrastructure/
- https://www.firecrawl.dev/blog/firecrawl-v2-series-a-announcement
- https://www.firecrawl.dev/blog/category/customer-stories
- https://www.firecrawl.dev/pricing
- https://github.com/firecrawl/firecrawl-mcp-server
- https://www.linkedin.com/posts/eric-ciarla_we-shut-down-our-250k-arr-ai-startup-almost-activity-7339309843272376321-_4Ll
