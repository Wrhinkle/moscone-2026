# Scalekit

> Auth infrastructure for AI apps: OAuth for MCP servers, delegated identity for agents calling third-party tools, and enterprise SSO/SCIM for the humans behind them.

- **Category:** security-identity
- **AIEWF 2026 tier:** bronze
- **Founded:** 2023–2024 (sources conflict: Tracxn says 2023, funding press says 2024 — Reported, not fully reconciled). Incorporated in Delaware, US (Tracxn lists Lewes, DE); founding team is ex-Freshworks, suggesting significant India presence.
- **Website / GitHub:** [scalekit.com](https://www.scalekit.com/) / [github.com/scalekit-inc](https://github.com/scalekit-inc)

## What they do

Scalekit sells three layers of auth for B2B/AI products, all API-first with drop-in SDKs (Node, Python, Go, Java — MIT-licensed on GitHub):

1. **AgentKit** — the flagship agent-facing product. When your agent needs to act in Salesforce, Gmail, Jira, etc., Scalekit manages the OAuth flow per end-user, stores tokens in an AES-256 encrypted vault (the agent never sees raw credentials), validates scopes per tenant before each API call, and executes tool calls with pagination/rate-limit/retry handling. Everything is logged as a delegation chain (which user authorized, which agent acted, which tool, what scope, what result) exportable to SIEM. It ships 100+ pre-built connectors (marketed as reach into "3,000+ tools") with framework-agnostic tool schemas usable from LangChain, OpenAI, Anthropic, Vercel AI SDK, and Mastra. The key design choice: agents act as the *specific user who triggered them* (delegated identity inheriting SSO permissions), not as an org-wide service account.
2. **MCP Auth** — drop-in OAuth 2.1 authorization server for Model Context Protocol servers, addressing the March 2025 MCP spec change that mandated OAuth for remote MCP servers. Lets a team expose an MCP server that Claude Desktop/Cursor/VS Code users can hit with real authentication, backed by the customer's existing IdP (they publish an "SSO-backed MCP auth" pattern).
3. **Auth for SaaS** — conventional B2B auth: SAML/OIDC SSO, SCIM provisioning, RBAC, passwordless, org management. This is the original product; the agent stack was layered on top and went GA per their blog.

Pricing is public (real commercial product): free tier 5,000 tool calls/month; Growth at $99/month for 100k tool calls ($0.50/1k overage, custom connectors, EU residency +$99); Enterprise adds VPC/on-prem, 99.99% SLA, SIEM integrations. SOC 2, ISO 27001, HIPAA-ready; multi-region US/EU; claimed <50ms p95.

## Founders & origins

**Verified:** Satya Devarakonda (co-founder/CEO) and Ravi Madabhushi (co-founder), both ex-Freshworks. The team previously built Freshworks' in-house authentication platform (reported as serving 50k+ businesses / 2M users), and started Scalekit after seeing SaaS teams struggle with enterprise-ready identity. **Name-collision warning:** LinkedIn/press also surface a "Rishi Panchal, CEO of ScaleKit Funding" — that is an unrelated lending company, not this one.

## Funding

- **Seed, $5.5M, announced September 16, 2025** — co-led by **Together Fund** and **Z47** (formerly Matrix Partners India), with angels Adam Frankl, Oliver Jay, and Jagadeesh Kunda. **Verified** (Crunchbase, SecurityWeek, The SaaS News, Z47's own announcement, Yahoo Finance).
- Total raised: $5.5M (single round per Tracxn). No Series A found in public sources as of 2026-07-02.

## Evidence of real-world use

- **Named customers (Reported — homepage logos/testimonials):** Von, SiftHub, Napkin.ai. One testimonial describes agents acting across Salesforce, Gong, and Google Drive on behalf of customers; another mentions shipping "OpenClaw agents" on Scalekit's connectivity layer.
- **Public pricing with usage metering** — signals a functioning commercial product, not vaporware.
- **OSS surface:** ~66 repos under scalekit-inc (SDKs, developer docs, examples). Star counts not verified — likely modest; the SDKs are clients, not community projects.
- Heavy content marketing on MCP auth (xmcp integration guide, OAuth 2.1 quickstarts) suggests real developer funnel around MCP, the hot adoption vector.
- No large-brand documented case studies found; usage evidence is early-stage-credible but thin. **Unverified:** revenue, MAU scale.

## Relevance to agentic AI engineering

Scalekit sits at the **tool-calling and governance layer** of the agent stack — the "who is this agent acting as, and what is it allowed to touch" problem. It's a productized answer to the concerns in *Governance by Construction for Generalist Agents* (permissions enforced structurally, before the call, rather than by model behavior) and *ClawLess: A Security Model of AI Agents*; the audit/delegation-chain logging maps to *CaMeLs Can Use Computers Too*'s system-level security framing. Its multi-connector orchestration is the infrastructure counterpart to *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. For a back-office agent (e.g., a job-packet auditor touching email, Drive, and a CRM), this is the layer that replaces hand-rolled OAuth and shared service accounts.

## Use cases & considerations

**Use cases:** (1) ship a remote MCP server with real OAuth 2.1 instead of API keys; (2) customer-facing agent that acts in each customer's SaaS accounts with per-user tokens; (3) internal agents inheriting employee SSO permissions; (4) getting SSO/SCIM enterprise-ready for a B2B AI product without building SAML.

**Considerations:** direct competitors are **WorkOS** (also in this repo's security-identity set, far larger and also pushing agent/MCP auth), **Composio** (connector/tool-calling overlap), **Auth0/Okta**, **Arcade.dev**, and **Nango/Paragon** on integrations. Lock-in is real — token vault plus connector schemas sit in the critical path. Seed-stage vendor risk for an auth dependency deserves weight; the free tier and MIT SDKs make evaluation cheap. Open questions: connector depth vs. Composio, and whether "3,000+ tools" means first-class connectors or long-tail API proxying.

## Sources

- https://www.scalekit.com/
- https://www.scalekit.com/pricing
- https://www.scalekit.com/mcp-auth
- https://docs.scalekit.com/authenticate/mcp/quickstart/
- https://www.scalekit.com/blog/scalekit-auth-stack-for-ai-apps-is-now-ga
- https://github.com/scalekit-inc
- https://github.com/scalekit-inc/scalekit-sdk-python
- https://www.crunchbase.com/funding_round/scalekit-b744-seed--ddc058dd
- https://www.securityweek.com/scalekit-raises-5-5-million-to-secure-ai-agent-authentication/
- https://z47.com/news/scalekit-raises-5-5m-to-launch-authentication-stack-for-ai-agents
- https://www.thesaasnews.com/news/scalekit-raises-5-5-million-in-seed-round
- https://tracxn.com/d/companies/scalekit/__5NWX1_9LQVoxRsVxcnbUdMOp8kuh2vdhk1TxIFBXzwA
- https://www.together.fund/portfolio/scalekit
