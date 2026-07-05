# Sourcegraph

> Enterprise code search and code intelligence platform — the "code graph" layer that grounds AI coding agents in very large, multi-repo codebases; its frontier coding agent Amp was spun out as a separate company in December 2025.

- **Category:** coding-agents
- **AIEWF 2026 tier:** gold
- **Founded:** 2013, San Francisco, by Stanford grads Quinn Slack and Beyang Liu (Verified — Wikipedia, Contrary Research)
- **Website / GitHub:** https://sourcegraph.com · https://github.com/sourcegraph (core repo taken private August 2024; formerly Apache-2.0, relicensed June 2023)

## What they do

Sourcegraph's core product is Code Search: a platform that indexes every repository, branch, and language across an organization (cloud or self-hosted) and builds a code graph — definitions, references, cross-repo dependencies — that you query via a web UI, API, or increasingly via agents. For an engineer, the buy is "grep across 100k repos with symbol-level precision," plus Batch Changes for executing large-scale automated changes across hundreds or thousands of repos.

Since 2025 the platform has pivoted from "AI assistant" (Cody) to "agentic code intelligence." Cody Free/Pro were discontinued in July 2025; the enterprise offering (from ~$59/user/mo) now centers on: **Deep Search**, an agentic loop where an AI agent uses Sourcegraph's search tools — including a file-finding subagent and a sandboxed scripting tool for programmatic aggregation across many searches — to answer natural-language questions about a codebase with citations; and **Agentic Batch Changes** (public beta June 30, 2026; self-hosted in Sourcegraph 7.5, July 8, 2026), which adds AI planning/orchestration on top of the Batch Changes execution engine for fleet-wide code migrations.

The big structural fact: on December 2, 2025, Sourcegraph split into two companies. **Sourcegraph** (new CEO Dan Adler) keeps the enterprise code search/intelligence business; **Amp Inc.** (led by founders Slack and Liu) takes Amp, the frontier coding agent (CLI + VS Code extension, multi-step agentic workflows, shared team threads, agentic code review), which launched 2025 with credit-based/pay-as-you-go pricing and has experimented with an ad-supported free tier. Both retain the same investors (Craft, Redpoint, Sequoia, Goldcrest, a16z). For AIEWF 2026 purposes, the gold-tier sponsor "Sourcegraph" is most likely the code-intelligence company, but expect Amp adjacency in any conversation.

## Founders & origins

- **Quinn Slack (CEO 2013–2025, now Amp):** self-taught programmer, Stanford, ex-Palantir (Verified).
- **Beyang Liu (CTO, now Amp):** Stanford, started at Google; inspiration partly from using Google Code Search as a Google intern (Verified).

They met at Palantir, where understanding an internal API often meant scheduling a meeting — Sourcegraph began in 2013 as a side project to make "code search like Google's" universal (Verified — Contrary Research, company about page).

## Funding

- **Series A, Oct 2017:** $20M — Goldcrest Capital, Redpoint (Verified)
- **Series B, Mar 2020:** $23M — Craft Ventures; +$5M extension Jul 2020, Felicis (Verified)
- **Series C, Dec 2020:** $50M — Sequoia (Verified)
- **Series D, Jul 2021:** $125M — Andreessen Horowitz, at a $2.625B valuation (Verified)
- **Total raised:** ~$223M (Verified; one 2025 source says $245M — Reported). No public raise since 2021; ~$50M ARR reported by Latka (Reported, single source).

## Evidence of real-world use

- Named customers across sources: Uber, Lyft, Dropbox, Yelp, Stripe, Canva; company claims trust of "AI research labs and the biggest global banks" (mix of Verified early adopters and Reported/vendor claims).
- Documented case study: Nine's platform engineering team — ~$276K/year saved, 1,200 hours annually, via Code Search + Batch Changes (Reported — vendor-published, treat numbers accordingly).
- Public pricing page and self-hosted enterprise deployment path = real commercial product; "250,000+ repositories served" (Reported).
- Caveat: the core product went closed-source (repo private since Aug 2024), so GitHub-star signals are stale; community goodwill took a hit in HN discussions of the relicensing (Reported).

## Relevance to agentic AI engineering

Sourcegraph is the retrieval/grounding layer for agentic SWE at enterprise scale: coding agents fail on big brownfield codebases without precise code context, which is exactly what the code graph provides. Deep Search is a production instance of the agentic-search-over-tools pattern (*The Evolution of Tool Use in LLM Agents*; *Agentic Search in the Wild*), and its subagent + sandboxed aggregation design is relevant to *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*. Agentic Batch Changes speaks directly to the long-horizon, multi-repo failure modes in *SWE-EVO* and *SlopCodeBench*, and to the brownfield thread (*One Developer Is All You Need*). Code-graph-as-context also parallels the graph-based agent memory work (*Graph-based Agent Memory: Taxonomy, Techniques, and Applications*).

## Use cases & considerations

Use cases: (1) grounding context for coding agents across huge multi-repo estates (code graph as the agent's retrieval tool); (2) fleet-wide migrations/refactors via (Agentic) Batch Changes; (3) natural-language codebase Q&A with citations for onboarding and incident archaeology; (4) self-hosted code intelligence for regulated/air-gapped orgs.

Considerations: enterprise-only posture post-July 2025 (no free/pro tier) and closed source mean real lock-in with no self-serve evaluation path for individuals. The Amp split leaves open questions about roadmap focus and where agent innovation accrues. Competitors: GitHub code search + Copilot, Glean (code), Cursor/Windsurf codebase indexing, Greptile, grep.app/open-source Zoekt-based stacks. Case-study metrics are vendor-sourced.

## Sources

- https://en.wikipedia.org/wiki/Sourcegraph
- https://research.contrary.com/company/sourcegraph
- https://sourcegraph.com/blog/why-sourcegraph-and-amp-are-becoming-independent-companies
- https://sourcegraph.com/blog/announcing-sourcegraphs-series-d-round
- https://sourcegraph.com/about
- https://sourcegraph.com/case-studies (incl. Nine case study)
- https://sourcegraph.com/docs/deep-search
- https://finance.yahoo.com/technology/ai/articles/sourcegraph-launches-agentic-batch-changes-140000070.html
- https://ampcode.com/
- https://tracxn.com/d/companies/sourcegraph/__VKOX0-AKdgV8MrEkAWvpxYcwQPfPjxyEjHJQ8TbiBCU
- https://getlatka.com/companies/sourcegraph
