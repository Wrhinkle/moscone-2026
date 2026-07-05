# Cerebras

> Builds the largest chip ever made (a whole silicon wafer) and sells the fastest LLM inference available — thousands of tokens per second on open-weight models, via an OpenAI-compatible API.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2015, Sunnyvale, CA (Verified)
- **Website / GitHub:** https://www.cerebras.ai · https://inference-docs.cerebras.ai · https://github.com/Cerebras

## What they do

Cerebras designs the Wafer-Scale Engine (WSE), a processor built from an entire 300mm wafer instead of dicing it into individual chips. The current WSE-3 packs ~900,000 cores with on-wafer SRAM and enormous memory bandwidth, which eliminates the HBM/interconnect bottleneck that limits token generation speed on GPU clusters. The practical consequence: single-stream decode speeds an order of magnitude faster than GPU serving — gpt-oss-120B at ~3,000 tokens/sec, GLM-4.7 at ~1,000 tok/s, DeepSeek R1 70B at ~1,500 tok/s (Verified across Cerebras posts and independent press).

What you'd actually buy as an engineer is **Cerebras Inference**: an OpenAI-compatible chat-completions API over a catalog of open-weight models (Llama 3.x/4, Qwen3-32B/235B, GLM-4.7, gpt-oss-120B, Kimi K2.6 — their first trillion-parameter open-weight model). There is a free developer tier, pay-as-you-go token pricing (roughly $0.10–$6/M tokens depending on model; flat rate combining input+output rather than split pricing — Reported), and enterprise reserved capacity. Cerebras is also available as a provider through OpenRouter. The original business — selling CS-2/CS-3 systems and building AI supercomputers (Condor Galaxy with G42) — still exists, but inference-as-a-service is the growth story.

## Founders & origins

Founded 2015 by Andrew Feldman (CEO), Gary Lauterbach (CTO), Michael James, Sean Lie, and Jean-Philippe Fricker (Verified). All five worked together at SeaMicro, the low-power server company Feldman and Lauterbach founded in 2007 and sold to AMD for $334M in 2012 (Verified). The founding bet — that AI workloads deserved a purpose-built, wafer-scale processor — predates the LLM era by years; inference speed became the killer app only in 2024–25.

## Funding

- Series A: $27M, May 2016 — Benchmark, Foundation Capital, Eclipse (Verified)
- Series F: $250M, Nov 2021 at >$4B valuation — Alpha Wave, Abu Dhabi Growth Fund (Verified)
- Series G: $1.1B, Sept 2025 at $8.1B — Fidelity, Atreides; Tiger Global, Valor, 1789 Capital participating (Verified)
- Series H: $1.0B, Jan 2026 at $89.01/share — Benchmark ($225M), Alpha Wave, Fidelity (Reported)
- **IPO: May 14, 2026** on Nasdaq — raised $5.55B at $185/share, the largest US tech IPO since 2019; opened around $350, implying ~$95B valuation (Reported, multiple press summaries). The first S-1 (Sept 2024) was withdrawn during a CFIUS review of G42's stake; the company refiled after clearing it.

Total private capital raised: roughly $3.1B+ before IPO (computed from rounds above).

## Evidence of real-world use

- **OpenAI**: Jan 14, 2026 partnership — 750MW of Cerebras compute integrated into OpenAI's inference stack for latency-sensitive/agentic workloads, worth >$10B per CNBC (Verified); reportedly a >$20B master agreement expandable to 2GW by 2030 (Reported, single source).
- **Perplexity**: Sonar (Llama 3.3 70B-based search model) runs on Cerebras at ~1,200 tok/s, with an on-record CTO endorsement (Verified).
- **Mistral**: Le Chat's "Flash Answers" speed comes from Cerebras serving Mistral Large (Verified).
- **G42 / UAE**: the uncomfortable one — G42 was 85–87% of 2024 revenue; Abu Dhabi-linked entities (G42 + MBZUAI) still ~86% of 2025's ~$510M revenue (Reported from S-1 coverage). Real usage, but extreme concentration.
- Public pricing page, free tier, and OpenRouter listing = real self-serve commercial product, not just enterprise logos.

## Relevance to agentic AI engineering

Agent loops are serial: plan → tool call → observe → repeat, often across dozens of turns. Decode speed multiplies through the whole trajectory, which is why Cerebras markets directly at coding agents ("20x faster" claims vs. Claude Sonnet 4.5). This connects to the long-horizon degradation and iteration-count themes in *SlopCodeBench* and *SWE-EVO* (faster inference = more repair iterations per wall-clock budget), to the multi-tool orchestration overhead discussed in *The Evolution of Tool Use in LLM Agents*, and to speculative/asynchronous tool-calling work like *Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling*. For voice, sub-second time-to-first-token is exactly the bottleneck papers like *LTS-VoiceAgent* and *VoiceAgentRAG* architect around — Cerebras attacks it in hardware.

## Use cases & considerations

Use cases: (1) real-time voice agents where LLM latency dominates the turn budget; (2) high-iteration coding/SWE agents on open models (GLM-4.7, Qwen3, Kimi K2.6) at ~10x better price-performance than frontier closed models; (3) reasoning models where long chains-of-thought at 1,000+ tok/s become interactive; (4) parallel agent fleets (search, extraction) needing throughput.

Considerations: open-weight models only — no Claude/GPT frontier closed models on the API; historically limited context windows and model-catalog lag vs. GPU providers (verify current limits per model before committing); UAE revenue concentration is a business-risk flag even post-IPO; capacity has been demand-constrained. Competitors: Groq and SambaNova (custom-silicon speed), Together AI, Fireworks, Baseten (GPU-based open-model serving). Open question as of 2026-07-02: how much of the OpenAI 750MW deal displaces third-party API capacity vs. expands it.

## Sources

- https://en.wikipedia.org/wiki/Cerebras_Systems
- https://techcrunch.com/2025/09/30/a-year-after-filing-to-ipo-still-private-cerebras-systems-raises-1-1b/
- https://www.cerebras.ai/press-release/series-g
- https://www.cerebras.ai/press-release/cerebras-powers-perplexity-sonar-with-industrys-fastest-ai-inference
- https://www.cerebras.ai/blog/mistral-le-chat
- https://www.cerebras.ai/blog/glm-4-7
- https://www.cerebras.ai/blog/cerebras-kimi-k2-Enterprise
- https://inference-docs.cerebras.ai/models/overview
- https://openai.com/index/cerebras-partnership/
- https://www.cnbc.com/2026/01/14/cerebras-scores-openai-deal-worth-over-10-billion.html
- https://www.datacenterdynamics.com/en/news/openai-signs-10-billion-deal-with-cerebras-with-750mw-of-big-chip-compute/
- https://fortune.com/2026/05/14/cerebras-one-of-the-biggest-ipos-of-the-year/
- https://www.techtimes.com/articles/316698/20260515/cerebras-raises-555-billion-ai-chip-ipo-86-revenue-dependence-uae-entities-unresolved.htm
- https://openrouter.ai/provider/cerebras
- https://costbench.com/software/llm-api-providers/cerebras-inference/
