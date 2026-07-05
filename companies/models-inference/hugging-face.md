# Hugging Face

> The GitHub of machine learning: the default public registry for open models, datasets, and demos, plus paid inference routing and enterprise hosting on top.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2016, New York City (Verified — Wikipedia, Contrary Research agree)
- **Website / GitHub:** https://huggingface.co | https://github.com/huggingface

## What they do

The core product is the Hugging Face Hub — a git-based registry hosting roughly 2.4M models, 730K+ datasets, and ~1M Spaces (hosted demo apps) as of spring 2026 (Reported — HF's own "State of Open Source" blog plus third-party trackers). Practically, it's where every open-weight model (Llama, Qwen, DeepSeek, Mistral, Gemma) is published and versioned, and `huggingface_hub` / `transformers` are how you pull them into code. The `transformers` library (~160K GitHub stars, ~150M+ monthly PyPI downloads, Reported) has become the de facto model-definition format: other runtimes (vLLM, llama.cpp converters, ONNX exporters) treat HF checkpoints as the interchange standard.

On the inference side, **Inference Providers** (launched late 2024, matured through 2025) is a single OpenAI-compatible API that routes requests to 15+ serving partners — Groq, Together, Fireworks, Cerebras, SambaNova, Replicate, Nebius, and HF's own infrastructure — so you pick a model on the Hub and get an endpoint without negotiating with each GPU vendor. This is the concrete "models-inference" integration surface: one API key, provider failover, unified billing. They also sell dedicated Inference Endpoints, AutoTrain, and an Enterprise Hub tier ($20/user/month public pricing; Verified — public pricing page) with SSO, audit logs, regional storage, and private model hosting.

Two newer bets: **smolagents**, a minimalist code-first agent framework (agents write Python rather than JSON tool calls), and **LeRobot**, an open robotics stack expanded via the April 2025 acquisition of Pollen Robotics — robotics datasets grew from ~1,100 (2024) to ~27,000 (2025) to become the Hub's largest dataset category (Reported — HF blog).

## Founders & origins

Clément Delangue (CEO), Julien Chaumond (CTO), and Thomas Wolf (Chief Science Officer) — three French founders, company based in NYC (Verified). The company began as a teen-oriented chatbot app named after the 🤗 emoji. The pivot: when Google released BERT in late 2018, the team open-sourced a PyTorch implementation within about a week; its explosive adoption led them to formally pivot in 2019 to open ML infrastructure (Verified — Wikipedia, Contrary Research, founder interviews).

## Funding

- Total raised: ~$400M over 8 rounds (Reported — Tracxn).
- Series D: $235M, August 2023, led by Salesforce Ventures at a $4.5B post-money valuation, with Google, Amazon, Nvidia, Intel, AMD, Qualcomm, and IBM participating (Verified — multiple outlets).
- Earlier: Series C $100M (May 2022, Lux Capital, ~$2B valuation) (Reported).
- No publicly confirmed round after the 2023 Series D as of 2026-07-02; revenue estimates of ~$70M ARR (2023) growing to ~$130M (2024) are Reported (Sacra) and unaudited.

## Evidence of real-world use

Strong and unusually verifiable for this category: the Hub itself is the evidence (2B+ cumulative model downloads; official org accounts operated by Meta, Google, Microsoft, Amazon, Bloomberg, Nvidia, OpenAI). Reported 2,000+ paying enterprise customers including Intel, Pfizer, Bloomberg, eBay, and Grammarly (Reported — Sacra/Contrary; individual logos not independently case-studied). `transformers` is a dependency of a large share of production ML Python stacks; PyPI download volume is a harder signal than any logo wall. Public pricing pages exist for Enterprise Hub, Endpoints, and Inference Providers (real commercial products, not vaporware).

## Relevance to agentic AI engineering

Hugging Face sits at the model-supply layer of the agent stack: if you're running open-weight models behind agents, weights and tokenizers almost certainly come from the Hub, and Inference Providers is a pragmatic multi-provider routing layer. smolagents' code-as-action design is directly relevant to the agentic SWE benchmark work in this repo's landscape (the code-first tool-use pattern those benchmarks stress), and HF co-authored GAIA, a widely used general-assistant/agent benchmark. Hub-hosted evals and leaderboards connect to the tool-use/governance thread — open, reproducible evaluation is their institutional stance. Less directly relevant to the agent-memory and voice-agent paper clusters, though open ASR/TTS checkpoints (Whisper variants, Parakeet, Kokoro) that voice-agent stacks depend on are distributed via the Hub.

## Use cases & considerations

Use cases: (1) source and version open-weight models/datasets for a self-hosted agent stack; (2) one OpenAI-compatible endpoint over many inference vendors via Inference Providers, with easy A/B across providers; (3) private model registry via Enterprise Hub for teams fine-tuning domain models; (4) Spaces for fast internal demos.

Considerations: HF's own serving has historically lagged specialist providers on price/performance — Inference Providers is an aggregator margin business, and going direct to Groq/Together may be cheaper at scale. Revenue is small relative to the $4.5B valuation. smolagents competes with LangGraph, OpenAI Agents SDK, and CrewAI and is not the enterprise default. Lock-in is low (git-based, open formats) — which is also why monetization is the open question. Competitors: GitHub/Kaggle (registry), Replicate/Together/Fireworks (inference), W&B (ML platform).

## Sources

- https://en.wikipedia.org/wiki/Hugging_Face
- https://research.contrary.com/company/hugging-face
- https://sacra.com/c/hugging-face/
- https://tracxn.com/d/companies/hugging-face/___89yhA9z0-ZrLstW87xWDVe15Bkl70IZOkQf38SXzmQ
- https://huggingface.co/blog/huggingface/state-of-os-hf-spring-2026
- https://huggingface.co/docs/inference-providers/index
- https://github.com/huggingface/smolagents
- https://github.com/huggingface/transformers
- https://huggingface.co/blog/huggingface-hub-v1
- https://productmint.com/hugging-face-business-model/
