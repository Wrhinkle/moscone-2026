# Unsloth

> Open-source toolkit (two brothers + a small team) that makes fine-tuning and RL-training open LLMs ~2x faster with 70%+ less VRAM, plus the de-facto-standard quantized GGUF releases everyone grabs off Hugging Face.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, San Francisco (founders are Australian brothers) (Verified — YC company page, GitHub blog)
- **Website / GitHub:** https://unsloth.ai · https://github.com/unslothai/unsloth · https://huggingface.co/unsloth

## What they do
Unsloth's core is an open-source Python library that rewrites the training path for open-weight LLMs — hand-derived backprop and custom Triton kernels instead of stock PyTorch autograd — yielding roughly 2x faster fine-tuning with up to 70% less VRAM across 500+ models (Llama, Qwen, Gemma, Mistral, DeepSeek, gpt-oss, Phi, GLM), with claimed zero accuracy loss (Verified claims — GitHub README; independent comparisons like the 2026 Axolotl-vs-Unsloth-vs-TRL evals broadly corroborate the speed/VRAM edge). It covers LoRA/QLoRA, full fine-tuning, pretraining, and reinforcement learning (GRPO at ~80% less VRAM, "ultra-long-context RL"), plus vision, audio, and embedding models; a Feb 2026 update added 12x-faster MoE training (Verified — GitHub, Unsloth changelog/substack).

Second product surface: **Dynamic 2.0 GGUF quantizations** on Hugging Face — per-layer adaptive quantization with hand-curated calibration data that lets giant models (e.g., DeepSeek-V3.1 671B) run at 1–3 bits with unusually small quality loss. These quants have become the default download for local-inference users; HN threads routinely say "already quantized into a sane format by Unsloth" (Verified — unsloth.ai docs, Hugging Face, HN). Third: **Unsloth Studio**, a desktop/web UI (Windows/Mac/Linux) for no-code local training and running of models, with tool-calling, web search, and sandboxed code execution (Verified — GitHub, unsloth.ai). Monetization is Pro/Enterprise (multi-node, "up to 30x faster training," claimed +30% accuracy) at contact-us pricing — no public pricing page (Verified — unsloth.ai).

## Founders & origins
**Daniel Han** (algorithms; ex-NVIDIA, where he made algorithms like TSNE ~2000x faster; maintains the Hyperlearn OSS package; known for finding and fixing 20+ bugs in Gemma, Llama, Mistral, and Phi) and his brother **Michael Han** (design/product) (Verified — YC page, unsloth.ai/about, GitHub blog). The library launched December 2023 as a two-person OSS project; they went through the **2024 GitHub Accelerator** ($40K) and **Y Combinator S24**. Team size ~8 (Reported — YC page).

## Funding
- Pre-seed/seed: **~$500K** (Sept/Oct 2024), around the YC S24 batch (Reported — Crunchbase, CB Insights aggregations).
- Investors named across aggregators: Y Combinator, GitHub Fund/Accelerator, Transpose Platform, Redpoint Ventures, Samsung NEXT, Microsoft M12 (Reported — Tracxn/CB Insights/startupintros; individual investor participation not independently confirmed).
- No Series A found in public sources as of 2026-07-02. Total raised: roughly the seed amount — strikingly small relative to adoption; the leverage is OSS, not capital.

## Evidence of real-world use
- **67.8K GitHub stars, 6.1K forks** (Verified — github.com/unslothai/unsloth, fetched 2026-07-02); crossed 50K in Feb 2026.
- **10M+ monthly / 150M+ total model downloads** on Hugging Face, among the top download sources on the Hub (Reported — company/YC page; HF org page shows individual quant repos with hundreds of thousands of downloads each).
- Works directly with model labs — Google, OpenAI, Meta, Mistral, NVIDIA — on day-zero quantizations and bug fixes (Gemma gradient-accumulation loss explosion, gpt-oss Harmony chat-template mismatches); featured at Google I/O, OpenAI DevDay, LlamaCon (Reported — company; the specific bug fixes are Verified in GitHub discussions and llama.cpp issues).
- Ecosystem integration: official Hugging Face TRL docs have an Unsloth integration page; HF published a joint "train with Unsloth on HF Jobs" blog; **Red Hat Developer** (Apr 2026) documents Unsloth inside its Training Hub for LoRA/QLoRA (Verified — huggingface.co, developers.redhat.com).

