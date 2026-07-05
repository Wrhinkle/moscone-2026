# Kimchi (kimchi.dev)

> Open-source terminal coding agent plus a managed multi-model inference and spend-control platform, built by Cast AI to deliver frontier-quality agentic coding on cheap open-weight models.

- **Category:** coding-agents
- **AIEWF 2026 tier:** gold
- **Founded:** Launched ~late 2025 as a product line of Cast AI (Verified via Cast AI press releases and the getkimchi GitHub org; Cast AI itself founded 2019, Miami, FL / Vilnius, Lithuania — Verified)
- **Website / GitHub:** https://kimchi.dev · https://github.com/getkimchi/kimchi · parent: https://cast.ai/kimchi/

## Disambiguation note

The AIEWF 2026 sponsor page links "Kimchi" (gold tier) directly to **kimchi.dev**, so this profile covers that product — Cast AI's coding platform — not the name-colliding **Kimchi AI "anti-social network"** (joinkimchi.com), a pre-launch consumer AI-companion app with a waitlist and no disclosed team or funding. The consumer-ai category assignment likely stems from that collision; kimchi.dev is squarely a devtools/infrastructure company. Both candidates are documented here so the categorization can be corrected upstream if desired.

## What they do

Kimchi is three things sold as one platform. First, an **open-source CLI coding agent** (Apache 2.0, TypeScript, built on the pi-mono SDK) that runs in your terminal like Claude Code or Codex CLI. Its differentiator is **multi-model orchestration with role-based delegation**: an orchestrator classifies each step of a task and routes it to specialized roles (builder, reviewer, explorer, researcher) backed by different open-weight models — Kimi-k2.7, MiniMax-M3, Nemotron — reserving expensive frontier models for the hardest steps. A "/ferment" mode hands off a whole task and returns a finished PR with persistent cross-session plans; it supports LSP integration (TypeScript, Go), AGENTS.md/CLAUDE.md context files, and remote "teleport" cloud sandboxes for long-running sessions.

Second, a **managed inference layer** serving those open-weight models, priced aggressively ($0.75–$4.50 per 1M output tokens vs. a claimed ~$12.10 average for proprietary models), deployable serverless on Cast AI's clusters or fully sovereign in your AWS/GCP/Azure/on-prem environment with air-gap support and SOC 2 / GDPR / ISO 27001 / PCI-DSS posture. Third, a **spend console** with budget controls per API key, user, team, or org, plus tag-based request tracking for cost attribution. A visual kanban UI for parallel agent tasks ("Kimchi Studio") is announced as coming soon (Reported).

## Founders & origins

Kimchi has no separate founding team; it is "made by the creators of Cast AI" (Verified — stated on kimchi.dev and Cast AI's site). Cast AI was founded by **Yuri Frayman** (CEO), **Leon Kuperman**, and **Laurent Gil** (Verified — TechCrunch, Cota Capital, Cast AI press releases), serial founders who previously built and sold Zenedge (acquired by Oracle). Kimchi extends Cast AI's Kubernetes cost-optimization DNA into AI coding: same thesis (automated resource/cost arbitrage), new workload (agent tokens instead of cloud compute).

## Funding

No Kimchi-specific funding exists; capital is Cast AI's:
- **Series C, ~April 2025: $108M**, led by G2 Venture Partners and SoftBank Vision Fund 2, with Aglaé Ventures, Hedosophia, Cota Capital, Vintage, Creandum, Uncorrelated (Verified — Cast AI press release + TechCrunch), at a near-unicorn ~$850–900M post-money valuation (Reported — TechCrunch/TFN sourcing).
- **Strategic investment, January 2026**, reportedly pushing valuation over $1B (Reported — FinSMEs; amount not found in public sources).
- Total raised across all Cast AI rounds: not independently computed here; Series C alone confirmed at $108M.

## Evidence of real-world use

- **GitHub:** getkimchi/kimchi at ~2.1k stars, 101 forks, 164 releases, v0.1.58 shipped July 3, 2026, 620+ commits — active, real OSS velocity (Verified).
- **Named customer:** Ivox.ro (Andrei Temneanu) cites a 12x cost reduction — "62% of our token volume now costs what 12% used to" (Reported — testimonial on kimchi.dev, echoed in press).
- **Independent review:** engineer Kadir Keleş's write-up concludes "kimchi.dev works," praising reliability over long sessions (Reported).
- **Parent traction:** Cast AI claimed 2,100 customers at Series C (Reported — company press release).
- Public pricing page and free tier with no card required (Verified) — a real commercial product, though Kimchi itself is early-access-era young. Distinguish this from joinkimchi.com, which has zero usage evidence (waitlist only).

## Relevance to agentic AI engineering

Kimchi sits at the intersection of three areas in this repo's landscape: **agentic SWE benchmarks** — its MiniMax-M3 integration is marketed on a 59% SWE-bench Pro score, making it a live case study in whether open-weight models close the frontier gap on real GitHub-issue tasks; **tool-use and governance** — the spend console, per-team budget controls, and sovereign/air-gapped deployment are exactly the agent-governance controls enterprises keep asking for; and **agent memory**, via ferment mode's persistent cross-session plans and RTK token-optimization of context. Its router is a production instance of the model-cascade/routing pattern from the cost-aware orchestration literature.

## Use cases & considerations

Use cases: (1) cutting agentic coding spend by routing bulk work to open-weight models; (2) sovereign/on-prem coding agents for regulated environments; (3) org-wide token cost attribution and budgets; (4) a hackable Apache-2.0 harness for building custom agents.

Considerations: young product (v0.1.x) with rapid churn; orchestration quality vs. simply using Claude/GPT frontier models directly is unproven beyond vendor benchmarks; inference lock-in to Cast AI's platform for the managed tier; competes with Claude Code, OpenAI Codex CLI, Cursor CLI, Aider, and OpenRouter-style routing layers. Open questions: independent benchmarks of the router, and whether the "gold sponsor" push converts to adoption beyond early adopters.

## Sources

- https://www.ai.engineer/worldsfair/2026 (sponsor list; Kimchi gold tier, links to kimchi.dev)
- https://kimchi.dev/ and https://kimchi.dev/pricing
- https://github.com/getkimchi/kimchi
- https://cast.ai/kimchi/
- https://cast.ai/press-release/minimax-m3-comes-to-kimchi-coding/
- https://cast.ai/press-release/cast-ai-closes-108m-series-c-round/
- https://techcrunch.com/2025/04/30/cast-ai-raises-108m-to-get-the-max-out-of-ai-kubernetes-and-other-workloads/
- https://www.finsmes.com/2026/01/cast-ai-receives-strategic-investment.html
- https://kadirkeles.com/blog/12-my-take-on-kimchi-dev
- https://joinkimchi.com/ (disambiguation candidate, ruled out)

*Profile compiled 2026-07-02.*
