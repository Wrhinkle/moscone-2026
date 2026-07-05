# HumanLayer

> Started as a human-approval API for AI agents; now sells CodeLayer, an IDE/collaboration platform for orchestrating fleets of coding agents (Claude Code, Codex) with humans reviewing at every phase.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, San Francisco (Verified — YC profile, Tracxn agree). YC Fall 2024 (F24) batch.
- **Website / GitHub:** https://www.humanlayer.dev · https://github.com/humanlayer/humanlayer · https://github.com/humanlayer/12-factor-agents

## What they do

HumanLayer v1 was an API + Python/TypeScript SDK that let any agent (framework-agnostic) pause and contact a human for approval or input over Slack, email, or SMS before executing high-stakes tool calls — born from Dex Horthy's own SQL-warehouse-cleanup agent that needed sign-off before dropping tables. That SDK-era code in the main GitHub repo is now explicitly marked deprecated by the maintainers.

The current product, **CodeLayer** (the humanlayer.dev product), is an AI IDE and team-collaboration layer for running many coding-agent sessions in parallel: local and cloud daemons manage sessions, multi-repo git worktrees isolate parallel work, and "Tasks" group sessions with versioned "Artifacts" (research docs, designs, plans) that teammates comment on before implementation. It codifies their **QRSPI workflow** (Questions → Research → Design → Structure → Plan → Implement) — an evolution of their open-source Research→Plan→Implement / "Advanced Context Engineering for Coding Agents" methodology. Notably BYOK: you plug in your own Claude Code/Codex/Copilot subscriptions or API keys; HumanLayer charges for the orchestration layer, not tokens. Public pricing: free for teams of ≤3 (200 sessions/mo), Pro $100/user/mo, Enterprise with SSO/audit logs/on-prem (Verified — pricing on their site, so a real commercial product).

Positioning is anti-slop: "ship 2-3x faster without AI slopping up your codebase" — the bet is that once multiple people ship AI-written code, the bottleneck is communication, review, and context management, not code generation.

## Founders & origins

**Dexter "Dex" Horthy**, solo founder/CEO (Verified — YC, Crunchbase/FounderTrace). Previously ~7 years at Replicated (Series C dev-tools startup, also in this repo under cloud-compute) as engineer, SE, PM, and executive on Kubernetes-native deployment for customers like HashiCorp, DataStax, H2O.ai; started coding at NASA JPL in high school (Reported — YC profile). Author of the viral **12-Factor Agents** guide (April 2025) and widely credited with coining the term **"context engineering"** (Reported across YC, Anthropic's blog, press). Team size listed as 2 as of the founding-engineer job posting.

## Funding

- **Pre-seed/convertible note, $500K, Oct 2024** — Y Combinator (Reported — Tracxn/Crunchbase).
- **">$3M total"** from YC, Pioneer Fund, and angels including Guillermo Rauch (Vercel CEO) and Paul Klein (Browserbase CEO) (Reported — HumanLayer's own YC job posting; no independent press confirmation found).
- No priced seed/Series A announcement found in public sources as of 2026-07-02. Total raised: ~$3M+ (Reported, company-stated).

## Evidence of real-world use

- **OSS pull:** humanlayer/humanlayer at ~11.1k stars / ~920 forks; 12-factor-agents near ~10k stars and a front-page HN staple (Verified — GitHub). Strong mindshare signal, though the starred SDK is the deprecated product.
- **Anthropic featured HumanLayer** in its "How three YC startups built their companies with Claude Code" post — independent editorial validation of the CodeLayer workflow (Verified).
- **Named customers on site:** Upstart, Casco, Osmosis, Ambral, Nautilus, SQDS, Weave, Ristto, Roadrunner (Reported — logos on landing page; only Upstart is a recognizable public company; no written case studies found).
- **Traction claims:** "MRR grew 100% last month," several large engineering-team pilots closed since Q4 2025 (Reported — company's own job posting/YC page; unaudited).
- Documented methodology result: a ~35k-line merged PR to BoundaryML's BAML Rust codebase produced via their ACE-FCA context-engineering approach (Reported — their own repo write-up).
- Caution: several third-party "CodeLayer case study" pages (e.g., skywork.ai) contain generic, likely AI-generated customer anecdotes — disregarded here.

## Relevance to agentic AI engineering

This sits at the **human-in-the-loop orchestration layer for agentic SWE**: parallel session management, plan-first workflows, and structured review gates. The QRSPI/spec-first approach is a production answer to the questions in *From Plan to Action: How Well Do Agents Follow the Plan?* and to the long-horizon quality decay measured by *SlopCodeBench: Benchmarking How Coding Agents Degrade Over Long-Horizon Iterative Tasks* — their entire pitch is preventing exactly that degradation. Team-scale parallel agents connect to *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*, and the "real work ≠ benchmark tasks" framing echoes *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering*. The legacy approval-API DNA (and human review loops in the current product) ties to the governance thread, e.g. *Governance by Construction for Generalist Agents*.

## Use cases & considerations

Use cases: (1) an engineering team standardizing how everyone runs Claude Code — shared plans, worktrees, review of research/plan artifacts before code; (2) running 5-10 parallel agent sessions on a large brownfield codebase without merge chaos; (3) adopting the free RPI/12-factor methodology without buying anything; (4) enterprise rollout of coding agents with audit logs and approval gates.

Considerations: young company, tiny team, solo founder — key-person and continuity risk; the pivot from approval-SDK to IDE means the famous OSS repo isn't the product you'd buy; customer evidence is mostly logos and self-reported growth. $100/user/mo on top of model subscriptions needs clear ROI. Competitors: Anthropic's own Claude Code teams features, Cursor (background agents), Devin/Cognition, Factory, Coder (also in this repo), Warp, Zed. Open question: does an orchestration layer survive as a standalone product if model vendors ship equivalent multi-session/team tooling natively?

## Sources

- https://www.humanlayer.dev/
- https://www.ycombinator.com/companies/humanlayer
- https://www.ycombinator.com/companies/humanlayer/jobs/oBCZzc7-founding-product-engineer
- https://github.com/humanlayer/humanlayer
- https://github.com/humanlayer/12-factor-agents
- https://github.com/humanlayer/advanced-context-engineering-for-coding-agents/blob/main/ace-fca.md
- https://claude.com/blog/building-companies-with-claude-code
- https://tracxn.com/d/companies/humanlayer/__XZbhI_kKRufCd1LnFm62x7HgBSEk6EtN315vIthngyQ
- https://www.crunchbase.com/organization/humanlayer
- https://foundertrace.com/companies/humanlayer/
- https://www.heavybit.com/library/article/whats-missing-to-make-ai-agents-mainstream
