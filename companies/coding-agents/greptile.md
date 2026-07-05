# Greptile

> AI code review agent that indexes your whole repository — not just the diff — and reviews every PR against full-codebase context.

- **Category:** coding-agents
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, San Francisco (YC W24) — Verified (YC directory, press)
- **Website / GitHub:** https://www.greptile.com · https://docs.greptile.com

## What they do

Greptile sells one thing: an AI code review agent for GitHub and GitLab. The differentiator is context strategy — before reviewing anything, it builds a graph index of the repository (files, functions, dependencies and their interconnections), then fans parallel agents out over a pull request to judge both the diff and its blast radius across the codebase. That's the pitch versus diff-only reviewers: cross-file logic bugs, security issues, and regressions that a reviewer staring at the patch can't see.

The current generation, **Greptile v3** (shipped with the Series A, Sept 2025), is a rewrite toward a more agentic architecture with a memory loop: it learns team standards by reading engineers' own PR comments over time, auto-ingests rule files like `CLAUDE.md` and `.cursorrules`, accepts custom rules in plain English, and pulls context from Jira/Notion. Notably, it's built to sit *inside* agentic workflows, not just human ones — an MCP server exposes review comments and team rules to coding agents/IDEs, PR comments ship with copy-paste prompts (with codebase context) for a coding agent to apply the fix, and there's a Claude Code plugin plus a `/greploop` iterative fix loop. A beta product, **TREX**, autonomously generates and runs tests in a sandbox. Company claims: v3 catches ~3x more critical bugs than v2; ~90% cache hit rates keep review costs down (Reported — vendor).

Commercially it's a real, publicly priced product: $30/seat/month with 50 review credits per seat ($1/extra credit), free for open source, discounts for pre-Series A startups. Enterprise: self-hosted/on-prem and air-gapped VPC deployment, SOC 2 Type II, HIPAA, GDPR, SSO/audit logs (Verified — pricing and enterprise pages).

## Founders & origins

Three Georgia Tech alumni, founded 2023 (Verified — YC, Georgia Tech news):

- **Daksh Gupta (CEO)** — Georgia Tech CS, ex-Amazon intern; the public face (and author of a famously blunt viral "no work-life balance" hiring tweet, Nov 2024 — Reported).
- **Soohoon Choi (CTO)** — Georgia Tech.
- **Vaishant Kameswaran** — Georgia Tech CS + linguistics.

Origin: started as a "chat with your codebase"/codebase-understanding API in YC W24, then converged on PR review as the wedge once full-codebase context proved most valuable there. ~35 employees, San Francisco (Reported — YC directory).

## Funding

- **Seed, June 2024:** $4.1M led by Initialized Capital, with angels incl. Rich Aberman (WePay) (Verified — company blog, FinSMEs).
- **Series A, Sept 2025:** $25M led by Benchmark (Eric Vishria joined the board), with Cory Levy, YC, Initialized (Verified — company blog, multiple press). Valuation ~$180M (Reported — TechCrunch, citing sources during the raise).
- **Total raised:** ~$30M (Verified).

## Evidence of real-world use

Strong for a company this size, and much of it is independently sourced:

- **Named customers:** Brex, NVIDIA, Coinbase, Substack, PostHog, Klaviyo, Retool, Zapier, Joby, Bilt, and YC's internal software team (Verified across company pages + press). Homepage claims "9,000+ teams"; the enterprise page says 2,000+ organizations — inconsistent, treat both as vendor figures (Reported).
- **Brex case study:** 500+ PRs reviewed daily, 30% faster merges, with a named principal engineer quote about signal-to-noise winning over skeptical reviewers (Reported — vendor case study, but named and specific).
- **Scale claims at Series A:** 500M+ lines of code reviewed and 180K+ bugs prevented in a single month; ~700K PRs/month (Reported — company blog).
- **Anthropic published a Claude API customer case study on Greptile** — an independent signal that Greptile runs meaningful inference volume (Verified — claude.com/customers/greptile).

## Relevance to agentic AI engineering

Greptile is the verification layer of the agentic SDLC: as code generation moves to agents, review becomes the bottleneck, and Greptile is positioned as the automated gate that also *feeds context back* to the generating agents (MCP server, copyable fix prompts). It maps directly onto this repo's agentic-SWE benchmark thread — *SlopCodeBench* and *SWE-EVO* (long-horizon degradation is exactly what a persistent reviewer counteracts), *ProdCodeBench* (production-derived quality vs. benchmark quality), and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* (their thesis that "good code" is org-contextual). The v3 comment-learning loop is applied agent memory in the spirit of *Memory for Autonomous LLM Agents* and *Graph-based Agent Memory*; the parallel-reviewer architecture echoes *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*; the review-as-policy-gate role connects to *Governance by Construction for Generalist Agents*.

## Use cases & considerations

Use cases: (1) automated PR gate for teams absorbing high volumes of agent-generated code; (2) encoding tribal knowledge/standards as plain-English rules enforced on every PR; (3) closing the loop with coding agents — Greptile findings piped back via MCP for automatic fixes; (4) air-gapped review in regulated environments.

Considerations: nearly all metrics are vendor-published; the 9,000-teams vs. 2,000-orgs discrepancy is a reminder to verify. Crowded, fast-moving category — direct competitors: CodeRabbit, Qodo, Graphite (Diamond), Cursor Bugbot, GitHub Copilot code review, and native review in Claude Code. No open-source escape hatch (unlike Qodo's PR-Agent lineage), so it's a pure SaaS/self-host commercial bet. Open question: whether standalone review survives as a layer or gets absorbed into generation platforms that review their own output. As of 2026-07-02, no down-round or churn signals in public sources.

## Sources

- https://www.greptile.com/ (product, pricing, customers)
- https://www.greptile.com/enterprise
- https://www.greptile.com/blog/series-a
- https://www.greptile.com/blog/seed
- https://www.greptile.com/blog/greptile-v3-agentic-code-review
- https://www.greptile.com/customers/brex
- https://www.ycombinator.com/companies/greptile
- https://techcrunch.com/2025/07/18/benchmark-in-talks-to-lead-series-a-for-greptile-valuing-ai-code-reviewer-at-180m-sources-say/
- https://www.finsmes.com/2024/06/greptile-raises-4-1m-in-seed-funding.html
- https://www.thesaasnews.com/news/greptile-raises-25-million-series-a
- https://claude.com/customers/greptile
- https://www.gatech.edu/news/2026/01/05/y-combinator-backing-and-30m-investment-take-startup-greptile-next-level
