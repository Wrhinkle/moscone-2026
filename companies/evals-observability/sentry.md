# Sentry

> Developer-first error tracking and application performance monitoring, now extended to LLM/agent observability and an AI debugging agent (Seer).

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** Open-source project started 2008 by David Cramer; company incorporated 2012, San Francisco (Verified)
- **Website / GitHub:** https://sentry.io · https://github.com/getsentry/sentry (44.2k stars, 4.7k forks as of 2026-07-02, Verified via GitHub API)

## What they do

Sentry is the default error-tracking layer for a large slice of the software industry: you drop an SDK into your app (SDKs exist for hundreds of languages/platforms), and unhandled exceptions, crashes, and performance regressions are captured with full stack traces, breadcrumbs, release/commit attribution, and distributed traces. The core loop is "alert → exact line of code → suspect commit → owner," integrated with GitHub, Slack, Jira, etc. Beyond errors it sells performance monitoring (tracing, profiling), session replay, cron/uptime monitoring, and code coverage (via the Codecov acquisition).

Since 2024–2025 Sentry has pushed hard into AI observability. **Agent Monitoring** auto-instruments agent invocations, tool calls, and LLM requests — tracking token usage, model calls, tool executions, and agent handoffs — with out-of-the-box integrations for OpenAI, Anthropic, Google GenAI, LangChain/LangGraph, Pydantic AI, the OpenAI Agents SDK, and the Vercel AI SDK in Python and Node.js. **Seer** is their AI debugging agent: it does root-cause analysis over error/trace data (Sentry claims 94.5% root-cause accuracy) and now ships as a natural-language "Seer Agent" for querying production issues. They also run an **MCP server** exposing ~16 tools so coding agents (Claude Code, Cursor, etc.) can pull real error context and trigger Seer directly.

The code is source-available under Sentry's own **Functional Source License** (converts to Apache-2.0 after two years; not OSI open source since a 2023 relicensing) — self-hosting is genuinely supported, but the business is the SaaS.

## Founders & origins

- **David Cramer** — created Sentry as `django-db-log` in 2008; self-taught engineer (dropped out of high school, managed a Burger King); grew the project while at Disqus (2010–2013). Was CEO, then CTO (2019), now Chief Product Officer. (Verified)
- **Chris Jennings** — co-founder and Chief Creative Officer; previously at GitHub and Disqus; met Cramer through open-source collaboration. (Verified)
- **Milin Desai** (ex-VMware) became CEO in January 2020. (Verified)

The company was bootstrapped off the open-source project's organic adoption before taking venture money — a well-documented "OSS to unicorn" story.

## Funding

- Series D, Feb 2021: $60M led by Accel, with NEA and BOND; $1B valuation, total then $127M. (Verified — Sentry press release + Crunchbase News)
- Series E, May 2022: $90M co-led by BOND and Accel, with NEA and K5 Global; >$3B valuation. (Verified)
- Total raised: ~$217M as of the Series E. (Verified) No later primary rounds found in public sources.
- Acquisitions: Codecov (Nov 2022, code coverage), among others. (Verified)

## Evidence of real-world use

Strong — this is one of the most-deployed devtools in existence, not a logo wall:
- **4M+ developers, ~100k+ organizations** claimed; 18k+ paid customers with 200% enterprise growth per a company press release (Reported — company figures).
- **Documented case studies:** Disney+ (error tracking across streaming devices; teams wrote a custom Sentry SDK where none existed), Atlassian/Bitbucket (claims ~4,160 engineering hours saved/year; migrated self-hosted → SaaS in 5 days). GitHub, Vercel, Cloudflare, Instacart, Lyft, Microsoft appear as customers. (Verified for Disney+/Atlassian via published case studies; others Reported.)
- **OSS gravity:** 44k+ GitHub stars on the main repo, an enormous SDK ecosystem, and a public pricing page with a free tier — real commercial product with bottoms-up adoption.

## Relevance to agentic AI engineering

Sentry sits at the **observability/debugging layer of the agent stack**, on both sides of the loop: (1) monitoring your agents in production (traces across multi-step tool calls and handoffs — directly relevant to the tool-use/governance research thread in this repo, since tool-call traces are the raw material for governance and failure analysis), and (2) feeding production context *to* coding agents via its MCP server, which connects to the agentic-SWE-benchmark line of work — Seer is effectively an automated bug-localization/repair agent operating on real production telemetry rather than benchmark repos. For long-running agent fleets, its trace store functions as externalized episodic memory of agent behavior (adjacent to the agent-memory papers here, though Sentry itself makes no memory claims). Less relevant to the voice-agent papers except as generic latency/error monitoring.

## Use cases & considerations

Use cases: (1) instrument a production LLM agent to see token spend, tool-call failures, and which step of a multi-agent trace degraded; (2) wire the Sentry MCP server into Claude Code/Cursor so fixes are grounded in real stack traces; (3) standard error+performance monitoring for the app around the agent; (4) Seer for triage automation on high-volume issue queues.

Considerations: event-volume pricing can climb steeply at scale (a perennial complaint); FSL is source-available, not OSI open source — self-hosting large Sentry is operationally heavy (Atlassian abandoned it); Seer accuracy claims are vendor-reported; AI observability competitors include Datadog (LLM Observability), Langfuse, LangSmith, Arize Phoenix, Braintrust, and W&B Weave — Sentry's edge is incumbency in the existing error-tracking workflow rather than eval tooling depth (it is not an evals platform).

## Sources

- https://sentry.io/ and https://sentry.io/solutions/ai-observability/
- https://blog.sentry.io/scaling-observability-for-multi-agent-ai-systems/
- https://thenewstack.io/sentrys-seer-agent-debug/
- https://www.zenml.io/llmops-database/model-context-protocol-mcp-server-for-error-monitoring-and-ai-observability
- https://research.contrary.com/company/sentry
- https://cra.mr/sentry-from-the-beginning/
- https://sentry.io/about/press-releases/sentry-raises-60-million-in-series-d-funding-at-1-billion-valuation/
- https://sentry.io/about/press-releases/sentry-raises-90-million-in-series-e-funding-to-expand-and-drive-adoption-of-developer-first-application-monitoring/
- https://news.crunchbase.com/enterprise/sentry-unicorn-funding-bond-accel/
- https://sentry.io/customers/disney-plus/ and https://sentry.io/customers/atlassian/
- https://sentry.io/about/press-releases/sentry-application-monitoring-achieves-200-increase-in-enterprise-growth/
- https://sentry.io/about/press-releases/sentry-acquires-codecov/
- https://www.infoq.com/news/2023/12/functional-source-license/
- https://api.github.com/repos/getsentry/sentry (stars/forks, fetched 2026-07-02)
