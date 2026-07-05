# Stripe

> Internet payments infrastructure at $1.9T/year scale, now building the default money-movement rails for AI agents: an agentic commerce protocol, an MCP server for its APIs, and usage-based billing for AI products.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** supporting
- **Founded:** 2010, Palo Alto (via Y Combinator); dual HQ South San Francisco + Dublin (Verified — extensively documented)
- **Website / GitHub:** https://stripe.com · https://github.com/stripe · https://github.com/stripe/ai · https://docs.stripe.com/mcp

## What they do

Core business: a payments API suite — card acquiring/checkout, Connect (marketplace payouts), Billing (subscriptions and metered usage), Issuing (programmatic virtual cards), Radar (ML fraud detection), plus Atlas, Treasury, Terminal, and stablecoin rails. Private company; total payment volume was **$1.9 trillion in 2025, up 34% YoY** (Verified — Stripe annual letter + press coverage). Public per-transaction pricing (2.9% + 30¢ baseline) — a real, self-serve commercial product, not enterprise vaporware.

The AIEWF-relevant layer has three parts:

- **Agentic Commerce Protocol (ACP)** — co-developed with OpenAI, announced Sept 2025; the open standard behind **Instant Checkout in ChatGPT**. Stripe positions ACP as the programmatic commerce flow between agents and merchants, with delegated/shared payment tokens so an agent never holds raw card credentials (Verified — Stripe + OpenAI announcements, wide coverage).
- **Agentic Commerce Suite** (launched 2026): a single integration for merchants covering product discovery by agents, agentic checkout, payments, fraud screening, and order-event webhooks back into existing commerce stacks (Verified — Stripe newsroom + Forrester coverage of Sessions 2026).
- **Developer tooling for agents:** the **Stripe Agent Toolkit** (`stripe-agent-toolkit` on pip, `@stripe/agent-toolkit` on npm) wraps Stripe APIs as function-callable tools for OpenAI Agents SDK, LangChain, CrewAI, Vercel AI SDK; a **hosted, OAuth-authenticated MCP server at mcp.stripe.com** exposes ~25 payment operations plus docs search (Verified — Stripe docs + GitHub). Issuing provides single-use virtual cards with programmatic spend controls for agent purchases.

Adjacent bets: a **Payments Foundation Model** — a transformer trained on tens of billions of transactions, used to improve fraud/card-testing detection (Reported — Stripe's own Sessions 2025 announcement); and **Tempo**, a payments-specific L1 blockchain joint venture with Paradigm aimed at sub-cent machine-to-machine settlement (Verified as a JV, not an acquisition).

## Founders & origins

**Patrick Collison** (CEO) and **John Collison** (President), brothers from Limerick, Ireland. Dropped out of MIT and Harvard respectively; previously built Auctomatic (out of their company Shuppa), sold to Live Current Media for $5M in 2008 when they were 19 and 17. Started Stripe (originally /dev/payments) in 2010, went through Y Combinator the same year (Verified — Wikipedia, YC library, multiple profiles).

## Funding

Not a startup in any meaningful sense. ~$9.8B raised across ~24 rounds (Reported — Crunchbase-derived sources); $2M seed in 2011 from Thiel, Musk, Sequoia, a16z, SV Angel (Verified). Recent valuation marks came via employee tender offers, not primaries: **$91.5B (Feb 2025) → $106.7B (Sept 2025) → $159B (Feb 2026)**, with Thrive Capital, Coatue, and a16z buying (Verified — CNBC, TechCrunch, Payments Dive). No IPO planned; leadership says it isn't a priority (Reported — TechCrunch quoting Collison).

## Evidence of real-world use

The base platform is one of the most-integrated APIs on the internet (millions of businesses; OpenAI's ChatGPT subscriptions run on Stripe — Verified via checkout flows and coverage). For the agentic products specifically: Instant Checkout in ChatGPT is live with Etsy and Shopify-ecosystem merchants (Verified); Agentic Commerce Suite launch adopters include **Coach, Kate Spade, URBN (Anthropologie/Urban Outfitters/Free People), Revolve, Ashley Furniture, ABT Electronics**, and platforms **Squarespace, Wix, Etsy, WooCommerce, commercetools, BigCommerce** (Reported — Stripe's launch press release; treat as commitments, not yet documented volume). The MCP server and agent toolkit have real community usage (third-party tutorials, Composio/PulseMCP listings). Metronome — acquired ~$1B, closed Jan 2026 — is the billing engine behind many usage-priced AI products (Verified — Stripe newsroom, Payments Dive).

## Relevance to agentic AI engineering

Stripe is the canonical "irreversible action" tool call. Its MCP server and toolkit are live industrial instances of the trajectory in *The Evolution of Tool Use in LLM Agents*, and payments are the sharpest test case for *Governance by Construction for Generalist Agents*: ACP's delegated payment tokens, Issuing's single-use cards with spend limits, and OAuth-scoped MCP access are governance-by-construction patterns, not prompts. Voice-commerce checkout intersects with *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*; agent memory research maps onto wallet-held cross-session purchase preferences; and Metronome-style token-metered billing is how agentic SWE products (the ones agentic SWE benchmarks measure) actually monetize.

## Use cases & considerations

Use cases: (1) give a back-office or ops agent scoped payment/invoice/refund tools via mcp.stripe.com instead of hand-wrapping REST; (2) accept agent-originated checkout (ACP) as a merchant with one integration; (3) meter and bill an AI product per-token/per-run via Billing/Metronome; (4) issue constrained virtual cards so a procurement agent can actually buy things.

Considerations: the agent-payments protocol war is unresolved — Stripe/OpenAI's ACP vs Google-led AP2, Visa Intelligent Commerce, Mastercard Agent Pay, Coinbase's x402; betting on one interface carries churn risk. Stripe lock-in is real (proprietary tokens, fee structure at 2.9%+ hurts thin-margin agent microtransactions — hence Tempo). Main competitors: **PayPal** (also an AIEWF 2026 sponsor, nearly mirror-image agentic strategy), **Adyen**, card networks' agent rails. Liability rules for agent-initiated purchases and fraud are still settling. Open question: whether agent-mediated checkout volume becomes material or stays demo-scale in 2026.

## Sources

- https://stripe.com/blog/agentic-commerce-suite · https://stripe.com/newsroom/news/agentic-commerce-suite
- https://stripe.com/use-cases/agentic-commerce
- https://docs.stripe.com/mcp · https://github.com/stripe/ai
- https://www.cnbc.com/2026/02/24/stripe-value-stock-sale-tender-offer.html
- https://techcrunch.com/2026/02/24/stripes-valuation-soars-74-to-159-billion/
- https://www.paymentsdive.com/news/stripe-valued-at-159b-in-tender-offer-ipo-payments/812883/
- https://stripe.com/newsroom/news/stripe-2025-update (annual letter, tender offer)
- https://stripe.com/newsroom/news/stripe-completes-metronome-acquisition · https://www.paymentsdive.com/news/stripe-to-buy-metronome/807055/
- https://www.forrester.com/blogs/stripe-sessions-2026-stripe-is-rearchitecting-payments-for-an-agentic-ai-economy/
- https://www.siliconrepublic.com/business/stripes-crypto-joint-venture-tempo-launches-payments-protocol-for-ai
- https://en.wikipedia.org/wiki/Patrick_Collison · https://www.ycombinator.com/library/Kx-patrick-john-collison-co-founders-of-stripe
- https://news.crunchbase.com/fintech/unicorn-stripe-secondary-sale-valuation/
