# Together AI

> A GPU "neocloud" for open-source models: serverless inference APIs over 200+ open models, fine-tuning, and rentable NVIDIA clusters, differentiated by in-house systems research (FlashAttention lineage).

- **Category:** models-inference
- **AIEWF 2026 tier:** platinum
- **Founded:** June 2022, San Francisco, as Together Computer Inc. (Verified — company about page, Tracxn, Contrary Research)
- **Website / GitHub:** https://www.together.ai · https://github.com/togethercomputer · https://docs.together.ai

## What they do
Together sells three layers of the open-model stack. (1) **Serverless inference**: OpenAI-compatible endpoints over 200+ open-weight models — Llama, DeepSeek, Qwen, Mistral, Kimi, image/video models — with public per-token pricing, plus **dedicated endpoints** for reserved-capacity latency guarantees. (2) **Fine-tuning**: managed LoRA, full fine-tuning, and DPO pipelines whose outputs you can serve on the same platform or download. (3) **GPU clusters**: self-service and contracted NVIDIA capacity (H100 through GB200) for training, which is why press now files them under "neocloud" alongside CoreWeave/Lambda. Newer surfaces include a code sandbox for agent code execution, an evaluations suite, and Batch APIs (Verified — together.ai/products, docs).

The engineering pitch is that their research group makes the same hardware go further: chief scientist Tri Dao authored **FlashAttention** (used broadly across the industry, including OpenAI, Anthropic, and Meta), and the company deploys work like **ATLAS** adaptive speculative decoding (learns from production traffic to speed decoding) and **ThunderKittens** GPU kernels directly into its serving stack (Verified — Together research blog, GitHub). Practically: you'd integrate Together where you want open-weights economics with a proprietary-API developer experience, or when you need burst GPU capacity without a hyperscaler commitment.

## Founders & origins
Founded 2022 by **Vipul Ved Prakash** (CEO; previously founded Cloudmark, acquired by Proofpoint, and Topsy, acquired by Apple in 2013), **Ce Zhang** (CTO, ex-ETH Zurich professor), **Chris Ré** (Stanford professor, Hazy Research; prior exits to Apple), **Percy Liang** (Stanford, CRFM), and **Tri Dao** (chief scientist, FlashAttention author) (Verified — company site, Contrary Research, Wikipedia). Origin story: decentralize/open the AI stack against closed-lab concentration — their first splash was **RedPajama** (2023), an open reproduction of the LLaMA training dataset (1.2T tokens; v2 reached 30T tokens) with Stanford CRFM, ETH DS3Lab, and Ontocord (Verified — together.ai blog, VentureBeat).

## Funding
- 2023 seed: $20M led by Lux Capital (Reported — Sacra/Contrary aggregations).
- Nov 2023 Series A: **$102.5M** led by Kleiner Perkins, NVIDIA participating, ~$500M valuation (Verified — Newcomer, company blog).
- Mar 2024 Series A extension: **$106M** led by Salesforce Ventures at **$1.25B** (Verified — company blog, TechCrunch list).
- Feb 2025 Series B: **$305M** led by General Catalyst, co-led by Prosperity7 (Aramco), at **$3.3B**; NVIDIA, Salesforce Ventures, Coatue, Kleiner Perkins et al. participating (Verified — company blog, PR Newswire).
- **Jul 1, 2026 Series C: $800M led by Aramco Ventures at $8.3B valuation**, with Vista Equity Partners, General Catalyst, Emergence, NVIDIA, March Capital, Pegatron, S Ventures (Verified — TechCrunch, 2026-07-01 — announced literally yesterday as of this writing).
Total raised: ~$1.3B (computed from the above).

## Evidence of real-world use
- TechCrunch (Jul 2026) reports **annualized bookings above $1.15B** as of last quarter and "thousands of paying customers" (Reported — single outlet, likely company-sourced).
- Named customers with substance beyond logos: **Cursor, Cognition, Decagon** (TechCrunch), **Zoom, Salesforce** (company site); documented case studies include **Zomato** (support bot at 1,000+ msgs/minute) and **Dippy AI** (4M+ tokens/min on dedicated endpoints) (Reported — together.ai/customers).
- OSS footprint: `togethercomputer/RedPajama-Data` (widely used; OpenLLaMA trained on RedPajama), **Mixture-of-Agents** repo (65.1% AlpacaEval 2.0 with open models), FlashAttention lineage (Verified — GitHub).
- Public per-token pricing page = real self-serve commercial product (Verified).

## Relevance to agentic AI engineering
Together is the inference/compute substrate under many agent products — Cursor and Cognition as customers puts it directly beneath the coding-agent wave benchmarked by **SWE-EVO**, **FeatureBench**, **OmniCode**, and **ProdCodeBench** in this repo's landscape. Its code sandbox targets exactly the isolated-execution need raised in **Verifiable Software Worlds for Computer-Use Agents** and the tool-use orchestration surveyed in **The Evolution of Tool Use in LLM Agents**. Cheap, fast open-model serving (ATLAS speculative decoding, dedicated low-latency endpoints) matters for latency-bound voice stacks like **LTS-VoiceAgent** and **VoiceAgentRAG**, and fine-tuning + open weights is the standard path to specialized sub-agents and memory/summarization models discussed in **Memory for Autonomous LLM Agents**.

## Use cases & considerations
Use cases: (1) swap OpenAI-compatible endpoints to open weights (DeepSeek/Qwen/Llama) for cost-sensitive agent loops; (2) fine-tune a small model on your domain (e.g., construction back-office document classification) and serve it on the same platform; (3) rent H100/GB200 clusters for training without hyperscaler contracts; (4) dedicated endpoints for latency-sensitive voice/support agents.

Considerations: no frontier proprietary models — quality ceiling is whatever open weights offer; per-token prices are undercut by aggressive rivals (**Fireworks AI, Baseten, Groq, DeepInfra, Fal**) and hyperscalers (Bedrock, Vertex); neocloud economics are capex-heavy and competitive (CoreWeave, Lambda, Nebius); lock-in is low (OpenAI-compatible API, downloadable fine-tunes). Open questions: margin durability as inference commoditizes, and how much of the $1.15B bookings is GPU-cluster rental vs. the higher-margin API business.

## Sources
- https://www.together.ai/about-us
- https://www.together.ai/products
- https://www.together.ai/customers
- https://www.together.ai/blog/together-ai-announcing-305m-series-b
- https://www.together.ai/blog/series-a2
- https://www.together.ai/blog/redpajama
- https://techcrunch.com/2026/07/01/neocloud-together-ai-raises-800m-leaps-to-8-3b-valuation/
- https://www.newcomer.co/p/cloud-platform-startup-together-ai
- https://research.contrary.com/company/together-ai
- https://www.prnewswire.com/news-releases/together-ai-raises-305m-series-b-to-scale-ai-acceleration-cloud-for-open-source-and-enterprise-ai-302380967.html
- https://github.com/togethercomputer/RedPajama-Data
- https://github.com/togethercomputer/moa
- https://venturebeat.com/ai/redpajama-replicates-llama-to-build-open-source-state-of-the-art-llms
