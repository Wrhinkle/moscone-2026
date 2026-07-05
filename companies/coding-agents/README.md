# Coding Agents

Autonomous or assisted software-engineering agents and AI coding products — Devin-style ticket-to-PR agents, terminal/IDE coding agents, AI code review, and the infrastructure that makes agent-written code shippable. The real-world problem is twofold: (1) most engineering work is delegable grunt work (migrations, bug backlogs, test coverage, dependency bumps) that agents can now do end-to-end, and (2) once agents generate code at volume, the bottleneck moves downstream to review, context, and governance — verifying that a torrent of machine-written PRs is actually correct, on-convention, and safe to merge. This category holds both sides of that trade: the companies generating the code and the companies checking it.

## How to read this category

The load-bearing entries are **[Cognition](cognition.md)** (Devin — the reference case for autonomous ticket-to-PR agents, $26B valuation, ~$492M reported ARR), **[GitHub](github.md)** (the substrate everything else plugs into, now betting on Agent HQ as the multi-vendor agent control plane), and **[OpenHands](openhands.md)** (the open-source reference implementation that most agentic-SWE benchmarks actually run). Read those three and you understand the poles: closed frontier autonomy, platform gravity, and open infrastructure.

The axis that differentiates the rest is **where they sit in the agent SDLC pipeline**:

