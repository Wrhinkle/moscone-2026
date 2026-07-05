# Baseten

> An AI inference platform: you bring a model (open-weights, fine-tuned, or fully custom) and Baseten runs it in production — optimized runtimes, autoscaling GPUs across 18 clouds, observability, and OpenAI-compatible APIs — so app teams don't build serving infrastructure themselves.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** 2019, San Francisco (Verified — company about page, Contrary Research, Crunchbase)
- **Website / GitHub:** https://www.baseten.co · https://github.com/basetenlabs · https://docs.baseten.co

## What they do
Baseten sells production inference in three shapes. (1) **Model APIs**: OpenAI-compatible per-token endpoints over popular open-weights models (DeepSeek, Qwen, GLM, Kimi, Nemotron). (2) **Dedicated Deployments**: your model — open, fine-tuned, or fully custom — on reserved autoscaling GPU capacity, packaged with **Truss**, their MIT-licensed open-source serving framework (`truss push --watch` gives a live-reload dev loop; `--promote` ships to prod; supports vLLM, SGLang, TensorRT-LLM, PyTorch, diffusers). (3) **Chains/compound workflows**: multi-model pipelines (e.g., STT → LLM → TTS) where steps run on independently scaled hardware but stream directly between each other — this is how Bland AI gets sub-400ms end-to-end phone calls (Verified — docs.baseten.co, GitHub, customer case study).

Underneath is the part they actually differentiate on: the **Baseten Inference Stack** (kernel/runtime-level optimization, speculative decoding, a model performance team that co-tunes deployments) and **multi-cloud capacity management** — as of the June 2026 Series F they claim 1B+ inference requests/day across 87 clusters on 18 cloud environments, arbitraging GPU supply so customers get capacity and failover without cloud contracts (Reported — company Series F announcement; scale figures are company-sourced). They also launched **Baseten Training** (2025) for fine-tuning models you then serve on the same platform (Verified — company blog/docs). Engineer translation: it's the "we are your inference team" vendor — closer to forward-deployed infrastructure than a raw token API.

## Founders & origins
**Tuhin Srivastava** (CEO), **Amir Haghighat** (CTO), and **Philip Howes** founded Baseten in 2019; **Pankaj Gupta** is also cited as a co-founder (Verified for first three — company site, Crunchbase; Reported for Gupta). Srivastava and Howes grew up together in Australia and previously co-founded Shape (HR analytics, acquired by Reflektive, 2018); all three met as early employees at Gumroad around 2012, where they felt the pain of shipping ML without infra teams (Verified — Contrary Research, Greylock portfolio note).

