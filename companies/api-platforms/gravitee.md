# Gravitee

> Open-source-rooted API management platform that has repositioned as an "AI agent management" control plane — one gateway/governance layer for REST APIs, Kafka/event streams, LLM traffic, and MCP/A2A agent traffic.

- **Category:** api-platforms
- **AIEWF 2026 tier:** gold
- **Founded:** 2015, Lille, France (Verified — company site, Crunchbase, press all agree; team now distributed with significant UK/US presence)
- **Website / GitHub:** https://www.gravitee.io · https://github.com/gravitee-io/gravitee-api-management

## What they do

The core product is a full API management stack: a Java-based gateway with 50+ pre-built policies (auth, rate limiting, transformation), a management console, a developer portal, analytics, and an Access Management module (OIDC/IAM). The Community Edition is Apache 2.0 open source; revenue comes from an enterprise edition and Gravitee Cloud SaaS, deployable on-prem, self-hosted, or managed. A long-standing differentiator versus Kong/Apigee is being **event-native**: the same gateway fronts asynchronous APIs and Kafka/MQTT/WebSocket streams with protocol mediation, not just HTTP.

Since 2025 the company has bet hard on agents. Gravitee 4.8 shipped **Agent Mesh**: an AI gateway that governs LLM calls, agent-to-agent (A2A protocol) traffic, and agent-to-tool traffic; an **MCP Agent Tool Server** that converts existing HTTP proxy APIs into MCP servers so agents can consume your existing API estate as tools; an **Agent Catalog** that inventories A2A agent cards (capabilities, I/O types, security schemes); and an AI-era IAM story for agent identity. They also exposed their own management APIs over MCP so Claude/Cursor-style clients can administer the platform. Practically, what you'd buy: one control plane where every API, event stream, model endpoint, MCP server, and agent gets the same policy enforcement, subscription plans, and observability.

## Founders & origins

Started in 2015 as an open-source project by four French developers: **David Brassely (CTO), Nicolas Géraud (CCO), Titouan Compiègne, and Azize Elamrani** (Verified — TechCrunch, Tracxn, company bios). **Rory Blundell** is CEO and is listed as a founder in TechCrunch and company materials, though origin-story coverage (Oxx) frames the start as the developer team and describes Blundell scaling it commercially from ~4 people/$0.5M revenue; exact joining date not found in public sources. The commercial entity was originally GraviteeSource SARL.

## Funding

- **Series A, ~$11M (July 2021)** — investors include AlbionVC and Oxx (Reported — startupintros/Tracxn; amount single-sourced).
- **Series B, $30M (Sept 2022)** — led by Riverside Acceleration Capital, with Kreos Capital, AlbionVC, Oxx (Verified — GlobeNewswire, Riverside).
- **Series C, $60M (May 2025)** — led by Sixth Street Growth, with Riverside Acceleration Capital and AlbionVC (Verified — TechCrunch, Sixth Street, GlobeNewswire).
- **Total:** company and TechCrunch say "$125M+"; Tracxn counts $101M across equity rounds — the gap is likely debt/undisclosed rounds (discrepancy noted, Unresolved). ARR was ~$22M in FY2024, ~130 employees at Series C (Reported — TechCrunch).

## Evidence of real-world use

- **Michelin**: documented case study — 230+ of Michelin's ~660 RESTful APIs standardized on Gravitee across isolated network zones and distributed plants (Reported — vendor case study, but detailed and specific).
- Named enterprise customers: **Roche, Blue Yonder, Tide** among "hundreds of customers" (Reported — TechCrunch, vendor).
- **Gartner Magic Quadrant Leader for API Management, 2024 and 2025** (Verified — company + press; note Gartner placements are pay-to-brief but Leader quadrant is a real market signal).
- OSS: main repo has ~426 stars but ~29,800 commits, 850 release tags, Apache 2.0 — low star count for a 10-year-old project, but heavy sustained engineering activity; adoption skews enterprise-download rather than GitHub-social (Verified — repo).
- Microsoft published a co-marketing piece on Gravitee for the AI agent era (Nov 2025) (Verified — microsoft.com).

## Relevance to agentic AI engineering

Gravitee is a production answer to the **tool-use and governance** problem in this repo's landscape: who may call which tool, under what identity, with what rate limits and audit trail — enforced at a gateway rather than in agent code. The MCP Tool Server (existing APIs → agent tools) and A2A catalog directly operationalize the tool-provisioning and inter-agent-protocol questions the governance papers raise; the AI-IAM work maps to agent-identity concerns. Its event-stream gateway is relevant to agents consuming real-time data. Largely orthogonal to the agentic SWE benchmark and agent-memory threads; voice-agent relevance is indirect (fronting realtime APIs).

## Use cases & considerations

Use cases: (1) expose an existing internal API estate to agents as governed MCP servers instead of writing bespoke servers; (2) central LLM/AI gateway for cost, security, and observability across teams; (3) unified governance of Kafka streams + REST APIs; (4) inventorying/authorizing A2A agents in a large org. Considerations: this is enterprise middleware — expect enterprise sales and per-gateway pricing (no simple public price list for the platform); the agent features are less than a year old and thinner than the mature APIM core. Competitors: **Kong (incl. Kong AI Gateway), Google Apigee, MuleSoft, Tyk, WSO2, Solace** (event side), and lighter AI-gateway plays (**LiteLLM, Portkey, Cloudflare AI Gateway**). Open question: whether an API-management incumbent or agent-native newcomers win the agent-governance layer.

## Sources

- https://www.gravitee.io/ and https://www.gravitee.io/company
- https://techcrunch.com/2025/05/20/gravitee-a-platform-that-helps-companies-manage-apis-raises-60m/
- https://sixthstreet.com/investment_announce/gravitee-raises-60-million-series-c-for-agentic-api-and-event-management-led-by-sixth-street-growth/
- https://www.globenewswire.com/news-release/2022/09/08/2512451/0/en/Gravitee-io-raises-30m-to-transform-the-way-APIs-are-managed-and-secured.html
- https://github.com/gravitee-io/gravitee-api-management
- https://www.gravitee.io/case-studies/michelin
- https://www.gravitee.io/platform/agent-mesh and https://www.gravitee.io/blog/gravitee-4.8-agent-mesh
- https://www.gravitee.io/blog/product-releases-mcp-platform-api-support
- https://www.oxx.vc/portfolio-founder-stories/beyond-apis-gravitee-ceo-rory-blundell-on-building-digital-infrastructure-for-the-future/
- https://tracxn.com/d/companies/gravitee.io/__T6qDeMCDvM9aQ_EDpsYST6B2t66ETffLRJ1p4Ami-Gc
- https://startupintros.com/orgs/gravitee
- https://www.microsoft.com/en-gb/industry/blog/cross-industry/2025/11/17/gravitee-api-management-ai-agent-era/
