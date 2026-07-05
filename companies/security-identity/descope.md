# Descope

> Drag-and-drop customer identity (CIAM) platform from the Demisto founding team, now repositioning as the OAuth/identity layer for AI agents and MCP servers.

- **Category:** security-identity
- **AIEWF 2026 tier:** silver
- **Founded:** 2022, Los Altos, CA / Tel Aviv (Verified — TechCrunch, Forbes, company site)
- **Website / GitHub:** https://www.descope.com · https://github.com/descope (also https://www.descope.ai for the agentic product)

## What they do

Descope's core product is customer identity and access management: passwordless auth (passkeys, magic links, social login, OTP), MFA, SSO/SAML for B2B tenants, and RBAC, all wired together through a visual "Flows" builder — you design the auth journey in a drag-and-drop editor instead of writing session logic, then embed it via web components or call it through SDKs (Node, Python, Go, mobile, and more, all open source on GitHub). It's a hosted service in the Auth0/Stytch/Clerk mold; the differentiator is the no/low-code flow layer plus a genuinely usable free tier (7,500 MAU, 50 tenants, SSO included), with public pricing above that.

The 2025–2026 strategic bet is the **Agentic Identity Hub** (2.0 announced January 26, 2026), which packages three things engineers otherwise hand-roll: (1) **Inbound Apps** — your app becomes its own OAuth 2.1 identity provider so external agents (Claude, Cursor, custom agents) can authenticate and get scoped, user-consented tokens; (2) **Outbound Apps** — a managed credential vault with 50+ prebuilt OAuth connection templates (Gmail, Slack, GitHub, HubSpot, Snowflake…) so your agent can call third-party tools without you storing/refreshing tokens; (3) **MCP Auth SDKs/APIs** — Descope acts as the authorization server for remote MCP servers, handling OAuth 2.1, PKCE, dynamic client registration, and tool-level scope enforcement (`descope/descope-mcp` for Python, `descope/mcp-express` middleware for Node). Hub 2.0 added agents as first-class identities alongside human users, policy controls keyed on roles/JWT claims/tenants, and agent action audit logs streamable to SIEMs.

## Founders & origins

Eight co-founders, all ex-**Demisto** (SOAR platform acquired by Palo Alto Networks for $560M in 2019): **Slavik Markovich** (CEO), **Rishi Bhargava**, Gilad Shriki, Meir Wahnon, Dan Sarel, Aviad Lichtenstadt, Doron Sharon, and Guy Rinat (Verified — Forbes, Tracxn, Calcalist). The stated origin story: they kept rebuilding authentication at every prior company and decided identity was the "never-ending story" worth productizing. Founded April 2022, launched from stealth February 2023.

## Funding

- **$53M seed**, Feb 2023, led by Lightspeed Venture Partners and GGV Capital (now Notable Capital), with Dell Technologies Capital, Unusual Ventures, TechAviv, J Ventures, Cerca Partners, SVCI (Verified — TechCrunch, company PR).
- **$35M seed extension**, Sep 2025, existing investors only, led by Notable Capital and Lightspeed; earmarked for agentic-identity R&D (Verified — SecurityWeek, Calcalist, company PR).
- **Total raised: $88M** — unusually, all still labeled "seed"; no priced Series A disclosed. Valuation: not found in public sources.

## Evidence of real-world use

- Named customers with actual case studies: **Navan** (passwordless + risk-based MFA across web/mobile) and **CARS24** (SSO for dealers, Google Workspace enforcement) on Descope's customer pages; **GoFundMe, You.com, Branch** cited as customers (Reported — company site, so treat as vendor-claimed but specific).
- Company claims **1,000+ organizations** and, via a DevRev case study, **~300M daily participant sessions** (Reported — vendor and partner sources).
- Agentic Hub 2.0 launch included customer quotes from **WisdomAI** and **Cequence Security** using the MCP auth product specifically (Reported).
- Public pricing page, active G2 reviews, and a substantial open-source SDK footprint under github.com/descope — real commercial traction, though most usage evidence flows through Descope's own channels.

## Relevance to agentic AI engineering

Descope competes head-on with WorkOS (see `companies/security-identity/workos.md`) for the **identity/governance layer of the agent stack**: delegated authority, scoped tokens, consent, and audit for non-human actors. It maps to this repo's **tool-use/governance** thread — τ-bench-style policy compliance presumes exactly this enforcement layer, and Descope's tool-level OAuth scopes are the runtime complement to policy-following evals. The Outbound Apps credential vault is the missing piece for **agentic SWE and back-office agents** that must touch Gmail/GitHub/Snowflake with real user credentials rather than god-mode API keys. Marginal relevance to agent-memory and voice papers, though a voice agent acting on a caller's account needs the same delegated-auth primitives.

## Use cases & considerations

1. Add OAuth 2.1 auth to a remote MCP server in hours (mcp-express / Python SDK) instead of hand-rolling the spec.
2. Let ChatGPT/Claude connect to your SaaS app safely by making it an OAuth provider (Inbound Apps).
3. Give an internal back-office agent scoped, revocable access to Gmail/Slack/CRM via the token vault.
4. Standard CIAM for a new product with a generous free tier.

**Considerations:** hosted lock-in (flows, user store, token vault all live in Descope); eight founders and $88M of perpetual "seed" is an unusual structure worth watching; agentic identity is a land-grab with fast-moving specs (MCP auth changed twice in 2025). Competitors: WorkOS, Auth0/Okta (incl. Auth0 for AI Agents), Stytch, Clerk, Frontegg, Arcade.dev on the tool-auth side. Open question: whether standalone agent-identity survives once model providers and IdPs ship it natively.

## Sources

- https://techcrunch.com/2023/02/15/passwordless-authentication-startup-descope-lands-whopping-53m-seed-round/
- https://www.forbes.com/sites/brucerogers/2023/06/12/israeli-founder-team-creates-ciam-company-descope-with-53-million-seed-round/
- https://www.descope.com/press-release/agentic-identity-hub-2.0
- https://www.descope.com/press-release/seed-funding-advisory-board
- https://www.securityweek.com/descope-raises-35-million-in-seed-round-extension/
- https://www.calcalistech.com/ctechnews/article/hjh1ylknxe
- https://www.descope.com/customers (Navan, CARS24 stories)
- https://www.descope.com/pricing
- https://www.descope.com/use-cases/ai
- https://github.com/descope · https://github.com/descope/descope-mcp · https://github.com/descope/mcp-express
- https://devrev.ai/case-study/descope
- https://www.infoworld.com/article/4122386/descope-introduces-agentic-identity-hub-2-0-for-managing-ai-agents.html
- https://tracxn.com/d/companies/descope/__0utnwmPOyCyxjuZyhMlP0AjlE71LRDHbgEIBXpHI2eg