## Funding
- Apr 2022: emerged from stealth with **$20M** (seed + Series A), Greylock leading (Verified — Greylock, TechCrunch-era coverage; a low-quality aggregator's "First Round/Sequoia" version appears wrong).
- Mar 2024 Series B: **$40M**, IVP and Spark Capital (Verified — company blog, press).
- Feb 2025 Series C: **$75M** led by IVP and Spark at **$825M** valuation; total then $135M (Verified — Businesswire, company blog).
- Sep 2025 Series D: **$150M** led by BOND at **$2.15B**; CapitalG, Premji participating (Verified — Fortune, Businesswire).
- Jan 2026 Series E: **$300M** at **$5B**, co-led by IVP and CapitalG; **NVIDIA invested $150M** (Verified — Bloomberg, Businesswire, company blog).
- Jun 2026 Series F: **$1.5B** at up to **$13B** (two tranches, $11B/$13B), led by Altimeter, Conviction, Spark (Verified — company blog, multiple outlets).
Total raised: ~$2.1B (computed). Three rounds in ten months signals both hypergrowth (company claims ~20x YoY revenue) and capex-hungry economics.

## Evidence of real-world use
- Documented case studies with numbers, not just logos: **Zed** (2x faster edit-prediction completions vs. prior provider, targeting P50 <200ms), **Writer** (Palmyra-Med/Fin 70B models, +60% tokens/sec via TensorRT-LLM), **Bland AI** (sub-400ms voice pipeline on Chains) (Verified — baseten.co/customers).
- Named customers in funding coverage: **Cursor, Mercor, Clay, OpenEvidence, Lovable, Abridge, Descript** (Reported — company/press announcements).
- Third-party validation: NVIDIA published a Baseten case study and invested $150M; Google Cloud blog documents their 225% cost-performance work (Verified).
- Truss is open source with public adoption; a "6,000+ stars" figure circulates but I could not independently confirm the count (Unverified). Public pricing page = real self-serve product (Verified).

## Relevance to agentic AI engineering
Baseten sits directly under the coding-agent wave this repo tracks — Cursor and Zed as customers put it beneath the systems benchmarked by **SWE-EVO**, **FeatureBench**, and **ProdCodeBench**, where fast custom-model inference (Zed's Zeta) is the product. Chains is a production answer to the multi-model orchestration surveyed in **The Evolution of Tool Use in LLM Agents**, and its streaming step-to-step design is exactly the latency architecture argued for in **LTS-VoiceAgent**, **VoiceAgentRAG**, and **Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling** — Bland AI's deployment is a live instance of the τ-Voice-style full-duplex problem. Fine-tune-then-serve (Training + Dedicated Deployments) is the standard path to specialized sub-agent and memory/summarization models discussed in **Memory for Autonomous LLM Agents**.

## Use cases & considerations
Use cases: (1) serve a fine-tuned domain model (e.g., a construction back-office document classifier) without owning GPU ops; (2) latency-critical voice agents via Chains (STT/LLM/TTS pipeline, one vendor); (3) swap OpenAI calls to open-weights Model APIs for cost-sensitive agent loops; (4) burst/failover capacity through their multi-cloud layer.

Considerations: dedicated-deployment economics favor sustained traffic — low-volume workloads are cheaper on serverless rivals; Truss is open but the capacity-management and performance layer is proprietary (moderate lock-in; APIs are OpenAI-compatible); competitors: **Together AI, Fireworks, Modal, Fal, Replicate, Groq**, plus hyperscalers. Open questions: margin durability as inference commoditizes, whether a $13B valuation (~tripled in 5 months) prices in flawless execution, and how much revenue concentrates in a few AI-native whales like Cursor.

## Sources
- https://www.baseten.co/ and https://www.baseten.co/about-us/
- https://docs.baseten.co/development/model/overview
- https://github.com/basetenlabs/truss
- https://www.baseten.co/resources/customers/zed-industries-serves-2x-faster-code-completions-with-baseten/
- https://www.baseten.co/resources/customers/writer/
- https://www.baseten.co/resources/customers/ (Bland AI, Descript)
- https://www.baseten.co/blog/announcing-baseten-75m-series-c/
- https://fortune.com/2025/09/05/exclusive-baseten-ai-inference-unicorn-raises-150-million-at-2-15-billion-valuation/
- https://www.businesswire.com/news/home/20250905680113/en/Baseten-Secures-$150M-Series-D-as-the-Premier-Inference-Platform-for-AIs-App-Layer
- https://www.baseten.co/blog/announcing-baseten-s-300m-series-e/
- https://www.bloomberg.com/news/articles/2026-01-20/ai-inference-startup-baseten-raises-300-million-at-5-billion-valuation
- https://www.baseten.co/blog/announcing-our-series-f/
- https://www.citybiz.co/article/863525/baseten-raises-1-5-billion-series-f-at-up-to-13-billion-valuation/
- https://greylock.com/portfolio-news/baseten-self-serve-apps-for-ml/
- https://research.contrary.com/company/baseten
- https://www.nvidia.com/en-us/case-studies/baseten/
- https://cloud.google.com/blog/products/ai-machine-learning/how-baseten-achieves-better-cost-performance-for-ai-inference
