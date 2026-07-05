# Unblocked

> A "context engine" that ingests a team's code, tickets, docs, and chat history so both human engineers and AI coding agents can get answers grounded in the organization's actual decisions and history.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** platinum
- **Founded:** 2021, Vancouver, Canada (Verified — TechCrunch, T-Net/BC Technology, Crunchbase; public launch October 2023)
- **Website / GitHub:** https://getunblocked.com · no significant public OSS presence found (product is closed-source SaaS)

## What they do

Unblocked builds a retrieval layer over the artifacts an engineering org accumulates: repos on GitHub, Slack threads, Jira/Confluence, Notion, Google Drive. It constructs a unified model of the engineering system and answers questions like "why does this service retry three times?" with the PR, ticket, and Slack argument where that decision was made. The pitch used to be aimed at humans (a Slack bot / web app that answers codebase questions); since 2025 the company has repositioned squarely as **context infrastructure for AI coding agents**: an **MCP server** that feeds Claude Code, Cursor, and Copilot organizational context at generation time, plus a CLI and an API for wiring context into internal tools (support, incident response, ticket enrichment).

Technically the interesting claims are about retrieval quality, not model quality: conflict resolution across contradictory docs using recency/authority signals, personalization scoped to the asker's repos and history, token-optimized context packing (they claim "48% fewer tokens, 83% faster" versus a baseline agent on identical prompts — Reported, vendor benchmark), and permission-aware retrieval that enforces the source systems' ACLs. Newer products sit on top of the same engine: **AI Code Review** (PR review that knows house conventions and prior decisions) and a **CI Failure Agent**. SOC 2 Type II, SSO/SCIM, no training on customer data (Reported — company security page).

## Founders & origins

Founded by **Dennis Pilarinos** (Verified — TechCrunch, company blog). Background: director-level roles at Microsoft (Azure) and Amazon (AWS); founded **Buddybuild**, a mobile CI/CD platform **acquired by Apple in 2018**, then spent ~2 years at Apple where his team's work fed into Xcode Cloud. Unblocked is his second developer-tools company, born from the observation that engineers lose hours to hunting for the "why" behind code. Some sources describe co-founding team members from Microsoft/Amazon/Meta/Apple (Reported — company about page); Pilarinos is the only founder named consistently in public sources.

## Funding

- **Seed, October 2023:** $8.3M led by Amplify Partners, with First Round Capital and XYZ Capital; angels include Stewart Butterfield (Slack), John Lilly, Mike Vernal (Verified — T-Net, company blog).
- **Series A, May 2025:** US$20M from B Capital, Radical Ventures, and Artisanal Ventures (Verified — TechCrunch, company blog, T-Net).
- **Total raised:** ~US$30M (Verified — TechCrunch). No later rounds found in public sources as of 2026-07-05.

## Evidence of real-world use

Stronger than logo-wall average. Named customers with detail: **Drata** (published case study: fragmented docs across 200+ integrations; claims onboarding time down 30% and "1–2 hours saved per engineer per day" — note TechCrunch quotes Pilarinos saying one to two hours *per week*, so treat the magnitude as vendor-reported and inconsistent), plus **AppDirect, Big Cartel, TravelPerk** (Verified — TechCrunch) and testimonials from **Nava Benefits** and **Cloudbeds** engineers describing Claude Code + Unblocked MCP workflows (Reported — company site). A public self-serve pricing page ($19–$35/user/month tiers plus Enterprise, 21-day trial, no credit card) signals a real commercial product rather than pure enterprise theater. Platinum sponsorship at AIEWF 2026 indicates serious go-to-market spend. No public usage/revenue numbers found.

## Relevance to agentic AI engineering

Unblocked is a commercial bet on the thesis running through this repo's agent-memory thread — *Are We Ready For An Agent-Native Memory System?*, *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*, and *Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents* — applied to the org-knowledge domain: agents fail less when retrieval is structured, deduplicated, and authority-weighted rather than raw RAG over a doc dump. Its ACL-enforcing retrieval is a practical instance of the concerns in *Governance by Construction for Generalist Agents*. And the product directly targets the gap named in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* and *ProdCodeBench*: real SWE work is brownfield and context-starved (cf. *One Developer Is All You Need*), not greenfield puzzle-solving.

## Use cases & considerations

Use cases: (1) MCP server in Claude Code/Cursor so agents cite the team's actual conventions and past decisions instead of hallucinating rationale; (2) accelerating onboarding onto legacy/brownfield codebases; (3) deflecting internal "how does X work" support questions via Slack bot or API; (4) context-aware PR review and CI-failure triage.

Considerations: value scales with how messy your Slack/Jira/Confluence sprawl is — small or well-documented teams gain less. Ingesting all org communication is a significant data-governance decision despite SOC 2. Vendor-reported ROI numbers are inconsistent (hours/day vs hours/week). Crowded space: Glean (Unblocked publishes a comparison page), Sourcegraph, Atlassian Rovo, plus coding agents building their own memory/indexing — the open question is whether context becomes a standalone layer or gets absorbed by agent vendors.

## Sources

- https://getunblocked.com/
- https://getunblocked.com/about/
- https://getunblocked.com/pricing/
- https://getunblocked.com/blog/series-a/
- https://getunblocked.com/blog/customer-story-drata/
- https://techcrunch.com/2025/05/06/unblocked-raises-20-million-for-its-ai-assistant-to-help-devs-understand-legacy-codebases/
- https://www.bctechnology.com/news/2025/5/7/Vancouver-based-Unblocked-Announces-US-20M-Series-A-Financing-to-Help-Developers-Understand-the-Missing-Context-Behind-Their-Code.cfm
- https://www.bctechnology.com/news/2023/10/13/Vancouver-based-Unblocked-Publicly-Launches-Announces-8.3-Seed-Financing-Round-Led-by-Amplify-Partners-with-First-Round-Capital-and-XYZ-Capital.cfm
- https://www.crunchbase.com/organization/getunblocked
