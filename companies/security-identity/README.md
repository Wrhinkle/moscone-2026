# Security & Identity

Auth/SSO/SCIM/identity, secrets management, security scanning, network access, agent permissions and audit.

This category exists because agents broke the assumption underneath every existing security product: that the actor behind a credential is a human who can be trusted to hold it. An agent with a pasted OAuth token in an env var inherits its user's *entire* permission set for an *unbounded* time, executes non-deterministically, and leaves no usable audit trail — and the March 2025 MCP spec change (mandatory OAuth for remote MCP servers) turned that from a hygiene concern into a compliance gate. Every company in this folder is converging on the same answer from a different starting point: scoped, short-lived, delegated, logged access for non-human actors. The incumbents (Auth0/Okta, 1Password, Snyk, Tailscale) are retrofitting agent identity onto human-identity or dev-security platforms; the dev-first challengers (WorkOS, Descope) are land-grabbing MCP auth from the CIAM side; and a wave of agent-native startups (Keycard, Runlayer, Scalekit) is betting the whole company that agent IAM is a new category, not a feature.

## How to read this category

Start with **WorkOS** ([workos.md](workos.md)) — platinum sponsor, $2B valuation, and the clearest picture of what "identity layer for agents" means commercially (OAuth 2.1 for MCP servers, with Cursor and OpenAI as named customers). Then read **Keycard** ([keycard.md](keycard.md)) and **Runlayer** ([runlayer.md](runlayer.md)) as a pair: they are the two purest agent-native bets, and they split the problem cleanly — Keycard is the *credential issuer* (composite identity, task-scoped short-lived tokens), Runlayer is the *runtime gateway* (MCP registry, scanning, traffic inspection). Almost everything else in the folder can be placed on two axes those three define:

- **Incumbent retrofit vs. agent-native build:** Auth0, 1Password, Snyk, and Tailscale are extending mature platforms (Token Vault, Unified Access, Evo ADS, Aperture respectively); WorkOS, Descope, Scalekit, Keycard, and Runlayer built for the agent era.
- **Identity/credentials vs. code/traffic:** WorkOS, Auth0, Descope, Scalekit, Keycard, and 1Password answer "who is this agent and what may it touch"; Snyk and Aikido scan what agents *write* and *install*; Tailscale and Runlayer govern what agents *send over the wire*.

**Inth** ([inth.md](inth.md)) is the outlier — privacy/consent governance rather than IAM — filed here because its "agent-written code that moves user data" thesis is audit-and-permissions-shaped, but its own profile flags the placement as imprecise.

## Profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [WorkOS](workos.md) | Drop-in enterprise-readiness APIs (SSO, SCIM, RBAC) now acting as OAuth 2.1 server for MCP | Platinum | ~$195–200M raised; $100M Series C (Mar 2026) at $2B | Cursor migrated off Auth0 to WorkOS; OpenAI is a named SSO customer |
| [Snyk](snyk.md) | Dev-first scanning (SCA/SAST/container/IaC) repositioning as the enforcement layer for AI coding agents | Gold | ~$1.3–1.6B raised; $7.4B down round Dec 2022, IPO still unfiled | Acquired Invariant Labs, the team behind the original MCP tool-poisoning research and `mcp-scan` |
| [Keycard](keycard.md) | IAM built specifically for agents: composite identity, task-scoped short-lived credentials, per-handoff narrowing | Gold | $38M ($8M a16z/boldstart + $30M Series A) at Oct 2025 stealth exit | Founders = Passport.js creator/Auth0 chief architect + Snyk's ex-CTO; no named customers yet |
| [Runlayer](runlayer.md) | Governed MCP gateway: registry of 18k+ scanned servers, IdP-scoped permissions, runtime traffic inspection | Gold | $42M (Khosla + Felicis) in under a year | Half of Gusto uses it daily; a Fortune 500 bank monitors 100k+ employees' AI activity through it (per Fortune) |
| [Auth0](auth0.md) | The "don't build your own login" CIAM platform, now shipping Token Vault + CIBA human-approval for agents | Silver | Acquired by Okta for ~$6.5B (2021); >$330M raised pre-acquisition | Its async-authorization flow lets a long-running agent pause and push "wire this payment?" to a human out-of-band |
| [1Password](1password.md) | Password/secrets manager pivoting to identity-and-access for humans *and* agents (Unified Access) | Silver | ~$920M raised; $6.2B valuation (2022 Series C) | Environments MCP Server delivers secrets into coding-agent sessions without putting them in the prompt |
| [Descope](descope.md) | Drag-and-drop CIAM from the Demisto team; Agentic Identity Hub makes your app its own OAuth 2.1 IdP for agents | Silver | $88M raised — all still labeled "seed," no priced Series A | Eight co-founders, all ex-Demisto (sold to Palo Alto for $560M) |
| [Tailscale](tailscale.md) | Zero-config WireGuard mesh giving every machine — and agent — an identity-bound private address; Aperture AI gateway in alpha | Silver | ~$275M raised; $1.5B valuation (Series C, Apr 2025) | 10,000 paid business customers, doubled in ~10 months; AI labs use tailnets to reach scattered GPU capacity |
| [Aikido](aikido.md) | All-in-one AppSec (10 scanner categories) with aggressive noise filtering and auto-fix PRs, aimed at AI-generated code | Silver | ~$85–95M raised; $1B valuation Jan 2026 — fastest EU cyber unicorn | Its researchers broke the chalk/debug npm compromise and tracked the Shai-Hulud worm before official advisories |
| [Scalekit](scalekit.md) | Auth stack for AI apps: MCP OAuth, delegated per-user agent identity, token vault with 100+ connectors | Bronze | $5.5M seed (Sep 2025, Together Fund + Z47) | Design choice: agents act as the specific user who triggered them, never as an org-wide service account |
| [Inth](inth.md) | YC-backed privacy/consent governance (DSARs, audit evidence) built on the open-source c15t consent SDK | Supporting | YC Spring 2026; no disclosed round | c15t claims 3M+ npm downloads with Zed, Infisical, and Expo as users — but it's GRC, not IAM |

Tier values are taken verbatim from each profile.

## Related papers

The **tool-use/governance** cluster is this category's research backbone — nearly every profile above cites one of these as the problem statement its product answers:

- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — argues permissions must be enforced structurally, before the call, not by model behavior. This is the thesis Keycard, Scalekit, and Auth0's Token Vault productize.
- [ClawLess: A Security Model of AI Agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md) — a security model for agents cited by the Keycard, Scalekit, and Auth0 profiles as the framing for system-level (not prompt-level) control.
- [CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) — system-level containment for computer-use agents; the delegation-chain audit logging in Scalekit and Keycard maps directly to it.
- [The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — multi-tool orchestration presumes exactly the credential plumbing WorkOS, Descope, and Scalekit sell.

Two adjacent clusters matter at the edges:

- [SWE-EVO](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md) and [SlopCodeBench](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) — the longer coding agents run unattended, the more credential scoping and audit matter (the Keycard `keycard run` and Snyk Evo ADS story).
- [Do Agents Need Semantic Metadata?](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md) — connects to permission-filtered retrieval (Auth0's FGA-gated RAG).

## Open questions

1. **Standalone category or absorbed feature?** Nearly every profile asks it: does agent IAM survive as its own product once Okta, the model providers, or the IdPs ship it natively? Keycard and Runlayer are pure-plays on "yes"; WorkOS and Auth0 are hedged bets on "no."
2. **Which spec wins?** MCP auth changed twice in 2025; Okta is pushing Cross App Access (XAA) as a vendor-led OAuth extension while Keycard bets on neutral standards (Client ID Metadata Documents, WIMSE, RFC 8693 token exchange). Whoever picks wrong rebuilds.
3. **Where does enforcement live** — credential issuance (Keycard, Auth0), the network (Tailscale Aperture, Runlayer), or inside the dev workflow (Snyk Evo ADS)? Enterprises will not buy all three layers from three vendors forever.
4. **Can scanning keep pace with agent-speed supply chains?** Aikido's Shai-Hulud reporting shows self-propagating npm malware iterating in weeks; agents that `npm install` autonomously are the ideal victim, and install-time blocking (Safe Chain) is still a bolt-on.
5. **Adoption proof is lopsided.** WorkOS, Tailscale, and Runlayer have documented usage; Keycard has zero named customers and Aperture is alpha. The gap between the category's funding ($400M+ across these companies in 18 months) and its verified production deployments is the thing to watch at AIEWF 2026.
