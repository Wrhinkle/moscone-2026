# Venice

> Privacy-first, "uncensored" AI platform: a consumer chat/image app plus an OpenAI-compatible inference API over open-source models, with no server-side storage of user conversations and an optional crypto-token payment rail.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** ~2023–2024; public launch May 2024 (Reported — TechCrunch says "about two years old" as of July 2026; The Block covered the launch). CEO in Colorado area, CTO in Seattle; largely distributed.
- **Website / GitHub:** https://venice.ai · https://docs.venice.ai · https://github.com/veniceai

## What they do

Venice runs a ChatGPT-style consumer app (text, image, code, "characters") and a developer API, differentiated on two axes: **privacy** and **model neutrality**. Conversations are encrypted client-side, requests are routed through a proxy to GPUs, and nothing is stored on Venice's servers — chat history lives in the user's browser (Verified: company docs + TechCrunch). It hosts 200+ models: curated open-source models (Llama, DeepSeek, Qwen, etc.) run "uncensored" on Venice-controlled infrastructure, with optional pass-through routing to closed models like OpenAI/Anthropic for users who want them (Verified).

For engineers, the relevant surface is the **Venice API**: OpenAI-compatible chat completions plus image generation, embeddings, and TTS, priced per million tokens with a public pricing page (Verified). The unusual part is the second payment rail: stake the **VVV token** (launched on Base, January 2025 — Verified) to mint **DIEM** (added August 2025 — Reported), which grants a daily pro-rata allocation of inference capacity instead of per-request billing — effectively "stake once, get ongoing API compute." Only ~8% of users pay with crypto; the business is mostly conventional subscriptions and API usage (Verified: TechCrunch).

## Founders & origins

- **Erik Voorhees** (CEO) — well-known early Bitcoin entrepreneur: SatoshiDice, ShapeShift founder. Started Venice out of conviction that AI, like money, should be permissionless and private, and frustration with centralized-model content policies (Verified).
- **Jesse Proudman** (President/CTO, Seattle) — founded Blue Box (cloud infra, acquired by IBM in 2015) and Strix Leviathan (crypto trading); ex-VP at Betterment, where he moonlighted on Venice in 2024 before going full-time (Verified: GeekWire).
- **Teana Baker-Taylor** (COO) — former VP at Circle (Reported: GeekWire).

## Funding

- **Series A, announced July 1, 2026: $65M at $1B equity valuation**, led by **Dragonfly**, with Coinbase Ventures, North Island Ventures and others (Verified: TechCrunch, The Block, GeekWire). First outside capital; investors got ~8.98% equity plus a grant of 1.5M VVV and warrants on 5M more (Reported: The Block/Crypto Briefing). Company kept its ~30M-token VVV treasury intact.
- Prior to this, self/community-funded — the January 2025 VVV token launch and subscriptions funded operations (Reported).
- **Total conventional raised: $65M.** Notably already profitable (since Q1 2026) with **$70M+ annualized run-rate revenue** at raise time (Reported: TechCrunch, single primary source).

## Evidence of real-world use

- **3M+ active/registered users** (up from ~2M in Feb 2026) and ~850K unique monthly site visitors (Reported: TechCrunch/company).
- **~1.7M API calls/day** (Reported: TechCrunch).
- Profitability + public per-token pricing page = a real commercial product, not just token speculation.
- Developer ecosystem signals: an official **ElizaOS plugin** (`elizaos-plugins/plugin-venice`), Venice-authored guides for launching ElizaOS agents (including on Akash), community SDKs (e.g., an unofficial PHP client), and active API docs repo on GitHub (Verified).
- Caveat: no named enterprise customers or case studies found — usage evidence is consumer/prosumer scale plus indie agent developers, not B2B logos.

## Relevance to agentic AI engineering

Venice sits in the **model/inference layer** of an agent stack: a drop-in OpenAI-compatible endpoint for open-weight models when an agent needs privacy guarantees, no content-policy refusals, or crypto-native metering (the DIEM model is interesting for autonomous agents that must pay for their own compute without a credit card). Its ElizaOS integration targets exactly the autonomous social/crypto agent scene. Relative to this repo's landscape: relevant to **tool-use/governance** research (an "uncensored" inference layer shifts the safety burden to the orchestration layer — guardrail work applies), and to agentic SWE benchmark work only insofar as its hosted open models (DeepSeek, Qwen) are the same families benchmarked there; it is not itself an agent framework, memory system, or voice stack.

## Use cases & considerations

**Use cases:** (1) privacy-sensitive assistants where prompts must not be retained by the provider; (2) autonomous agents funding inference via staked VVV/DIEM rather than billing accounts; (3) cheap open-model endpoints (chat/image/TTS) behind an OpenAI-compatible SDK swap; (4) applications needing fewer refusal behaviors than frontier hosted models.

**Considerations:** "Uncensored" is a compliance and brand-safety risk for anything user-facing — you own moderation. Privacy claims (proxying, no storage) require trust in Venice's implementation; no third-party audit found in public sources (Unverified). Browser-local history is a real limitation for multi-device users. Token mechanics add regulatory and price-volatility exposure. Competitors: OpenRouter, Together AI, Fireworks, Groq on open-model inference; DuckDuckGo AI Chat, Brave Leo, local tools like Ollama on private consumer AI. Open questions: enterprise traction, GPU/data-center buildout economics, durability of $70M ARR (single-source figure).

## Sources

- https://techcrunch.com/2026/07/01/venice-ai-becomes-a-unicorn-with-65m-series-a-as-its-privacy-first-ai-platform-takes-off/
- https://www.geekwire.com/2026/private-ai-venice-ai-led-by-crypto-vet-erik-voorhees-and-seattles-jesse-proudman-raises-65m/
- https://www.theblock.co/post/406934/venice-ai-funding-equity-valuation-dragonfly
- https://www.theblock.co/post/293593/erik-voorhees-founds-generative-ai-platform-venice
- https://cryptobriefing.com/venice-65m-series-a-billion-valuation/
- https://docs.venice.ai/overview/pricing
- https://venice.ai/token
- https://docs.venice.ai/welcome/guides/ai-agents
- https://github.com/elizaos-plugins/plugin-venice
- https://github.com/veniceai
- https://venice.ai/blog/how-to-launch-an-elizaos-agent-on-akash-using-venice-api-in-less-than-10-minutes
- https://decrypt.co/resources/what-is-venice-ai-the-privacy-focused-chatbot
