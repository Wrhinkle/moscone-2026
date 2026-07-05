# CopilotKit

> Open-source frontend framework plus an open protocol (AG-UI) for wiring AI agents into user-facing apps — chat UIs, generative UI, shared state, and human-in-the-loop approvals over any agent backend.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** bronze
- **Founded:** 2023, Seattle (Verified — Techstars Seattle 2023 cohort per GeekWire/press; founders are Israeli-born brothers, so some coverage frames it as Israeli-founded)
- **Website / GitHub:** https://www.copilotkit.ai · https://github.com/CopilotKit/CopilotKit · https://github.com/ag-ui-protocol/ag-ui

## What they do

CopilotKit is the "last mile" between an agent backend and the user. The open-source framework (MIT, TypeScript) is a three-layer stack: frontend SDKs (React/Next.js GA; Angular, Vue, React Native supported; Slack/Teams in beta), a runtime layer (Express/Hono), and adapters to agent backends (LangGraph, CrewAI, Mastra, Pydantic AI, or custom). The layers talk over **AG-UI (Agent–User Interaction)**, an event-based protocol streamed over SSE that CopilotKit created and spun out as an open standard — think "MCP for the agent↔UI boundary": standardized events for token streaming, tool calls, state deltas, and interrupts, so any compliant frontend can drive any compliant agent.

Concretely, what you integrate: React hooks/components (`useAgent`, prebuilt chat UI) that give you streaming chat with tool-call rendering, **generative UI** (the agent emits structured events that render as real interactive components instead of text walls), **bidirectional shared state** (agent reads/writes app state, UI reflects agent progress), and **human-in-the-loop interrupts** (agent pauses for user approval mid-run). v1.62.x shipped July 2026; 1,389 releases and ~12.5k commits indicate a fast-moving codebase.

Commercially, they sell an enterprise layer ("Enterprise Intelligence Platform"): self-hosted deployment, managed scaling, Slack/Teams distribution, premium features. No public pricing — "talk to an engineer" enterprise motion (Verified — copilotkit.ai).

## Founders & origins

**Atai Barkai (CEO)** — previously media infrastructure at Meta and led flagship iOS apps at Doximity; BS/MS in physics from UPenn. **Uli Barkai** (growth/partnerships) — financial economics at Columbia, philosophy at Tel Aviv University. Brothers. (Verified — TechCrunch, GeekWire, press.) Origin story (Reported): they first built tawkitAI, an AI podcast platform, open-sourced their internal copilot infrastructure, saw developer pull, and pivoted — renaming to CopilotKit during/after Techstars Seattle 2023. ~25 employees as of May 2026 (Reported — TechCrunch).

## Funding

- **Seed, $7M** — previously unannounced, disclosed with the A (Verified — TechCrunch, GeekWire).
- **Series A, $20M (announced May 5, 2026)** — led by Glilot Capital, NFX, and SignalFire (Verified — TechCrunch, GeekWire, Calcalist).
- **Total raised: $27M** (Verified).

## Evidence of real-world use

- **GitHub: ~35.8k stars, ~4.4k forks, "used by 1.7k" repos**, MIT license (Verified — repo, 2026-07-02). Plus a separate ag-ui-protocol org.
- **AG-UI ecosystem adoption is the strongest signal**: first-party integrations documented by Google ADK (listed in Google's own ADK docs under Agentic UI), Microsoft Agent Framework, AWS Strands Agents, and AWS Bedrock AgentCore Runtime (added March 2026); framework support in LangChain/LangGraph, CrewAI, Mastra, Pydantic AI, Agno, AG2 (Verified — vendor blog posts cross-checked with press; Google/Microsoft/AWS docs referenced in third-party coverage).
- **Docusign**: named case study with a VP quote about using the SDK for in-app agentic experiences; **Evergreen Wealth** CTO quote on AG-UI decoupling agent framework from frontend (Reported — vendor site). TechCrunch names **Deutsche Telekom, Docusign, Cisco, S&P Global** as enterprise users (Reported — company claims via press).
- Claims of "millions of installs per week" and "trusted by a significant share of the Fortune 500" are company statements (Unverified independently). The homepage logo wall (Apple, Walmart, Disney...) should be read skeptically — likely OSS usage, not paying customers.

## Relevance to agentic AI engineering

CopilotKit owns the **agent↔human interaction layer** — the part of the stack the repo's tool-use/governance papers mostly assume away. AG-UI's interrupt/approval events are the concrete mechanism for the human-review loops that *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too* argue must be structural, not bolted on. Shared state between agent and app is a practical instance of the agent-state concerns in *From Plan to Action: How Well Do Agents Follow the Plan?* (surfacing plan/progress to users). Their "self-learning agents via in-context reinforcement learning" claim brushes against the agent-memory literature (*Memory for Autonomous LLM Agents*, *Are We Ready For An Agent-Native Memory System?*) but is marketing-stage (Unverified as shipped capability). Complementary, not competitive, with orchestration peers in this folder (LangChain, Temporal, Inngest) — it sits above them.

## Use cases & considerations

Use cases: (1) putting a production chat/copilot UI over an existing LangGraph or CrewAI backend without writing SSE plumbing; (2) generative UI — agent renders forms/charts/approve-reject cards instead of text (e.g., a Job Packet Readiness Auditor front end with human sign-off); (3) one UI codebase targeting agents on Google ADK, Microsoft Agent Framework, and AWS Strands via AG-UI; (4) distributing an internal agent into Slack/Teams.

Considerations: React-first — other frontends lag GA. AG-UI is open but CopilotKit-governed; protocol standards wars are live (Google's A2UI/Open-JSON-UI, MCP Apps — CopilotKit is hedging by supporting all three). Enterprise pricing is opaque. Competitors: **Vercel AI SDK (+ AI Elements), assistant-ui, LangChain's Agent Chat UI**, and DIY over raw SSE/WebSockets. Open question: whether the UI-protocol layer stays independent or gets absorbed by the cloud vendors now adopting it.

## Sources

- https://techcrunch.com/2026/05/05/copilotkit-raises-27m-to-help-devs-deploy-app-native-ai-agents/
- https://www.geekwire.com/2026/seattles-copilotkit-raises-27m-as-some-of-the-biggest-names-in-tech-adopt-its-ai-agent-protocol/
- https://www.calcalistech.com/ctechnews/article/bkbjddprbx
- https://github.com/CopilotKit/CopilotKit
- https://github.com/ag-ui-protocol/ag-ui
- https://www.copilotkit.ai/
- https://www.copilotkit.ai/ag-ui
- https://www.copilotkit.ai/blog/microsoft-agent-framework-is-now-ag-ui-compatible
- https://www.copilotkit.ai/blog/ag-ui-protocol-bridging-agents-to-any-front-end
- https://www.copilotkit.ai/blog/build-with-googles-new-a2ui-spec-agent-user-interfaces-with-a2ui-ag-ui
- https://www.marktechpost.com/2025/12/11/copilotkit-v1-50-brings-ag-ui-agents-directly-into-your-app-with-the-new-useagent-hook/
- https://virtuslab.com/blog/ai/git-hub-all-stars-4-copilot-kit-solving-the-last-mile-problem-for-ai-agents
