# Oxylabs

> Bootstrapped Lithuanian web-data infrastructure giant: one of the two largest proxy/scraping platforms in the world (Bright Data's arch-rival), now shipping MCP servers and an AI Studio to feed live web data to agents.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2015, Vilnius, Lithuania — incubated in the Tesonet accelerator (Verified — company about page, Wikipedia/Tesonet, Crunchbase)
- **Website / GitHub:** https://oxylabs.io · https://github.com/oxylabs · https://aistudio.oxylabs.io

## What they do

The base business is proxy infrastructure: residential, datacenter, mobile, ISP, and SOCKS5 proxies, with a claimed **177M+ residential IP pool** across ~195 countries (company-claimed; treat exact counts skeptically — the number has grown from "102M" to "177M" in company copy). On top sit engineer-facing products: **Web Scraper API** (submit a URL, get parsed results back; billed per *successful* result, Micro plan from ~$49/mo), **Web Unblocker** (~$9.40/GB; CAPTCHA/anti-bot/JS-rendering bypass, rebranded from "Next-Gen Residential Proxies" in 2023), a headless **Scraping Browser**, **Scheduler** for recurring jobs, and prebuilt **datasets**. Public per-GB/per-result pricing pages across every product = real self-serve commercial motion (Verified).

The AI layer is recent and aggressive. **OxyCopilot** (2024) is an AI assistant that generates scraping/parsing code from prompts inside the Scraper API. **AI Studio** (aistudio.oxylabs.io) is the agent-native surface: five apps — AI-Scraper (natural-language structured extraction), AI-Crawler, Browser Agent, AI-Search, AI-Map (site-structure mapping) — exposed via Python/JS SDKs and a native **MCP server** (github.com/oxylabs/oxylabs-ai-studio-py, MIT, v0.8.1 April 2026, ~94 stars). Practically: it's the "give my agent unblocked live-web access" dependency, same slot as Bright Data's Web MCP but with a much smaller OSS footprint so far.

## Founders & origins

Muddier than usual. Company databases (Crunchbase, Tracxn) list **Mindaugas Čaplinskas** as founder (Reported); Oxylabs grew out of **Tesonet**, the Vilnius startup studio co-founded by **Tomas Okmanas** and **Eimantas Sabaliauskas** (also behind Nord Security/NordVPN), so they are frequently credited as co-founders (Reported — Wikipedia/Tesonet, press). **Julius Černiauskas** led the company as CEO from 2020 and is now listed as Chairman of the Board, with **Juras Juršėnas** as COO (Verified — company about page, press interviews). The company's own materials avoid naming founders — likely deliberate given the Tesonet association.

## Funding

**No outside VC — bootstrapped/self-funded** (Verified across Latka, Dealroom, press). Revenue estimates vary wildly by source: **$43.7M ARR** (GetLatka) vs **~$105M** (Owler) — both Reported, no audited figures; ~480–500 employees (Verified-ish, multiple sources). Instead of raising, they acquire: **Webshare** (Silicon Valley self-serve proxy company, Sept 2022) and **ScrapingBee** (French scraping-API startup, June 2025) — both Verified (press, Tech.eu). Company claims 160+ patents (company-claimed).

## Evidence of real-world use

- **Named case studies:** trivago (residential proxies for accommodation-price data), Wiser Solutions (retail intelligence), Price2Spy (price monitoring, 750+ end clients), Crawly (1B+ requests/month through Oxylabs), Epicup (SEO data) — all company-published, so curated but named and specific (Reported).
- Company claims **15,000+ clients** (company-claimed, about page).
- **Litigation as evidence of scale:** a years-long patent war with Luminati/Bright Data — first suit filed 2018, settled with prejudice Feb 2020; further Bright Data suits followed, and Oxylabs counter-sued for patent infringement in Jan 2022 (Verified — press releases, Proxyway). You don't get sued repeatedly by the market leader unless you're the #2 taking share.
- OSS footprint is broad but shallow: the oxylabs GitHub org has many SDK/tutorial repos; the AI Studio MCP server is young (~94 stars vs Bright Data MCP's ~2.5k).

## Relevance to agentic AI engineering

Same slot as Bright Data in this landscape: the **live-web retrieval layer** for agents, complementary to internal-corpus RAG. Their MCP + Web Scraper API pipeline is exactly the substrate studied in *Agentic Search in the Wild* and a working example of the tool-tier design discussed in *The Evolution of Tool Use in LLM Agents*; AI Studio's Browser Agent is the environment assumed by *AI Planning Framework for LLM-Based Web Agents* and *WebXSkill*. The governance caveat from *CaMeLs Can Use Computers Too* and *Governance by Construction for Generalist Agents* applies verbatim: scraped pages entering an agent's context are a prompt-injection surface — sanitize MCP outputs. For *Deep Researcher Agent*-style pipelines, AI-Search/AI-Crawler compete with Tavily, Exa, and Firecrawl as the fetch backend.

## Use cases & considerations

Use cases: (1) competitor/supplier price-and-signal monitoring agents via Web Scraper API + Scheduler (maps to this repo's signal-intelligence backlog item); (2) MCP-based live-web grounding for research agents where geo-accurate, unblocked access matters; (3) ScrapingBee/Webshare as cheaper self-serve entry points into the same stack; (4) Browser Agent for form-filling/interactive extraction without running your own browser farm.

Considerations: per-GB residential pricing ($99+/GB entry) gets expensive at agent volumes; bootstrapped + acquisitive means no funding-driven urgency but also less ecosystem spend than Bright Data (visible in the OSS star gap); residential-IP sourcing ethics deserve diligence (they market "ethically sourced" — company-claimed); revenue figures unverifiable. Competitors: **Bright Data, Zyte, Apify, Decodo (Smartproxy), ScraperAPI**, plus **Firecrawl/Tavily/Exa** on the agent-search side. Open question: whether AI Studio can win agent-builder mindshare late, or remains an add-on for existing proxy customers.

## Sources

- https://oxylabs.io/about-us · https://oxylabs.io/pricing · https://oxylabs.io/products/scraper-api
- https://aistudio.oxylabs.io/ · https://github.com/oxylabs/oxylabs-ai-studio-py
- https://oxylabs.io/blog/oxylabs-model-context-protocol
- https://en.wikipedia.org/wiki/Tesonet · https://en.wikipedia.org/wiki/Tomas_Okmanas
- https://www.crunchbase.com/organization/oxylabs · https://tracxn.com/d/companies/oxylabs/__QRySzS6ai55a-R-cC3a-fCTK5vLQA45Uz_0Ai4H59dk
- https://getlatka.com/companies/oxylabs.io · https://www.owler.com/company/oxylabs
- https://tech.eu/2025/06/20/helsing-raises-600m-oxylabs-acquires-scrapingbee-and-uk-s-new-entrepreneur-advisor/
- https://oxylabs.io/resources/case-studies (trivago, Wiser, Price2Spy, Epicup, Crawly)
- https://oxylabs.io/legal-timeline · https://proxyway.com/news/oxylabs-goes-on-offensive-against-bright-data
- https://unicorns.lt/en/news/oxylabs-vadovas-j-cerniauskas-startuoliai-tures-ismokti-gyventi-naujoje-realybeje
