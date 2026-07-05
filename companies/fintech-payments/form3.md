# Form3

> Cloud-native payments infrastructure: a single API layer that connects banks and fintechs to the world's clearing and settlement schemes.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** supporting
- **Founded:** 2016, London, UK (Verified)
- **Website / GitHub:** https://www.form3.tech

## What they do
Form3 runs a cloud microservices platform that abstracts away the plumbing of payment schemes (Faster Payments, BACS, SEPA, CHAPS, card rails, etc.) behind a single API, handling connectivity, processing, clearing, and settlement so banks and neobanks don't have to integrate with each scheme directly. It's payments-as-infrastructure — the kind of system an AI/back-office engineer would call from an agent that needs to move money or reconcile transactions, rather than a tool an AI engineer builds with directly. One-line founders/funding note: co-founded 2016 by Mike Walters, Michael Mueller, and CTO Steve Cook; a Series C including Visa, Goldman Sachs, Mastercard, and Barclays reached $220M total, with a September 2024 $60M tranche valuing the company at ~$570M, and ~$278M raised overall across 9 rounds (Verified, Crunchbase/TechCrunch).

## Evidence of real-world use
Named customers include neobanks Klarna, N26, and SumUp plus multiple banking-as-a-service providers building on Form3's APIs — concrete production usage, not just landing-page logos (Verified, TechCrunch).

## Relevance to agentic AI engineering
Relevant to the fintech/back-office agent stack as the payment-execution layer an agent orchestrates against (e.g., an AI ops agent triggering a settlement) rather than an AI-native product itself; watch for whether they expose agent/MCP-friendly APIs going forward.

## Sources
- https://www.form3.tech/
- https://techcrunch.com/2024/09/10/form3-a-quiet-giant-in-uk-fintech-raises-60m-at-a-570m-valuation/
- https://www.crunchbase.com/organization/form3-financial-cloud
