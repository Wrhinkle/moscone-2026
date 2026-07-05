# Postman

> The default API client used by tens of millions of developers, now rebuilt as an "AI-native" API platform — betting that APIs' next big consumer is agents, and selling the tooling to design, test, govern, and expose APIs (and MCP servers) to them.

- **Category:** api-platforms
- **AIEWF 2026 tier:** silver
- **Founded:** 2014, Bangalore, India (side project since 2012; HQ now San Francisco) (Verified — Wikipedia, company site, YourStory)
- **Website / GitHub:** https://www.postman.com · https://github.com/postmanlabs

## What they do

The core product is the API workspace nearly every backend developer has touched: an API client for composing/sending requests, collections that bundle requests with tests and docs, environments, mock servers, monitors, and a collaboration layer (workspaces, Private API Network) sold per-seat. The **Postman API Network** is a public directory of 100,000+ APIs, which matters because it's the raw material for their agent story.

Since 2025 Postman has pivoted hard to agents. The **AI Agent Builder** suite lets you compare LLMs and APIs side by side, and **Flows** (a visual low-code editor) chains API calls and model calls into agentic workflows. Full **MCP support** landed in 2025: you can send/debug MCP requests in the client like any HTTP request, and an MCP/AI Tool Builder generates custom MCP servers from any APIs in their network — pick the endpoints your agent actually needs, click Build, download a model-agnostic server that works with Claude, Cursor, etc. (Verified — Postman blog + docs.)

On **March 1, 2026** they shipped a rebuilt platform (Verified — Postman blog): Git-native collections in a YAML-based Collection v3 format (diffable, AI-readable), offline-capable, one collection holding HTTP/GraphQL/gRPC/MCP/MQTT/WebSocket/AI requests, a CLI unifying local and CI runs, local code-based mocks, an **Agent Mode** assistant that generates tests/stubs/client code against your collections, and an **API Catalog** — a governance/system-of-record layer over an org's API portfolio with natural-language querying. What you'd actually buy: seats for the workspace, plus enterprise governance (Catalog, Private API Network, SSO/org controls).

## Founders & origins

**Abhinav Asthana** (CEO) built Postman as a free Chrome extension in 2012 while at Yahoo Bangalore to make API testing less painful; after it passed ~500k organic users he incorporated the company in October 2014 with former colleagues **Ankit Sobti** (CTO) and **Abhijit Kane**. The name is a pun on the POST request. (Verified — Wikipedia, YourStory, company About page.)

## Funding

- **Seed, ~$1M (2015)** — Nexus Venture Partners (Verified — press, Wikipedia)
- **Series A, $7M (2016)** — Nexus (Reported — TechCrunch's later "total $207M" arithmetic is consistent)
- **Series B, $50M (June 2019)** — led by CRV, at ~$365M valuation (Verified — TechCrunch, PitchBook)
- **Series C, $150M (June 2020)** — led by Insight Partners, $2B valuation (Verified — TechCrunch, Insight)
- **Series D, $225M (Aug 2021)** — led by Insight, with Coatue, Battery, BOND; **$5.6B valuation** (Verified — TechCrunch, Insight)
- **Total: ~$433M.** No round since 2021; secondary-market pricing reportedly ~$3.2B, a ~40% markdown (Reported — The Arc, premieralts; treat as estimate). Third-party trackers put ARR at ~$313M for 2024 (Reported — Getlatka; unaudited). Acquisitions: Orbit, liblab (SDK generation, Nov 2025), Fern (API docs/SDKs, Dec 2025) (Reported — single aggregator source for dates).

## Evidence of real-world use

Unusually strong. **40M+ developers and 500,000 organizations, including 98% of the Fortune 500** (Reported — company figures, but repeated in independent BusinessWire coverage and directionally consistent with a decade of default-tool status). Named case studies include **X (Twitter)** and **Built** (vendor case studies). Public per-seat pricing = real commercial product. The annual **State of the API Report** (2025: one in four developers now design APIs specifically for AI agents) is itself a sign of platform-scale telemetry. April 2026: announced a **Microsoft collaboration** on model choice and unified API governance (Verified — BusinessWire). Caveat: user counts are cumulative/self-reported; the secondary-market markdown suggests investors question monetization at that scale.

## Relevance to agentic AI engineering

Postman sits squarely on the **tool-use and governance** thread of this repo: the API→MCP-server generation pipeline is the industrialized version of the tool-provisioning question in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and the API Catalog / Private API Network governance layer is a commercial take on the concerns in *Governance by Construction for Generalist Agents*. The AI-readable YAML Collection v3 format and natural-language catalog search connect to *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* — machine-readable API descriptions are exactly the metadata agents retrieve against. Agent Mode generating contract/integration tests from collections brushes against the agentic-SWE evaluation thread (e.g., *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*), since API contract tests are a natural verifiable reward signal. Memory and voice threads: largely orthogonal.

## Use cases & considerations

Use cases: (1) generate a scoped MCP server from an internal or public API instead of hand-writing one; (2) evaluate/compare LLM + API combinations in Flows before committing code; (3) contract-test the APIs your agents call, in CI via the CLI; (4) enterprise API catalog so agents (and humans) discover governed internal APIs. Considerations: per-seat SaaS with real lock-in at the collection/workspace layer (Git-native v3 mitigates this); the agent features are ~1 year old atop a mature client; free tier has tightened over the years, pushing teams to paid plans. Competitors: **Bruno, Insomnia, Hoppscotch** (clients — Bruno explicitly markets Git-native/offline against Postman), **Kong, Apigee, Gravitee** (governance/gateway side), **Composio, Arcade** (agent tool platforms). Open question: whether agents consume APIs via curated MCP catalogs like Postman's or generate integrations ad hoc from raw OpenAPI specs.

## Sources

- https://en.wikipedia.org/wiki/Postman_(software)
- https://www.postman.com/company/about-postman/
- https://yourstory.com/2017/07/techie-tuesdays-abhinav-asthana-postman
- https://techcrunch.com/2020/06/11/api-platform-postman-nabs-150m-series-c-on-2b-valuation/
- https://techcrunch.com/2021/08/18/api-platform-postman-valued-at-5-6-billion-in-225-million-fundraise/
- https://www.insightpartners.com/ideas/postman-closes-225-million-series-d-round-at-a-5-6-billion-valuation-to-power-the-api-first-world/
- https://blog.postman.com/new-postman-is-here/
- https://blog.postman.com/postman-launches-full-support-for-model-context-protocol-mcp-build-better-ai-agents-faster/
- https://learning.postman.com/docs/postman-ai-agent-builder/overview/
- https://www.postman.com/product/mcp-server/
- https://www.businesswire.com/news/home/20251008162423/en/One-in-Four-Developers-Now-Design-APIs-for-AI-Agents-According-to-Postmans-2025-State-of-the-API-Report
- https://www.businesswire.com/news/home/20260416207345/en/Postman-Announces-Collaboration-with-Microsoft-to-Expand-AI-Model-Choice-Accelerate-Developer-Workflows-and-Unify-API-Governance
- https://www.postman.com/customer-stories/x/ and https://www.postman.com/case-studies/built/
- https://www.thearcweb.com/article/postman-valuation-plunges-40-in-secondary-market-faQV7VkMLbUivVGt
- https://getlatka.com/companies/postman
- https://valueforstartups.in/postman_report
