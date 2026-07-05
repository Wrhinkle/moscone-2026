# GitHub

> The default home of the world's source code, now repositioning itself as the control plane where AI coding agents — its own Copilot and everyone else's — do their work.

- **Category:** coding-agents
- **AIEWF 2026 tier:** supporting
- **Founded:** February 2008, San Francisco (Verified). Microsoft subsidiary since 2018; folded into Microsoft's CoreAI division in 2025 (Verified).
- **Website / GitHub:** https://github.com · https://github.com/github (notably `github/github-mcp-server`)

## What they do

GitHub is the dominant code-hosting and collaboration platform: git repos, pull requests, issues, Actions (CI/CD), Packages, code search, and Advanced Security. Per Octoverse 2025 it hosts 630M+ repositories for 180M+ developers, with ~43M PRs merged per month — it is effectively the substrate of professional software work (Verified — GitHub Octoverse, Forbes coverage).

The AI layer is **GitHub Copilot**, which has evolved through three distinct shapes: (1) inline completions (2021–2023); (2) **agent mode** in VS Code (announced Feb 2025) — a synchronous agentic loop that edits across files, runs terminal commands, and self-corrects; and (3) the asynchronous **Copilot coding agent** (2025) — you assign it a GitHub issue, it spins up an ephemeral Actions-based environment, works autonomously, and opens a draft PR for human review. Copilot is model-plural (Anthropic, OpenAI, Google models selectable) and extensible via MCP; GitHub also ships a curated **MCP Registry** (Sept 2025) and its own open-source GitHub MCP server, which exposes repos/issues/PRs/Actions as tools to any MCP client — Claude, Cursor, Windsurf included (Verified — GitHub blog/docs).

The strategic bet is **Agent HQ** (GitHub Universe, Oct 2025): a "mission control" for orchestrating third-party coding agents — Anthropic, OpenAI, Google, Cognition, xAI — from GitHub, VS Code, CLI, and mobile under one Copilot subscription, with branch controls, agent-level identity, and audit surfaces. Translation for engineers: GitHub is trying to own the PR-review-and-governance choke point for agent-written code regardless of whose agent wrote it (Verified — Visual Studio Magazine, The New Stack).

## Founders & origins

Founded by **Chris Wanstrath, Tom Preston-Werner, and PJ Hyett**, with **Scott Chacon** commonly counted as a fourth cofounder (Verified). Started as a bootstrapped side project to make git hosting social ("social coding"). Preston-Werner left in 2014 following an internal investigation; Wanstrath was CEO through the Microsoft acquisition, succeeded by Nat Friedman (2018) and Thomas Dohmke (2021). **Dohmke announced his departure in Aug 2025; Microsoft chose not to appoint a new CEO — GitHub leadership now reports into CoreAI under Jay Parikh, with Julia Liuson overseeing revenue/engineering** (Verified — CNBC, GeekWire, Axios). That org change is the single most important recent fact: GitHub is less an autonomous company and more Microsoft's AI-developer-tools surface.

## Funding

- Bootstrapped 2008–2012 (Verified)
- **Series A, Jul 2012:** $100M, Andreessen Horowitz (Verified)
- **Series B, Jul 2015:** $250M led by Sequoia, ~$2B valuation (Verified)
- **Acquired by Microsoft, announced Jun 2018, closed Oct 2018: $7.5B in stock** (Verified)
- Total raised pre-acquisition: ~$350M (Verified)

## Evidence of real-world use

Usage evidence is overwhelming and among the best-documented in software: 180M+ developers, ~1B commits pushed in 2025 (Verified — Octoverse). Copilot: 20M cumulative users by Jul 2025 (Verified — Microsoft earnings coverage); ~4.7M paid subscribers by early 2026 and 90% of Fortune 100 usage (Reported — third-party stat roundups citing Microsoft figures); adopted by 50,000+ organizations (Reported). Octoverse claims 80% of new GitHub developers touch Copilot in week one (Reported — vendor). The famous "55% faster task completion" figure is GitHub's own controlled study — real research, but vendor-run. Public per-seat pricing (Free/Pro/Pro+/Business/Enterprise) confirms a mature commercial product.

## Relevance to agentic AI engineering

GitHub sits at three points of the agent stack simultaneously: **execution substrate** (issues→agent→PR is the canonical agentic-SWE loop that benchmarks like *SWE-EVO* and *SlopCodeBench* stress-test, and the review bottleneck it creates is exactly the concern in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering*); **tool provider** (the GitHub MCP server is arguably the most-used real-world tool surface in the patterns surveyed by *The Evolution of Tool Use in LLM Agents*); and **governance layer** (Agent HQ's branch controls, agent identity, and org-level MCP allowlists are a production implementation of the concerns in *Governance by Construction for Generalist Agents*). Multi-agent orchestration across vendors connects to *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*.

## Use cases & considerations

Use cases: (1) delegating scoped issues (bug fixes, test coverage, dependency bumps) to the Copilot coding agent with PR-gated review; (2) using the GitHub MCP server to give any agent (not just Copilot) governed repo/CI access; (3) Agent HQ as a multi-vendor agent evaluation harness on real work; (4) org-level MCP/agent policy enforcement for compliance.

Considerations: deep Microsoft entanglement — post-Dohmke, roadmap priorities are set by CoreAI, and Copilot economics favor Azure. Per-seat + premium-request pricing gets opaque at agent scale. Competitors: Cursor, Claude Code, Sourcegraph/Amp, Devin (Cognition), GitLab Duo — though GitHub's moat is hosting gravity, not model quality. Open question: whether "any agent" neutrality in Agent HQ survives competitive pressure with first-party Copilot.

## Sources

- https://github.blog/news-insights/octoverse/octoverse-a-new-developer-joins-github-every-second-as-ai-leads-typescript-to-1/
- https://www.forbes.com/sites/janakirammsv/2025/11/01/10-key-takeaways-from-github-octoverse-2025-report/
- https://github.com/newsroom/press-releases/agent-mode
- https://github.com/newsroom/press-releases/coding-agent-for-github-copilot
- https://docs.github.com/copilot/concepts/agents/coding-agent/about-coding-agent
- https://visualstudiomagazine.com/articles/2025/10/28/github-introduces-agent-hq-to-orchestrate-any-agent-any-way-you-work.aspx
- https://thenewstack.io/github-agent-hq/
- https://github.blog/ai-and-ml/github-copilot/meet-the-github-mcp-registry-the-fastest-way-to-discover-mcp-servers/
- https://docs.github.com/en/copilot/concepts/context/mcp
- https://www.cnbc.com/2025/08/11/microsofts-github-chief-is-leaving-competition-ramps-up-in-ai-coding.html
- https://www.geekwire.com/2025/github-will-join-microsofts-coreai-group-with-departure-of-ceo-thomas-dohmke/
- https://www.axios.com/2025/08/11/github-ceo-dohmke-step-down
- https://www.secondtalent.com/resources/github-copilot-statistics/
