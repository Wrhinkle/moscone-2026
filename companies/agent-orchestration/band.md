# Band

> A "Slack/WhatsApp for AI agents": a hosted communication and governance layer where agents built on any framework — plus humans — meet in shared, persistent chat rooms to discover each other, exchange context, and delegate work.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2024 (Reported — StartupHub.ai); exited stealth April 23, 2026 (Verified). HQ listed as San Francisco (PR Newswire) and Kochav Ya'ir, Israel (StartupHub) — likely US/Israel dual footprint; legal name reported as Thenvoi AI Ltd. (its GitHub SDK org was originally `thenvoi`, now `band-ai`).
- **Website / GitHub:** [band.ai](https://www.band.ai) · [docs.band.ai](https://docs.band.ai) · [github.com/band-ai/band-sdk-python](https://github.com/band-ai/band-sdk-python)

**Disambiguation note:** This is NOT Band Protocol (the crypto oracle project) and not the Korean group-communication app BAND by Naver. This is BAND, the 2026-launch agent-interaction-infrastructure startup at band.ai — confirmed as the AIEWF 2026 sponsor context (it also co-hosted an AIEWF side-event happy hour with Arize AI, AWS, CrewAI, and YugabyteDB). Despite the consumer-ai category slot, the product is B2B/developer infrastructure.

## What they do
Band is a hosted interaction layer for multi-agent systems. Instead of wiring point-to-point integrations between agents, you connect each agent to Band via an SDK; agents then join durable "rooms" where they and human teammates exchange structured messages, share context, discover peers, and delegate tasks. Band owns the room history, so an agent can resume from platform-held context rather than each framework maintaining its own memory of the conversation. Transport is WebSocket (Phoenix Channels) plus REST; each agent gets per-room scoped context isolated from its other rooms, and built-in platform tools for chat, contacts, memory, and participant management.

The Python SDK (MIT-licensed) ships framework adapters for LangGraph, Pydantic AI, the Anthropic SDK, Claude Agent SDK, CrewAI, Gemini, Google ADK, Parlant, Letta, Agno, Codex, and OpenCode, plus bridge adapters: an A2A bridge/gateway that exposes Band peers as A2A JSON-RPC endpoints (so external A2A clients can discover and message Band agents), and ACP support for editors like Cursor and Claude Code. Co-founder Goomanovsky's framing on Product Hunt: "A2A is the protocol. Band is the network." Governance features — human-in-the-loop approvals, permission enforcement, monitoring of agent interactions — are the enterprise pitch. Pricing is public and self-serve (Reported): Free (10 remote agents, 50 rooms), Pro at $17.99/mo (40 agents, 250 rooms), Enterprise custom.

## Founders & origins
- **Arick Goomanovsky (CEO)** — Verified: Israeli Unit 8200 alum, two prior exits — co-founded Sygnia (acquired by Temasek, ~$250M reported) and Ermetic (acquired by Tenable, ~$300M reported).
- **Vlad Luzin (CTO)** — Verified across Team8/CTech: ~20 years in distributed systems; former VP of AI & Cloud Platform at Verint, senior roles at CME Group, and headed Multi-Agent AI incubation at Samsung Telecom Research; graduate of Israel's DDR&D (MoD R&D directorate).

Origin thesis (per Team8's investment memo): the shift from a "copilot era" to a "workforce era" where teams run many heterogeneous agents that need a shared coordination substrate with audit trails.

## Funding
- **$17M Seed**, announced April 23, 2026, led by/with Sierra Ventures, Hetz Ventures, and Team8 — **Verified** (VentureBeat, PR Newswire, ynet, CTech, Team8). Total raised: $17M. No later rounds found as of 2026-07-02.

## Evidence of real-world use
Early and thin — be honest about this. No named customers in any public source; the launch PR cites unnamed "early adopters in software development, enterprise automation, and advanced R&D." Signals that do exist: a public self-serve pricing page (real commercial product), an active MIT-licensed SDK (v1.1.0 released June 22, 2026; only 8 stars/5 forks as of research date), a Product Hunt launch with 204 upvotes (#6 of the day) but zero written reviews, and AIEWF 2026 sponsorship alongside CrewAI/Arize/AWS. Verdict: credible founders and real product surface, but adoption is unproven as of 2026-07-02.

## Relevance to agentic AI engineering
Band sits at the agent-to-agent coordination layer — above per-agent tool-calling (MCP), implementing/extending A2A and ACP. Directly relevant repo research: *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering* (Band's rooms are essentially that coordination substrate productized), *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too* (Band's permission/HITL layer is a commercial take on system-level agent governance), *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and the agent-memory line (*Memory for Autonomous LLM Agents*, *Are We Ready For An Agent-Native Memory System?*) — Band's platform-owned durable room context is one answer to agent-native memory across heterogeneous frameworks.

## Use cases & considerations
Use cases: (1) coordinating a mixed fleet — e.g., a Claude Code agent, a CrewAI research crew, and a Letta memory agent — in one auditable room; (2) exposing internal agents to partners via the A2A gateway without custom APIs; (3) human-approval checkpoints over long-running multi-agent back-office workflows (relevant to the Ridgeline back-office agent backlog).

Considerations: hosted platform = the conversation history and coordination graph live in Band's cloud (lock-in, data-retention questions; enterprise tier gates custom retention). Very young — protocol churn risk if A2A/ACP evolve. Competitors: raw A2A/agent2agent implementations, LangGraph Platform, CrewAI's own orchestration, Microsoft Agent Framework/AutoGen, IBM ContextForge-style gateways. Open questions: conflict resolution and state consistency across agents (raised, unanswered, in their Product Hunt thread), and whether an independent network wins versus framework-native orchestration.

## Sources
- https://venturebeat.com/orchestration/talking-to-ai-agents-is-one-thing-what-about-when-they-talk-to-each-other-new-startup-band-debuts-universal-orchestrator
- https://www.prnewswire.com/news-releases/band-exits-stealth-with-17m-to-build-the-communication-and-interaction-layers-for-the-internet-of-agents-302751810.html
- https://team8.vc/all-agents-one-network-why-we-invested-in-band/
- https://www.calcalistech.com/ctechnews/article/hkuomtva11l
- https://www.ynetnews.com/business/article/hkkpu5utbe
- https://www.startuphub.ai/startups/band
- https://github.com/thenvoi/thenvoi-sdk-python (redirects to band-ai/band-sdk-python)
- https://www.producthunt.com/products/band
- https://www.band.ai/ and https://www.band.ai/pricing (site returned 403 to direct fetch; content via search index)
- https://www.ai.engineer/worldsfair/2026
