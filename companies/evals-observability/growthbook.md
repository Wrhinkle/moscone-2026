# GrowthBook

> Open-source, warehouse-native feature-flagging and A/B-testing platform: flags and experiment stats are computed against your own data warehouse instead of a vendor's ingestion pipeline.

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** 2020, YC Winter 2022 batch (Verified — YC, Crunchbase)
- **Website / GitHub:** https://www.growthbook.io · https://github.com/growthbook/growthbook

## What they do
GrowthBook is an open-core (MIT-licensed core) feature-flag and experimentation engine. Instead of shipping event data to a proprietary store, it queries your existing warehouse (Snowflake, BigQuery, Redshift, Postgres, etc.) to compute experiment results, which keeps PII in-house and avoids a duplicate data pipeline. It handles flag delivery/targeting, SDKs across major languages, statistical analysis (Bayesian/frequentist), and product-analytics dashboards — the kind of infra teams use to safely roll out and measure changes, including changes to agent behavior/prompts.

## Founders & origins / Funding
Founded by Graham McNicoll (CEO, ex-CTO of Education.com) and Jeremy Dorn (CTO, ex-Chief Architect at Education.com). Went through YC W22. Raised a Series A on June 17, 2025, bringing total funding to ~$23.1M, with investors including Khosla Ventures, AlleyCorp, Lockheed Martin Ventures, Nexus Venture Partners (Verified — multiple sources).

## Evidence of real-world use
7,700+ GitHub stars; 3,000+ companies and 2,600 monthly-active orgs processing 100B+ event lookups. Named customers include Khan Academy, Dropbox, Treatwell, and toom (Reported — GrowthBook customer page/blog).

## Relevance to agentic AI engineering
Feature-flag/experimentation infra is directly reusable for gradually rolling out agent/prompt changes and running online evals (A/B testing prompts, model versions, or agent policies) — complements this repo's evals-observability entries like Braintrust and PostHog.

## Sources
- https://www.growthbook.io/
- https://github.com/growthbook/growthbook
- https://www.ycombinator.com/companies/growthbook
- https://blog.growthbook.io/7-000-github-stars-top-open-source-platform/
- https://www.growthbook.io/customers
