# Optiver

> A 40-year-old Amsterdam proprietary trading firm and options market maker that has become one of the most public enterprise adopters of agentic AI for software engineering.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** gold
- **Founded:** 1986, Amsterdam, Netherlands (Verified — Wikipedia, MarketsWiki, company site)
- **Website / GitHub:** [optiver.com](https://www.optiver.com/) · [github.com/optiver](https://github.com/optiver)

## What they do

Optiver (from the Dutch *optieverhandelaar*, "option trader") is a proprietary trading firm and market maker: it quotes two-sided prices in exchange-listed options, futures, equities, and ETFs across 50+ exchanges, profiting from the bid-ask spread while taking no outside capital and serving no clients. It is one of the largest options market makers in the world, with ~2,700 employees across offices in Amsterdam, Chicago, Sydney, Shanghai, and other hubs (Verified).

It is at AIEWF 2026 not as a vendor but as an **enterprise adopter and talent buyer**. Its engineering org maintains millions of lines of latency-sensitive C++/Python and ships 120+ commits/day; it has publicly reorganized its SDLC around AI coding agents rather than bolting agents onto human workflows (Verified — company tech blog, Driver case study). It also hosted an evening event at the Fair, "Optiver: The Agentic SDLC Loop," and Matt Nassr (Head of Global Data Engineering and AI Transformation) led a session on shared foundations for agentic software development (Verified — ai.engineer schedule).

Two distinct AI efforts are documented: an **Applied AI team** embedding LLMs into trading workflows, and a newer independent **AI Lab** (New York, headed by Andrew Arnold, ex-Shopify/Google ML; plus a Shanghai lab launched earlier) doing longer-horizon research (Reported — eFinancialCareers).

## Founders & origins

Founded April 9, 1986 by **Johann Kaemingk**, **Ruud Vlek**, and **Chris Oomen** as a single floor trader in options on Amsterdam's European Options Exchange (now Euronext) (Verified — Wikipedia, MarketsWiki). Expanded to Paris/Frankfurt/London in the early 1990s, Sydney 1996, US 1999 (Chicago ~2002); closed all floor trading in 2003 to go fully electronic.

## Funding

Not a venture-backed company — no rounds exist. Amro Bank took a majority stake in 1989; Optiver bought back all external shareholders by end of 1998 and has been employee/insider-owned since (Verified). Scale in lieu of funding: 2025 net trading income of €4.556B (+30% YoY) and net profit of €1.769B, per its published annual results (Verified — optiver.com financial results).

## Evidence of real-world use

As an adopter, the evidence is what they've shipped internally and disclosed:

- **Agentic SDLC in production:** Optiver's "Engineering the Agentic SDLC" blog documents a three-layer framework (SDLC workflows → agent primitives → shared substrate of measurement/orchestration/governance) and reports, for an exchange-connectivity project: 75% reduction in time-to-market, 85% reduction in engineering effort, ~90% review-ready agent output (Reported — self-published, but unusually concrete).
- **Named vendor relationship:** Driver's customer story states Optiver cut manual context management for coding agents by ~90% after a failed in-house RAG-over-code attempt ("chunking source code destroyed dependency relationships and call graphs" — Nassr) (Reported — vendor case study, corroborated by Nassr's public talks).
- **LLM trading evaluation:** the Applied AI team ran frontier LLMs through Optiver's 88-question intern theory exam and market-making simulations; models matched interns on theory (median intern score 61%; press coverage notes Claude outperformed most interns) but failed at sequential belief-updating, EV-maximizing commitment, and adversarial reasoning (Verified — Optiver tech blog + eFinancialCareers).
- **Hiring signal:** open "AI Engineer" and "Software Engineer – Developer Experience (AI Tools)" roles explicitly scoped to building production agents that orchestrate data, workflows, and decisions firm-wide; senior AI hires poached from Goldman Sachs, Apple, Shopify (Verified — optiver.com job listings).

## Relevance to agentic AI engineering

Optiver is a reference case for **agentic SWE at enterprise scale**: their intern-exam evaluation is essentially a domain-specific agentic benchmark in the spirit of the agentic SWE benchmark literature in this repo, and their findings (theory strong, multi-step belief updating weak) mirror what those benchmarks show about long-horizon tasks. Their "shared substrate" layer — measurement, execution, orchestration, *governance* — maps directly onto the tool-use/governance research thread, and their RAG-for-code failure → compiler-based context pivot is a concrete data point for the agent memory/context-management line of work. No voice-agent relevance.

## Use cases & considerations

For a builder/operator: (1) a template for redesigning an SDLC around agents (golden paths, backpressure gates, agent-friendly non-interactive tooling); (2) a sober read on where LLMs fail in adversarial, sequential-decision domains before you build a "trading agent"; (3) a hiring destination/competitor for agent-infrastructure talent alongside Jane Street, Citadel Securities, Jump, IMC, and Hudson River Trading.

Considerations: nothing here is buyable — Optiver sells no product, and its internal tooling is closed (its GitHub is ~9 minor repos). All performance numbers are self-reported or vendor-reported; treat the 75%/85% figures as directional. Their sponsorship is best read as recruiting.

## Sources

- https://en.wikipedia.org/wiki/Optiver
- https://www.marketswiki.com/wiki/Optiver
- https://www.optiver.com/about-us/
- https://www.optiver.com/insights/news/optiver-reports-robust-financial-results-for-2025/
- https://www.optiver.com/insights/technology-blog/engineering-the-agentic-sdlc/
- https://www.optiver.com/insights/technology-blog/where-ai-trading-models-work-and-where-they-still-fall-short/
- https://www.driver.ai/blog/optiver-customer-story
- https://www.efinancialcareers.com/news/optiver-ai-lab
- https://www.efinancialcareers-gulf.com/news/optiver-interns-need-to-pass-an-88-question-theory-exam-claude-outperforms-most-of-them
- https://optiver.com/working-at-optiver/career-opportunities/8019646002/
- https://www.ai.engineer/worldsfair/2026/llms.md
- https://github.com/optiver

*Profile compiled 2026-07-02.*
