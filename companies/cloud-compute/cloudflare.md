# Cloudflare

> Global edge network (CDN, security, DNS) that has become a serious serverless cloud — and in 2025–26 repositioned itself as the default infrastructure layer for deploying and securing AI agents.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** gold
- **Founded:** 2009, Palo Alto → San Francisco, CA (Verified — Wikipedia, company site)
- **Website / GitHub:** https://www.cloudflare.com · https://developers.cloudflare.com · https://github.com/cloudflare (agents SDK: https://github.com/cloudflare/agents)

## What they do

Cloudflare operates a reverse-proxy network in 300+ cities that sits in front of roughly 1 in 5 websites worldwide (Verified — W3Techs/Statista put it at ~20% of all sites, with Amazon CloudFront a distant second at ~1.6%). The classic business is CDN, DDoS mitigation, WAF, DNS, and Zero Trust networking. What matters for an AI engineer is the developer platform layered on that network:

- **Workers** — V8-isolate serverless functions running at every edge location; no cold-start containers.
- **Durable Objects** — globally addressable, single-threaded compute instances with attached SQLite/KV storage; the primitive underneath their agent stack.
- **Workers AI** — serverless GPU inference across the network; as of Agents Week 2026 it runs large open-weight models (e.g., Kimi K2.5 with 256k context, multi-turn tool calling, vision, structured outputs).
- **Agents SDK** (`cloudflare/agents`, MIT, ~5.2k stars) — stateful agent runtime on Durable Objects: WebSocket/voice/email/Slack channels, scheduling, MCP client/server support, sandboxed code execution, browser automation, workflows. Agents hibernate to zero cost when idle, so "millions of concurrent agents" is architecturally plausible rather than marketing.
- **AI Gateway + Mesh** — proxy/observability for LLM calls, and (launched 2026) "Mesh" for private networking and lifecycle security of agents reaching internal APIs, plus Gateway rules for detecting unsanctioned "Shadow MCP" traffic.

At Agents Week 2026 they shipped Sandboxes GA (persistent isolated environments with shell/filesystem), Artifacts (git-compatible versioned storage for agent code), Workflows v2 (50k concurrency durable execution), voice agents (~30 lines of code for real-time STT/TTS), Agent Memory, a Monetization Gateway on the x402 payments protocol (Cloudflare co-founded the x402 Foundation, reviving HTTP 402 so agents can pay for resources in stablecoins), and a Code Mode MCP server exposing the whole Cloudflare API in <1,000 tokens (claimed 81% token reduction vs. conventional MCP tool lists).

## Founders & origins

Matthew Prince, Michelle Zatlyn, and Lee Holloway founded Cloudflare in July 2009 (Verified). Prince and Zatlyn met at Harvard Business School; Prince and Holloway had previously built Project Honey Pot, an anti-spam tracking network that inspired Cloudflare. First office was above a nail salon in Palo Alto. Prince remains CEO; Zatlyn is President/COO; Holloway built the core architecture but left before the IPO for health reasons (early-onset frontotemporal dementia, documented in Wired).

## Funding

Public company — NYSE: NET, IPO September 13, 2019 at $15/share, raising $525M (Verified). Pre-IPO: ~$330M+ across Series A ($2.1M, 2009, Pelion/Venrock), Series B ($20M, NEA), Series C ($50M), Series D ($110M, 2015, at $1.8B valuation — unicorn), Series E ($150M, 2019); corporate investors included Microsoft, Qualcomm Ventures, Google CapitalG, plus Union Square Ventures (Verified via CB Insights/Tracxn). Q1 2026: $639.8M revenue, +34% YoY, 4,416 customers paying >$100k/yr; FY2026 guidance ~$2.8B (Verified — 10-Q/earnings coverage). Note: announced a ~20% workforce reduction alongside Q1 2026 earnings, framed as AI-driven restructuring (Reported).

## Evidence of real-world use

The core network's usage is unambiguous (~20% of the web). For the agent stack specifically: the Agents SDK has 5.2k stars, 342 releases, and 30+ example apps; Knock published a documented human-in-the-loop agent build on the SDK; Cloudflare worked with Anthropic on remote MCP server infrastructure, and in 2025 a wave of companies (Atlassian, Asana, Intercom, PayPal, Stripe, Webflow among those announced) launched remote MCP servers on Cloudflare (Reported — Cloudflare blog; independent confirmation per-company not verified here). Public per-request pricing exists for Workers, Durable Objects, and Workers AI — a real commercial product, not a demo.

## Relevance to agentic AI engineering

Cloudflare is betting on being the deployment substrate for agents: durable per-agent state (Durable Objects + Agent Memory connects to the agent-memory literature in this repo, e.g. MemGPT-style persistent-context work), sandboxed code execution and Code Mode (directly relevant to the tool-use/governance papers — executable code actions vs. JSON tool calls, à la CodeAct), voice agents over WebSockets (voice-agent papers), and MCP governance/Shadow-MCP detection (tool-use governance). Sandboxes + Artifacts also make it a plausible runner for agentic SWE workloads of the kind measured by SWE-bench-style benchmarks.

## Use cases & considerations

1. Host stateful, long-lived agents (chat/voice/email) that cost nothing when idle — Agents SDK + Durable Objects.
2. Deploy a remote MCP server with OAuth in front of your product's API.
3. LLM traffic control: AI Gateway for caching, rate-limiting, and observability across providers.
4. Cheap burst inference on open-weight models via Workers AI instead of managing GPUs.

Considerations: the agent stack is TypeScript/V8-first (Python support is limited); Durable Objects are a proprietary programming model — real lock-in; Workers AI's model catalog trails Together/Fireworks/Baseten on breadth and raw GPU flexibility; many Agents Week 2026 features are weeks old (waitlists, betas). Competitors: Vercel and Fastly (edge compute), AWS/GCP/Azure (general cloud + Bedrock/Vertex agents), Fly.io/Modal (stateful/GPU workloads), Together/Fireworks (inference). Open question: whether x402/Monetization Gateway sees adoption beyond Cloudflare's own ecosystem.

## Sources

- https://en.wikipedia.org/wiki/Cloudflare
- https://www.cloudflare.com/our-story/
- https://developers.cloudflare.com/agents/
- https://developers.cloudflare.com/workers-ai/
- https://developers.cloudflare.com/durable-objects/
- https://github.com/cloudflare/agents
- https://blog.cloudflare.com/agents-week-in-review/
- https://blog.cloudflare.com/workers-ai-large-models/
- https://blog.cloudflare.com/building-agents-at-knock-agents-sdk/
- https://www.cloudflare.com/press/press-releases/2026/cloudflare-launches-mesh-to-secure-the-ai-agent-lifecycle/
- https://www.cbinsights.com/research/cloudflare-ipo-investor-analysis/
- https://tracxn.com/d/companies/cloudflare/__IL42hIOXmhTb0V8Oh8yXCcrIq4P15QTAj0oBxVCSuKw
- https://techcrunch.com/2019/09/13/cloudflare-cofounder-michelle-zatlyn-on-the-companys-successful-ipo-and-whats-next/
- https://www.stocktitan.net/sec-filings/NET/10-q-cloudflare-inc-quarterly-earnings-report-580158f0de78.html
- https://w3techs.com/technologies/details/cn-cloudflare
- https://www.statista.com/chart/35487/market-share-of-reverse-proxy-services-cloudflare/
