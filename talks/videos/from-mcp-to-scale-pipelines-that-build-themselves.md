# From MCP to Scale: Pipelines That Build Themselves

> Rafael Levi of Bright Data shows how to stop paying LLM token costs for parsing web pages by having an agent write, run, and maintain conventional scrapers instead.

- **Speaker:** Rafael Levi, Bright Data
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=zTZ0qunQXnM) (AI Engineer channel; ~25m, released 2026-06-07)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Levi opens with the complaint he keeps seeing on Reddit: "I need to scan 10,000 products, but that's so many tokens if I need to parse everything with LLM." His answer is that you should never ask the model to parse pages at scale. Instead, the agent should use the LLM once to write a scraper, then run that scraper as ordinary code. This session is a follow-up to his earlier talk on the Bright Data MCP server, which handles CAPTCHA and bot-detection systems so the agent can fetch pages in the first place.

The workflow rests on two pieces. First, a public Bright Data skills repository on GitHub that teaches the agent scraper-building practices. Second, the Bright Data MCP, which exposes 66 tools, including scrape-as-markdown for token-light text extraction and full-HTML fetches the agent uses to discover the selectors it needs. Levi's demo runs in Claude Code, his stated preference over Codex. He prompts it to build a scraper for walmart.com with two inputs, keyword search and max pages, and notes that Walmart runs aggressive anti-bot systems that block plain fetches. The build takes about three minutes. Levi says the same job used to take a day or a day and a half of manual selector work, and that building the scraper instead of LLM-parsing three pages of results saves roughly a million tokens.

For a clean test, the audience picks Very.com, a UK marketplace Levi says he has never touched. The agent pulls HTML through the MCP, writes a parser and an output schema, and collects 90 products. The token breakdown Claude produces at the end shows about a 62 percent saving versus manual LLM parsing, a figure Levi calls low and attributes to the site's relatively structured HTML. He also runs a control: asked to search Walmart without the MCP, Claude's plain fetch hits a "robot or human" verification screen; the same request through scrape-as-markdown returns full product listings.

Maintenance is the other half of the argument. Levi describes daily collections where a Claude session spins up every 30 minutes, validates the collected data, and shuts down if everything passes. When a selector breaks, the agent fixes the scraper in about five minutes, so nobody wakes up at night for a missing field. He frames the MCP as most useful for roughly 20 percent of domains, the ones behind Akamai, DataDome, or Cloudflare, which he says tend to be the most valuable targets such as real estate and large e-commerce sites.

The infrastructure claims: over 150 million IPs, about 500 prebuilt per-domain APIs that return JSON directly (for Amazon the agent skips scraper-building entirely), remote browsers that run on Bright Data servers, and 5,000 free MCP requests per month. The remote browsers replay pre-recorded human mouse movement and typing, including deliberate mistakes, so behavior trackers see a person. Levi says that once the session is masked as human, Claude Haiku is enough for browsing agents; he never uses top models for that.

On legality, Levi is direct: Bright Data only touches public data, never behind logins, and never accepts a site's terms. He cites the company's court wins after being sued by Meta and by X, summarizing the ruling as public data is public data regardless of how it is collected. He closes with personal-scale uses: a listener that watched apartment listings every half hour and found the house he now lives in, and a restaurant-reservation listener that has been waiting two months for a table to open.

## Notable moments

- [0:02:16](https://www.youtube.com/watch?v=zTZ0qunQXnM&t=136s) The Walmart demo starts in Claude Code: a scraper with keyword-search and max-pages inputs, built in about three minutes.
- [0:06:19](https://www.youtube.com/watch?v=zTZ0qunQXnM&t=379s) The audience picks Very.com as an unrehearsed target and the agent builds a working scraper that collects 90 products.
- [0:11:20](https://www.youtube.com/watch?v=zTZ0qunQXnM&t=680s) Control test without the MCP: a plain fetch to Walmart hits the "robot or human" verification screen, then succeeds through scrape-as-markdown.
- [0:18:34](https://www.youtube.com/watch?v=zTZ0qunQXnM&t=1114s) Levi recounts the Meta and X lawsuits and the ruling he summarizes as public data is public data.

## Connections

- [Bright Data](../../companies/memory-rag-search/bright-data.md) profiles the speaker's company, including the Web MCP, the 150M-IP network, and the Meta and X litigation Levi cites.
- [Firecrawl](../../companies/memory-rag-search/firecrawl.md) competes on the same agent-facing web extraction problem Levi demos.
- [Apify](../../companies/memory-rag-search/apify.md) is the closest rival for agent-built and agent-maintained scraping pipelines.
