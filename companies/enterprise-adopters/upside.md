# Upside (GetUpside)

> A consumer cash-back app that pays retailers' marketing budgets to shoppers, using machine learning to price the incentive for each individual transaction.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** Not precisely dated in public sources; operating as Upside Services, Inc. (Washington DC area). (Unverified year)
- **Website / GitHub:** https://www.upside.com — no public GitHub found

## What they do
Upside (formerly GetUpside) is a consumer app claiming 5M+ users earning cash back on gas, groceries, and dining at ~45,000 partner merchants (Shell, BP, Circle K, Domino's, Taco Bell, etc.). The engineering-relevant core is not the coupon UX but the pricing engine behind it: Upside's ML platform computes a "margin-bound" personalized offer per customer per visit — the minimum incentive needed to change that specific person's buying behavior — rather than a flat rewards rate. That is a real-time, per-user dynamic-pricing/propensity model running against transaction and location data, with retailers guaranteed a fixed profit margin on every redemption. This is a note on disambiguation: a separate, unrelated company also uses the name "Upside" (upside.tech, "the data layer for agentic GTM," an MCP-integrated revenue-intelligence tool for B2B sales teams). Given this profile's assigned category (enterprise-adopters) and hint (consumer rewards/data company), this profile covers GetUpside/Upside.com, not upside.tech.

## Founders & origins
Not found in detail from primary sources within this research pass; secondary aggregators (Tracxn) name Alex Kinnier and Scott Case as co-founders/co-CEOs, Kinnier ex-Google. (Reported, single-source-class aggregator; not independently verified here.)

## Funding
Reported (secondary sources): ~$250M raised across 6 rounds, including a $165M round led by General Catalyst at a reported $1.5B valuation; investors reportedly include Bessemer Venture Partners and Vista Equity Partners. Not verified against a primary press release in this pass — treat as Reported, not Verified.

## Evidence of real-world use
Verified via company blog/press: personalization case studies (Progressive Grocer, CSP Daily News) describing live dynamic-offer machine learning in production across grocery and fuel retail, plus a stated $1B+ cumulative cash back paid and 550k+ app store reviews at 4.8 stars — real consumer-scale usage, not just a landing-page claim.

## Relevance to agentic AI engineering
Limited direct relevance to agent tooling/stacks; relevant mainly as a case study in production ML-driven pricing/personalization at consumer scale (real-time inference, guardrailed optimization against a margin constraint) — adjacent to evals/observability concerns around live decisioning systems rather than to agent orchestration, memory, or tool-calling.

## Sources
- https://www.upside.com/
- https://www.upside.com/blog/how-getupside-personalizes-the-grocery-experience
- https://progressivegrocer.com/how-getupside-personalizes-grocery-experience
- https://www.cspdailynews.com/technologyservices/getupside-offers-personalization-maximize-profits
- https://tracxn.com/d/companies/upside/__o79gPvcnSguxiyATR0v6jgiqSE2YTDPleKcvCwL0I5Q
- https://www.restaurantbusinessonline.com/technology/upside-raises-165m-cash-back-restaurant-app
- (disambiguation candidate, not covered here) https://www.upside.tech/
