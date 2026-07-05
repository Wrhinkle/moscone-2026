# Arcee AI

> A small US open-model lab that went from model-merging tooling and enterprise small language models (SLMs) to training its own Apache-licensed 400B-parameter foundation model family (Trinity) from scratch.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, Miami, FL (Verified — Refresh Miami, Tracxn, company blog; team ~30 people as of Jan 2026 per TechCrunch)
- **Website / GitHub:** https://www.arcee.ai · https://github.com/arcee-ai · https://huggingface.co/arcee-ai · https://docs.arcee.ai

## What they do
Three layers, in chronological order of the company's evolution. (1) **MergeKit**: the de-facto standard open-source toolkit for model merging — combining several fine-tuned checkpoints into one model without additional training or GPUs (SLERP, TIES, DARE, linear). ~7.2k GitHub stars, LGPL-3.0 (Verified — GitHub). (2) **Enterprise SLM platform**: training/merging/deploying small domain-specific models inside a customer's VPC, plus **Arcee Conductor** (intelligent routing between SLMs and frontier LLMs per query), **Arcee Orchestra** (agentic workflow builder connecting models to external systems), and hosted **Arcee Cloud** (Verified — docs.arcee.ai, company blog). (3) **Foundation models**: **AFM-4.5B** (4.5B params, 8T training tokens, function-calling/agentic-reasoning support, runs on CPUs and low-RAM GPUs; served by Together AI among others) and the **Trinity** family — **Trinity Nano** (6B) and **Trinity Mini** (26B, Dec 2025), and **Trinity Large** (~400B sparse MoE, 256 experts with 4 active per token, ~13B active params; Jan 2026 preview), all Apache-2.0 (Verified — TechCrunch, VentureBeat, Hugging Face). **Trinity-Large-Thinking**, a reasoning variant pitched at "complex, long-horizon AI agents," followed in April 2026 (Reported — VentureBeat and secondary press).

The engineering story that got attention: a ~30-person team trained the full Trinity family from scratch in ~6 months for ~$20M on 2,048 NVIDIA Blackwell B300s, positioning it against Llama 4 Maverick and Chinese open models (GLM-4.5), with output pricing around $0.90/M tokens (Verified — TechCrunch, Jan 2026). The explicit pitch is "a permanently open, Apache-licensed, frontier-grade US alternative" at a time when most competitive open weights are Chinese.

## Founders & origins
Founded 2023 by **Mark McQuade** (CEO, early Hugging Face employee, ex-Roboflow), **Jacob Solawetz** (co-founder/CTO at founding, ex-Roboflow), and **Brian Benedict** (CRO) (Verified — company blog, AWS Startups profile, VentureBeat). **Lucas Atkins** is CTO as of the Trinity era and led model training (Reported — TechCrunch Jan 2026). Early on Arcee effectively acqui-merged with MergeKit: creator **Charles Goddard** joined and the project moved under the Arcee org (Reported — Arcee blog "seed round & merger with mergekit"). Origin thesis: enterprises need small, ownable, domain-adapted models rather than rented frontier APIs.

