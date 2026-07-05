# PayPal

> Global payments network (wallet, checkout, Venmo, Braintree processing, PYUSD stablecoin) now repositioning as the payment and merchant-catalog rail for AI shopping agents.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** platinum
- **Founded:** 1998 (as Confinity), Palo Alto, CA; merged with X.com in 2000, renamed PayPal 2001 (Verified — extensively documented)
- **Website / GitHub:** https://www.paypal.com · https://www.paypal.ai · https://github.com/paypal/agent-toolkit

## What they do

Core business: two-sided payments — a consumer wallet/checkout (PayPal, Venmo, buy-now-pay-later, Fastlane guest checkout, Honey/rewards) and merchant processing (Braintree, Zettle, Hyperwallet payouts), plus **PYUSD**, a Paxos-issued regulated stablecoin (launched Aug 2023, now multi-chain). Scale, from Q1 2026 earnings (Verified — SEC 8-K): TPV **$464B in a single quarter** (up 11% YoY), **439M active accounts**, ~225M monthly actives, revenue up 7%. Public company, NASDAQ: PYPL, spun back out of eBay in 2015.

The AIEWF-relevant layer is **agentic commerce infrastructure**, built out fast since April 2025:

- **PayPal Agent Toolkit + remote MCP servers** (April 2025, PayPal Dev Days): open-source library (github.com/paypal/agent-toolkit, TypeScript first) exposing payments, invoicing, disputes, shipment tracking, catalog, subscriptions, and reporting APIs as tool calls. Framework adapters for MCP, OpenAI Agents SDK, LangChain, CrewAI, Vercel AI SDK, Amazon Bedrock. PayPal claims the industry's first *remote* MCP server for payments (Reported — their dev blog; plausible on timing). Docs at paypal.ai/docs.
- **Agentic Commerce Services** (announced Oct 28, 2025): **Agent Ready** — existing PayPal merchants can accept payments initiated by AI agents (conversational or browser-automated) with PayPal's fraud detection, buyer protection, and dispute resolution, "no additional technical lift"; GA early 2026. **Store Sync** — pushes merchant catalogs/inventory into AI discovery surfaces and drops orders back into existing fulfillment systems; launch integrations via Wix, Cymbio, Commerce (BigCommerce/Feedonomics), Shopware (Verified — press release + independent coverage).
- **Protocol posture:** adopted OpenAI's **Agentic Commerce Protocol (ACP)**, supports OpenAI's delegated payments API, participates in the Google-led **AP2** agent-payments standards group, and has a merchant-side agentic solution with Google Cloud (Verified/Reported mix — the ACP and Google Cloud items are Verified).

Engineer translation: PayPal is selling "don't integrate every agent surface — integrate us," acting as the aggregation, trust, and settlement layer between agents (ChatGPT, Perplexity, Copilot) and tens of millions of merchants.

## Founders & origins

Confinity founded Dec 1998 by **Max Levchin, Peter Thiel, and Luke Nosek** (Ken Howery and Yu Pan also credited as co-founders); merged March 2000 with **Elon Musk's** X.com; the combined company became PayPal — the origin of the "PayPal Mafia" (Verified). IPO Feb 2002; acquired by eBay for ~$1.5B in Oct 2002; independent again July 2015. Current CEO: **Alex Chriss** (ex-Intuit), since Sept 2023, who drove the agentic pivot (Verified).

## Funding

Public company — venture history is ancient and moot. NASDAQ: PYPL; Q1 2026 revenue up 7% YoY on $464B quarterly TPV (Verified — 8-K). No recent capital raises relevant to evaluation.

## Evidence of real-world use

The base network is among the most-used fintech systems on earth (439M active accounts — Verified). For the *agentic* products specifically, evidence is early but concrete and shipping, not vaporware:

