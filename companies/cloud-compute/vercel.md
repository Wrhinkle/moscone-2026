# Vercel

> The company behind Next.js, repositioning from "frontend cloud" to "AI cloud": managed deployment infrastructure plus an open-source AI SDK, a multi-provider AI Gateway, agent sandboxes, and the v0 app-generation product.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** supporting
- **Founded:** 2015, San Francisco, CA — as ZEIT; rebranded to Vercel April 2020 (Verified — Wikipedia, company history sources)
- **Website / GitHub:** https://vercel.com · https://github.com/vercel (Next.js: https://github.com/vercel/next.js · AI SDK: https://github.com/vercel/ai)

## What they do

Vercel's core business is a managed platform for deploying web applications: git-push → build → global edge deployment, with serverless functions, caching, and preview URLs per branch. It is the commercial steward of **Next.js**, the dominant React framework, which it optimizes for on its own infrastructure. The platform runs ~2.7M deployments/day, each in an isolated Firecracker microVM orchestrated by an internal system code-named Hive (Reported — Vercel blog).

Since 2023–24 the company has layered an AI stack on top, and by 2026 markets itself as "agentic infrastructure":

- **AI SDK** (`vercel/ai`, ~25.4k stars) — provider-agnostic TypeScript toolkit: unified API for text/structured-output/tool calls across OpenAI, Anthropic, Google, etc.; a `ToolLoopAgent` class for multi-step agents; UI hooks for React/Svelte/Vue (Verified — GitHub).
- **AI Gateway** — a routing/observability proxy in front of model providers (failover, spend tracking, unified billing); the AI SDK uses it by default. Vercel publishes a "production index" from Gateway traffic: in April 2026, 22.2% of requests ended in a tool call (up from 11.4% in Oct 2025) and ~59% of tokens were in tool-call requests (Reported — Vercel blog).
- **Vercel Sandbox** (GA) — the microVM layer exposed as a product for running untrusted, agent-generated code; CLI and SDK open-sourced (Reported — Vercel blog).
- **v0** — prompt-to-app generation (Next.js/React output, deployable to Vercel); 4M+ users since 2024 GA (Reported — Vercel blog).
- **June 2026:** launched **eve**, an opinionated open-source agent framework; Vercel Services (backends + frontends in one project); and enterprise identity controls (Vercel Passport, Enterprise Managed Users) (Reported — SiliconANGLE, Businesswire).

What you'd actually buy: hosting (Hobby free tier → Pro → Enterprise, public pricing), Gateway usage, Sandbox compute. What you'd adopt free: Next.js, AI SDK, eve.

## Founders & origins

Founded 2015 as ZEIT by **Guillermo Rauch** (CEO), **Tony Kovanen**, and **Naoyuki Kanezawa** (Verified — Wikipedia, multiple histories). Rauch, an Argentine self-taught developer, created Socket.IO and Mongoose, sold his previous startup Cloudup to Automattic (2013), and co-created Next.js (2016). Kovanen left in 2017 (later founding engineer at agent-framework startup Mastra, Reported); Kanezawa reportedly remains at Vercel in infrastructure (Reported — Grokipedia/Tracxn-derived sources).

## Funding

Total raised ~$863M (Reported — Tracxn). Key rounds, all Verified via multiple press sources unless noted:

- Series A (Apr 2020, ~$21M, Accel/CRV) and Series B (Dec 2020, $40M, Bedrock) (Reported)
- Series C: $102M, Jun 2021, led by Bedrock
- Series D: $150M, Nov 2021, led by GGV, valuation >$2.5B
- Series E: $250M, May 2024, led by Accel, $3.25B valuation
- Series F: $300M, Sep 2025, co-led by Accel and GIC, **$9.3B valuation**, plus a ~$300M tender offer; new investors BlackRock, Khosla, General Catalyst, Schroders

## Evidence of real-world use

Strong. Next.js is one of the most-deployed web frameworks in existence, and Vercel's platform usage (2.7M deployments/day) is first-party but plausible. Documented case studies: The Weather Company (350M DAU forecasts), Elkjøp (Nordic retailer, >$1B digital revenue, 7-week release-cycle reduction), GitBook (30k sites), Notion (running third-party/agent-generated code on Vercel infra) (Reported — Vercel customer pages; performance numbers are vendor-published). Vercel names OpenAI, PayPal, Ramp, and Supreme as customers (Reported — landing-page logos, treat accordingly). AI SDK adoption (25.4k stars, large provider ecosystem) is independent evidence the AI tooling is used beyond Vercel hosting. Vendor-reported: agents now trigger over half of deployments on the platform, up from <3% in early 2026 (Reported — single first-party source).

## Relevance to agentic AI engineering

Vercel sits at three points of the agent stack: (1) **execution** — Sandbox is a commercial answer to the isolated-environment problem that agentic SWE benchmarks like *ProdCodeBench* and *SWE-EVO* assume, and that *Verifiable Software Worlds for Computer-Use Agents* theorizes; v0 itself is a coding agent of the kind the *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* paper argues we measure badly; (2) **tool-calling plumbing** — the AI SDK's tool-loop and the Gateway's tool-call telemetry map directly to *The Evolution of Tool Use in LLM Agents*; (3) **governance** — the June 2026 enterprise identity controls are a product-side echo of *Governance by Construction for Generalist Agents*: constrain what deployed agents can reach rather than trusting them.

## Use cases & considerations

1. Ship an agent-backed product UI fast: AI SDK + Next.js + Gateway, one vendor.
2. Run untrusted agent-generated code in Sandbox instead of building Firecracker infra.
3. Use AI Gateway as a provider-failover/spend layer even if hosted elsewhere.
4. v0 for internal-tool prototyping by non-frontend engineers.

Considerations: hosting costs at scale are a chronic complaint versus raw AWS/Cloudflare; the SDK is TypeScript-first (weak fit for Python agent teams); Next.js's tight coupling to Vercel's platform is a soft lock-in; eve is weeks old and unproven. Competitors: Cloudflare (Workers + Agents SDK — the closest analog), Netlify, AWS Amplify; on gateways, OpenRouter and LiteLLM; on sandboxes, E2B, Daytona, Modal. Open question: whether Gateway/Sandbox win usage from teams that don't host on Vercel.

## Sources

- https://en.wikipedia.org/wiki/Vercel
- https://rauchg.com/about
- https://vercel.com/blog/series-f
- https://www.gic.com.sg/newsroom/all/vercel-closes-series-f-at-9-3b-valuation-to-scale-the-ai-cloud/
- https://tracxn.com/d/companies/vercel/__uPuJfXzfvAQs0wmUuqRiXFxW4uGbcaKUHjHks8VPbrI
- https://github.com/vercel/ai
- https://vercel.com/docs/ai-gateway
- https://vercel.com/blog/ai-gateway-production-index
- https://vercel.com/blog/vercel-sandbox-is-now-generally-available
- https://vercel.com/blog/introducing-the-new-v0
- https://vercel.com/customers
- https://vercel.com/blog/elkjops-digital-transformation-with-next-js-and-vercel
- https://siliconangle.com/2026/06/17/vercel-launches-new-framework-enterprise-controls-agentic-ai-infrastructure/
- https://www.businesswire.com/news/home/20260617093685/en/Vercel-Brings-New-Agent-Framework-Full-Stack-Capabilities-and-Enterprise-Controls-to-Its-Agentic-Infrastructure-Platform
- https://vercel.com/blog/vercel-funding-series-d-and-valuation
- https://medium.com/history-of-vercel/history-of-vercel-2015-2020-6-7-zeit-and-next-js-dc480a88e0b8
