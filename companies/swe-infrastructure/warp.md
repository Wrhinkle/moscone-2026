# Warp

> The Rust-based terminal that turned itself into an "Agentic Development Environment" — a place to launch, steer, and monitor coding agents instead of just typing shell commands.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** June 2020, New York City (Verified — Wikipedia, Tracxn, company site)
- **Website / GitHub:** https://www.warp.dev · https://github.com/warpdotdev/warp

**Disambiguation note:** there is an unrelated warp.co (AI payroll/HR, CEO Ayush Sharma, $60M Series B from Battery Ventures in June 2026). This profile is warp.dev, the terminal company. Do not mix their funding numbers.

## What they do

Warp started (2021–2023) as a modern terminal emulator written in Rust for macOS, later Linux (Feb 2024) and Windows (Feb 2025): GPU-rendered, with an IDE-like input editor, block-based output, and "Warp Drive" for saving and sharing parameterized commands and runbooks across a team.

In June 2025 the pitch changed. Warp 2.0 repositioned the product as an "Agentic Development Environment": the terminal is the harness for coding agents. You type a prompt or a command into the same input box; agents run in parallel threads ("agent multi-threading"), each with its own task list, diff review, and permission prompts, while classic shell use stays available. At launch Warp claimed #1 on Terminal-Bench (52%) and 71% on SWE-bench Verified (Verified — Warp's own benchmark posts plus leaderboard coverage; vendor-run numbers, treat accordingly).

Two big 2026 moves (both Verified — Warp blog, GitHub, press): in April 2026 Warp open-sourced the terminal/client (AGPL + MIT, with financial support from OpenAI reported; Warp Drive stays closed), and shipped **Oz**, an orchestration platform for cloud agents — CLI, API, TypeScript SDK, managed or self-hosted sandboxed environments (`oz-agent-worker` lets you run agents on your own infra), a scheduler for recurring agent jobs, and per-run audit trails/observability. Practically: Warp the app is what an engineer installs; Oz is what a platform team integrates to run fleets of background agents.

Pricing is credit-metered (AI + compute + platform credits). Business plan ~$50/user/mo with 1,500 monthly credits, BYOK for OpenAI/Anthropic/Google models, SSO, and zero-data-retention; self-serve caps at 50 seats, Enterprise above that (Verified — public pricing page and docs).

## Founders & origins

Zach Lloyd, founder/CEO (Verified). Previously Principal Engineer at Google leading Google Docs/Sheets/Slides, interim CTO at TIME, and co-founder/CTO of SelfMade. Origin story (Reported — Sequoia spotlight, Changelog interview): Lloyd saw the terminal as the last unreformed developer surface — collaborative-editing lessons from Docs applied to the command line. No co-founders are prominently credited; treat Warp as a single-founder company.

## Funding

- Seed, 2020: $6M led by GV, with BoxGroup and Neo (Verified)
- Series A, 2021 (announced April 2022 as "$23M raised"): $17M led by Dylan Field, Figma CEO (Verified)
- Series B, June 2023: $50M led by Sequoia Capital (Verified)
- Total: ~$73M (Verified — Tracxn, Crunchbase, Wikipedia agree). Angels include Sam Altman, Marc Benioff, Jeff Weiner, Elad Gil (Reported).
- No post-2023 round found in public sources as of 2026-07-02, despite explosive 2025–26 revenue reporting; a new round would not be surprising.

## Evidence of real-world use

- Docker case study with a concrete outcome: onboarding time for a provisioning team cut ~25% via shared Warp Drive runbooks (Reported — Warp customer page, so vendor-published but specific).
- Marketing claims: 800k+ developers, engineers at "56% of the Fortune 500," Microsoft named (Reported — landing-page numbers, not independently audited).
- Revenue trajectory: 20VC (2026) episode titled "adding $1M ARR every week"; Sacra/Aakash Gupta report $1M ARR added every 5–6 days, revenue up 19x in a year, 700k+ active developers (Reported — founder-sourced figures).
- OSS signal: ~63k GitHub stars and 5k+ forks within two months of open-sourcing (Reported — forkable.io analysis).
- Public pricing page with self-serve team plans = real commercial product.

## Relevance to agentic AI engineering

Warp sits at the harness layer of the agent stack — the thing that runs agents, not the model. Its benchmark-first marketing connects directly to this repo's agentic-SWE evaluation thread: *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* is the right skeptical lens on Warp's Terminal-Bench/SWE-bench claims, and *SlopCodeBench* (long-horizon degradation) is the failure mode Oz's long-running scheduled agents will hit. Agent multi-threading maps to *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*; Oz's per-run audit trails and permissioning are a commercial take on *Governance by Construction for Generalist Agents*.

## Use cases & considerations

Use cases: (1) team-standard terminal replacing tribal runbooks (the Docker pattern); (2) parallel background coding agents with human diff review; (3) Oz-scheduled recurring agent jobs (triage, dependency bumps, report generation) on your own infra; (4) BYOK agent harness where the model bill stays on your API keys.

Considerations: competes head-on with Claude Code, OpenAI Codex, and Cursor — all moving fast, some model-vertically-integrated; credit-based pricing has drawn public criticism as hard to predict (kilo.ai blog); Warp Drive (the collaboration layer, arguably the moat) is not open source, so lock-in concentrates there; historical community friction over login requirements and telemetry predates the open-sourcing. Open question: whether OpenAI's financial support of the open-sourcing signals deeper alignment that constrains model neutrality.

## Sources

- https://www.warp.dev/ · https://www.warp.dev/pricing · https://www.warp.dev/customers/docker · https://www.warp.dev/enterprise
- https://www.warp.dev/blog/reimagining-coding-agentic-development-environment
- https://www.warp.dev/blog/swe-bench-verified
- https://www.warp.dev/blog/oz-orchestration-platform-cloud-agents
- https://www.warp.dev/blog/warp-is-now-open-source
- https://www.warp.dev/blog/warp-new-pricing-flexibility-byok
- https://en.wikipedia.org/wiki/Warp_(terminal)
- https://github.com/warpdotdev · https://github.com/warpdotdev/oz-agent-worker
- https://tracxn.com/d/companies/warp/__42PBtguUZBLgOmbA-BIyMxCS0onQSYmda10_KkgFBwA
- https://www.thetwentyminutevc.com/zach-lloyd
- https://sacra.com/c/warp/
- https://aakashgupta.medium.com/the-1m-arr-every-10-days-playbook-how-warp-cracked-the-ai-agent-code-4682cc9be034
- https://sequoiacap.com/article/warp-spotlight/
- https://www.forkable.io/p/why-warp-finally-opened-up-its-code
- https://docs.warp.dev/support-and-community/plans-and-billing/plans-pricing-refunds/
- https://blog.kilo.ai/p/warps-new-pricing-still-doesnt-add
- (Disambiguation only) https://www.finsmes.com/2026/06/warp-raises-60m-in-series-b-funding.html
