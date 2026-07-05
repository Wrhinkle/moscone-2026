# Entire, Inc.

> A developer-platform startup, founded by GitHub's former CEO, building git-native provenance/audit infrastructure for AI-agent-generated code.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** supporting
- **Founded:** 2025/2026 launch, remote-first (Verified — TechCrunch, Bloomberg, GeekWire)
- **Website / GitHub:** https://entire.io/ ; open-source CLI "Checkpoints" (linked from site)

## What they do
Entire addresses a real pain point in agentic coding: coding agents lose context between sessions, and generated code carries no record of the prompts/decisions/tool calls that produced it. Their first product, **Checkpoints**, is a git-aware open-source CLI: on every agent-generated commit it writes a structured "checkpoint" object tied to the commit SHA, then pushes that metadata to a separate branch (`entire/checkpoints/v1`) as an append-only audit log alongside your normal git history. Architecturally they describe three layers: a git-compatible database unifying code/intent/constraints/reasoning, a "context graph" for multi-agent coordination, and an AI-native SDLC layer. Works with any git-based project, integrates into existing tooling rather than replacing it. Confirmed as the organizer of the "Agent Run" AIEWF 2026 side event (per event listings).

## Founders & origins
Founded/led by **Thomas Dohmke**, former CEO of GitHub (7 years at GitHub, 4 as CEO, ~10 years total at Microsoft) (Verified — Bloomberg, TechCrunch, GeekWire, Axios, all Feb 2026).

## Funding
$60M seed round at a $300M valuation — reported as the largest seed round in developer-tools history — led by Felicis, with Madrona, Microsoft's M12, Basis Set, 20VC, Cherry Ventures, Picus Capital, and Global Founders Capital; angel backers include Gergely Orosz, Theo Browne, Jerry Yang, Olivier Pomel, and Garry Tan (Verified — multiple outlets, Feb 2026).

## Evidence of real-world use
Checkpoints is open source and publicly available now (not just announced); ~15 employees scaling to 30+ engineers. Too new for third-party case studies, but the launch itself carries unusually strong credibility signals (founder pedigree, investor roster, immediate OSS release rather than vaporware).

## Relevance to agentic AI engineering
Directly targets the SDLC/agent-governance gap in this repo's focus areas: audit trails, reproducibility, and multi-agent coordination for coding agents — a core concern as teams adopt Devin/Cursor/Claude Code-style agents in production.

## Sources
- https://entire.io/company
- https://entire.io/news/former-github-ceo-thomas-dohmke-raises-60-million-seed-round
- https://techcrunch.com/2026/02/10/former-github-ceo-raises-record-60m-dev-tool-seed-round-at-300m-valuation/
- https://www.bloomberg.com/news/articles/2026-02-10/former-github-ceo-thomas-dohmke-raises-60-million-for-new-startup
- https://www.geekwire.com/2026/former-github-ceo-launches-new-developer-platform-with-huge-60m-seed-round/
- https://siliconangle.com/2026/02/10/entire-launches-60m-build-ai-focused-code-management-platform/
