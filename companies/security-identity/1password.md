# 1Password

> Password/secrets manager pivoting into an identity-and-access platform for humans *and* AI agents.

- **Category:** security-identity
- **AIEWF 2026 tier:** silver
- **Founded:** 2005, Toronto/Canada area (AgileBits) — Verified
- **Website / GitHub:** https://1password.com | https://github.com/1Password

## What they do
1Password is the well-known consumer/enterprise password manager, now extended with **Unified Access**, a platform for discovering, authenticating, and auditing AI agents alongside human users. For engineers, the relevant surface is credential/secrets delivery to agents at runtime (via Go/Python/JS SDKs) instead of `.env` files or hardcoded keys, plus an **Environments MCP Server** that lets tools like OpenAI Codex pull credentials into a coding session without putting secrets in the prompt/context.

## Founders, funding & evidence of use
Founded by Roustem Karimov and Dave Teare — **Verified**. Raised ~$920M total: $200M Series A (Accel, 2019), $100M Series B ($2B valuation, 2021), $620M Series C ($6.2B valuation, 2022, led by ICONIQ) — **Verified** (TechCrunch, Crunchbase). Real use: partnerships with OpenAI, Anthropic, Cursor, GitHub, and Vercel around agent credential security; Okta's 2026 "Businesses at Work" report cites 370% YoY growth for 1Password among 8,000+ sampled apps.

## Relevance to agentic AI engineering
Directly addresses non-human identity — a load-bearing gap as agents get tool-calling access to real systems; complements MCP gateway and agent-orchestration tooling in this repo.

## Sources
- https://1password.com/press/2026/mar/1password-unified-access
- https://1password.com/solutions/agentic-ai
- https://techcrunch.com/2021/07/27/1password-raises-100m-at-a-2b-valuation/
- https://www.crunchbase.com/organization/1password
