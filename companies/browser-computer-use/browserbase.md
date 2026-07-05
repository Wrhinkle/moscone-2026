# Browserbase

> Cloud infrastructure for running headless browsers at scale, so AI agents (and plain scripts) can browse, click, and extract from the live web without you operating a browser fleet.

- **Category:** browser-computer-use
- **AIEWF 2026 tier:** platinum
- **Founded:** January 2024, San Francisco (Verified — Contrary Research, press coverage)
- **Website / GitHub:** https://www.browserbase.com · https://github.com/browserbase/stagehand

## What they do

Browserbase runs Chromium-based headless browsers in the cloud and exposes them via API. You (or your agent) request a session; Browserbase gives you a remote browser with proxying/stealth options, CAPTCHA handling, session recording/replay for debugging, and auto-scaling to thousands of concurrent sessions. You connect with Playwright/Puppeteer over CDP, so existing automation code ports over — the pitch is "stop maintaining your own browser farm; treat browsers as a metered utility."

The layer most relevant to agent builders is **Stagehand**, their MIT-licensed open-source SDK (~23.3k GitHub stars, TypeScript-first with Python/Go/Rust/C#/PHP ports in progress as of 2026-07-02). Stagehand mixes deterministic code with natural-language primitives: `act()` performs an instruction like "click the login button," `extract()` pulls structured data validated against a Zod schema, and an agent mode runs multi-step workflows autonomously. The design point — use code where the page is known, AI where it isn't — is a pragmatic answer to the brittleness of pure-selector automation and the cost/nondeterminism of pure-LLM agents.

Two more pieces round out the stack: **Director** (launched June 2025), a no-code tool that turns plain-English instructions into runnable browser workflows for non-developers, and an open-source **MCP server** that lets Claude, GPT, or Gemini drive Browserbase sessions as standard tools. Pricing is public and usage-based: free tier, $20/mo Developer (25 concurrent browsers), $99/mo Startup, custom Scale — the OSS layers are free and funnel demand to paid infrastructure.

## Founders & origins

**Paul Klein IV**, solo founder and CEO (Verified). Previously a software engineer at Twilio, then co-founder/CTO of Stream Club (virtual events), acquired by Mux in late 2021; at Mux he ran headless-browser tech for live streaming. Origin story (Reported — Contrary Research, podcast interviews): by late 2023 he kept fielding "how do I run browsers for AI automation" questions, concluded no adequate managed solution existed, and started Browserbase in January 2024.

## Funding

- **Seed:** $6.5M, June 2024, led by Kleiner Perkins with Basecase Capital and AI Grant (Verified — VC News Daily, fundz.net)
- **Series A:** $21M, October/November 2024, led by CRV with Kleiner Perkins (Verified; sources vary on Oct vs. Nov announcement)
- **Series B:** $40M, June 2025, led by Notable Capital with CRV and Kleiner Perkins, at a **$300M valuation** (Verified — multiple press sources)
- **Total raised:** $67.5M. Angels include Jeff Lawson (Twilio), Guillermo Rauch (Vercel), Patrick Collison (Stripe) (Reported).

## Evidence of real-world use

Strong and unusually well-documented for a two-year-old company:

- **Named customers with published case studies:** Vercel built "Prism," an internal web-intelligence system on Browserbase that crawls customer sites for churn prediction and a "ship velocity index" (documented case study on Browserbase's blog — actual usage, not a logo wall). Convergence built a consumer web agent on it. Perplexity is a named customer (Reported — Series B press).
- **Scale metrics (Reported — Contrary Research):** 1,000+ paying organizations, 20,000+ developers, ~50M browser sessions in 2025 (vs. ~25M in 2024), ~$3M revenue in the first 16 months, ~45 employees by mid-2025.
- **OSS adoption:** Stagehand at ~23.3k stars/1.6k forks with active releases (Verified — GitHub).
- Public pricing page = real self-serve commercial product.

## Relevance to agentic AI engineering

Browserbase is the execution substrate for the web-agent slice of the stack: it's what "computer use" resolves to when the target is a website rather than a desktop. It connects directly to this repo's tool-use/computer-use landscape — *AI Planning Framework for LLM-Based Web Agents* and *WebXSkill: Skill Learning for Autonomous Web Agents* assume exactly this kind of managed browser runtime; *Verifiable Software Worlds for Computer-Use Agents* and *CaMeLs Can Use Computers Too* address the safety/verification gaps that arise once agents act on live sites; *Agentic Search in the Wild* characterizes the autonomous web-browsing trajectories Browserbase sessions host. Via its MCP server it also plugs into the multi-tool orchestration story (*The Evolution of Tool Use in LLM Agents*).

## Use cases & considerations

**Use cases:** (1) web-agent products that need to act on sites without APIs — form-filling, portal logins, checkout flows; (2) structured extraction from JS-heavy pages at scale (Stagehand `extract()` + schemas); (3) back-office automation against vendor/insurer/permit portals that will never ship an API; (4) agent evals/QA that need reproducible, recorded browser sessions.

**Considerations:** Stagehand is portable (MIT, runs on local browsers), but the managed infra is the moat — session costs at high concurrency deserve modeling before committing. Stealth/CAPTCHA features sit in a legal-and-ToS gray zone; know your target sites. Competition is thick: Hyperbrowser and Browserless (direct), Bright Data (data-access angle), plus the risk that OpenAI/Anthropic computer-use stacks or agentic browsers commoditize the layer. Open question: whether Director's non-developer market materializes or the business stays purely dev-infra.

## Sources

- https://research.contrary.com/company/browserbase
- https://github.com/browserbase/stagehand
- https://www.browserbase.com/blog/case-study-vercel
- https://www.browserbase.com/blog/case-study-convergence
- https://www.upstartsmedia.com/p/browserbase-raises-40m-and-launches-director
- https://vcnewsdaily.com/browserbase/venture-capital-funding/lyqhnkzngq
- https://www.fundz.net/fundings/browserbase-funding-round-seed-5f4b90
- https://pulse2.com/browserbase-web-browser-automation-company-raises-21-million-series-a/
- https://venturebeat.com/technology/exclusive-browserbase-launches-headless-browser-platform-that-lets-llms-automate-web-tasks
- https://www.okta.com/blog/company-and-culture/founders-in-focus-paul-klein-iv-of-browserbase/
- https://www.browserbase.com/customer-stories
