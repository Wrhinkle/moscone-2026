# Composio

> Managed tool-calling infrastructure: one SDK/MCP layer that gives AI agents authenticated access to 1,000+ SaaS apps, so you don't build and maintain integrations yourself.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, San Francisco + Bengaluru (Verified — Tracxn, Together Fund, Elevation Capital all agree)
- **Website / GitHub:** https://composio.dev · https://github.com/ComposioHQ/composio

## What they do

Composio sells the integration layer for agents. Instead of hand-writing an OAuth flow, token refresh, and function schema for every app your agent touches, you install their SDK (TypeScript or Python) and get 1,000+ pre-built "toolkits" — Gmail, Slack, GitHub, Salesforce, Notion, HubSpot, etc. — exposed as tools to any major framework: OpenAI/OpenAI Agents, Anthropic, LangChain/LangGraph, LlamaIndex, Vercel AI SDK, CrewAI, AutoGen, Google ADK/Gemini, Mastra. Auth (OAuth 2.0/2.1, API keys), per-user connected accounts, and execution are handled server-side by Composio.

Two newer layers matter for 2026. **Tool Router (beta)** addresses the context-window problem of dumping thousands of tool definitions on a model: the agent searches/routes to relevant tools at runtime instead of loading them all. **Rube** is their consumer-facing MCP server that plugs 500+ apps into MCP clients (Claude, ChatGPT, Cursor) with no code. Their current positioning ("the skill layer of AI") is a bet on agents that accumulate reusable skills and learn from execution feedback across the platform — that's the pitch behind the Series A, and it's more vision than shipped product today (Unverified as a product capability as of 2026-07-02).

Practically, what you buy: hosted auth + tool execution + tool search, usage-priced. Public pricing page exists — free tier around 20k tool calls/month, a low-cost starter tier (~$29/mo reported), and enterprise plans with SOC 2 claims.

## Founders & origins

**Soham Ganatra (CEO) and Karan Vaidya** (Verified — Lightspeed, Together Fund, Tracxn). Reported origin story (Lightspeed/Together Fund): they met at a Physics Olympiad camp, became roommates at IIT Bombay, and both previously led engineering teams working on integrations — the pain that became the company. Prior employers not confirmed in sources I checked (Not found in public sources at the level of specific companies).

## Funding

- **Seed, ~$4M (2024):** co-led by Together Fund and Elevation Capital (Verified — Together Fund's own post, press).
- **Series A, $25M (announced July 22, 2025):** led by Lightspeed Venture Partners, with Elevation Capital, Together Fund, and angels incl. Gokul Rajaram and Dharmesh Shah (Verified — Lightspeed post, multiple press outlets). Note: Composio's own blog headline says "$29M," which appears to be total raised; one outlet reported "$24M" — the $25M/$29M-total framing is the consensus.
- **Total raised: ~$29M** (Verified). Y Combinator is listed among investors on Crunchbase (Reported).

## Evidence of real-world use

- **GitHub: ~29.1k stars, ~4.6k forks, MIT license, 860+ releases**, active PyPI/npm packages (Verified, repo itself). Strong OSS signal, though stars ≠ production use.
- **11x** (AI SDR company): documented case study — integrated Outlook, Salesforce, Calendly, People Data Labs for their Alice/Mike agents in ~a week; Composio claims $4.2M in enterprise deals influenced and 380 engineering hours saved (Reported — vendor case study, numbers are Composio's).
- **SwarmZero** and **Assista AI**: named case studies (agent orchestration and productivity startups respectively) (Reported — vendor site).
- **AWS published a Composio case study** (Amazon Bedrock usage) — an independent-ish co-marketing signal (Reported).
- Public usage-based pricing page = real commercial product. Customer roster skews toward AI-agent startups rather than named enterprises so far.

## Relevance to agentic AI engineering

This is squarely the **tool-use layer** of the agent stack: tool provisioning, auth, and runtime tool selection. Tool Router is a production response to the tool-selection/context problem studied in the repo's tool-use and governance papers — and the auth/permissioning layer is where governance of agent actions actually gets enforced (who can call which tool as which user). The "skill layer"/collective-learning pitch connects to the agent-memory literature (persisting successful trajectories as reusable skills). Less relevant to agentic SWE benchmarks (SWE-bench-style coding) or voice-agent papers, except that voice/SDR agents like 11x's are exactly the consumers of this layer.

## Use cases & considerations

Use cases: (1) an agent that reads/writes across Gmail + CRM + calendar per end-user, with per-user OAuth handled for you; (2) shipping MCP access to hundreds of apps into Claude/Cursor via Rube; (3) SDR/support agents needing many SaaS actions fast (the 11x pattern); (4) replacing a growing pile of in-house integration glue.

Considerations: your agent's credentials and actions flow through Composio's hosted service — real trust/lock-in surface, and enterprise buyers will want the SOC 2 details. Vendor-published ROI numbers should be discounted. Competitors: **Arcade.dev, Pipedream (Connect), Merge.dev, Paragon/Nango**, plus DIY MCP servers and Zapier's agent tooling. Open question: whether the "self-improving skills" layer becomes real differentiation or the company remains a (very good) integration catalog in a space where MCP is commoditizing connectors.

## Sources

- https://composio.dev/ and https://composio.dev/pricing
- https://composio.dev/blog/series-a
- https://github.com/ComposioHQ/composio
- https://lsvp.com/stories/investing-in-composio-building-the-backbone-of-ai-agent-intelligence/
- https://www.together.fund/perspectives/insights/investing-in-composio-building-the-learning-layer-for-agentic-ai
- https://www.elevationcapital.com/portfolio/composio
- https://tracxn.com/d/companies/composio/__S4CqdyIkWZd1BSTOwnjS82Hz0ppMkmDoAP_j4_oMBfk
- https://composio.dev/case-study/11x
- https://composio.dev/case-studies/swarmzero-case-study
- https://composio.dev/content/assista-case-study
- https://aws.amazon.com/solutions/case-studies/composio-case-study/
- https://composio.dev/blog/introducing-tool-router-(beta)
- https://india.entrepreneur.com/news-and-trends/composio-raises-usd-25-mn-from-lightspeed-to-advance/494938
