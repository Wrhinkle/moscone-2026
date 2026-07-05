# Exa

> A search engine built from scratch for AI agents, not humans: embeddings-based retrieval over its own web index, sold as an API that agents call for search, page contents, structured entity lists, and full research runs.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, San Francisco (as Metaphor Systems, YC S21; rebranded to Exa January 2024) (Verified — YC, TechCrunch, company site)
- **Website / GitHub:** https://exa.ai · https://github.com/exa-labs

## What they do

Exa (legal/press name "Exa Labs") operates its own web crawl and index and trains retrieval models over it — embeddings-based "neural" search rather than a keyword index with an LLM bolted on, plus keyword and auto modes. The pitch is Google-for-AIs: results ranked for what a model needs (dense, relevant text, token-efficient) rather than what a human clicks. The company publishes benchmark claims — leading FRAMES (54.4%), Tip-of-the-Tongue (54.2%), and SEAL-0 vs. Perplexity and Brave — which are company-reported, not independently audited.

The product surface an engineer actually touches (all Verified via docs/site):

- **Search API** — semantic/keyword/auto web search; latency tiers from ~180 ms "instant" to deeper modes.
- **Contents/crawling** — fetch and extract pages, with "highlights" excerpting (company claims ~90% token reduction).
- **Answer API** — search + grounded synthesized answer with citations, one call.
- **Websets** — the differentiated one: asynchronous agentic search that returns a *structured table of entities* ("all Series A fintechs in Texas with hiring pages"), built on a 70M+ company-record graph; used heavily for CRM enrichment and sales/research ops.
- **Research/Deep Research** — multi-step research agent as an API with structured outputs.
- **exa-mcp-server** — open-source MCP server (~4.5k GitHub stars, Verified) so Claude/Cursor-style agents get Exa tools directly.

Public pay-as-you-go pricing exists (~$5/1k searches, contents billed separately, 2,000 free searches) — a real self-serve commercial motion. SOC 2 Type II and zero-data-retention options for enterprise (Verified — site).

## Founders & origins

**Will Bryk** (CEO; Harvard CS/physics, early engineer at Cresta) and **Jeff Wang** (Harvard CS & philosophy, ~3 years on data/web infra at Plaid) — freshman-year roommates who founded Metaphor in 2021, about a year before ChatGPT (Verified — TechCrunch, YC). They launched a consumer semantic search engine in Nov 2022, then pivoted to a developer API when AI companies became the obvious customer. Team draws from Harvard/MIT/OpenAI backgrounds (Reported).

## Funding

- **Seed:** $5M (Reported — TechCrunch).
- **Series A:** $17M, July 2024, led by Lightspeed (Guru Chahal), with NVentures (Nvidia) and YC (Verified — TechCrunch, Latham & Watkins).
- **Series B:** $85M, Sept 2025, led by Benchmark (Peter Fenton joined board) at **$700M valuation**; Lightspeed, YC, NVentures participated (Verified — company blog, SiliconANGLE).
- **Series C:** $250M, May 2026, led by a16z (Sarah Wang joined board) at **$2.2B valuation** (Verified — Bloomberg, company blog).
- **Total raised:** ~$357M (computed from above).

## Evidence of real-world use

Stronger than most in this category: **Cursor, Cognition (Devin), HubSpot, monday.com, OpenRouter, CodeRabbit, 11x, StackAI, WebFX, Browserbase** are named customers with several published case studies (Verified — exa.ai/customers; still company-curated). Specifics beat logos: monday.com cites **2.7M CRM enrichments** via Websets; **Databricks** was described by TechCrunch as a marquee customer using Exa to curate training data; Cursor/Cognition use it for agent web search. Claimed **400k+ developers** (Reported — Series C coverage). The MCP server's ~4.5k stars and presence across MCP registries indicate genuine community adoption. Reported ~$12M ARR estimates (Getlatka) are Unverified.

## Relevance to agentic AI engineering

Exa is a leading candidate for the **web-retrieval tool slot** in an agent stack — the live-web complement to internal RAG, and increasingly a "research agent as API." Directly relevant repo papers: *Agentic Search in the Wild* (Exa's query traffic *is* that trajectory data — its API is built for agent-issued, not human, queries), *Deep Researcher Agent* (Exa's Research API is the commercial version of that pattern), *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* (Websets' structured entity outputs are a bet that agents want typed records, not blue links), and *The Evolution of Tool Use in LLM Agents* (search/contents/answer/research as graduated tool tiers). Its use inside Cursor, Devin, and CodeRabbit ties it to the agentic-SWE thread (*FeatureBench*, *OmniCode*) as the retrieval layer coding agents lean on. Governance caveat: piping searched web content into agents is the injection surface *CaMeLs Can Use Computers Too* warns about. The ~180 ms fast mode is also the kind of latency budget *VoiceAgentRAG* targets for voice-agent retrieval.

## Use cases & considerations

Use cases: (1) grounding a back-office or research agent with cited live-web answers (Answer API) instead of hallucinated facts; (2) Websets for lead/vendor/prospect list-building — e.g., "all roofing suppliers or insurance adjusters in a metro" style entity tables for a construction back office; (3) MCP server dropped into Claude Code/Cursor for agent web access with zero glue code; (4) Research API as an outsourced deep-research step in a longer pipeline.

Considerations: additive pricing (search + contents) compounds at agent volumes; index freshness/coverage vs. Google is unverifiable from outside; benchmark claims are self-published; Websets jobs are asynchronous (minutes, not ms). Competitors: **Tavily, Brave Search API, Perplexity Sonar, Firecrawl, Bright Data, SerpAPI**, plus model-native search from OpenAI/Anthropic/Google — the open question is whether frontier labs' built-in search commoditizes the standalone layer, or whether an agent-first index stays defensible.

## Sources

- https://exa.ai/ and https://exa.ai/about
- https://exa.ai/customers
- https://exa.ai/pricing
- https://exa.ai/blog/announcing-series-b
- https://exa.ai/blog/announcing-series-c
- https://techcrunch.com/2024/07/16/exa-raises-17m-lightspeed-nvidia-ycombinator-google-ai-models/
- https://www.bloomberg.com/news/articles/2026-05-20/andreessen-backed-ai-search-startup-exa-valued-at-2-2-billion
- https://siliconangle.com/2025/09/03/nvidia-backs-85m-round-ai-search-startup-exa/
- https://www.ycombinator.com/companies/exa
- https://www.lw.com/en/news/2024/10/latham-watkins-advises-exa-in-us17-million-series-a-financing-from-lightspeed-and-nvidia
- https://github.com/exa-labs/exa-mcp-server
- https://exa.ai/blog/stack-ai-exa · https://exa.ai/blog/webfx-exa
