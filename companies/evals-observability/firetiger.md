# Firetiger

> AI agents that watch your production systems, verify PRs actually work, and triage incidents before customers notice.

- **Category:** evals-observability
- **AIEWF 2026 tier:** bronze
- **Founded:** 2026 (publicly launched Feb 18, 2026), Silicon Valley (Verified — company blog, Sequoia)
- **Website:** firetiger.com (note: distinct from unrelated "Firetiger Technologies" consulting firm and an Israeli cybersecurity startup of the same name — disambiguated via Sequoia's investment post)

## What they do
Firetiger sells natural-language-configured "agents" that sit across a company's observability stack (OpenTelemetry, Datadog), databases (Postgres, MySQL, ClickHouse, Iceberg), cloud (AWS/GCP), and collaboration tools (Slack, PagerDuty, Linear, GitHub). Two products: **Change Monitors**, which watch a specific PR's diff across staging/canary/prod to confirm both "did this deploy stay healthy" and "did the intended change actually work"; and always-on agents that detect production anomalies, identify affected customers/services, and generate root-cause hypotheses, handing fixes to human or coding agents (Cursor, Codex, Claude Code via MCP) and then re-verifying the fix. Positioning: closing the loop between AI-generated code and production verification.

## Founders & funding
Founders Rustam Lalkaka (7 years building infra at Cloudflare) and Achille (built data planes/observability at Twitch, Segment, Twilio) — Verified via company blog. $7.6M seed led by Sequoia Capital, with angels including Matthew Prince and Calvin French-Owen (Verified — Sequoia Capital article).

## Evidence of real-world use
Named customers: Clerk, Kernel, Avora, Architect, Town, Voxel, Judgment Labs, with quotes describing adoption as "standard practice ... on the majority of PRs" (Verified — firetiger.com).

## Relevance to agentic AI engineering
Directly targets the evals/observability layer of the agent stack — closed-loop verification for AI-written code, adjacent to eval frameworks and incident-response agents discussed elsewhere in this repo.

## Sources
- https://www.firetiger.com/
- https://blog.firetiger.com/introducing-firetiger/
- https://sequoiacap.com/article/partnering-with-firetiger-validation-at-the-speed-of-ai/
