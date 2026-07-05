# Tailscale

> Zero-config mesh VPN built on WireGuard that gives every machine (and increasingly every AI agent) a stable identity-bound address on a private network — now extending into identity-linked governance of AI/agent traffic with Aperture.

- **Category:** security-identity
- **AIEWF 2026 tier:** silver
- **Founded:** 2019, Toronto, Canada (Verified — Wikipedia, Tracxn, BetaKit)
- **Website / GitHub:** https://tailscale.com · https://github.com/tailscale/tailscale (~22k stars)

## What they do

Tailscale is a mesh overlay network ("tailnet") built on **WireGuard**. Each device runs a client that registers with Tailscale's coordination server, authenticates via your existing identity provider (Google, Okta, Entra, GitHub), and then talks **peer-to-peer with end-to-end WireGuard encryption** — NAT traversal is automatic, with DERP relays as fallback when direct paths fail. The practical effect: every laptop, server, container, or GPU box gets a stable private IP and DNS name (MagicDNS) reachable from anywhere with no port forwarding, firewall holes, or VPN concentrator.

On top of the mesh: **ACL "grants"** (policy-as-code tying access to user/device identity), **Tailscale SSH** (SSH auth via tailnet identity instead of key sprawl), **Funnel/Serve** (expose local services publicly or tailnet-only), a **Kubernetes operator**, and **tsnet**, a Go library that embeds a Tailscale node directly inside your application process — useful for making a service or agent addressable without touching the host network. The client daemon, CLI, and DERP relay code are open source; the GUI apps and control plane are proprietary. The third-party open-source control server **Headscale** (~27–30k stars) is tolerated and even supported by Tailscale employees — an unusual posture that has earned significant community goodwill.

The 2026 push is **Aperture**, an AI gateway in private alpha since January 27, 2026: it routes coding-agent and LLM traffic (Claude Code, Codex, Gemini CLI; OpenAI-compatible and self-hosted endpoints) through an identity-aware gateway, so orgs get per-user/per-machine attribution of API usage, token metrics, MCP and local tool-call logging, S3/SIEM export, and no API-key distribution. Expansion into chat, MCP/API connectors, and sandboxes was announced February 2026 (SiliconANGLE), plus a partnership with AI-security firm Highflame (April 2026) for real-time evaluation of agent traffic at the network layer.

## Founders & origins

**Avery Pennarun** (CEO), **David Crawshaw**, and **David Carney**, all ex-Google, founded the company in 2019 (Verified). **Brad Fitzpatrick** (LiveJournal/memcached creator, Go team at Google) is listed as a co-founder by Wikipedia but is more commonly described as the famous first engineering hire (Reported — sources disagree on the label). Origin: Pennarun's "New Internet" thesis — that networking should be identity-based and human-scale rather than perimeter-based; he'd previously sold a college startup to IBM and worked on Google Fiber.

## Funding

- **Seed:** Heavybit and Uncork Capital (Verified as participants; amount not found in public sources).
- **Series A:** $12M, Nov 2020, led by Accel (Verified).
- **Series B:** $100M USD, May 2022, led by CRV and Insight Partners; ~$1B valuation (Verified).
- **Series C:** $160M USD (C$230M), April 2025, led by Accel with CRV, Insight, Heavybit, Uncork; angels incl. George Kurtz (CrowdStrike CEO) and Anthony Casalena (Squarespace). **$1.5B valuation** (Verified — BetaKit, Yahoo Finance, Tracxn).
- **Total raised:** ~$275M (Verified — Tracxn/Crunchbase).

## Evidence of real-world use

Strong and unusually well documented:

- **10,000 paid business customers as of Jan 2025**, doubled from 5,000 in ~10 months, 100%+ YoY growth, 500k+ weekly active users (Verified — BetaKit interview with Pennarun).
- Named case studies on tailscale.com/customers: **Instacart, Mercury, Duolingo, Hugging Face, Cribl, Patreon, Chainalysis**; press adds **Mistral, Cohere, Revolut, Airbus**. Pennarun's framing: "the network that powers AI" — AI labs use tailnets to reach scattered GPU capacity across clouds (Verified customers; the AI-lab usage pattern Reported via BetaKit).
- Massive homelab/self-hoster community (r/Tailscale, HN threads); public free tier (3 users/100 devices) and self-serve pricing page.
- Aperture is alpha — real-world Aperture usage is **Unverified** at this date.

## Relevance to agentic AI engineering

Tailscale is becoming the **network + identity substrate under agent infrastructure**: Aperture answers "which human/machine identity is behind this LLM call or MCP tool invocation, and what did it do" — the enforcement/audit layer that this repo's **tool-use/governance** thread (τ-bench-style policy-compliance evaluation) presumes exists. For the **agentic SWE** thread, the coding agents benchmarked on SWE-bench (Claude Code, Codex) are exactly the workloads Aperture governs, including inside CI sandboxes like GitHub Actions without public exposure. tsnet is also a clean way to give a long-running agent a private, identity-bound network presence for reaching internal tools. Not relevant to agent-memory or voice-agent papers except as transport.

## Use cases & considerations

1. Connect dev machines to scattered GPU boxes across neoclouds/on-prem with zero firewall work.
2. Give self-hosted MCP servers and internal tools tailnet-only exposure instead of public endpoints + API keys.
3. Pilot Aperture for org-wide visibility into coding-agent/LLM/MCP usage tied to SSO identity.
4. Embed tsnet in an agent service so it can reach internal systems under device-level ACLs.

**Considerations:** control plane is proprietary SaaS (Headscale mitigates but is unofficial); Aperture is experimental alpha, not production-proven; relay throughput can bottleneck when NAT traversal fails. Competitors: NetBird, ZeroTier, Twingate, Cloudflare (WARP/Zero Trust and its own AI gateway), plain WireGuard. Open question: whether Aperture wins the AI-gateway slot against LiteLLM/Portkey/Cloudflare AI Gateway, which attack it from the LLM-proxy side rather than the network side.

*Confidence statements as of 2026-07-02.*

## Sources

- https://en.wikipedia.org/wiki/Tailscale
- https://tailscale.com/company
- https://tailscale.com/customers
- https://tailscale.com/opensource
- https://tailscale.com/blog/aperture-private-alpha
- https://tailscale.com/use-cases/securing-ai
- https://tailscale.com/blog/agents-are-coming
- https://github.com/tailscale/tailscale
- https://github.com/juanfont/headscale
- https://betakit.com/tailscale-hits-10000-paid-business-clients-after-doubling-customer-base-in-past-10-months/
- https://betakit.com/corporate-vpn-startup-tailscale-secures-230-million-cad-series-c-on-back-of-surprising-growth/
- https://finance.yahoo.com/news/tailscale-rakes-160m-series-c-113113825.html
- https://tracxn.com/d/companies/tailscale/__HoO0OVaODdbZEsDLJ7_OTsp344lrcNrb7eGx_aw5Lrk
- https://siliconangle.com/2026/02/17/secure-networking-startup-tailscale-launches-identity-linked-governance-ai-tools-agents/
- https://www.businesswire.com/news/home/20260403439638/en/Highflame-and-Tailscale-Partner-to-Secure-AI-Agents-and-Model-MCP-Interactions-at-the-Network-Layer
- https://thenewstack.io/tailscale-aperture-ai-agent-infrastructure/
