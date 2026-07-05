# Coinbase

> Public crypto exchange whose Developer Platform now ships wallet and payments infrastructure purpose-built for autonomous AI agents.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** supporting
- **Founded:** 2012, San Francisco, CA (Verified)
- **Website / GitHub:** https://www.coinbase.com/developer-platform · https://github.com/coinbase/agentkit

## What they do
Beyond its core exchange, Coinbase's relevant surface for AI engineers is the **Coinbase Developer Platform (CDP)**: **AgentKit**, an open-source, framework- and wallet-agnostic SDK that gives an AI agent its own crypto wallet and on-chain transaction ability (works with LangChain, Vercel AI SDK, OpenAI Agents SDK, etc., in Python and TypeScript); and **x402**, an open payments protocol (co-created with Cloudflare) that reactivates the HTTP 402 status code to let agents pay per-request for APIs/resources autonomously, machine-to-machine, without human checkout. Coinbase reports x402 has processed 50M+ transactions. "Agentic Wallets" extends this with built-in spending/earning guardrails for autonomous agents.

## Founders & funding
Founded by Brian Armstrong (ex-Airbnb engineer, Y Combinator) and Fred Ehrsam (ex-Goldman Sachs); Ehrsam left operating role in 2017 but remains a board member/shareholder (Verified). Raised ~$547M privately (seed via YC, Series A led by USV, Series B led by a16z) before going public via direct listing on Nasdaq in April 2021 (Verified, Wikipedia/Crunchbase).

## Evidence of real-world use
AgentKit has 1.3k GitHub stars, 749 forks, and published PyPI/npm packages (Verified via repo). x402 has a named integration with Sam Altman's World (World ID + AgentKit beta, announced March 2026) for agent identity verification — a concrete third-party production use case (Verified, CoinDesk/The Block).

## Relevance to agentic AI engineering
Directly relevant to the "agents that transact" layer of the stack: tool-calling agents need payment rails and identity/authorization primitives to act autonomously in the real world, which is exactly what AgentKit/x402 target — adjacent to this repo's fintech-payments and security-identity themes.

## Sources
- https://www.coinbase.com/developer-platform/products/agentkit
- https://github.com/coinbase/agentkit
- https://www.coindesk.com/tech/2026/03/17/sam-altman-s-world-teams-up-with-coinbase-to-prove-there-is-a-real-person-behind-every-ai-transaction
- https://en.wikipedia.org/wiki/Coinbase
- https://www.ai.engineer/worldsfair/2026
