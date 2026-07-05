# FriendliAI

> The inference-engine research lab turned cloud: the team whose Orca paper invented continuous batching now sells managed GPU serving that runs open and custom models with fewer GPUs than you'd need on vLLM.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, Seoul, South Korea — spun out of Seoul National University; HQ relocated to Redwood City, CA in late 2023 (Verified — Crunchbase News, SDxCentral, company site)
- **Website / GitHub:** https://friendli.ai · https://friendli.ai/docs · https://github.com/friendliai

## What they do
FriendliAI sells GPU inference in three shapes, all on the same proprietary engine (formerly "PeriFlow," now "Friendli Inference"): (1) **Model APIs / Serverless Endpoints** — pay-per-token, OpenAI-compatible endpoints over popular open-weights models (they promote GLM, EXAONE, Llama-family, plus audio/vision models); (2) **Dedicated Endpoints** — your fine-tuned or custom model on managed autoscaling GPUs, with one-click deploy of any of 580,000+ Hugging Face models via a "Deploy this model" button on the Hub itself; (3) **Container** — the engine self-hosted in your own cluster for on-prem/VPC requirements (Verified — friendli.ai, Hugging Face blog).

The differentiation is genuinely technical, not just packaging. CEO Byung-Gon Chun's SNU lab published **Orca** (OSDI 2022), the paper that introduced iteration-level scheduling — what the industry now calls **continuous batching** — which directly inspired vLLM and became standard in essentially every LLM serving framework (Verified — USENIX OSDI 2022, VentureBeat, Cerebral Valley). The commercial engine layers custom GPU kernels, speculative decoding, KV-cache management (host KV cache on dedicated endpoints), and multi-cloud autoscaling on top; marketing claims include "2×+ faster inference," "50% fewer GPUs," up to 90% GPU cost savings, and a 99.99% uptime SLA (Reported — company site; treat numbers as vendor-sourced). Notably, they patented the batching technique, sued Hugging Face in Delaware in July 2023 alleging TGI's continuous batching infringed it, settled confidentially on Jan 8, 2025 — and announced a strategic partnership with Hugging Face two weeks later (Verified — Bloomberg Law, TechCrunch, HF blog). That arc says a lot: the IP was real enough to litigate and the tech good enough to partner on.

## Founders & origins
**Byung-Gon Chun** (Founder/CEO) — Professor of Computer Science at Seoul National University (on sabbatical), previously an AI/systems researcher at Microsoft and Facebook; founded the company in 2021 to commercialize his lab's serving research (Verified — Crunchbase News, VentureBeat, company site). **Gyeong-In Yu** (CTO) — Chun's PhD student and an Orca co-author; part of the founding team, though public sources title only Chun as "founder" (Reported — Crunchbase person profile, personal site). Other formal co-founders: Not found in public sources.

## Funding
- Late 2021 seed: **$6M**, led by Capstone Partners (Verified — Crunchbase News, SDxCentral).
- Aug 2025 seed extension: **$20M**, led again by Capstone Partners; Sierra Ventures, Alumni Ventures, KDB Investment, KB Securities participating (Verified — Crunchbase News exclusive, SiliconANGLE, company announcement).
- Total raised: ~$26M (some trackers say $26.5M). Valuation undisclosed. Strikingly small next to competitors — Baseten has raised ~$2.1B for the same category — implying either capital efficiency from the engine's GPU savings or a much smaller GPU-fleet ambition (Verified amounts; comparison is my note).

## Evidence of real-world use
- **LG AI Research**: FriendliAI is the API provider for the EXAONE 4.0 foundation model — a named, load-bearing production role, not a logo (Verified — company blog, Crunchbase News).
- **SK Telecom**: case study claims eval-to-production in hours, 3× cost cut, 5× throughput (Reported — company customer page; vendor-published numbers).
- **Scatter Lab** (Korean consumer chatbot, "1B+ monthly interactions"), **Upstage**, **NextDay AI** (Reported — customer pages).
- Crunchbase News reports ~25–30 large clients and 2025 revenue tracking 6–7× over 2024 (Reported — single source, company-provided).
- Third-party signals: Hugging Face Hub integration as an official deployment/inference provider (Verified); "fastest GPU inference provider" per Artificial Analysis is cited in the HF partnership blog but is a point-in-time benchmark (Reported). Public pricing page exists = real self-serve product (Verified).

## Relevance to agentic AI engineering
Agent loops are inference-bound: multi-step tool-calling of the kind surveyed in **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration** multiplies token volume, so per-token cost and continuous-batching throughput directly gate what agents are economical to run. Friendli endpoints expose OpenAI-compatible **tool calling with strict, engine-level structured-output guarantees** (constrained JSON) — the enforcement substrate that "**Governance by Construction for Generalist Agents**"-style approaches assume. For coding agents measured by **SWE-EVO**, **FeatureBench**, and **ProdCodeBench**, this is where a fine-tuned open-weights SWE model would actually be served. Their speculative decoding and audio-model serving also touch the latency arguments in **Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling** and the full-duplex constraints benchmarked by **τ-Voice**.

## Use cases & considerations
Use cases: (1) serve a fine-tuned domain model (e.g., a construction-document extractor) from Hugging Face to a dedicated endpoint in a day, the LG EXAONE pattern; (2) swap closed-model API calls in high-volume agent loops to cheaper open-weights serverless endpoints; (3) on-prem/VPC inference via Container where data can't leave; (4) tool-calling backends needing guaranteed-schema JSON.

Considerations: engine is proprietary (no vLLM-style OSS core — lock-in is at the runtime layer, mitigated by OpenAI-compatible APIs); vendor-published performance numbers should be re-benchmarked on your workload; far less capitalized than **Baseten**, **Together AI**, and **Fireworks AI** (also competing: Modal, Replicate, hyperscaler endpoints) — an open question whether ~$26M sustains a GPU-capacity business, or whether Container/licensing is the real model; customer proof is strongest in Korea (LG, SKT, Scatter Lab) — US enterprise traction is less documented.

## Sources
- https://friendli.ai/ and https://friendli.ai/customers
- https://friendli.ai/products/dedicated-endpoints
- https://friendli.ai/docs/guides/tool-calling
- https://friendli.ai/blog/llm-function-calling
- https://friendli.ai/news/friendliai-raises-20m-in-seed-extension-round
- https://friendli.ai/blog/lg-ai-research-partnership-exaone-4.0
- https://news.crunchbase.com/ai/inference-platform-friendliai-raises-seed-extension-chun/
- https://www.sdxcentral.com/news/startup-tackling-ai-inference-bottlenecks-bags-20m/
- https://siliconangle.com/2025/08/29/friendliai-raises-20m-funding-accelerate-ai-inference-workloads/
- https://www.usenix.org/conference/osdi22/presentation/yu (Orca paper)
- https://venturebeat.com/infrastructure/the-team-behind-continuous-batching-says-your-idle-gpus-should-be-running
- https://cerebralvalley.beehiiv.com/p/friendliai-the-inference-engine-behind-vllm
- https://huggingface.co/blog/friendliai-partnership
- https://techcrunch.com/2025/01/10/hugging-face-settles-suit-with-ai-startup-friendliai-which-had-accused-it-of-patent-infringement/
- https://news.bloomberglaw.com/ip-law/korean-generative-ai-firm-sues-us-company-over-batching-patent
- https://gyeongin.github.io/ and https://www.crunchbase.com/person/gyeong-in-yu
