# OpenRouter

> A unified API and marketplace that sits in front of 400+ LLMs from 60+ providers — one key, one OpenAI-compatible endpoint, automatic provider routing and fallbacks — so you swap models without rewriting code or managing a dozen vendor accounts.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, New York (Verified — TechCrunch, Tracxn, funding coverage)
- **Website / GitHub:** https://openrouter.ai · https://openrouter.ai/docs · https://github.com/OpenRouterTeam

## What they do
OpenRouter is an AI gateway, not a GPU host: it runs no models itself. You call one OpenAI-compatible chat-completions endpoint with a model slug (e.g. `anthropic/claude-sonnet-4`, `deepseek/deepseek-v4`), and OpenRouter routes the request to one of the underlying providers serving that model — first-party labs or third-party inference hosts (Together, Fireworks, DeepInfra, etc.) — picking on price, latency, and observed uptime. If a provider errors or rate-limits, it transparently falls back to the next one and bills you only for the successful run (Verified — docs). Routing is tunable per-request: provider allow/deny lists, `:nitro` (throughput-sorted) and `:floor` (cheapest) variants, and data-policy filters for compliance.

Billing is prepaid credits with pass-through model pricing plus a 5.5% platform fee on non-crypto credit purchases (min $0.80; 5% flat for crypto). BYOK mode lets you plug in your own provider keys and pay OpenRouter 5% of the equivalent platform cost, with the first 1M BYOK requests/month free (5M on enterprise) (Verified — pricing page and docs). Around this core they've built org features (usage caps, per-key limits, centralized billing), a public model/app rankings page, and `openrouter.ai/data` — aggregate usage data that has become the de facto public scoreboard for which models developers actually use.

## Founders & origins
**Alex Atallah** (CEO) co-founded OpenSea in 2018 and was its CTO through the NFT boom; he stepped down in July 2022 to build "from zero to one" and started OpenRouter in early 2023, initially as a window-shopping layer for the post-LLaMA wave of models. Co-founder: **Louis Vichy** (Verified for Atallah — The Block, TechCrunch, LinkedIn; Reported for Vichy — funding coverage).

## Funding
- Seed, ~Feb 2025: **$12.5M** led by a16z (Verified — Sacra, funding press).
- Series A, announced Jun 2025: **$28M** led by Menlo Ventures, Sequoia participating; announced together as "$40M raised" at ~$500–547M valuation (Verified — Menlo Ventures, TechCrunch).
- Series B, May 2026: **$113M** led by CapitalG, with NVentures (NVIDIA), ServiceNow Ventures, MongoDB Ventures, Snowflake Ventures, Databricks Ventures; ~**$1.3B** post-money (Verified — TechCrunch, multiple outlets).
Total raised: ~$153M (computed; some aggregators cite $173M — Unverified).

## Evidence of real-world use
Unusually strong, because their usage data is public: ~**25–29 trillion tokens routed per week** (~100T/month) as of May 2026, 5x growth in six months, ~8M users (Verified — TechCrunch, openrouter.ai rankings; figures are company-sourced but consistent with the public dashboard). Coding agents are the marquee workload: **Cline** runs on OpenRouter, there's a native **VS Code** integration, and community agents (Roo Code, Kilo Code) default to it; programming has passed 50% of token volume (Reported — company/press). The **"State of AI: An Empirical 100 Trillion Token Study"** (arXiv, 2026) was built on OpenRouter data — third-party researchers treating its telemetry as a census of LLM usage is itself adoption evidence. Public pricing, public rankings, enterprise tier = real commercial product. Caveat: token volume ≠ revenue; the take is a thin ~5% layer, and a large share of traffic is free-tier or hobbyist (roleplay was historically the top category).

## Relevance to agentic AI engineering
OpenRouter is the model-selection substrate under much of the agent stack this repo tracks. The coding agents measured by **FeatureBench**, **SWE-EVO**, **ProdCodeBench**, and **SlopCodeBench** are exactly the long-horizon, high-token workloads driving its growth — Cline-style agents burn tokens at rates where per-request routing to cheaper providers materially changes unit economics. Its fallback routing is a production answer to the reliability concerns in **The Evolution of Tool Use in LLM Agents** (multi-step chains die on any single provider outage), and org-level spend caps/key policies are a thin, practical slice of the control plane argued for in **Governance by Construction for Generalist Agents**. Its public usage data directly feeds empirical work like the benchmark-misalignment debate (**Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering**) by showing what models developers actually run versus what leaderboards rank.

## Use cases & considerations
Use cases: (1) A/B different models in an agent loop by changing a string, not an SDK — cheap way to test if a $0.30/M open model handles your document-extraction step; (2) resilience for production agents via automatic provider fallback; (3) one bill and usage caps across a small team instead of five provider accounts; (4) market intelligence — use rankings to pick models with real-world traction.

Considerations: added hop means marginal latency and a third party in your data path (check per-provider data policies); the 5.5% fee is real at scale, though BYOK softens it; thin-wrapper economics invite competition — **LiteLLM** (OSS), **Portkey**, **Kong/Cloudflare AI gateways**, **Vercel AI Gateway**, and every cloud's native multi-model endpoint (Bedrock, Vertex). Open questions: defensibility beyond network effects of the rankings data, and margin durability if labs cut exclusive direct deals with the biggest agent apps.

## Sources
- https://openrouter.ai/ and https://openrouter.ai/docs/faq
- https://openrouter.ai/docs/use-cases/byok
- https://openrouter.ai/pricing
- https://openrouter.ai/state-of-ai and https://openrouter.ai/data
- https://techcrunch.com/2026/05/26/openrouter-more-than-doubles-valuation-to-1-3b-in-a-year/
- https://www.theblock.co/post/360093/opensea-co-founder-alex-atallah-raises-40-million-for-ai-startup-openrouter
- https://menlovc.com/perspective/investing-in-openrouter-the-one-api-for-all-ai/
- https://sacra.com/c/openrouter/
- https://arxiv.org/html/2601.10088v1 (State of AI: An Empirical 100 Trillion Token Study)
- https://tracxn.com/d/companies/openrouter/__Lg9aF1YF73rpdFzOWAWfZHRphHDo22r0dbDoJyu5fUY
- https://techstartups.com/2026/05/26/openrouter-raises-113m-as-ai-token-usage-surges-to-100-trillion-monthly/
