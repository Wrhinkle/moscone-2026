# Stigg

> Monetization infrastructure for software companies — a runtime API layer that enforces pricing plans, feature entitlements, credits, and usage limits, now repositioned as the "usage runtime" that decides what every AI request and agent action is allowed to cost.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, Tel Aviv, Israel (Verified — seed press April 2022 describes a Tel Aviv company; funding databases agree); GTM org now built out in New York (Reported — Series A release)
- **Website / GitHub:** https://www.stigg.io · https://github.com/stiggio · https://docs.stigg.io

## What they do

Stigg sits between your application code and your billing provider. Instead of hardcoding "Pro plan gets 10 seats and 50K tokens" into your codebase and duplicating it in Stripe, you model the catalog (plans, add-ons, features, usage allotments) in Stigg and query it at runtime: SDKs (TypeScript/Node, Python, Go, Ruby, C#, Java, React — all public on GitHub) answer entitlement checks ("can this customer use feature X? how much quota remains?"), report usage events, and drive paywalls/checkout, while Stigg syncs state bidirectionally with Stripe, Zuora, or your existing billing system — explicitly no rip-and-replace migration required (Verified — docs and site).

**Stigg 2.0**, announced June 28, 2026 at the AI Engineer World's Fair itself (Verified — PR Newswire, June 30), reframes this for AI products: a real-time credits engine with zero-overdraft balances (financial-grade wallet/ledger with burn-down rules, expiry, priority consumption); a governance layer evaluating budgets and limits across arbitrary dimensions (per-user, per-team, per-agent) in under 5ms; a metering pipeline claimed at 1M+ events/second; and — notably — an **MCP server so AI agents can check entitlements and report usage directly** (Reported — company announcement; performance claims are vendor-stated, not independently benchmarked). Deployment options: hosted cloud API, BYOC (components run in your VPC), and BYODB where the customer owns the data layer. Alongside 2.0 they acquired **Received.ai** (invoicing/contract management) and added an Airwallex integration giving early-stage startups free end-to-end billing (Reported — same announcement).

Engineer translation: it's the enforcement point for "should this request be allowed and what does it debit," decoupled from both your code and your invoice generation.

## Founders & origins

**Dor Sasson (CEO)** and **Anton Zagrebelny (CTO)**, both ex-New Relic, founded Stigg after experiencing how painful pricing/packaging changes were across engineering and GTM (Verified — TechCrunch, BusinessWire seed release, company site). Seed angels included monetization leaders from Snowflake, Calendly, New Relic, and Cloudinary's co-founder/CTO (Verified — BusinessWire).

## Funding

- **Seed, April 2022: $6.4M** — Unusual Ventures, Emerge Ventures, strategic angels (Verified — BusinessWire, FinSMEs).
- **Series A, December 2024: $17.5M** — led by Red Dot Capital Partners; Unusual Ventures, Emerge, Redseed, Cerca Partners participating (Verified — TechCrunch, SiliconANGLE, PR Newswire).
- **Total raised: $24M** (Verified — stated consistently across Series A coverage).

## Evidence of real-world use

Stronger than logos-on-a-page: named customers with published, quantified case studies — **Webflow** (replatformed homegrown billing; add-on rollout from months to ~4 hours; previously 500+ engineering hours/year on billing work — Reported, Stigg's own case study), **Miro** (AI credit model shipped in under 6 weeks; hybrid seat + usage model in 3 months — Reported, Stigg case study), plus **PagerDuty, AI21 Labs, Upwork, Productboard, Qlik, HackerOne, Oyster, 8x8** (Verified as claimed customers across TechCrunch, press releases, and site; depth of usage unverified for most). Series A coverage cited "billions of API calls and tens of millions in monthly subscriptions" managed (Reported — company figures). Public SDKs and example repos exist on GitHub, and there's a public free tier with a published Growth plan (~$249/mo per TechCrunch, 2024) — a real self-serve commercial product. Amusingly on-point: OpenAI's February 2026 write-up of its own real-time "decision waterfall" for credit checks — concluding third-party billing platforms couldn't decide in real time — is exactly the gap Stigg 2.0 claims to fill (Reported — cited in Stigg's 2.0 announcement; interpret as positioning).

## Relevance to agentic AI engineering

Stigg is the metering-and-authority layer of the agent stack: when an agent loop calls tools that consume paid resources, something must answer "is this action within budget?" at call time, not at invoice time. Per-agent budget caps enforced in-band are a commercial instance of the constrained-authority patterns in *Governance by Construction for Generalist Agents*, and the MCP server — agents checking their own entitlements as a tool call — extends the trajectory in *The Evolution of Tool Use in LLM Agents*. For anyone selling agent products (coding agents priced per task, voice agents per minute), this is the credits/entitlements plumbing under those business models.

## Use cases & considerations

Use cases: (1) launch usage/credit-based pricing for an AI product without building a ledger; (2) enforce per-customer/per-agent token budgets at request time via SDK or MCP; (3) decouple plan/packaging experiments from deploys; (4) keep Stripe for payments while outsourcing entitlements.

Considerations: your entitlement source of truth living in a Series A vendor is real lock-in (BYODB mitigates); sub-5ms and 1M events/sec are vendor claims; Stigg is *not* a payment processor — you still need Stripe et al. Competitors: **Metronome, Orb, Lago (OSS), Schematic, OpenMeter, Amberflo**, and Stripe's own Billing/Meters moving up-stack. Open questions: Received.ai integration maturity; whether the MCP entitlement-check pattern sees genuine adoption.

## Sources

- https://www.stigg.io/ · https://docs.stigg.io · https://github.com/stiggio
- https://techcrunch.com/2024/12/11/stigg-makes-it-easy-to-change-your-saas-pricing/
- https://siliconangle.com/2024/12/11/stigg-raises-17-5m-simplify-saas-platform-feature-pricing-models/
- https://www.prnewswire.com/news-releases/stigg-raises-17-5m-to-modernize-software-monetization-as-ai-reshapes-saas-pricing-302329067.html
- https://www.businesswire.com/news/home/20220420005937/en/Stigg-Raises-$6.4-Million-Seed-Round-to-Free-Developers-from-Building-and-Maintaining-SaaS-Pricing
- https://www.finsmes.com/2022/04/stigg-raises-6-4m-in-seed-funding.html
- https://www.prnewswire.com/il/news-releases/stigg-2-0-decides-what-every-ai-request-is-allowed-to-cost-in-under-five-milliseconds-302814528.html
- https://www.stigg.io/customers/miro
- https://www.stigg.io/blog-posts/beyond-limits-replatforming-webflows-monetization-infrastructure-with-stigg
- https://www.calcalistech.com/ctechnews/article/h1zbwmwnkg
