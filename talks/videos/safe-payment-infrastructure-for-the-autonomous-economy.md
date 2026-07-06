# Building safe Payment Infrastructure for the autonomous economy
> Stripe's three building blocks for letting agents spend money safely: shared payment tokens, a 402-based machine payments protocol, and the Agentic Commerce Protocol.

- **Speaker:** Steve Kaliski, Stripe
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=KLSuFPj2ld0) (AI Engineer channel; ~19m, released 2026-06-06)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Kaliski, a principal software engineer at Stripe who led its card issuing team for four years and has spent the last two on agent payments, opens with the one-line takeaway: discovery and exploration benefit from non-determinism, but credentials, payments, and checkout require determinism. Agents are already economic actors, he notes; every Claude Code or Codex session spends money, just proxied through a subscription to a single vendor. The question is how to extend that to arbitrary businesses and payment methods.

He enumerates four failure modes when an agent operates a checkout page like a human: buying from the wrong place (a lookalike domain), buying the wrong thing, spending the wrong amount (currency drift, taxes, misparsed prices), and mishandling the credential itself. Pasting a raw card number into a browser automation gives no way to enforce limits and full exposure if anything upstream was wrong.

The first fix is shared payment tokens. An agent holds a credential collected from its human operator and shares a scoped token with a specific seller, encoding a mandate: this Visa card works only for this seller, only up to $25, only for 30 days. In the demo, a seller with a $50 payment intent gets declined by Stripe because the request exceeds the mandated amount, then succeeds at the lower price. The seller still receives brand, last four, and credit type, so existing risk systems keep working. Tokens span hundreds of payment method types and every use is auditable. In Q&A Kaliski confirms Stripe's recurring flows work like an OAuth access-and-refresh pattern on the same credential, and that Stripe's agent-facing product is built on these primitives.

The second piece, built with Tempo, is the machine payments protocol. Tool calls are HTTP requests, so a server can return a 402 status code with an encoded payload describing what is being bought, who gets paid, and how. The demo curls a protected endpoint, gets the 402, approves a one-cent payment in pathUSD on the Tempo blockchain, and retries successfully. Stripe supports several networks including Base and Tempo; transaction data lives on chain and Stripe replicates a product view of it.

The third piece is the Agentic Commerce Protocol, built with OpenAI: a standard set of APIs and objects describing how checkouts work, so the seller relays cart state as structured data rather than the agent scraping a UI. The demo uses Stripe Press, Stripe's book store, exposing its product catalog as JSON and running a checkout where every quantity change, shipping choice, and payment happens as an explicit request and response. Kaliski's closing advice to builders: keep discovery non-deterministic, make your product agent-friendly with structured flows, and push payments toward exclusively deterministic rails so the blast radius of a confused agent stays small.

## Notable moments
- [0:00:14](https://www.youtube.com/watch?v=KLSuFPj2ld0&t=14s) The thesis: discovery benefits from non-determinism, payments require determinism.
- [0:07:18](https://www.youtube.com/watch?v=KLSuFPj2ld0&t=438s) Shared payment token demo: Stripe declines a $50 charge against a $25 mandate.
- [0:09:20](https://www.youtube.com/watch?v=KLSuFPj2ld0&t=560s) The 402 flow: a tool call returns payment-required, the agent pays a penny on Tempo, and the call succeeds.
- [0:11:21](https://www.youtube.com/watch?v=KLSuFPj2ld0&t=681s) Agentic Commerce Protocol demo against Stripe Press with the raw request log alongside the chat UI.

## Connections
- [Stripe](../../companies/fintech-payments/stripe.md): company profile covering the agentic commerce protocol and agent payment rails this talk demos from the inside.
- [PayPal](../../companies/fintech-payments/paypal.md): the direct competitor positioning itself as the payment and merchant-catalog rail for AI shopping agents.
- [Coinbase](../../companies/fintech-payments/coinbase.md): ships the competing crypto-native wallet and payments stack for autonomous agents, adjacent to the Tempo and Base flows shown here.
- [OpenAI](../../companies/models-inference/openai.md): co-author of the Agentic Commerce Protocol described in the talk.
