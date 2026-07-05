# DoorDash

> The delivery/logistics marketplace that has become a large, publicly documented enterprise adopter of production agentic AI.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** 2013, San Francisco (Verified — public company, well known)
- **Website / GitHub:** careersatdoordash.com/blog (engineering blog); doordash.com

## What they do
DoorDash isn't an AI vendor — it's a logistics/marketplace company (consumers, merchants, "Dashers") that has built and published a substantial internal agentic AI platform. Per their engineering blog, they run a "Managed Agent Services" layer exposing business logic and grounding data as typed tools over Model Context Protocol (MCP), so any internal agent or external integration can call the same tool surface. They describe moving from single-agent chatbots to "deep agent" hierarchies — specialized sub-agents coordinated by an orchestrator for long-horizon tasks — and are adopting Google's Agent2Agent (A2A) protocol for peer-agent coordination. Their consumer-facing "Ask DoorDash"/DoorDash Assistant product sits on a hybrid keyword + dense-vector retrieval engine with reciprocal rank fusion reranking. They also publish a DoorDash Drive API MCP server for logistics integrations.

## Founders & origins / Funding
Public company (NYSE: DASH); founders Tony Xu, Stanley Tang, Andy Fang (Verified, general knowledge). Not relevant here as a funding story — the profile is about enterprise AI adoption, not a startup raise.

## Evidence of real-world use
Multiple detailed public engineering posts (MCP tool surface, deep-agent architecture, Ask DoorDash intelligence layer), an active DoorDash Drive MCP server used by third parties, and third-party case-study coverage (ZenML LLMOps database, Snowflake Summit coverage of DoorDash's open data architecture). This is unusually well-documented compared to typical "customer logo" evidence.

## Relevance to agentic AI engineering
Concrete reference architecture for multi-agent orchestration, MCP-based tool standardization, A2A inter-agent protocols, and RAG at consumer scale — directly relevant to tool-calling, agent orchestration, and SDLC/evals tracks at AIEWF.

## Sources
- https://careersatdoordash.com/blog/beyond-single-agents-doordash-building-collaborative-ai-ecosystem/
- https://careersatdoordash.com/blog/building-ask-doordash-part-two-intelligence/
- https://careersatdoordash.com/blog/building-doordash-assistant-an-engineering-overview/
- https://www.zenml.io/llmops-database/building-a-collaborative-multi-agent-ai-ecosystem-for-enterprise-knowledge-access
- https://siliconangle.com/2026/06/03/open-data-architecture-powers-real-time-logistics-snowflakesummit/
