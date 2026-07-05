# Keycard

> Identity and access management built specifically for AI agents: each agent gets its own identity, short-lived task-scoped credentials, runtime policy enforcement, and a full audit trail.

- **Category:** security-identity
- **AIEWF 2026 tier:** gold
- **Founded:** 2025, San Francisco (Verified — multiple press sources; emerged from stealth October 2025)
- **Website / GitHub:** https://www.keycard.ai/ • Docs: https://docs.keycard.ai/ • Console: console.keycard.ai

## What they do

Keycard is a control plane that sits between agents and the tools/APIs/data they touch. The core thesis: agents today inherit their user's full permissions (an OAuth token pasted into an env var), which is exactly wrong for a non-deterministic workload. Keycard instead resolves a composite identity — user + device + agent workload + task context — evaluates policy at credential-issuance time, and mints short-lived, least-privilege tokens bound to a specific task that expire when the task completes and are revocable immediately.

Concretely, you integrate via SDKs (Python and TypeScript) that make MCP servers and agents "Keycard-aware": bearer middleware, metadata endpoints, and grant decorators, with the SDK abstracting the OAuth 2.1 + PKCE handshake, identity binding, credential caching, and token refresh. Agents exchange Keycard-issued JWTs for scoped tokens to downstream services (GitHub, Google Calendar, AWS S3) via OAuth 2.0 Token Exchange (RFC 8693) — Keycard never proxies your data. A `keycard run` CLI virtualizes `.env` and `mcp.json`, injecting secrets in-memory while auditing shell, MCP, and credential events — aimed squarely at governing coding agents like Claude Code. Audit events stream to SIEMs (Splunk, Datadog). Standards posture is a differentiator: they claim the first production implementation of OAuth 2.1 Client ID Metadata Documents in MCP, and contribute to WIMSE and OAuth extensions. Identity plumbing plugs into existing infra (Okta SSO, SPIFFE, Kubernetes service accounts, mTLS). SOC 2 Type II certified.

In May 2026 they launched Keycard for Multi-Agent Apps (early access): delegated, session-based access across systems of agents, with permissions narrowed at each agent-to-agent handoff so no downstream agent inherits more access than its task requires.

## Founders & origins

Verified across company site and press: **Ian Livingstone** (CEO; former Snyk CTO — he and Creager helped scale Snyk from $30M to $300M ARR), **Matthew Creager** (Product/GTM; built Snyk's developer platform), and **Jared Hanson** (creator of Passport.js, former Auth0 Chief Architect through the Okta acquisition). The origin story is essentially "the Passport.js/Auth0 identity brain plus Snyk developer-security operators, applied to agents." In February 2026 Keycard acquired **Anchor.dev** (automated certificate issuance; team ex-Cloudflare/GitHub/Heroku, led by Wesley Beary) to extend governance to coding agents; terms undisclosed (Verified — GlobeNewswire).

## Funding

- **$8M Inception/seed**, co-led by Andreessen Horowitz and boldstart ventures (Verified).
- **$30M Series A**, led by Acrew Capital, with Essence Ventures, Exceptional Capital, Mantis VC, Modern Technical Fund, Tapestry Ventures, Vermillion Cliffs Ventures (Verified).
- **Total: $38M**, announced together at the October 2025 stealth exit. Angels include security/identity leaders from Auth0, Okta, Cloudflare, and Anthropic (Reported — company site).

## Evidence of real-world use

Thin so far — this is a very young company. As of 2026-07-02, no named customers or case studies in public sources; the product is in **early access with design partners**, and the multi-agent product launched in early access May 2026. No public pricing page. Positive signals: an independent developer walkthrough on DEV Community (building an authorized planning agent with MCP + Keycard), a WorkOS competitive teardown (competitors write comparison pages when you matter), the Anchor.dev acquisition, and real standards-body participation. Treat adoption claims as unproven; treat the team and protocol work as real.

## Relevance to agentic AI engineering

This is the identity/authorization layer of the agent stack — the enforcement mechanism between an agent's decision and its execution. It directly operationalizes the concerns in **Governance by Construction for Generalist Agents**, **ClawLess: A Security Model of AI Agents**, and **CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents** (system-level control rather than prompt-level trust). Scoped multi-tool access maps to **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**; the `keycard run` coding-agent governance story is the missing-infrastructure counterpart to long-horizon agentic SWE benchmarks like **SWE-EVO** and **SlopCodeBench** — the longer agents run unattended, the more credential scoping and audit matter.

## Use cases & considerations

Use cases: (1) OAuth for a custom MCP server so every tool call is tied to a verified user and logged; (2) governing coding agents' shell/API/secret access via `keycard run`; (3) department-scoped rollout of agent tooling with SIEM-integrated audit; (4) multi-agent delegation with per-handoff permission narrowing.

Considerations: early-access product, no public pricing, no named customers — expect design-partner dynamics. Central credential broker = availability and lock-in questions, partially mitigated by their standards-first posture. Competitors: WorkOS, Okta/Auth0 (Auth for GenAI), Arcade.dev, Astrix Security, Token Security, plus DIY OAuth. Open question: does agent IAM become a standalone category or a feature of Okta/WorkOS?

## Sources

- https://www.keycard.ai/
- https://www.keycard.ai/about/
- https://www.keycard.ai/announcement
- https://docs.keycard.ai/
- https://www.upstartsmedia.com/p/this-startup-raised-38m-to-secure
- https://www.securityweek.com/keycard-emerges-from-stealth-mode-with-38-million-in-funding/
- https://www.helpnetsecurity.com/2025/10/22/keycard-ai-agents-identity-access-platform/
- https://boldstart.vc/news/keycard-solving-the-ai-agent-identity-and-access-problem-welcome-to-boldstart/
- https://a16z.com/announcement/investing-in-keycard/
- https://www.globenewswire.com/news-release/2026/02/10/3235663/0/en/Keycard-Acquires-Anchor-dev-to-Unlock-Autonomous-Coding-Agents.html
- https://www.manilatimes.net/2026/05/15/tmt-newswire/globenewswire/keycard-launches-identity-and-access-for-multi-agent-apps/2344307
- https://workos.com/blog/keycard-vs-workos-agent-credentials-enterprise-authentication
- https://dev.to/kimmaida/i-built-a-secure-planning-agent-with-mcp-and-keycard-324a/comments
