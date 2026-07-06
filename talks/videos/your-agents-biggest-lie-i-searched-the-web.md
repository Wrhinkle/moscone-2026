# Your Agent's Biggest Lie: "I Searched the Web"

> How blocked web access turns into confident hallucination, with a live comparison of GPT-5 scraping five hostile sites with and without Bright Data's MCP.

- **Speaker:** Rafael Levi, Bright Data
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=btxGmN8RvNU) (AI Engineer channel; ~16m, released 2026-06-17)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Levi's claim is that a large share of agent hallucination is a web access problem wearing a reasoning problem's clothes. LLMs are tuned to please, so when a fetch fails they rarely say so. The agent hits a CAPTCHA or an empty page, reports no error, and fills the gap from training data, which may be two years stale, or invents numbers and citations outright. He cites broken citation links on ChatGPT and the familiar shopping failure where the agent produces a product link that 404s. He calls this the invisible failure mode: no error, no warning, just the wrong answer.

The blocking is real and growing. Levi says Cloudflare blocks AI crawling for about 20 percent of the web by default, and its recently released AI Labyrinth goes further than blocking: once it detects a bot it feeds it fake data, which makes hallucination worse rather than just leaving gaps. Hotels in Asia already serve different prices to phones, desktops, and proxies, so misleading data is a live problem beyond bot walls. Bright Data's countermeasure is to make the agent indistinguishable from a human, with pre-recorded mouse movement, human-like typing, and unique browser fingerprints, so the detection never triggers. He says the Labyrinth launch produced no measurable degradation in the petabytes Bright Data collects daily.

The demo runs identical prompts through GPT-5 twice against five sites chosen for heavy anti-bot systems: a Rightmove property listing, a LinkedIn company page, an Instagram account, an Amazon product, and a TikTok page. Without the MCP, GPT-5 reports zero successes out of five, having no live web access. With the Bright Data MCP the same tasks succeed, and Levi has the model itself write the head-to-head comparison. The MCP exposes 66 tools, including real Google, Bing, and DuckDuckGo searches, batch search for a hundred keywords at once, scrape-as-markdown to skip HTML token waste, pre-built APIs for common sites, and a remote scraping browser that solves CAPTCHAs itself. Asked about tool overload, Levi is direct: load two tools if you only need markdown scraping and search, not all 66.

On legality, Levi draws the company's line at login walls. Scraping behind a login means having accepted terms and conditions, which Bright Data treats as illegal, so it touches only publicly available data, and offers pre-collected datasets for buyers who can tolerate months-old data. He closes with the skills page: rather than parsing 10,000 pages with an LLM, an agent reads Bright Data's skill documentation, writes a parser once, and lets a script run it, which he says saves about 99 percent of the tokens. The MCP has a free tier of 5,000 requests per month.

## Notable moments

- [0:01:17](https://www.youtube.com/watch?v=btxGmN8RvNU&t=77s) Cloudflare blocks AI crawling for about 20 percent of the web, and AI Labyrinth feeds detected bots fake data.
- [0:04:18](https://www.youtube.com/watch?v=btxGmN8RvNU&t=258s) GPT-5 without the MCP goes zero for five against Rightmove, LinkedIn, Instagram, Amazon, and TikTok.
- [0:05:21](https://www.youtube.com/watch?v=btxGmN8RvNU&t=321s) Tour of the 66 MCP tools, from batch search to a CAPTCHA-solving remote browser.
- [0:12:29](https://www.youtube.com/watch?v=btxGmN8RvNU&t=749s) The skills approach: have the LLM build a parser instead of parsing pages, for about 99 percent token savings.

## Connections

- [Bright Data](../../companies/memory-rag-search/bright-data.md), the speaker's company and the platform behind the MCP demoed here.
- [Oxylabs](../../companies/memory-rag-search/oxylabs.md), a direct competitor in proxy and web data infrastructure for agents.
- [Firecrawl](../../companies/memory-rag-search/firecrawl.md), an adjacent vendor turning web pages into agent-ready markdown.
