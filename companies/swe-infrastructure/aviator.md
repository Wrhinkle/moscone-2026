# Aviator

> Merge automation and code-review workflow tooling (merge queues, stacked PRs) that has repositioned as the "landing layer" for AI-generated code — spec-driven agent runs that end in reviewable, queue-merged PRs.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** supporting
- **Founded:** 2021, San Francisco (Verified — Y Combinator S21 profile, Crunchbase)
- **Website / GitHub:** https://www.aviator.co · https://github.com/aviator-co (notably `aviator-co/av`)

## What they do

Aviator started as a developer-productivity suite for teams whose CI/merge pipeline is the bottleneck. The anchor product is **MergeQueue**: instead of clicking "merge," developers enqueue PRs; Aviator validates each against the latest mainline (batching, parallel/optimistic queues, monorepo-aware "affected targets"), catches semantic conflicts between concurrently merging PRs, and lands them automatically so main stays green. Around it sit **Stacked PRs** (the open-source `av` CLI for creating and rebasing chains of dependent PRs), **Team Reviews/Inbox** (review routing and a FlexReview-style ownership model), **Verify**, and **Releases**. It installs as a GitHub app; Enterprise adds self-hosted deployment, SSO/SAML, and audit logging.

The 2025–26 pivot is **Runbooks**, their agentic product: tasks arrive from Slack or GitHub, an agent researches the codebase and generates a step-by-step executable spec (the runbook), then executes it in ephemeral remote sandboxes (a Claude Code sandbox is named), emitting a **stacked PR per step** that humans review, with landing handled by MergeQueue. Runbooks are versioned and publishable to a shared team library (`aviator-co/runbooks-library` is open source), and agents respond to review commands like `/aviator revise` and auto-fix CI failures. The pitch, translated: replace ad-hoc "vibe coding" prompts with reusable, reviewable specs, and make agent output land through the same gated pipeline as human code.

## Founders & origins

**Ankit Jain**, co-founder and CEO (Verified — YC, Crunchbase, LinkedIn). Ex-Google and Adobe engineer; engineering lead at Homejoy, Sunshine, and Shippo; EIR at Unshackled; runs Xoogler.co, the ex-Google alumni network. YC lists him as the sole founder; no other co-founder is named in public sources (Unverified whether additional co-founders exist — Crunchbase's "Co-Founder" title implies at least one more, not identified). Origin framing: "ex-Googlers bringing Google-level engineering productivity" — i.e., productizing internal Google infra like TAP/submit queues.

## Funding

- **Pre-seed, announced May 2022: $2.3M**, led by Y Combinator, Elad Gil, AirAngels, and Xoogler Ventures, with 20+ angels (Verified — company announcement plus press coverage).
- No later priced rounds found in public sources; total raised appears to be ~$2.3M. Note a data-quality flag: Latka lists an "Aviator" as bootstrapped with $7.1M revenue and 47 employees, which conflicts with the YC-backed record and YC's stated team size of 6 — treat those revenue/headcount figures as Unverified and likely a name collision or stale scrape. Tracxn mentions an M&A offer in April 2025 (Reported, single source, no details).

## Evidence of real-world use

- Vendor-claimed customers: **Slack, Square, Figma, DoorDash, Benchling, Notion, Amplitude, Bosch, Lightspeed, the Tari Project** (Reported — logos/claims on aviator.co and the YC page; no independent public case studies found, so treat as logo-level evidence).
- **Public pricing page** with self-serve tiers — Free, Team $20/dev/mo, Scale $40/dev/mo (50 verified PRs/user then $1/PR), Enterprise — indicating a real commercial product with usage-based AI metering (Verified).
- OSS: `aviator-co/av` has ~496 stars, 41 forks, MIT license, 95 releases, latest v0.1.41 June 19, 2026 — modest but genuinely active (Verified — GitHub).
- Community/content: an active engineering blog and podcast on merge-queue practice, and a Google Cloud startup case study about their own infrastructure (Verified — cloud.google.com).

## Relevance to agentic AI engineering

Aviator sits at the **integration/landing layer** of the agent SDLC — the choke point that gets worse as agents raise PR volume. Long-horizon agentic coding of the kind *SWE-EVO* and *SlopCodeBench* benchmark produces many partially-trusted changes; a semantic-conflict-aware merge queue is the mechanism that keeps main green under that load. Runbooks' stacked-PR-per-step execution is a concrete instance of the coordination substrate assumed in *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*, and its sandboxed execution plus mandatory human-review gates before queue-merge is the workflow-level analog of *Governance by Construction for Generalist Agents* — control enforced by the pipeline, not the prompt.

## Use cases & considerations

Use cases: (1) monorepo teams (>~20 devs) drowning in merge conflicts/flaky-CI merge failures; (2) stacked-PR workflow on plain GitHub via the free `av` CLI; (3) landing coding-agent output (Claude Code et al.) through spec-driven runbooks with per-step review; (4) codifying repetitive large-scale code operations (migrations, coverage) as shared runbooks.

Considerations: GitHub's native merge queue covers the basic case for free — Aviator's edge is scale features (parallel/optimistic queues, affected-target monorepo logic); Runbooks is new (2025–26) and unproven versus the mature MergeQueue core; competitors include **Graphite** (closest, stacked PRs + AI review), **Mergify**, **Trunk**, and GitHub itself. Open questions: actual Runbooks adoption, and whether a ~$2.3M-raised company can outpace better-funded Graphite in the agent-era repositioning.

## Sources

- https://www.aviator.co / https://www.aviator.co/about-us / https://www.aviator.co/pricing
- https://www.aviator.co/merge-queue and https://docs.aviator.co/mergequeue
- https://www.aviator.co/runbooks and https://www.aviator.co/blog/aviator-runbooks-turn-ai-coding-multiplayer-with-spec-driven-development/
- https://www.ycombinator.com/companies/aviator
- https://www.aviator.co/news/announcing-our-2-3-million-seed-round
- https://github.com/aviator-co/av and https://github.com/aviator-co/runbooks-library
- https://www.crunchbase.com/organization/aviator-c798 and https://www.crunchbase.com/person/ankit-jain-a65c
- https://cloud.google.com/blog/topics/startups/aviator-scales-developer-collaboration-with-google-cloud
- https://getlatka.com/companies/aviator.co (conflicting data, flagged) and https://tracxn.com/d/companies/aviator/__bdeYB5BfuwOVNg4IBnfb0EEXhHTfzwepsddXaEfujyk