## Funding
- Jan 2024 seed: **$5.5M** total (WndrCo, Long Journey Ventures, Flybridge) (Verified — TechCrunch, company blog).
- Jul 2024 Series A: **$24M** led by Emergence Capital; Long Journey, Flybridge, Centre Street Partners, Arcadia Capital, Scott Banister participating (Verified — VentureBeat, company blog, Crunchbase).
- Jul 2025 strategic round: amount undisclosed, led by **Prosperity7 Ventures and M12** (Microsoft's venture fund); Hitachi Ventures, JC2 Ventures, Wipro, Samsung Next participating (Verified — company blog; amount Not found in public sources).
- Total raised: **~$50M** (Reported — TechCrunch, Jan 2026).

## Evidence of real-world use
- **IBM Research used MergeKit in Granite 4.0 development** — the strongest independent adoption signal (Reported — Arcee blog; consistent with Granite's published merging methodology).
- MergeKit's ~7.2k stars, 762 forks, an arXiv paper, and thousands of merged models on Hugging Face make it genuinely load-bearing OSS in the open-model ecosystem (Verified — GitHub, arXiv 2403.13257).
- Named customers: **Thomson Reuters, Guild** (Reported — AWS Startups profile; no detailed public case studies found).
- AFM-4.5B is served commercially by **Together AI** — third-party inference listing implies real demand (Verified — together.ai model page).
- Caveat: no public revenue figures; TechCrunch noted the pivot from services to foundation models, so commercial traction on Trinity itself is unproven as of 2026-07-02.

## Relevance to agentic AI engineering
Arcee sits at the "right-sized models for agents" position: cheap, open, function-calling-native SLMs (AFM-4.5B, Trinity Mini) are the natural engines for the routing/sub-agent patterns surveyed in **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**, and Conductor is literally a productized router. Trinity-Large-Thinking targets the long-horizon agent regime that **SlopCodeBench** and **SWE-EVO** benchmark, where degradation over iterations is the failure mode. Their GuardRails/governance components (announced with the 2025 strategic round) map to the concerns in **Governance by Construction for Generalist Agents**. Small CPU-deployable models also matter for latency-bound voice stacks (**LTS-VoiceAgent**, **VoiceAgentRAG**) where a 4.5B local model beats a round-trip to a frontier API.

## Use cases & considerations
Use cases: (1) route high-volume, low-complexity agent steps (classification, extraction, tool-argument filling) to AFM-4.5B/Trinity Mini via Conductor and reserve frontier models for hard steps; (2) merge domain fine-tunes with MergeKit instead of retraining — free, GPU-less, well-documented; (3) VPC/edge deployment of an Apache-licensed model where data cannot leave (healthcare, financial, defense); (4) a US-provenance open model where Chinese weights are a compliance blocker.

Considerations: Trinity Large is new and only preview-instruct as of early 2026 — benchmark claims are mostly base-model comparisons and company-sourced; the pivot from enterprise services to frontier-scale training raises burn/durability questions at ~$50M raised (competitors spend that per training run); competition is brutal — Meta Llama, Mistral, Qwen/DeepSeek/GLM on the open side, and every inference platform commoditizes serving. Lock-in is low (Apache-2.0, downloadable weights). Open questions: monetization mix (hosted API vs. platform vs. support), and whether the "sovereign US open model" angle converts to paying enterprises.

## Sources
- https://techcrunch.com/2026/01/28/tiny-startup-arcee-ai-built-a-400b-open-source-llm-from-scratch-to-best-metas-llama/
- https://techcrunch.com/2024/01/24/arcee-is-a-secure-enterprise-focused-platform-for-building-genai/
- https://venturebeat.com/ai/small-language-models-rising-as-arcee-ai-lands-24m-series-a
- https://venturebeat.com/technology/arcees-new-open-source-trinity-large-thinking-is-the-rare-powerful-u-s-made
- https://venturebeat.com/ai/arcee-opens-up-new-enterprise-focused-customizable-ai-model-afm-4-5b-trained-on-clean-rigorously-filtered-data
- https://www.arcee.ai/blog/arcee-ai-announces-new-strategic-funding-round
- https://www.arcee.ai/blog/arcee-ai-secures-24m-series-a-to-transform-the-landscape-of-small-language-models
- https://www.arcee.ai/blog/seedroundandmergekitmerger
- https://www.arcee.ai/blog/ibm-research-uses-arcee-mergekit-in-granite-4-0-model-development
- https://www.arcee.ai/blog/arcee-ai-from-small-language-model-pioneer-to-pioneering-slm-powered-agentic-ai-workflows
- https://github.com/arcee-ai/mergekit
- https://huggingface.co/arcee-ai/AFM-4.5B
- https://www.together.ai/models/arcee-ai-afm-4-5b
- https://docs.arcee.ai/arcee-foundation-models/afm-4.5b
- https://aws.amazon.com/startups/learn/arcee-ai-powers-small-languages-models-and-enables-big-ai-ambitions
- https://refreshmiami.com/news/arcee-ai-secures-24m-series-a-to-transform-the-landscape-of-small-language-models/
- https://arxiv.org/html/2403.13257v3
