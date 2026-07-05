# Merge

> One API (and now one agent tool-calling layer) that gives your B2B product hundreds of customer-facing integrations — HR, ATS, accounting, CRM, ticketing, file storage — without building each one yourself.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** June 2020, New York City (Verified — PR Newswire seed announcement, First Round Review, company blog)
- **Website / GitHub:** https://merge.dev · https://docs.merge.dev (no significant OSS presence; commercial platform)

## What they do

Merge's core product is a **Unified API**: you integrate once against Merge's normalized data model for a category (HRIS/payroll, ATS/recruiting, accounting, CRM, ticketing, file storage) and your customers get the whole category — 200+ underlying platforms like Workday, Greenhouse, NetSuite, Salesforce, Jira. Merge handles the per-platform auth, syncing, rate limits, and schema normalization; you read/write one common model. Pricing is per "Linked Account" (each end-customer connection): first 3 free, then $650/mo for up to 10 and $65 per additional account on the self-serve Launch tier, with contract-based Professional/Enterprise tiers above (public pricing page = real commercial product).

Since 2025 they've repositioned from "integrations for SaaS products" to "connective infrastructure for production AI," with three AI-facing layers: (1) an **MCP server** exposing their 220+ platform connectors to any MCP client with a few lines of code; (2) **Merge Agent Handler** (launched October 2025) — a tool-calling platform that gives agents authenticated, scoped access to thousands of pre-built tools across Salesforce, Slack, Jira, GitHub, Workday, etc., with permissioning, data-loss prevention, and audit trails, extended in June 2026 with **Agent Handler for Employees** (an IT gatekeeper that maps identity-provider users/groups to approved tools and actions across AI vendors, including a Microsoft Agent Store listing for M365 Copilot governance); and (3) **Merge Gateway**, an LLM routing layer (model routing, fallback, spend controls) — newest and least proven of the three (Reported — company site only, as of 2026-07-02).

## Founders & origins

**Shensi Ding (CEO) and Gil Feig (CTO)** (Verified — TechCrunch, PR Newswire, First Round Review). Friends since freshman year at Columbia (co-class presidents senior year). Ding: Credit Suisse tech IB, then Chief of Staff at Expanse (cybersecurity, acquired by Palo Alto Networks for ~$800M–1B). Feig: software engineer at LinkedIn, then founding engineer/Head of Engineering at Untapped (previously Jumpstart/Canvas — the company renamed repeatedly, which explains conflicting source names). Both hit the same wall — enterprise deals blocked on one-off integrations — and famously did ~100 customer interviews before writing code (Reported — SaaS Club podcast, First Round).

## Funding

- **Seed, $4.5M (May 2021):** led by NEA; angels incl. Mulesoft ex-CEO Greg Schott and Cloudflare CEO Matthew Prince (Verified — PR Newswire, press).
- **Series A, $15M (Nov 2021):** led by Addition, NEA participating (Verified — TechCrunch, PR Newswire, company blog).
- **Series B, $55M (Oct 2022):** led by Accel, with NEA and Addition; ARR reported up 30x YoY at the time (Verified — TechCrunch, SiliconANGLE, company blog).
- **Total raised: $75M** (Verified). No post-Series-B round found in public sources as of 2026-07-02.

## Evidence of real-world use

- **BILL**: 40+ HRIS integrations launched on Merge; documented case study claiming build time equal to one in-house integration (Reported — vendor case study).
- **Perplexity**: uses Agent Handler for data connectors in Perplexity Enterprise Pro (Reported — vendor site, but a strong, named AI-native logo).
- Homepage roster includes **OpenAI, Mistral AI, Dropbox, Zoom, Ramp, Drata, Freshworks, Korn Ferry, Navan/TripActions, AngelList, Apollo** — logos, not all documented case studies; the 2022 Series B press cited **2,500+ companies** on the platform (Verified count as of 2022; current count not published).
- SOC 2 Type II, ISO 27001, HIPAA, GDPR certifications and a self-serve pricing page — consistent with a mature commercial business, not vaporware.
- A CrewAI docs page ships a **MergeAgentHandlerTool** — third-party framework adoption signal (Reported).

## Relevance to agentic AI engineering

Merge sits in the **tool-use and governance layer** of the agent stack — the same territory as this repo's tool-use/governance research area: Agent Handler is essentially productionized answer to "who authorized this agent to take this action, as which user, and where's the audit log," which is the governance question the landscape papers keep circling. The MCP server makes their 220+ connectors consumable by any MCP-speaking agent, and the synced-data Unified API is a natural retrieval substrate for enterprise RAG/agent-memory pipelines (normalized HR/CRM/ticketing data instead of scraping each SaaS). Not relevant to the agentic SWE-benchmark or voice-agent threads except as the action layer those agents call into. Note the category label here (consumer-ai) is the repo's bucket assignment; the company is squarely B2B infrastructure.

## Use cases & considerations

Use cases: (1) shipping a full category of customer-facing integrations (e.g., "connect your HRIS") in one build; (2) giving an internal or product agent governed, audited tool access to Slack/Jira/Salesforce via Agent Handler instead of hand-rolled OAuth; (3) IT-side governance of employee AI agents (Agent Handler for Employees); (4) feeding normalized cross-SaaS data into RAG/analytics.

Considerations: all customer data and agent actions flow through Merge — meaningful vendor lock-in and a trust surface enterprises must diligence; per-Linked-Account pricing gets expensive at scale; the normalized model can lag platform-specific fields (their Professional tier's "custom fields" exists for this reason). Competitors: **Composio, Arcade.dev, Paragon, Nango, Apideck, Kombo** on integrations; MCP itself commoditizes connectors, which is exactly why Merge is racing up-stack into governance. Open question: whether Gateway (LLM routing) is a real third leg or a land-grab into LiteLLM/OpenRouter territory.

## Sources

- https://www.merge.dev/ and https://www.merge.dev/pricing
- https://www.merge.dev/blog/agent-handler and https://www.merge.dev/merge-agent-handler
- https://www.merge.dev/features/mcp
- https://www.merge.dev/case-studies
- https://techcrunch.com/2022/10/24/merge-raises-55m-series-b-for-its-unified-api/
- https://techcrunch.com/2021/11/03/merge-raises-15m-series-a-for-its-b2b-integrations-platform/
- https://www.prnewswire.com/news-releases/merge-raises-4-5m-seed-round-led-by-nea-301292705.html
- https://www.prnewswire.com/news-releases/merge-announces-15-mm-series-a-expands-partnerships-with-top-hr-recruiting-and-payroll-api-providers-301414932.html
- https://siliconangle.com/2022/10/24/merge-api-secures-55m-speed-software-integration-projects/
- https://siliconangle.com/2026/06/01/merge-launches-agent-handler-employees-gatekeeper-workplace-ai-agents/
- https://review.firstround.com/merges-path-to-product-market-fit/
- https://saasclub.io/podcast/gil-feig-merge-340/
- https://docs.crewai.com/en/tools/integration/mergeagenthandlertool
