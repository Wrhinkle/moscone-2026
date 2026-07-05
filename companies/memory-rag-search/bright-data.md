# Bright Data

> Web-data infrastructure at industrial scale: proxy networks, unblocking APIs, prebuilt datasets, and an MCP server that gives AI agents live, unblocked access to the public web.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** platinum
- **Founded:** 2014, Israel (as Luminati Networks, a division of Hola VPN) (Verified — Wikipedia, company blog)
- **Website / GitHub:** https://brightdata.com · https://github.com/brightdata

## What they do

Bright Data operates one of the largest web-data collection platforms in existence. The base layer is a proxy network — residential, ISP, datacenter, and mobile IPs across ~195 countries (company claims range up to 150M–400M+ IPs; treat exact counts as company-claimed) — used to route requests so scrapers look like real users. On top of that sit engineer-facing APIs: **Web Unlocker** (fetch any page through CAPTCHA/Cloudflare/JS-rendering walls, priced per successful request), **SERP API** (structured results from major search engines, from ~$1.50/1K requests), **Web Scraper APIs** (site-specific structured extractors for e-commerce, social, maps, etc.), **Scraping Browser** (remote browser sessions for agent/automation workloads), a **dataset marketplace** (350+ prebuilt datasets), and **Deep Lookup** (natural-language entity research API). Public pricing pages and free tiers across products = real self-serve commercial motion (Verified).

The AI-era pivot is **The Web MCP** (launched August 2025 after a private beta with ~15,000 developers): an MIT-licensed Model Context Protocol server (github.com/brightdata/brightdata-mcp, ~2.5k stars) exposing tools like `search_engine`, `scrape_as_markdown`, batch scrape/extract, and 60+ Pro-mode tools including browser control. Free tier of 5,000 requests/month; works with Claude, LangChain, CrewAI, LlamaIndex, and IDEs. Bright Data claims it powers 100M+ daily agent interactions (Reported — company/press, not independently verified). Practically: it is the "live web retrieval" tool you drop into an agent instead of building your own scraping + unblocking stack.

## Founders & origins

Founded 2014 by **Ofer Vilenski** and **Derry Shribman** (Verified), who had founded the peer-to-peer VPN **Hola** in 2008. Luminati originally monetized Hola's free-VPN userbase as residential exit nodes (~$20/GB) — a controversial origin worth knowing (Verified — Wikipedia, press). Sold to London PE firm **EMK Capital** in 2017 at a ~$200M valuation; renamed Bright Data in March 2021. **Or Lenchner** has been CEO since 2018 (Verified).

## Funding

Not a VC-track startup: PE-owned by **EMK Capital** since 2017 (~$200M acquisition value, Verified). No public post-2017 rounds found. Reported financials: crossed **$300M ARR in 2025**, ~50% YoY growth, targeting $400M in 2026; valuation "in excess of $1B" (Reported — Asymmetrix/CEO statements; no audited figures public).

## Evidence of real-world use

Strong and unusually well-documented for this category:

- **Litigation wins that define the industry:** In *Meta v. Bright Data* (N.D. Cal., Jan 2024), Judge Edward Chen granted Bright Data summary judgment — logged-off scraping of public data doesn't breach Meta's terms; discovery revealed **Meta itself had been a Bright Data customer** for e-commerce data (Verified — TechCrunch, court coverage). *X Corp v. Bright Data* was dismissed in May 2024, the court warning against platforms creating "information monopolies" (Verified). Being sued by Meta and X and winning is strong evidence of both scale and legal posture.
- **Named customers:** Yutori (co-founder Devi Parikh cites their browser infrastructure for scaling AI agents), Bitget, Remazing, Cervello (Reported — company customer stories, so treat as curated). Hugging Face published an official integration blog for the Web MCP.
- OSS/community: MCP repo ~2.5k stars, free-tier adoption, listings across LangChain/LlamaIndex tool ecosystems (Verified).

## Relevance to agentic AI engineering

Bright Data is the **retrieval-from-the-live-web layer** of the agent stack — the counterpart to internal-corpus RAG. It's directly relevant to *Agentic Search in the Wild: Intents and Trajectory Characteristics of Autonomous Web-Search Agents* (their SERP/MCP tools are exactly the substrate such agents run on), *AI Planning Framework for LLM-Based Web Agents* and *WebXSkill: Skill Learning for Autonomous Web Agents* (unblocked page access and remote browsers are the environment those papers assume), and *The Evolution of Tool Use in LLM Agents* (the Web MCP's Rapid/Pro tool tiers are a live example of multi-tool orchestration design). The governance angle matters too: piping arbitrary scraped web content into agents is the prompt-injection surface *CaMeLs Can Use Computers Too* and *Governance by Construction for Generalist Agents* address — an operator should sanitize/sandbox MCP outputs. For deep-research patterns (*Deep Researcher Agent*), Bright Data competes with Tavily/Exa/Firecrawl as the search-and-fetch backend.

## Use cases & considerations

Use cases: (1) a weekly signal-intelligence agent tracking competitors, suppliers, or specific people via SERP API + scrape-as-markdown (matches this repo's backlog item); (2) grounding a research agent with live, geo-accurate web data instead of stale index snapshots; (3) structured e-commerce/social datasets for market analysis without building scrapers; (4) Scraping Browser as the execution environment for browser-using agents.

Considerations: per-request/per-GB pricing climbs fast at agent volumes; the residential-IP sourcing model carries ethical/reputational history (Hola exit nodes) even though the company now runs compliance/KYC programs; target sites change and per-site scrapers can break; legal wins cover *public* data in the US — logged-in or personal-data scraping is a different risk class. Competitors: **Oxylabs, Zyte, Apify, Decodo (Smartproxy), ScraperAPI**, and on the agent-search side **Firecrawl, Tavily, Exa**. Open question: whether model providers' built-in web search erodes the standalone agent-retrieval market, or whether unblocking-at-scale stays a defensible moat.

## Sources

- https://en.wikipedia.org/wiki/Bright_Data
- https://brightdata.com/about · https://brightdata.com/ai · https://brightdata.com/ai/mcp-server
- https://github.com/brightdata/brightdata-mcp
- https://insideainews.com/2025/08/12/bright-data-launches-the-web-mcp-for-ai-agents-live-web-access/
- https://siliconangle.com/2025/08/12/bright-data-debuts-free-tier-web-mcp-support-real-time-ai-interaction-web/
- https://techcrunch.com/2024/01/24/court-rules-in-favor-of-a-web-scraper-bright-data-which-meta-had-used-and-then-sued/
- https://www.quinnemanuel.com/the-firm/news-events/client-alert-meta-v-bright-data-significant-decision-for-web-scraping-industry/
- https://www.lowenstein.com/news-insights/publications/client-alerts/meta-v-bright-data-ruling-has-important-implications-for-webscraping-activities-by-investment-advisers-im
- https://asymmetrixintelligence.substack.com/p/bright-data-reaches-300m-arr-amidst
- https://www.emkcapital.com/our-portfolio/bright-data
- https://brightdata.com/customer-stories · https://brightdata.com/pricing/serp
- https://huggingface.co/blog/BrightData/web-mcp-hugging-face-agent
