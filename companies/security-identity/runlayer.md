# Runlayer

> A governed gateway and control plane that lets enterprises run MCP servers and AI agents with real authentication, permissions, scanning, and audit — the "corporate app store plus firewall" for agent tooling.

- **Category:** security-identity
- **AIEWF 2026 tier:** gold
- **Founded:** 2025 (August 2025 per TechCrunch; launched from stealth November 2025), San Francisco — Verified
- **Website / GitHub:** https://www.runlayer.com · https://github.com/runlayer · https://pypi.org/project/runlayer/

## What they do

Runlayer sits between AI clients (Claude, ChatGPT, Cursor, internal agents) and the tools those clients call over the Model Context Protocol. Instead of every employee wiring MCP servers directly into their client with pasted API keys, the company runs everything through Runlayer's gateway: a registry of 18,000+ cataloged MCP servers plus your internal ones, each scanned for known vulnerabilities, data-leakage risk, and "permission drift" before it's allowed in. At runtime the gateway does real-time inspection of tool calls, outputs, and inferred intent — the threat-detection layer for prompt-injection-style attacks that MCP itself doesn't provide.

The identity story is the enterprise hook: it integrates with IdPs like Okta and Microsoft Entra, so agent and user permissions are scoped centrally, OAuth grants are managed in one place, and every agent session leaves an audit trail. There's also "shadow AI discovery" (finding unmanaged agents/plugins employees already use), spend/adoption analytics tied to teams, and — post-Series A — an agent-enablement layer where employees build governed agents with memory, triggers, and scoped permissions, packaging internal APIs as reusable MCPs and skills. A CLI (`runlayer` on PyPI) scans MCP configurations across clients and deploys the authenticated proxy. It integrates with Cursor Hooks (official partnership) and Anthropic's MCP Tunnels for connecting firewalled internal systems.

Practically, what you'd buy: a commercial, cloud-hosted control plane (no public pricing page — sales-led enterprise motion) that replaces ad-hoc MCP config files with centrally governed, logged, permission-scoped tool access.

## Founders & origins

Verified across TechCrunch and company sources: **Andrew Berman** (CEO) — third-time founder (Nanit baby monitors; Vowel, an AI video-conferencing tool acquired by Zapier in 2024), then Director of AI at Zapier, where he built one of the first MCP servers working directly with OpenAI and Anthropic. **Vitor Balocco** — former Staff AI Engineer at Zapier, speaks on MCP security. **Tal Peretz** — also ex-Zapier; reportedly (single source) a former ML lead in the Israeli Air Force. Notable advisors/angels: **David Soria Parra** (lead creator of MCP), Travis McPeak (head of security at Cursor), Nikita Shamgunov (Neon). The origin story is essentially "we built Zapier's MCP surface and saw the security hole firsthand."

## Funding

- **Seed, ~Nov 2025:** $11M from Khosla Ventures (Keith Rabois) and Felicis, with eight unicorn founders as angels — Verified (TechCrunch, company blog).
- **Series A, June 24, 2026:** $30M led by Felicis (preempted; Khosla participating). Fortune reports Vinod Khosla wanted "every available dollar" of the round — Verified (Fortune, SecurityWeek, FinSMEs).
- **Total raised:** $42M — Verified. Valuation: Not found in public sources.

## Evidence of real-world use

Unusually strong for a company this young. Named customers (company site + Fortune): Instacart, Gusto, Opendoor, dbt Labs, AngelList, PagerDuty, Decagon, Lemonade, Jane, Homebase — 12+ unicorns per Fortune. Documented usage, not just logos: Fortune reports **half of Gusto uses it daily**, and a Fortune 500 bank monitors 100,000+ employees' AI activity across 200,000 devices through it (Reported — single outlet, but a strong one). The Cursor Hooks partnership is public on Runlayer's blog. GitHub org exists (e.g., a pinned fork of Okta's MCP server) but the core product is closed-source.

## Relevance to agentic AI engineering

This is the tool-use/governance layer of the agent stack: the productized answer to the risks documented in this repo's tool-use/governance landscape — prompt-injection attacks on tool-calling agents (AgentDojo-style benchmarks) and pre-deployment risk assessment of agent tool access (ToolEmu's LM-emulated sandbox line of work). It's complementary to agentic SWE work (coding agents like Cursor are a first-class client via hooks) and to agent-memory research insofar as its enablement layer ships scoped memory per governed agent. Adjacent AIEWF profiles: WorkOS (security-identity) and Keycard cover agent identity; Runlayer is the runtime gateway on top.

## Use cases & considerations

1. Roll out MCP tooling to a whole company without per-employee API keys — IdP-scoped access plus audit.
2. Security review/monitoring of third-party MCP servers before engineers adopt them.
3. Expose internal APIs to Claude/Cursor/ChatGPT as governed internal MCPs.
4. Shadow-AI discovery and AI spend attribution for compliance teams.

**Considerations:** closed-source gateway in the critical path of all agent traffic = availability and lock-in risk; no public pricing; the category is crowding fast (Cisco's open-source mcp-scanner, ContextForge, Zapier MCP itself, plus IdPs and API gateways like Gravitee moving in); and platform vendors (Anthropic, OpenAI) could absorb gateway features natively. Open question: whether "MCP gateway" stays a standalone category or collapses into identity providers.

## Sources

- https://techcrunch.com/2025/11/17/mcp-ai-agent-security-startup-runlayer-launches-with-8-unicorns-11m-from-khoslas-keith-rabois-and-felicis/
- https://fortune.com/2026/06/24/exclusive-vinod-khosla-felicis-runlayer-nanit-30-million-enterprise-ai/
- https://www.runlayer.com/ (product, customers)
- https://www.runlayer.com/blog/runlayer-raises-11m-to-scale-enterprise-mcp-infrastructure
- https://www.runlayer.com/blog/cursor-hooks
- https://www.securityweek.com/runlayer-raises-30-million-in-series-a-funding/
- https://github.com/runlayer · https://pypi.org/project/runlayer/

*Profile compiled 2026-07-02.*
