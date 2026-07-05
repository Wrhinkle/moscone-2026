# Apify

> A cloud platform and marketplace of ~48,000 ready-made web scrapers ("Actors") that turns any website into structured data an app — or an AI agent via MCP — can consume.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2015, via Y Combinator Fellowship (Mountain View); headquartered in Prague, Czech Republic since 2016 (Verified — company site + press)
- **Website / GitHub:** https://apify.com · https://github.com/apify · https://mcp.apify.com

## What they do

Apify is a full-stack web scraping and browser automation platform. The core unit is the **Actor**: a containerized program (typically Node.js or Python, often driving Playwright/Puppeteer) that runs on Apify's cloud with managed proxies, scheduling, storage (datasets/key-value stores), and an auto-generated API. You can write your own Actors or pull from **Apify Store**, a marketplace of 30,000–48,000+ ready-made scrapers for Google Maps, Instagram, TikTok, LinkedIn, Amazon, etc. (the company site claimed 48,311 Actors as of 2026-07-02). Third-party developers monetize Actors — Apify pays out 80% of revenue; top independent creators reportedly earn $10k+/month — making it a genuine two-sided marketplace, not just a hosted tool.

Two pieces matter most for AI engineers. First, **Crawlee**, their open-source crawling library for Node.js (~23.7k GitHub stars) and Python, explicitly positioned for "extracting data for AI, LLMs, RAG, or GPTs." Second, the **Apify MCP server** (mcp.apify.com, OAuth-enabled hosted endpoint; ~1.6k stars on GitHub), which exposes any Store Actor as a tool to MCP clients (Claude, VS Code, Cursor, ChatGPT) with **dynamic tool discovery** — the agent searches the Store for a scraper at runtime instead of being pre-configured. They also ship native integrations for LangGraph, CrewAI, and Mastra, a RAG Web Browser Actor for agent web search/browsing, and experimental **agentic payments** (x402 USDC-on-Base and Skyfire) so agents can pay for Actor runs without holding an API token.

## Founders & origins

**Jan Čurn (CEO) and Jakub Balada** — Verified across the company's About page and press. They met studying computer science (Charles University's Faculty of Mathematics and Physics, per company bio), launched in the 2015 Y Combinator Fellowship, and moved the company back to Prague in 2016. Čurn remains CEO.

## Funding

Notably capital-light. Seed funding totaling roughly **$0.5M through 2019** (Reported — company statements via press), then bootstrapped and profitable. In **April 2024** raised **~€2.8M (~$3M)** led by J&T Ventures with participation from Reflex Capital (Verified — Vestbee, The Recursive, Tech Funding News). Total raised: roughly **$3.5M** — tiny relative to revenue: Čurn reported **$7.5M revenue and $1M profit in 2023, growing ~80% YoY** (Reported); one tracker (Getlatka) lists $13.3M ARR for 2024 (Reported, single source).

## Evidence of real-world use

Strong and documented, not just logos:

- **Intercom's Fin** — Apify's own case-study blog documents that Fin, Intercom's support chatbot, uses Apify crawling to ingest customer websites/docs; Fin resolved 18% of support queries after enablement (Reported — Apify blog, but specific and dated).
- **Groupon** — uses Apify for merchant lead generation via web data (Reported — Apify success stories).
- Company claims **67,000 customers** and 1+ PB of data processed monthly (Reported — About page); enterprise page names T-Mobile, Microsoft, Samsung, Princeton (logos-on-page tier).
- OSS: Crawlee at ~23.7k stars plus an active Python port; a working marketplace where third parties earn real money is itself usage evidence.

## Relevance to agentic AI engineering

Apify sits in the **data-acquisition/tool layer** of an agent stack: it is the "hands on the open web" that feeds RAG indexes and agent memory. The MCP server's runtime Actor discovery is a live instance of the multi-tool orchestration problem studied in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and its web-facing agents connect to *AI Planning Framework for LLM-Based Web Agents*, *WebXSkill: Skill Learning for Autonomous Web Agents*, and *Agentic Search in the Wild*. Scraped-output schemas bear on *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*; agentic payments and letting agents pull arbitrary Store tools raise exactly the concerns in *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too* (untrusted web content entering the loop).

## Use cases & considerations

Use cases: (1) feed fresh web data into a RAG/agent-memory pipeline (the Intercom Fin pattern); (2) give an agent web-search + scraping tools via one hosted MCP endpoint instead of writing per-site scrapers; (3) lead-gen/market-monitoring pipelines from Maps/social scrapers; (4) self-host crawling with Crawlee, graduating to the platform for proxies/scale.

Considerations: per-result pricing ($1–10 per 1,000 results typical) can compound at scale; Store Actor quality varies by third-party maintainer; scraping social platforms carries ToS/legal exposure the customer bears; injecting arbitrary scraped web content into agents is a prompt-injection surface. Main competitors: **Bright Data** (also AIEWF, same category), Zyte, Firecrawl, Browserbase (adjacent), ScrapingBee. Open question: how durable per-site scrapers remain as anti-bot arms races and generic computer-use agents advance.

## Sources

- https://apify.com/about
- https://apify.com/success-stories
- https://blog.apify.com/intercom-customer-support-ai-chatbot-web-scraping/
- https://github.com/apify/apify-mcp-server
- https://github.com/apify/crawlee
- https://docs.apify.com/platform/integrations/mcp
- https://docs.apify.com/academy/actor-marketing-playbook/store-basics/how-actor-monetization-works
- https://apify.com/pricing
- https://www.vestbee.com/insights/articles/czech-apify-secures-around-3-m
- https://therecursive.com/czech-apify-secured-e2-8m-investment-to-fuel-growth-in-web-data-extraction/
- https://techfundingnews.com/prague-based-apify-snaps-e2-8m-for-ai-web-data-extraction-platform/
- https://getlatka.com/companies/apify
