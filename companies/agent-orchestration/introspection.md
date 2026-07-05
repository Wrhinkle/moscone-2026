# Introspection

> Managed cloud infrastructure for running production AI agents defined as git-versioned "Pi recipes," with GitOps deploys, A/B testing, and per-tenant sandboxed isolation in the customer's own cloud.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** Not found in public sources (team described as having prior experience scaling agents at xAI, Superhuman, and Predibase — Reported, unattributed to named individuals)
- **Website / GitHub:** https://www.introspection.dev/

Disambiguation note: generic word "introspection" surfaces mostly unrelated software-engineering/philosophy content; anchored here to introspection.dev, the only AI-agent-infrastructure company by this name found.

## What they do
Introspection lets a team define an agent as a "Pi recipe" — a git folder of agents, tools, and skills, built on the open-source Pi coding-agent runtime (now stewarded by Earendil, Mario Zechner/Armin Ronacher's venture) — then deploy the exact same commit locally and to Introspection's managed cloud. Deployment is GitOps-style: commit-pinned, with PR previews and one-click rollback. Each run executes in a single-tenant, confidential-computing sandbox inside the customer's own cloud/VPC/region (not co-mingled across tenants), with credentials injected at the network edge so keys never enter the sandbox, and access gated by the customer's own identity provider. It supports orchestrator/worker multi-agent patterns, judge-based automatic evaluation, pattern detection, and statistically-significant A/B testing of agent variants against real traffic, with full tracing of turns/tool-calls/tokens/cost.

## Founders & funding
Not found in public sources — no named founders or funding round located on the site or in press coverage; team background (xAI/Superhuman/Predibase alumni) is reported but unattributed to specific people. Treat as Unverified for founders/funding specifically.

## Evidence of real-world use
No named customers found; the homepage shows a sample dashboard ("Hey there, Roland") suggesting a live product, and reference implementations cover customer-support triage, Sentry/incident-response auto-triage with fix PRs, and GTM/lead-qualification orchestration. No independent case studies, pricing page, or GitHub star count located — usage evidence is currently Unverified/company-sourced only.

## Relevance to agentic AI engineering
Directly in-category for agent orchestration: addresses the production-deployment gap between "agent works in a demo" and "agent runs safely, observably, and rollback-ably at scale" — commit-pinned deploys, sandboxing, and A/B eval are exactly the SDLC/observability concerns relevant to teams shipping multi-agent systems, and complementary to eval/observability tooling and MCP-based tool integration covered elsewhere in this repo.

## Sources
- https://www.introspection.dev/
- https://newsletter.pragmaticengineer.com/p/building-pi-and-what-makes-self-modifying
- https://pi.recipes/
