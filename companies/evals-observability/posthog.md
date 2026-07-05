# PostHog

> Open-source, all-in-one product analytics platform (events, session replay, feature flags, experiments) that has expanded into LLM observability — trace, cost, and latency tracking for AI features tied to the same user data as the rest of your product.

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** January 2020, Y Combinator W20; all-remote, US-incorporated with London roots (Verified — company handbook, press)
- **Website / GitHub:** https://posthog.com · https://github.com/PostHog/posthog

## What they do

PostHog is a developer-first product analytics suite delivered as one platform on a shared event store (ClickHouse under the hood): product and web analytics, session replay, feature flags, A/B experiments, surveys, error tracking, a data warehouse/CDP, and SQL access over all of it. You instrument once with their SDKs and every product reads the same events. The core repo is open source and self-hostable for hobby use; the commercial product is usage-based cloud with a free tier per product — a deliberate "pay per event/replay/flag request" posture rather than seats.

The reason they land in this category: **LLM analytics / AI observability**. Their SDKs and integrations (OpenAI/Anthropic wrappers, LangChain, LiteLLM, Vercel AI SDK) capture LLM generations as traces and spans — inputs, outputs, token counts, model, latency, error rates, and per-user/per-org cost. The differentiator versus dedicated LLM-observability tools is correlation: the same platform holds the user's session replay, funnel position, and feature-flag state, so you can ask "did the slow, expensive generation actually hurt retention" in one query, and A/B test prompts with the same experiments product you use for UI changes.

Their 2025–2026 "Act 2" pushes into agentic devtools: **PostHog AI** (analytics copilot exposed in-app and via MCP tools/skills to Claude Code, Cursor, Codex) and **PostHog Code**, a desktop agent launching Spring 2026 that watches PostHog signals — errors, frustration patterns, LLM trace anomalies — and generates tasks, fixes, and pull requests with human checkpoints (Verified — posthog.com/code, docs).

## Founders & origins

**James Hawkins** (CEO) and **Tim Glaser** (CTO) — Verified. They worked together previously (Hawkins in sales leadership at Arachnys, where Glaser was an engineer — Reported). They entered YC W20 with a different product, pivoted repeatedly, and built PostHog out of frustration at having to ship user data to third-party analytics vendors to understand feature usage; open-source, self-hostable analytics was the founding wedge (Verified — company handbook "How we got here", Contrary Research).

## Funding

- **Seed, March 2020:** $3M (Verified)
- **Series A, 2020:** $9M, later announced as $12M total, led by GV with YC Continuity (Verified — company blog)
- **Series B, 2021:** $15M (Reported)
- **Series D, June 2025:** $70M led by **Stripe** at a $920M valuation; some secondary sources date it 2024 — the 2025 date is better supported (Reported)
- **Series E, September 2025:** $75M led by **Peak XV Partners** at ~$1.4B valuation — unicorn status (Verified — multiple press sources)
- **Total raised:** ~$182–194M; Tracxn reports $194M across 7 rounds (Reported — sources disagree at the margin)

Stripe leading the Series D is a notable strategic signal from a company that itself runs massive product analytics.

## Evidence of real-world use

Strong and unusually verifiable for a devtool. The main repo had **35,000+ GitHub stars** as of mid-2026 with very high commit velocity (Reported). Public, self-serve pricing with a generous free tier means a large long tail of real usage; PostHog markets "100,000+ companies" scale claims (Reported — company marketing, treat as directional). Documented case studies exist at posthog.com/customers — **ElevenLabs** is a detailed one, using analytics, replays, surveys, and flags across launches (Verified). Raycast, Mistral AI, and Y Combinator itself appear among cited users (Reported — company materials). Ecosystem signals: LiteLLM and the Vercel AI SDK both document PostHog as a supported observability provider — third-party docs recommending them is stronger evidence than logos.

## Relevance to agentic AI engineering

PostHog occupies the production-telemetry end of the evals/observability layer: trace and span capture for LLM calls connects to *The Evolution of Tool Use in LLM Agents*, and the audit-trail requirements in *Governance by Construction for Generalist Agents*. It is weaker on the offline-eval discipline the agentic-SWE benchmark papers (*SWE-EVO*, *ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*) formalize — PostHog gives you the production traces those papers say you should be mining into datasets, but not a CI eval harness. PostHog Code itself is an instance of the pattern those benchmarks measure: an agent acting on observability signals to open PRs.

## Use cases & considerations

Use cases: (1) one-stop analytics + flags + experiments for a small AI product team that doesn't want four vendors; (2) per-user/per-org LLM cost accounting to price an AI feature; (3) prompt A/B testing via experiments with retention as the metric; (4) session replay + LLM trace side-by-side to debug "the agent did something weird" reports.

Considerations: LLM analytics is younger and thinner than dedicated eval platforms — **Braintrust, LangSmith, Langfuse, Arize, W&B Weave** all offer deeper scoring/eval-CI loops; PostHog's bet is breadth and data co-location. Product analytics competitors: Amplitude, Mixpanel, Statsig; flags: LaunchDarkly. Usage-based pricing can surprise at replay/event volume. The platform's breadth (many half-deep products) is the honest critique; open-source core limits lock-in. Open question: whether PostHog Code ships as more than a demo.

## Sources

- https://posthog.com/handbook/story
- https://posthog.com/blog/posthog-announces-9-million-dollar-series-A
- https://research.contrary.com/company/posthog
- https://tracxn.com/d/companies/posthog/__tWY33MozggoGzQ9VYs8-O9tG9o6ZXDONwy37RdpGE_0
- https://www.thesaasnews.com/news/posthog-raises-75m-series-e-at-1-4b-valuation/
- https://traded.co/vc/deal/posthog-raises-75-million-series-e-round-led-by-peak-xv-partners-at-1-4-billion-valuation/
- https://posthog.com/ai-observability
- https://posthog.com/docs/llm-analytics/start-here
- https://posthog.com/code
- https://posthog.com/docs/posthog-ai
- https://posthog.com/customers/elevenlabs
- https://github.com/posthog/posthog
- https://docs.litellm.ai/docs/observability/posthog_integration
- https://ai-sdk.dev/providers/observability/posthog