## Relevance to agentic AI engineering
Unsloth is the cheapest on-ramp to **specialized sub-agent models**: fine-tune or RL-train a small open model for one job (classification, extraction, routing) instead of paying frontier-API rates in an agent loop. Its GRPO/RL support is directly relevant to training tool-calling behavior of the kind surveyed in **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**. Unsloth's own docs benchmark Dynamic GGUFs on **Aider Polyglot** — i.e., quantized local models driving coding agents, the territory of **ProdCodeBench** and **FeatureBench** in this repo's landscape. Cheap distilled/quantized models are also the practical substrate for memory-summarization components (**Memory for Autonomous LLM Agents**) and for local low-latency voice pipelines (**LTS-VoiceAgent**), given Unsloth's audio-model training support.

## Use cases & considerations
Use cases: (1) fine-tune Qwen/Gemma-class models on a single consumer GPU or free Colab for domain tasks (e.g., construction back-office document classification); (2) GRPO-train a small model for reliable structured tool-calling; (3) pull Unsloth Dynamic GGUFs to run big open models locally for private inference; (4) Studio for non-engineers to build datasets and train without code.

Considerations: single-GPU focus in the free tier — multi-node is paywalled Enterprise with opaque pricing; dual **Apache-2.0/AGPL-3.0** licensing deserves legal review for embedded commercial use; tiny team (~8) and ~$500K raised means bus-factor and support risk; NVIDIA-first (AMD/Intel "soon"). Competitors: **Axolotl, LLaMA-Factory, Hugging Face TRL/PEFT**, and managed fine-tuning on **Together AI/Fireworks**. Open question: whether Enterprise revenue can fund the pace the OSS community now expects.

## Sources
- https://unsloth.ai/ and https://unsloth.ai/about
- https://github.com/unslothai/unsloth
- https://www.ycombinator.com/companies/unsloth-ai
- https://github.blog/news-insights/company-news/2024-github-accelerator-meet-the-11-projects-shaping-open-source-ai/
- https://venturebeat.com/ai/github-accelerator-fuels-open-source-ai-revolution-empowering-startups-to-democratize-access
- https://www.crunchbase.com/organization/unsloth-ai · https://www.cbinsights.com/company/unsloth-ai/financials · https://tracxn.com/d/companies/unsloth/__piG5Tisuqt46uep5LTkKXw7aYYlsr3duu7VRHwuI31Q
- https://huggingface.co/unsloth · https://huggingface.co/docs/trl/unsloth_integration · https://huggingface.co/blog/unsloth-jobs
- https://unsloth.ai/blog/dynamic-v2 · https://unsloth.ai/docs/basics/unsloth-dynamic-2.0-ggufs · https://unsloth.ai/docs/basics/unsloth-dynamic-2.0-ggufs/unsloth-dynamic-ggufs-on-aider-polyglot
- https://unslothai.substack.com/p/unsloth-2026-update-faster-moe
- https://developers.redhat.com/articles/2026/04/01/unsloth-and-training-hub-lightning-fast-lora-and-qlora-fine-tuning
- https://dev.to/ultraduneai/eval-003-fine-tuning-in-2026-axolotl-vs-unsloth-vs-trl-vs-llama-factory-2ohg
- https://news.ycombinator.com/item?id=47793254
- https://github.com/unslothai/unsloth/discussions/4921 · https://github.com/ggml-org/llama.cpp/issues/21516
