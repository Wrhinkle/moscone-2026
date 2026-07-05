# WorkOS

> Drop-in APIs that make a B2B app "enterprise-ready" — SSO, SCIM, RBAC, audit logs, and increasingly OAuth/identity for AI agents and MCP servers — so dev teams don't build identity plumbing themselves.

- **Category:** security-identity
- **AIEWF 2026 tier:** platinum
- **Founded:** 2019, San Francisco (Verified — Contrary Research, Crunchbase/Tracxn)
- **Website / GitHub:** https://workos.com · https://github.com/workos (SDKs for Node, Python, Go, Ruby, .NET, etc.)

## What they do

WorkOS sells identity infrastructure as a set of APIs and hosted components. The core historical product is **Enterprise SSO**: one integration that normalizes SAML/OIDC across Okta, Entra ID, Google Workspace, and dozens of other IdPs, priced per enterprise connection ($125/connection/month with volume discounts). Alongside it: **Directory Sync (SCIM)** for user provisioning/deprovisioning, an **Admin Portal** (self-serve IdP setup UI you hand to your customer's IT admin), **Audit Logs**, and **RBAC**.

**AuthKit** is the newer full user-management layer — hosted login UI, sessions, MFA, magic links, bot protection — free up to 1M MAUs, which is an aggressive land-grab against Auth0/Clerk (Verified via workos.com/pricing). The portfolio has expanded into **Fine-Grained Authorization** (Zanzibar-style relationship-based permissions, from the Warrant acquisition), **Radar** (device fingerprinting / bot and fraud detection), and **Vault** (encryption key management / secrets storage, BYOK).

The 2025–2026 strategic push is agent identity: AuthKit acts as a spec-compliant **OAuth 2.1 authorization server for MCP servers** (Protected Resource Metadata discovery, Resource Indicators, PKCE), works with the official MCP SDKs, and lets an MCP tool inherit enterprise SSO. Reported (WorkOS blog + third-party writeups): 2026 additions include agent-facing CLI workflows and "Pipes MCP" session-scoped, time-bounded access to third-party data connections instead of standing OAuth grants.

## Founders & origins

**Michael Grinich**, founder & CEO (Verified). Previously co-founded Nylas (email APIs); before that a designer/engineer at Dropbox, MIT alum. Origin story (Verified — Contrary Research, Generalist): at Nylas he saw that scaling meant selling to enterprises, which meant building SSO, audit logs, and access control from scratch. He left, took a year off, and in 2019 started WorkOS to productize exactly that "enterprise-ready" checklist. No public co-founder is consistently named; sources describe Grinich as sole founder (Reported).

## Funding

- **Series A:** $15M led by solo capitalist Lachy Groom, with Lightspeed and Abstract (Verified; first funding activity dated Mar 2020 per Tracxn).
- **Series B:** $80M, June 2022, led by Greenoaks; simultaneous acquisition of Modulz (Radix UI) (Verified — WorkOS blog, TechCrunch, Fenwick).
- **Warrant acquisition** (fine-grained authorization), 2024 (Reported).
- **Series C:** $100M, announced March 2026, led by Meritech and Sapphire with Audacious, Craft, Abstract, Greenoaks participating; **$2B valuation** (Verified — WorkOS blog, multiple press). Stated purpose: securing agentic software.
- **Total raised:** ~$195–200M (computed from the above; Tracxn listed $99M before Series C).
- Reported (single source, Sacra-adjacent summaries): crossed $30M ARR and 1,000+ customers in 2025 — treat revenue figure as Reported, not Verified.

## Evidence of real-world use

Unusually strong, and documented beyond logos:

- **Cursor** migrated off Auth0 to WorkOS; founder Arvid Lunnemark cites faster logins and Auth0's "opaque pricing" (Verified — workos.com/customers case study).
- **OpenAI** uses WorkOS for enterprise SSO (Verified — named case study with an OpenAI enterprise GTM quote).
- **Vercel** (Guillermo Rauch quote; enterprise deals incl. The Washington Post), **Webflow** (SCIM on SSO), **Perplexity**, **PlanetScale**, **Indeed** (chose WorkOS over Auth0), plus Anthropic, Replit, Sierra, Baseten, Temporal, Gamma, Clay, Exa listed in the Series C announcement (customer-page quotes Verified; the longer Series C list is company-claimed, Reported).
- Public, self-serve pricing page and 1,000+ customers claim; independent reviews and comparison chatter (dev.to, HN) confirm active adoption among AI startups.

## Relevance to agentic AI engineering

WorkOS sits at the **identity/governance layer of the agent stack**: who is this agent acting for, what can it touch, and what's the audit trail. Concretely: OAuth 2.1 auth for MCP servers, scoped/time-bounded tokens for agent data access (Pipes), FGA for per-tool permission checks, and audit logs for agent actions. This maps directly to this repo's **tool-use/governance** research thread — policy-compliant agent behavior of the kind τ-bench measures presumes an enforcement layer like this — and to the **agentic SWE** thread, since the coding-agent companies benchmarked on SWE-bench (Cursor, Devin-class tools) are literally WorkOS customers needing enterprise SSO to sell. Less relevant to agent-memory and voice-agent papers, except that voice/support agents acting on user data need the same delegated-auth primitives.

## Use cases & considerations

1. Add enterprise SSO/SCIM to a B2B AI product in days to unblock an enterprise deal.
2. Stand up a remote MCP server with real OAuth 2.1 + enterprise SSO instead of hand-rolled API keys.
3. Replace Auth0/Clerk with AuthKit (free ≤1M MAU) plus FGA for per-resource agent permissions.

**Considerations:** per-connection SSO pricing ($125/mo/connection) gets expensive at high enterprise-customer counts; hosted-service lock-in (auth flows, user store) is real; FGA and Radar are newer and less battle-tested than core SSO. Competitors: Auth0/Okta, Clerk, Stytch, Frontegg, Descope, BetterAuth (OSS), and Cloudflare's MCP auth tooling. Open questions: how durable the MCP-auth moat is once IdPs ship native agent support; sole-founder key-person concentration.

*Confidence statements as of 2026-07-02.*

## Sources

- https://workos.com/customers
- https://workos.com/pricing
- https://workos.com/blog/series-b
- https://workos.com/blog/series-c
- https://workos.com/blog/mcp-2026-spec-agent-authentication
- https://workos.com/mcp
- https://research.contrary.com/company/workos
- https://techcrunch.com/2022/06/01/workos-raises-80m-to-add-enterprise-features-like-sso-to-apps/
- https://tracxn.com/d/companies/workos/__7gQxbtUfILNBDucMkVvZ1mOzLY5-T0nyreiU5xMI528
- https://www.fenwick.com/insights/experience/fenwick-represents-workos-in-80-million-series-b-financing-and-acquisition-of-modulz
- https://siliconangle.com/2026/03/03/jetstream-security-guild-ai-workos-land-fresh-funding-amid-growing-agentic-ai-infrastructure-push/
- https://www.generalist.com/p/workos
- https://sacra.com/c/workos/
