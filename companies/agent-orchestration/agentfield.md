# AgentField

> Open-source control plane that turns AI agent code into governed, observable production infrastructure — build agents like APIs, not scripts.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** Not found in public sources (recent — product/docs suggest 2025); San Francisco/Toronto-linked team (**Unverified**)
- **Website / GitHub:** https://agentfield.ai · https://github.com/Agent-Field/agentfield

## What they do
AgentField (styled "AgentField" / "Agentfield") is a stateless, horizontally-scaling Go control plane that exposes agent logic — written in Python, Go, or TypeScript — as REST endpoints with queuing, retries, cross-agent routing, async execution, and durable human-in-the-loop pause/resume built in. It gives each agent a W3C-style decentralized cryptographic identity for enforceable permissions and verifiable audit trails, plus fleet management (canary deploys, A/B testing) and automatic tracing/workflow DAGs. It integrates with coding harnesses like Claude Code, Codex, and Gemini CLI, and is designed to fan out to 10,000+ coordinated agents backed by Postgres.

**Founders (Reported):** Oktay Goktas, PhD and Santosh Kumar Radha, PhD — previously built Agnostiq/Covalent (acquired by DataRobot, 2025), bringing distributed-computing infra experience.

**Funding:** Not found in public sources beyond named backers Panache Ventures and Brightspark Ventures (amounts undisclosed) (**Reported**).

## Evidence of real-world use
Open source, Apache 2.0, GitHub repo shows ~2.3k stars and 1,200+ commits — real developer traction, not just a landing page.

## Relevance to agentic AI engineering
Directly maps to the agent-orchestration/tool-calling and governance layer of an agent stack: multi-agent coordination, identity/audit for autonomous agents, and durable async execution — comparable ground to LangGraph, Temporal-for-agents, or agent identity/IAM discussions at AIEWF.

## Sources
- https://agentfield.ai/about
- https://github.com/Agent-Field/agentfield
- https://www.crunchbase.com/organization/agent-field
- https://www.producthunt.com/products/agentfield