- **Generation** — agents that write code: Cognition, [Factory](factory.md), [OpenHands](openhands.md), [Cline](cline.md), [Kimchi](kimchi.md), [GitHub](github.md) Copilot, and [Builder.io](builder-io.md) (the PM/designer-facing niche).
- **Review / verification** — the counterweight, monetizing the AI-slop problem: [Qodo](qodo.md) (the category's platinum sponsor), [Greptile](greptile.md), [Baz](baz.md).
- **Context / grounding** — feeding agents what they need to not hallucinate: [Sourcegraph](sourcegraph.md) (code graph), [Tessl](tessl.md) (versioned, evaluated skills), [IMPECCABLE](impeccable.md) (design rules for frontend output).
- **Specialized infrastructure** — plumbing other agents call: [Morph](morph.md) (fast edit-apply model), [Weco AI](weco-ai.md) (metric-driven code optimization), [Conductor/Orkes](conductor.md) (durable workflow execution — arguably an orchestration company that happens to be filed here).

A second axis worth tracking: **open vs. closed**. OpenHands (65k+ stars), Cline (64k+), and Kimchi are open-core with BYO-model economics; Cognition, Factory, and the review vendors are closed platforms. The open question threading the whole category is whether standalone layers (review, context) survive or get absorbed into the generation platforms.

## Start here

1. **[cognition.md](cognition.md)** — the company that defined the category with Devin; also the cautionary tale (13.86% SWE-bench demo → Answer.AI's 3-of-20 real-task result → $492M ARR anyway).
2. **[qodo.md](qodo.md)** — the platinum sponsor and the clearest articulation of the review-as-bottleneck thesis the whole verification side is built on.
3. **[openhands.md](openhands.md)** — if you're building rather than buying: the open agent loop, SDK, and eval harness the research community standardized on.

## All profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Qodo](qodo.md) | Multi-agent PR review and code-integrity layer that verifies code (human- or agent-written) rather than generating it | Platinum | $120M total; $70M Series B (Mar 2026, Qumra) | Customers include Nvidia, Walmart, Red Hat; donated its 11.9k-star PR-Agent to a community org to go all-in on the platform |
| [Greptile](greptile.md) | Code review agent that graph-indexes the whole repo and judges each PR's blast radius, not just the diff | Gold | ~$30M; $25M Series A led by Benchmark at ~$180M | v3 feeds review findings *back* to coding agents via MCP; Anthropic published it as a Claude API case study |
| [Sourcegraph](sourcegraph.md) | Enterprise code search / code graph that grounds agents in huge multi-repo estates; Deep Search + Agentic Batch Changes | Gold | ~$223M; last priced $2.625B (2021, a16z) | Split in two in Dec 2025 — founders left with the Amp coding agent; the sponsor here is the code-intelligence company |
| [Tessl](tessl.md) | Registry + package manager for versioned, *evaluated* agent skills and specs — "npm for agent context" | Gold | $125M ($100M Series A, Index) at $500M+ | Founded by Snyk's Guy Podjarny; every registry skill ships with evals (e.g. HashiCorp terraform skill: 47%→96% agent success) |
| [Factory](factory.md) | Model-agnostic "droid" agents across terminal, IDE, CI, and Slack, sold hard into large enterprises | Gold | ~$220M; $150M Series C (Khosla) at $1.5B | Enterprise rollouts at MongoDB, EY, Bayer; led Terminal-Bench at Droids GA (58.75%) |
| [Kimchi](kimchi.md) | Open-source terminal agent with multi-model routing — cheap open-weight models for bulk work, frontier only when needed | Gold | Cast AI capital ($108M Series C; >$1B valuation) | A Cast AI product line, not a startup — token-cost arbitrage applied to coding agents; claimed 12x cost reduction |
| [Cognition](cognition.md) | Devin, the autonomous AI software engineer, plus the Windsurf IDE and its own SWE-1.x model family | Silver | ~$1.6B+ raised; $26B post (May 2026) | Goldman Sachs' CIO called Devin "our new employee"; claims 89% of Cognition's own commits are Devin-written |
| [Baz](baz.md) | Reviewer agents for PRs plus a Planner that pre-empts vulnerabilities before code is written | Silver | $17M extended seed (Battery, boldstart) | Founders sold Bridgecrew to Palo Alto Networks for ~$200M; moving review *upstream* to the planning stage |
| [Builder.io](builder-io.md) | Fusion: a coding agent for PMs and designers — Jira ticket or Figma frame in, design-system-conformant PR out | Bronze | ~$37M; last round $20M from Microsoft's M12 (2024) | Angular creator Miško Hevery is CTO; constrains generation with an indexed design system rather than free-form codegen |
| [OpenHands](openhands.md) | The leading open-source autonomous coding agent (ex-OpenDevin), now with a hosted cloud and agent SDK | Bronze | ~$23.8M; $18.8M Series A (Madrona) | 65k+ GitHub stars; the harness other labs use to publish *their* SWE-bench results — CMU's Graham Neubig is a co-founder |
| [Cline](cline.md) | Open-source BYO-key coding agent (IDE/CLI/SDK) with no server middleman and transparent per-task token costs | Supporting | $32M; Series A (Emergence) at $110M | Started as a hackathon project ("Claude Dev"); its forks (Roo Code, Kilo Code) are themselves major OSS agents |
| [Conductor (Orkes)](conductor.md) | Managed durable-execution engine (Netflix's Conductor OSS) repositioned as the runtime for production agents | Supporting | ~$89M+; $60M Series B (Apr 2026) | Really an agent-orchestration play, not a coding agent — 32k-star OSS engine run in production at Netflix, Tesla, LinkedIn |
| [GitHub](github.md) | The default home of source code, repositioning as the control plane where everyone's coding agents work | Supporting | Microsoft subsidiary ($7.5B, 2018) | Agent HQ orchestrates Anthropic/OpenAI/Google/Cognition agents under one subscription; no CEO since Aug 2025 — reports into Microsoft CoreAI |
| [IMPECCABLE](impeccable.md) | Open-source design skill (~45 anti-pattern rules) that stops agent frontend output looking like AI slop | Supporting | Seed via Renaissance Geek, a16z-backed | Built by jQuery UI creator Paul Bakaus; 40k+ GitHub stars and a GitHub partnership to bake it into Copilot |
| [Morph](morph.md) | "Fast Apply" inference model that merges LLM-proposed code edits into files at ~10,500 tok/s | Supporting | ~$5.75M (YC S23, as Autoinfra) | Sells the unglamorous bottleneck — edit application — as an API; cites JetBrains, Vercel, Webflow as users |
| [Weco AI](weco-ai.md) | Agent that treats code optimization as tree search: rewrite, run your eval, keep the best-scoring branch | Supporting | $8–9.3M seed (Golden Ventures) | Its AIDE research agent is cited as a building block by OpenAI, METR, Sakana, and Meta; 4–5x medal-rate gains on MLE-Bench |

**Expected-vs-actual:** all 14 companies expected in this category are present. Two additional profiles were re-filed *into* this folder: **Factory** (gold-tier generation agent) and **Kimchi** (whose profile notes it was likely miscategorized as consumer-ai upstream due to a name collision with joinkimchi.com). Both Conductor and Kimchi profiles carry disambiguation notes worth reading before citing them. No profiles are missing.

## Related papers

The agentic-SWE benchmark thread ([../../papers/swe-agents/](../../papers/swe-agents/)) is essentially *about* this category — nearly every profile cites it:

- [Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) — the thesis behind Qodo's, Greptile's, and Tessl's "quality is org-contextual" pitch, and the critique of Factory's and Cognition's benchmark-led marketing.
- [SlopCodeBench](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) and [SWE-EVO](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md) — long-horizon degradation, the exact failure mode the review layer (Qodo, Greptile, Baz) monetizes and Devin-style autonomy suffers.
- [ProdCodeBench](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md) and [FeatureBench](../../papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md) — production-derived and feature-level evaluation of the delegation pattern Cognition, Factory, and OpenHands sell.
- [OmniCode](../../papers/swe-agents/omnicode-a-benchmark-for-evaluating-software-engineering-ag.md) and [Reproducible, Explainable, and Effective Evaluations of Agents](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md) — OpenHands is frequently the scaffold these evaluations run on.
- [Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md) — the pattern behind Qodo's and Greptile's parallel reviewer fan-out and Kimchi's role-based delegation.
- [A Task-Level Evaluation of AI Agents in Open-Source Software](../../papers/swe-agents/a-task-level-evaluation-of-ai-agents-in-open-source-software.md) — grounding for what agents actually complete on real OSS work (cf. the Answer.AI Devin evaluation).

From other paper areas:

- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — the research counterpart to GitHub Agent HQ's branch controls, Cline's `.clinerules`, OpenHands' RBAC, and Kimchi's spend console.
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — the GitHub MCP server and Sourcegraph Deep Search are its most-used production instances.
- [Verifiable Software Worlds for Computer-Use Agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md) — sandboxed runtimes of the kind OpenHands and Devin execute in.
- [Memory for Autonomous LLM Agents](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) and [Graph-based Agent Memory](../../papers/memory-research-agents/graph-based-agent-memory-taxonomy-techniques-and-applicat.md) — applied by Greptile's comment-learning loop, Qodo's Context Engine, Devin Wiki, and Tessl's specs-as-memory.
- [Are We Ready for an Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md) — the AGENTS.md/CLAUDE.md organizational-context question Factory, Kimchi, and Greptile all touch.
- [Agentic Search in the Wild](../../papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md) — the retrieval pattern behind Sourcegraph Deep Search and Cognition's SWE-grep subagents.
- [One Developer Is All You Need](../../papers/planning-architecture/one-developer-is-all-you-need-a-case-study-of-an-ai-augment.md) — the brownfield, human-plus-agent-fleet regime Sourcegraph and Factory target.
- [How AI Coding Agents Shape Software Architecture](../../papers/planning-architecture/how-ai-coding-agents-shape-software-architecture.md) — the downstream architectural cost of agent-generated code the review layer exists to police.

## Open questions

1. **Does standalone review survive?** Qodo, Greptile, and Baz all bet that verification stays a separate layer; every generation platform (GitHub, Cursor, Claude Code) is building native review. Absorbed or entrenched by ~2027 is the category's biggest fork.
2. **Where does the margin live?** Cline takes zero inference margin, Kimchi arbitrages open-weight models, Cognition trains its own; nobody has proven pricing power when the underlying models do most of the work and labs subsidize competitors.
3. **Vendor metrics all the way down.** Nearly every ROI number in this folder (Monday.com's 73.8% acceptance, Factory's 31x, Cognition's 89% dogfooding, Kimchi's 12x) is vendor-published. The Answer.AI Devin evaluation remains one of the only independent audits — the category badly needs more.
4. **Benchmark misalignment.** SWE-bench-style wins keep failing to predict production usefulness (Devin's arc is the canonical example); whether the newer benchmarks in `papers/swe-agents/` become the buying criterion is unresolved.
5. **Context as the moat.** Sourcegraph, Tessl, and Greptile all argue the durable asset is context (code graph, evaluated skills, learned team standards), not the agent. If skills/context converge on open formats (MCP, plain markdown), the moat thins to evals and governance.
