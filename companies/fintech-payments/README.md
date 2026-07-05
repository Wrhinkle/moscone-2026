# Fintech & Payments

**Category definition:** Payments, cards, stablecoins, billing/monetization/entitlements.

This category exists because agents that *do things* eventually have to *pay for things* — or decide what a request is allowed to cost. Money movement is the sharpest version of the tool-call problem: actions are irreversible, regulated, and fraud-prone, so every company here is converging on the same primitives from different directions — scoped tool access (MCP servers over payment APIs), delegated/constrained credentials (single-use virtual cards, policy-bounded agent wallets, delegated payment tokens), and in-band budget enforcement (entitlement checks and credit ledgers evaluated at request time, not invoice time). The unresolved fight underneath all of it is the agent-payments protocol war: OpenAI/Stripe's **ACP** vs Google-led **AP2** vs Coinbase/Circle's crypto-native **x402**, with Visa and Mastercard running their own rails.

## How to read this category

Start with **[Stripe](stripe.md)** and **[PayPal](paypal.md)** — the two incumbents running nearly mirror-image agentic-commerce strategies (protocol + merchant aggregation + MCP toolkit), and between them they define the card-rails side of the protocol war. Then read **[Coinbase](coinbase.md)** and **[Circle](circle.md)** together as the crypto-rails counterargument: x402 machine-to-machine micropayments where card economics (2.9% + 30¢) simply can't go.

The rest of the category splits along a second axis — *moving money* vs *metering money*. **[Ramp](ramp.md)** and **[Form3](form3.md)** are money-movement platforms an agent orchestrates (Ramp is also the best live case study of agents making consequential financial decisions in production). **[Stigg](stigg.md)** and **[Revenium](revenium.md)** don't move money at all: they answer "is this AI request within budget, and what does it debit?" — the entitlements/FinOps layer under every usage-priced agent product.

## Companies

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [PayPal](paypal.md) | Global payments network repositioning as the payment and merchant-catalog rail for AI shopping agents | Platinum | Public (NASDAQ: PYPL) | $464B TPV in Q1 2026 alone; PayPal wallet is live inside ChatGPT Instant Checkout, and Perplexity's Instant Buy shipped before Black Friday 2025 |
| [Stripe](stripe.md) | Internet payments infrastructure now building the default money-movement rails for agents (ACP, hosted MCP, Issuing) | Supporting | Private, $159B tender-offer mark (Feb 2026) | $1.9T processed in 2025; co-authored the Agentic Commerce Protocol with OpenAI and bought Metronome (~$1B) for usage-based AI billing |
| [Circle](circle.md) | USDC issuer building agent wallets, sub-cent nanopayments, and a purpose-built L1 for machine-to-machine settlement | Gold | Public (NYSE: CRCL, June 2025 IPO) | Nanopayments settle USDC transfers down to $0.000001 — three orders of magnitude below where card economics work |
| [Coinbase](coinbase.md) | Crypto exchange whose Developer Platform ships wallets (AgentKit) and the x402 pay-per-request protocol for autonomous agents | Supporting | Public (NASDAQ: COIN, 2021 direct listing) | x402 revives HTTP status code 402 for agent micropayments and has reportedly processed 50M+ transactions |
| [Ramp](ramp.md) | Corporate cards + expense/AP/procurement, with production AI agents approving expenses and coding transactions to the ERP | Supporting | Private, $44B Series F (June 2026) | Its approval agents autonomously accept/reject real expenses with rationale — one of the clearest live examples of agents taking irreversible financial actions under policy |
| [Stigg](stigg.md) | Runtime entitlements/credits engine deciding what every AI request and agent action is allowed to cost | Gold | Series A, $24M total raised | Stigg 2.0 (announced at AIEWF itself) ships an MCP server so agents can check their own entitlements and report usage as tool calls |
| [Revenium](revenium.md) | No-code-change metering, budget limits, and anomaly/loop detection for AI spend across providers | Silver | $25.4M raised (latest Nov 2025) | Auto-shutoff for runaway/looping agents; joined the FinOps Foundation in June 2026 to push AI-spend governance standards |
| [Form3](form3.md) | Cloud-native single-API access to bank clearing and settlement schemes (Faster Payments, SEPA, BACS, CHAPS) | Supporting | ~$278M raised; ~$570M valuation (2024), Visa/Mastercard/Goldman on the cap table | The bank-grade settlement plumbing under neobanks like Klarna and N26 — the execution layer a money-moving agent ultimately calls |

**Expected vs. found:** all seven expected profiles (PayPal, Stigg, Revenium, Coinbase, Form3, Ramp, Stripe) are present, plus **Circle**, filed here as the stablecoin-infrastructure counterpart to Coinbase. Nothing is missing.

## Related papers

- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — the theory behind what this whole category builds in practice: constrained authority, delegation tokens, and audit trails for irreversible actions. Cited by nearly every profile here (Stripe's delegated payment tokens, Circle's policy-bounded Agent Wallets, Stigg's per-agent budget caps, Ramp's policy-enforced approvals).
- [The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — the MCP servers from PayPal, Stripe, Ramp, Stigg, and Circle's agent-drivable CLI are live industrial instances of this trajectory.
- [Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) — maps to wallet-held cross-session shopper identity (PayPal, Stripe) and Ramp's agents retaining vendor history and approval precedent.
- [Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md) — Ramp's `ramp-mcp` ETL-to-SQLite pattern is a pragmatic production answer to this paper's retrieval question.
- [From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation](../../papers/voice-realtime/from-text-to-voice-a-reproducible-and-verifiable-framework.md) — conversational/voice shopping checkout (PayPal, Stripe) is exactly the high-stakes voice tool-calling this framework evaluates.

## Open questions

1. **Which protocol wins — or do agents end up multi-homing?** ACP (Stripe/OpenAI) vs AP2 (Google) vs x402 (Coinbase/Circle) vs Visa/Mastercard rails is unresolved; every builder integration today carries churn risk, and every incumbent here is hedging across several.
2. **Is agent-mediated checkout volume real yet?** Instant Checkout, Agent Ready, and Instant Buy are live, but no company has published independently verified agent-originated payment volume — the numbers that exist are launch commitments and vendor claims.
3. **Who eats the fraud/chargeback liability for agent-initiated purchases?** The rules are still settling, and the answer determines whether merchants trust agent traffic at all.
4. **Do sub-cent machine-to-machine payments find product-market fit?** Circle's Nanopayments and Coinbase's x402 bet that agents paying per API call becomes a real economy; card-rail incumbents bet it stays niche.
5. **Does the "entitlement check as a tool call" pattern (Stigg's MCP server, Revenium's in-band budgets) see genuine adoption**, or does budget enforcement stay in the gateway/proxy layer?
6. **Are the vendor accuracy claims survivable?** Ramp's 99% policy-enforcement accuracy and Stigg's sub-5ms/1M-events-per-second figures are all self-reported; no independent benchmarks exist for any agentic-finance product in this category.
