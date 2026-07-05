# Automattic

> The company behind WordPress.com, WooCommerce, Tumblr, and Jetpack — steward of the open-source CMS that runs ~43% of the web, now repositioning WordPress as an "operating system for the agentic web" via MCP servers across its product line.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** gold
- **Founded:** 2005, San Francisco (Verified). Founded by Matt Mullenweg; note that Mike Little co-created the WordPress open-source project (2003) with Mullenweg but Automattic the company is Mullenweg's (Verified across Wikipedia/Contrary Research).
- **Website / GitHub:** https://automattic.com · https://automattic.ai · https://github.com/Automattic

## What they do

Automattic is the commercial center of gravity for WordPress. Core lines: **WordPress.com** (managed hosting/SaaS for the open-source CMS), **WooCommerce** (dominant open-source e-commerce plugin, acquired 2015), **WordPress VIP** (enterprise-grade managed WordPress, $25k minimum deals, typical $100k–$500k/yr), **Jetpack**, **Tumblr** (acquired 2019), plus a long tail of acquisitions: Day One (journaling), Pocket Casts, Beeper (multi-network messaging, acquired 2024 for a reported $125M), Parse.ly (content analytics), Pressable, Newspack, Akismet, Gravatar. Fully distributed company, ~1,500–1,700 people (Reported; headcount fell after 2024 alignment buyouts and an April 2025 ~16% restructuring).

Since 2025 the interesting engineering story is **automattic.ai**: Model Context Protocol servers for WordPress.com, WooCommerce, Beeper, Day One, Clay, and Pressable. WordPress.com MCP shipped read-only in October 2025, added OAuth 2.1 in January 2026, an official Claude connector in February 2026, and — the big one — **write capabilities in March 2026**, letting Claude, ChatGPT, and Cursor create posts, build pages, manage media/comments/taxonomy on live sites with human approval gates (Verified: Automattic blog + TNW + CMSWire). In parallel, Automattic drives the WordPress core **Abilities API** (WordPress 6.9), a central registry making WordPress functions discoverable to agents, and experimental tools like **Telex** (agent that generates custom Gutenberg blocks) and **Big Sky** (AI site builder on WordPress.com). WooCommerce has a published agentic-commerce roadmap.

## Founders & origins

Matt Mullenweg co-created WordPress (2003, a fork of b2/cafelog, with Mike Little), founded Automattic in August 2005 to commercialize it, and remains CEO; Toni Schneider (ex-Yahoo) was CEO 2006–2014 (Verified). Mullenweg also runs the WordPress Foundation and the open-source project itself — a governance concentration that became controversial during the 2024–25 WP Engine dispute (Verified; ongoing litigation, worth knowing before partnering).

## Funding

- ~$1.1M (2007) and $29.5M (2008), Polaris/True Ventures/Radar/NYT — Verified.
- $160M (May 2014), Insight Partners, ~$1.16–1.6B valuation — Verified round, valuation figures vary by source.
- $300M Series D (2019), Salesforce Ventures, $3B valuation — Verified.
- $288M (Feb 2021) at ~$7.5B valuation, Alta Park/BlackRock/ICONIQ and others — Verified.
- Total raised ~$986M (Crunchbase — Reported). Profitable for much of its history; no IPO; no public rounds since 2021.

## Evidence of real-world use

Among the strongest usage stories of any AIEWF sponsor: WordPress powers ~43% of all websites (Verified, widely corroborated). WordPress VIP customers include CNN, News Corp, NBCUniversal, Bloomberg, Salesforce, Capgemini, and the White House (Verified via wpvip.com and Google News Initiative; a Forrester TEI study claims 415% ROI — vendor-commissioned, treat accordingly). The MCP servers are new (2025–26), so agent-integration adoption evidence is thin so far — mostly Automattic's own posts and trade press, not independent case studies. Unverified: any named enterprise running write-capable agents against production WordPress at scale.

## Relevance to agentic AI engineering

Automattic is an enterprise adopter turned **agent-surface provider**: it's making the largest installed base of content infrastructure on the web tool-callable. Directly relevant repo threads: multi-tool orchestration ("The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration"), and the security/permissioning questions raised by write-capable MCP on production sites — "Governance by Construction for Generalist Agents," "CaMeLs Can Use Computers Too," and "ClawLess: A Security Model of AI Agents" all map cleanly onto human-approval gates and least-privilege OAuth scopes. Day One's MCP as an agent-readable personal journal touches the agent-memory line ("Are We Ready For An Agent-Native Memory System?"). WordPress sites as agent targets also connect to "Agentic Search in the Wild" (agents navigating real web content).

## Use cases & considerations

- Content-ops agents: draft/publish/update posts and pages on WordPress.com or WooCommerce product catalogs via MCP with approval loops — practical today for a small-business back office (e.g., a construction company's site/reviews/content pipeline).
- Agentic commerce experiments against WooCommerce order/customer data.
- Enterprise CMS with an agent story: VIP if budget is $25k+/yr.

Considerations: MCP write access to production sites is powerful and new — audit scopes and approval flows before trusting it; WordPress.com MCP ≠ self-hosted WordPress (self-hosted needs the Abilities API / plugins, still maturing). Governance risk: the Mullenweg/WP Engine conflict showed ecosystem decisions can be unilateral. Competitors: Wix and Squarespace (AI site builders), Shopify (agentic commerce), Webflow, Contentful/headless CMSes. Open question: whether third-party agent traffic actually materializes on WordPress surfaces or stays a demo.

## Sources

- https://en.wikipedia.org/wiki/Automattic
- https://research.contrary.com/company/automattic
- https://www.crunchbase.com/organization/automattic
- https://automattic.ai/mcp/
- https://automattic.com/2026/04/21/wordpress-operating-system-agentic-web/
- https://wordpress.com/blog/2026/03/20/ai-agent-manage-content/
- https://thenextweb.com/news/wordpress-com-mcp-write-capabilities-ai-agent
- https://www.cmswire.com/digital-experience/wordpresscom-enables-ai-agents-to-write-manage-content/
- https://make.wordpress.org/ai/2025/07/17/ai-building-blocks/
- https://developer.woocommerce.com/2025/10/03/ai-agentic-commerce-in-woocommerce/
- https://wpvip.com/case-studies/ · https://wpvip.com/about/
- https://techcrunch.com/2024/04/09/wordpress-com-owner-automattic-acquires-multi-service-messaging-app-beeper-for-125m/
- https://telex.automattic.ai/
- https://timeline.automattic.com/
