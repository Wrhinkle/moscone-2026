# Builder.io

> Visual development platform that turned a headless CMS / Figma-to-code business into an AI coding agent ("Fusion") that lets product managers and designers ship real code through PRs.

- **Category:** coding-agents
- **AIEWF 2026 tier:** bronze
- **Founded:** ~2018 (product launched 2019) — **Reported**; Tracxn lists 2013, which conflicts with TechCrunch's account, so treat the exact year as unverified. US-based (SF Bay Area, Reported).
- **Website / GitHub:** https://www.builder.io — https://github.com/BuilderIO

## What they do

Builder.io started as a visual headless CMS: marketing/e-commerce teams drag-and-drop pages that render through SDKs inside your existing React/Vue/Next.js app, so non-engineers ship content without engineering tickets. The second act was **Visual Copilot**, a Figma plugin that converts designs into framework code (React, Vue, Svelte, Angular, Qwik, Solid, HTML), can map to your own code components/design tokens, and on Enterprise plans lets you bring your own LLM (SOC 2 Type II).

The current flagship — and why they belong in a coding-agents category — is **Fusion**, launched 1.0 in November 2025. Fusion is an AI agent positioned upstream of tools like Cursor/Devin: it sits where PMs and designers work. You tag `@Builder.io` in Slack or assign a Jira ticket to the bot; it reads the requirement, creates a branch in GitHub/GitLab/Azure DevOps/Bitbucket, and opens a PR that engineers review. It indexes your design system components and docs so generated UI uses your primitives rather than generic markup, offers a visual canvas that edits real code with multiplayer collaboration, syncs bidirectionally with Figma, and connects to Supabase/Neon, Netlify, Linear, and arbitrary MCP servers. Model-agnostic: Anthropic, OpenAI, and Google models are selectable (**Verified** on their site).

## Founders & origins

**Steve Sewell** (CEO) and **Brent Locks** co-founded the company after working together on web apps at fashion e-commerce firm ShopStyle, where they felt the pain of engineering-gated content changes (**Verified**: TechCrunch, Traction interview). **Miško Hevery**, creator of Angular, joined as CTO (**Verified**: TechCrunch 2021); he built the Qwik framework at Builder.io. Sewell also created the open-source projects Mitosis and GPT Crawler (**Reported**).

## Funding

- Seed: $3.25M, Oct 2020, led by Greylock (**Reported**: Tracxn).
- $14M, Oct 2021, Greylock with Imaginary Ventures and angels incl. Michael Preysman (Everlane CEO) and Adam Blitzer (Datadog COO) (**Verified**: TechCrunch, PR Newswire).
- $20M, April 2024, led by M12 (Microsoft's venture fund) (**Verified**: CMS Critic, company posts).
- Total: ~$37.2M per Tracxn (**Reported**). No round announced since Apr 2024 found as of 2026-07-02.

## Evidence of real-world use

Strong, and unusually well-documented for this category:

- Named customers with real case studies: **Everlane** (publishes 100+ homepage variations/month, products launched 4x faster) and **Zapier** — both published on builder.io/customer-stories (**Verified**). **Alo Yoga, Afterpay, Vistaprint** named as customers; 400+ customers and 6x YoY growth claimed in 2021 (**Reported**: TechCrunch).
- OSS footprint: **Mitosis** (~13.8k GitHub stars; write-once components compiling to React/Vue/Qwik/etc.) and the **Qwik** framework originated here (**Verified**).
- Fusion claim of "10M+ designs and PRDs turned into production features" is vendor-reported and unaudited (**Unverified**).
- Public pricing pages and an active Figma plugin ecosystem indicate a real commercial product, not vaporware.

## Relevance to agentic AI engineering

Fusion is a concrete instance of the agentic-SDLC pattern this repo tracks: ticket-in, PR-out coding agents evaluated by the **agentic SWE benchmark** literature (SWE-bench-style end-to-end issue resolution) — but Builder.io's twist is constraining generation with an indexed design system, a form of grounded tool-use that reduces the free-form codegen failure modes those benchmarks expose. Its MCP-server integration surface makes it relevant to the repo's **tool-use/governance** work (who can let an agent open PRs from Slack, and under what review policy). Design-system indexing and repo/document context are a lightweight case of **agent memory** (persistent, structured context reused across tasks). Voice-agent papers are not relevant here.

## Use cases & considerations

Use cases: (1) let PMs/designers turn Jira tickets and Figma frames into reviewable PRs on marketing/UI-heavy surfaces; (2) Figma-to-code acceleration mapped to an existing component library (claimed 50-80% time savings, vendor figure); (3) headless CMS for e-commerce content velocity; (4) cross-framework component publishing via Mitosis.

Considerations: strongest on front-end/UI work — not a general backend coding agent (Devin, Cursor agents, GitHub Copilot Workspace, Vercel v0, Lovable, and Figma Make are the competitive set, each from a different angle). CMS + Fusion adoption creates platform lock-in at the content and workflow layer. Enterprise pricing is opaque (sales-led). Open question: how well PR quality holds outside design-system-covered UI code; no third-party benchmark results found.

## Sources

- https://techcrunch.com/2021/10/18/builder-io-aims-to-make-developers-happy-with-its-no-code-approach-to-digital-storefronts/
- https://www.builder.io/blog/fusion
- https://www.builder.io/news/fusion
- https://cmscritic.com/builderio-nets-20m-from-microsofts-venture-fund-what-it-means-for-the-future-of-headless-cms
- https://tracxn.com/d/companies/builder/__zMk_yU3jacqgr1EizCSxRt5LPyjSjapmfvi9jqYABvk
- https://traction.substack.com/p/how-builderio-got-early-traction
- https://www.builder.io/customer-stories/everlane
- https://www.builder.io/customer-stories/zapier
- https://www.builder.io/blog/figma-to-code-visual-copilot
- https://github.com/BuilderIO/mitosis
- https://www.prnewswire.com/news-releases/builderio-raises-14m-to-power-commerce-experiences-with-no-code-301401879.html
- https://www.prnewswire.com/news-releases/builderio-launches-fusion-1-0--the-first-ai-agent-for-product-design-and-code-302615215.html
