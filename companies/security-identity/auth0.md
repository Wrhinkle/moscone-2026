# Auth0

> Developer-first customer identity platform (login, SSO, tokens) — now owned by Okta and repositioning as the identity layer for AI agents via Token Vault, async human-approval flows, and fine-grained authorization for RAG.

- **Category:** security-identity
- **AIEWF 2026 tier:** silver
- **Founded:** 2013, Bellevue/Seattle WA (founders split between Seattle and Buenos Aires) — Verified
- **Website / GitHub:** [auth0.com](https://auth0.com) / [github.com/auth0](https://github.com/auth0) (incl. [auth0-mcp-server](https://github.com/auth0/auth0-mcp-server))

## What they do

Auth0 is the "don't build your own login" company: a hosted customer identity and access management (CIAM) platform that gives applications authentication (username/password, social, passwordless, passkeys), enterprise SSO (SAML/OIDC), MFA, and token issuance via SDKs and a hosted Universal Login page. You integrate it as an OAuth 2.0/OIDC authorization server; it issues the ID/access/refresh tokens your app and APIs consume. Acquired by Okta in May 2021, it operates as Okta's customer-identity product line (vs. Okta's workforce identity).

The AIEWF-relevant story is **Auth0 for AI Agents** (launched as "Auth for GenAI" in developer preview April 2025, GA announced late 2025/2026). Components, in engineer terms:

- **Token Vault** — a managed store for third-party OAuth tokens (Google, GitHub, Slack, etc.) that an agent uses on a user's behalf. The agent never holds refresh tokens; it requests short-lived access tokens per task, and the vault handles refresh. This is the piece most agent frameworks currently fake with env vars.
- **Asynchronous authorization** — CIBA-based human-in-the-loop approval, so a long-running agent can pause on a sensitive action ("wire this payment?") and push an approval request to the user out-of-band.
- **Fine-Grained Authorization (FGA)** — a ReBAC engine (Google Zanzibar-style, from the OpenFGA project Auth0/Okta open-sourced) used to filter RAG retrieval so an agent only surfaces documents the requesting user can actually see.
- **Auth for MCP + agent identity** — OAuth for MCP servers (GA May 2026 per Okta's newsroom), per-agent identities, on-behalf-of token exchange, and Cross App Access (XAA), Okta's proposed OAuth extension for agent-to-app communication (early access ~July 2026 — Reported).

## Founders & origins

Eugenio Pace (CEO) and Matias Woloski (CTO), both Argentine — Verified. Pace spent ~12 years at Microsoft (patterns & practices, where he literally co-wrote Microsoft's developer-identity guidance); Woloski ran engineering at consultancy Southworks. They built Auth0 in 2013 as a remote collaboration between Seattle and Buenos Aires. Pace led the Auth0 unit inside Okta post-acquisition; Woloski departed June 2024 — Verified.

## Funding

- Total raised: >$330M pre-acquisition — Verified.
- Series F: $120M, July 2020, led by Salesforce Ventures with Bessemer, Sapphire, Meritech, Trinity, Telstra Ventures, DTCP; valuation $1.92B — Verified.
- Bessemer participated Series A–F, holding ~20% — Reported (Business Insider).
- Acquired by Okta for ~$6.5B in an all-stock deal, announced March 2021, closed May 2021 — Verified. Okta (NASDAQ: OKTA) is public, so Auth0 no longer raises independently.

## Evidence of real-world use

Strong and long-standing: ~10,000 customers in 70+ countries at acquisition — Verified. Documented case studies (auth0.com/customers, corroborated by third-party lists): Signify/Philips Hue, NHS Leadership Academy (identity across 200+ trusts), Dunelm, Abbott, CVS Health; customer lists also cite EY, British Airways, Polaris — Reported per name. Public self-serve pricing with a real free tier = genuine commercial product. The agent story is newer: an Amazon Bedrock AgentCore integration guide, hackathon projects on Devpost using Token Vault, and Okta press on the XAA partner ecosystem — early but concrete developer traction rather than pure marketing.

## Relevance to agentic AI engineering

This is directly the tool-use/governance layer of the agent stack: scoped, auditable, revocable credentials for agents calling external APIs and MCP servers. It's an infrastructure counterpart to this repo's governance papers — *Governance by Construction for Generalist Agents*, *ClawLess: A Security Model of AI Agents*, and *CaMeLs Can Use Computers Too* all argue for system-level enforcement outside the model, which is exactly what Token Vault + async CIBA approval implement. Multi-tool orchestration surveyed in *The Evolution of Tool Use in LLM Agents* assumes credential plumbing like this. FGA-filtered retrieval connects to the retrieval-permissions questions in the memory/RAG cluster (e.g., *Do Agents Need Semantic Metadata?*).

## Use cases & considerations

Use cases: (1) an agent that reads/sends email or files on a user's behalf without storing raw refresh tokens; (2) human-approval gates for high-stakes agent actions (payments, contract sends) — relevant to any back-office agent; (3) permission-aware RAG over multi-tenant documents via FGA; (4) securing a public-facing MCP server with real OAuth.

Considerations: vendor lock-in to Okta's ecosystem; Auth0 pricing historically gets expensive at MAU scale, and AI-agent feature pricing is not yet clearly published; XAA is a vendor-led proposed standard, not yet broadly adopted. Competitors: WorkOS (also profiled in this repo, chasing the same agent-auth niche), Clerk, Stytch, Descope, AWS Cognito, Keycloak/Ory (OSS). Open question: whether agent identity standardizes on XAA or on neutral MCP-spec auth.

## Sources

- https://www.geekwire.com/2021/auth0-ceo-eugenio-pace-6-5-billion-deal-okta-advice-entrepreneurs/
- https://auth0.com/blog/okta-acquisition-announcement/
- https://auth0.com/blog/auth0-announces-120m-seriesf-funding/
- https://www.geekwire.com/2021/okta-pay-6-5b-acquire-seattles-auth0-identity-tech-startup-valued-1-9b-last-year/
- https://auth0.com/ai and https://auth0.com/ai/docs/intro/overview
- https://auth0.com/blog/introducing-auth0-for-ai-agents/
- https://auth0.com/blog/auth0-for-ai-agents-generally-available/
- https://auth0.com/features/token-vault
- https://www.okta.com/newsroom/articles/auth0-may-2026-product-innovations/
- https://www.okta.com/newsroom/press-releases/okta-announces-cross-app-access-partners/
- https://github.com/auth0/auth0-mcp-server
- https://auth0.com/customers and https://auth0.com/case-studies/signify
- https://auth0.com/blog/securing-amazon-bedrock-agentcore-agents-auth0-for-ai-agents/
- https://www.appsruntheworld.com/customers-database/products/view/auth0-authentication
