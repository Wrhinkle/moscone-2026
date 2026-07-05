# Circle

> Issuer of USDC, the second-largest dollar stablecoin, now building payment rails — wallets, micropayment protocols, and a purpose-built L1 — for AI agents that hold and spend money.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** gold
- **Founded:** October 2013, Boston, MA (Verified — Wikipedia, company history, press)
- **Website / GitHub:** https://www.circle.com · https://agents.circle.com · https://github.com/circlefin

## What they do

Core business: **USDC**, a fully-reserved dollar stablecoin (launched Sept 2018 via the Centre consortium with Coinbase; Circle took sole control in Aug 2023), plus **EURC**. Reserves sit in cash and short-dated Treasuries; Circle's revenue is mostly reserve interest income. Scale as of 2026: **~$77B USDC in circulation, $21.5T cumulative on-chain volume** (Reported — Circle earnings coverage via PYMNTS/blockchain.news). Public company since June 2025, NYSE: CRCL.

The developer platform is what matters for an engineer: **Circle Mint** (fiat on/off ramp for institutions), **CCTP** (native cross-chain USDC transfer), **Developer-Controlled Wallets** (API-managed custodial wallets using MPC so keys are never exposed), **Circle Gateway**, and **Paymaster** (gas abstraction — pay fees in USDC).

Two 2025–26 moves reposition Circle for the agentic economy:

- **Circle Agent Stack** (launched May 11, 2026 — Verified, press release + Businesswire + CoinDesk/Cointelegraph coverage): **Circle CLI** (a command interface designed to be driven by developers *or* agents), **Agent Wallets** (permissionless, policy-controlled wallets with predefined spending guardrails for autonomous agents), **Nanopayments** via Gateway (gas-free USDC transfers down to $0.000001 for machine-to-machine flows), and an **Agent Marketplace** (directory of agent-payable services). Live at agents.circle.com.
- **Arc**, an L1 blockchain purpose-built for stablecoin finance: testnet since Oct 2025 (150M+ transactions, ~0.5s settlement in the first 90 days — Reported, Circle/CoinGecko), **$222M token presale from BlackRock and Apollo at a ~$3B valuation** (Verified — CNBC), mainnet expected summer 2026 — i.e., not yet live as of 2026-07-02.

Circle also backs **x402**, the Coinbase-originated HTTP-402 payment standard (collaborators include AWS, Anthropic, Cloudflare), with published guides for autonomous agent payments using Circle Wallets + USDC + x402.

## Founders & origins

**Jeremy Allaire** (CEO) and **Sean Neville**, October 2013, as co-CEOs (Verified). Allaire's track record is unusually deep: co-founded Allaire Corp (ColdFusion) in 1995 with his brother JJ, IPO'd 1999, sold to Macromedia where he was CTO; founded Brightcove in 2004 and took it public in 2012. Neville stepped back to the board in late 2019, leaving Allaire sole CEO (Verified). Circle began as a consumer Bitcoin-payments app (Circle Pay, 2014) and pivoted to stablecoin infrastructure in 2018 — the "consumer" era is long gone.

## Funding

- ~**$1.1B raised privately** across venture rounds (Reported — Crunchbase via press), including $110M in May 2018 to build the stablecoin and a **$400M Series F (April 2022) at an $8B valuation** led by BlackRock and Fidelity (Verified).
- A 2021 SPAC merger at $9B was scrapped in late 2022 (Verified).
- **IPO June 5, 2025, NYSE: CRCL**: priced at $31, raised ~$1.1B, stock closed day one at $83.23 (+168%) — one of the largest IPO pops in decades (Verified — Fortune, Yahoo Finance).

## Evidence of real-world use

Strong and documented, well beyond logos: **Nubank** (25% of first-time crypto buyers in Brazil choose USDC — Circle case study), **Stripe** (stablecoin payments use USDC), **Visa** (USDC settlement in the US — Visa press release), **Grab** (Singapore Web3 pilot), remittance operators **Félix** (US→Mexico, distributed inside Nubank and Mercado Pago), **Thunes**, **Coins.ph**, **BCRemit**. Coinbase is a deep distribution partner. $21.5T in on-chain volume is the strongest single usage signal. Agent Stack itself is <2 months old at write time — real agent-payments adoption is Unverified.

## Relevance to agentic AI engineering

Circle is a candidate settlement layer for the agent stack: when an agent must pay per API call, x402 + Nanopayments is the crypto-rails answer to Stripe/PayPal's card-rails answer. Agent Wallets' policy guardrails are a production instance of the constrained-authority problem in *Governance by Construction for Generalist Agents* — spending is the canonical irreversible action. Circle CLI as an agent-drivable surface fits the trajectory in *The Evolution of Tool Use in LLM Agents*. Cross-session agent identity/balance held in a wallet touches the agent-memory line of work.

## Use cases & considerations

Use cases: (1) metered agent-to-API payments via x402 + USDC instead of API-key billing; (2) give a back-office or procurement agent a policy-bounded Agent Wallet rather than a stored card; (3) sub-cent machine-to-machine settlement (Nanopayments) where card economics fail; (4) programmatic cross-border payouts via CCTP/Mint.

Considerations: Agent Stack is brand new — expect API churn; Arc mainnet unshipped. Business concentration risk: revenue is interest-rate-sensitive reserve income. Competitors: **Tether** (larger stablecoin, weaker compliance posture), **PayPal PYUSD**, **Stripe/Bridge**, **Coinbase** (partner *and* competitor via CDP wallets), and card-network agent rails (Visa Intelligent Commerce, Mastercard Agent Pay). The agent-payments protocol war (x402 vs ACP vs AP2) is unresolved; Circle hedges but is clearly crypto-rails-first. Regulatory footing is comparatively strong post-GENIUS-era US stablecoin rules, but jurisdiction-by-jurisdiction compliance still lands on the builder.

## Sources

- https://en.wikipedia.org/wiki/Circle_(company) · https://en.wikipedia.org/wiki/Jeremy_Allaire
- https://www.circle.com/pressroom/circle-launches-ai-infrastructure-to-power-the-agentic-economy
- https://www.circle.com/blog/introducing-circle-agent-stack-financial-infrastructure-for-the-agentic-economy
- https://www.businesswire.com/news/home/20260511078086/en/Circle-Launches-AI-Infrastructure-to-Power-the-Agentic-Economy
- https://www.cnbc.com/2026/05/11/circle-closes-222-million-from-blackrock-apollo-for-arc-blockchain.html
- https://www.coindesk.com/business/2026/05/11/i-don-t-think-that-s-crazy-here-is-why-circle-is-betting-on-new-usd3-billion-blockchain
- https://fortune.com/2025/06/04/circle-ipo-share-price-31/ · https://fortune.com/2025/06/06/circle-internet-group-ipo-crcl-underpricing-stock-outlook-profits/
- https://www.circle.com/blog/autonomous-payments-using-circle-wallets-usdc-and-x402
- https://www.coinbase.com/developer-platform/discover/launches/x402 · https://blog.cloudflare.com/x402/
- https://www.circle.com/case-studies/nubank · https://www.circle.com/case-studies/felix · https://www.circle.com/case-studies/thunes
- https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.21951.html
- https://www.coingecko.com/learn/what-is-arc-stablechain
- https://www.pymnts.com/earnings/2026/circle-chases-agentic-growth-scale-stablecoin-infrastructure/
