# Foam

> An AI agent that reads your logs/traces/metrics, investigates production anomalies on its own, and pings the responsible engineer with a diagnosis and fix.

- **Category:** evals-observability
- **AIEWF 2026 tier:** bronze
- **Founded:** 2024, San Francisco, CA (Verified — company blog, Crunchbase)
- **Website:** foam.ai — disambiguated from the unrelated OSS Foam note-taking/wiki tool (foambubble); this is a distinct venture-backed observability company, tagline "If prod could talk, what would you ask?"

## What they do
Foam installs via read-only GitHub access (no code changes) and ingests logs, traces, and metrics into a unified view, running scheduled health checks (latency, error rate, LLM spend). When a threshold breaks, it automatically investigates — correlating signals to a single root cause — and posts a Slack report naming the culprit and a candidate fix, rather than another undifferentiated alert. It's designed to sit alongside existing tools like Datadog and Sentry, positioning itself as "the first telemetry and production system designed for LLMs," i.e. built for the alert-fatigue and non-deterministic-failure patterns of AI-heavy production stacks.

## Founders & funding
Founded by Perla Gámez (CEO, ex-South Park Commons, Affirm, Goldman Sachs), with co-founders Luke Mercado and Shawn Krisman (Verified — LinkedIn, company blog). $10M seed from Khosla Ventures, The House Fund, South Park Commons, and Max Levchin (Verified — foam.ai/blog/announcing-fundraise).

## Evidence of real-world use
Named customers/testimonials: Perplexity, Together AI, Orb, Braintrust, Stream, Lica, Atlas (Verified — company site quotes attributed to named CTOs).

## Relevance to agentic AI engineering
Sits squarely in the evals/observability slice of the agent stack, specifically framed around debugging LLM-application-layer failures and cost/latency drift.

## Sources
- https://foam.ai/
- https://foam.ai/blog/announcing-fundraise
- https://www.crunchbase.com/organization/foam-1445