- **OpenAI partnership (Oct 28, 2025, Verified — joint press release):** PayPal wallet inside ChatGPT Instant Checkout; PayPal processes card payments for Instant Checkout merchants via the delegated payments API; PayPal's ACP server to bring its merchant catalogs into ChatGPT during 2026 without per-merchant integrations. PayPal also rolled out ChatGPT Enterprise + Codex to its 24,000+ employees.
- **Perplexity (Verified):** partnership announced May 2025; **Instant Buy** launched Nov 2025 before Black Friday — in-chat checkout with PayPal/Venmo, PayPal merchants as merchant of record. Named early brands: Abercrombie & Fitch, Ashley, Fabletics, Adorama, Newegg.
- Agent Ready GA "early 2026" was the promise; treat current GA status as Reported. GitHub star counts for agent-toolkit: not confirmed in sources checked.

## Relevance to agentic AI engineering

PayPal is the money-movement tool call in the agent stack. Its MCP/toolkit design — scoped, auditable financial actions exposed to LLMs — is a live industrial case of the trajectory in *The Evolution of Tool Use in LLM Agents*, and the hardest version of the problem *Governance by Construction for Generalist Agents* addresses: irreversible, regulated actions (payments, disputes) demand constrained authority, delegation tokens, and audit trails by design (ACP's delegated payments API is exactly that shape). Conversational/voice shopping checkouts raise the verification problems in *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*; and agent memory research maps onto cross-session shopper preference/identity carried by the wallet.

## Use cases & considerations

Use cases: (1) give a commerce or back-office agent invoicing/refund/dispute/tracking tools via the MCP server instead of hand-wrapping REST APIs; (2) accept agent-originated checkout (ACP/Agent Ready) as a merchant without building per-surface integrations; (3) surface a product catalog to ChatGPT/Perplexity via Store Sync; (4) PYUSD for programmatic agent-to-agent settlement (speculative, PayPal-promoted).

Considerations: protocol war in progress — OpenAI/Stripe's ACP vs Google's AP2 vs Visa (Intelligent Commerce) and Mastercard (Agent Pay); PayPal hedges across several, but a builder betting on one interface today carries churn risk. Competitors: **Stripe** (its agent toolkit + ACP co-authorship), **Visa/Mastercard** agent rails, **Shopify** on catalogs, **Coinbase x402/crypto rails** for machine payments. Fraud/chargeback liability rules for agent-initiated purchases are still settling. Toolkit is TypeScript-first (Python "coming soon" per docs — check status). Underlying business is a low-growth incumbent; agentic revenue is not yet material in reported numbers.

## Sources

- https://newsroom.paypal-corp.com/2025-10-28-OpenAI-and-PayPal-Team-Up-to-Power-Instant-Checkout-and-Agentic-Commerce-in-ChatGPT
- https://newsroom.paypal-corp.com/2025-10-28-PayPal-Launches-Agentic-Commerce-Services-to-Power-AI-Driven-Shopping
- https://newsroom.paypal-corp.com/2025-11-PayPal-and-Perplexity-Launch-Instant-Buy
- https://about.pypl.com/news-details/2025/Perplexity-Selects-PayPal-to-Power-Agentic-Commerce/default.aspx
- https://developer.paypal.com/community/blog/paypal-agentic-ai-toolkit/ · https://developer.paypal.com/community/blog/paypal-model-context-protocol/
- https://github.com/paypal/agent-toolkit · https://www.paypal.ai/ · https://developer.paypal.com/store-sync/overview
- https://www.sec.gov/Archives/edgar/data/0001633917/000163391726000065/pypl1q-26earningsrelease.htm (Q1 2026 8-K)
- https://techcrunch.com/2025/10/28/paypal-partners-with-openai-to-let-users-pay-for-their-shopping-within-chatgpt/
- https://www.cnbc.com/2025/11/19/perplexity-ai-online-shopping-paypal.html
- https://cloud.google.com/blog/topics/financial-services/introducing-an-agentic-commerce-solution-for-merchants-from-paypal-and-google-cloud
- https://www.digitalcommerce360.com/2025/10/28/paypal-agentic-commerce-ai-driven-shopping-services/
