# NVIDIA

> The GPU company underneath essentially all frontier AI — and increasingly a software vendor selling open models (Nemotron), inference serving (Dynamo, NIM), and an agent toolkit on top of its silicon.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** April 1993, Santa Clara/Sunnyvale, CA (Verified — corporate history, widely documented; the founding meeting at a San Jose Denny's is company lore Jensen Huang has told repeatedly)
- **Website / GitHub:** https://www.nvidia.com · https://developer.nvidia.com · https://github.com/NVIDIA · https://github.com/ai-dynamo/dynamo

## What they do
The hardware layer is the obvious part: Blackwell-generation datacenter GPUs (GB200/GB300 NVL72 rack systems) shipping now, with the successor **Vera Rubin** platform (72 Rubin GPUs + 36 Vera CPUs per rack, ~10x perf/watt over Grace Blackwell, per NVIDIA) on track for H2 2026 (Reported — NVIDIA earnings commentary, CNBC). Plus the networking (NVLink, InfiniBand, Spectrum-X) that makes multi-node training and inference work.

What matters for an AI engineer in 2026 is the software stack NVIDIA sells on top, because it's turning into a direct participant in the inference/agents market rather than just the substrate:

- **CUDA / TensorRT-LLM** — the moat. vLLM, SGLang, and every serving stack in this repo's models-inference category ultimately compile down to it.
- **Dynamo** — open-source "datacenter-scale distributed inference serving framework" (github.com/ai-dynamo/dynamo): disaggregated prefill/decode, KV-cache-aware routing, multi-node serving. Dynamo 1.0 is positioned as production-ready (Verified — NVIDIA technical blog, GitHub).
- **NIM microservices** — prebuilt, GPU-optimized model containers with OpenAI-compatible APIs, licensed via **NVIDIA AI Enterprise**. This is the "buy" option: pull a container, get optimized inference on your own hardware or any cloud.
- **NeMo + NeMo Agent Toolkit** — agent lifecycle software (data curation, fine-tuning, evaluation, NeMo Guardrails, observability). The Agent Toolkit is an open-source, framework-agnostic library for instrumenting and optimizing teams of agents, with a documented Dynamo integration that infers per-request latency sensitivity from agent profiles (NVIDIA reports 4x p50 TTFT reduction vs. default routing) (Verified — GitHub, developer.nvidia.com).
- **Nemotron models** — NVIDIA's own open-weight model family. **Nemotron 3** (Nano/Super/Ultra) uses a hybrid Mamba-Transformer MoE with 1M-token context, pitched explicitly at high-throughput agentic workloads; **Nemotron 3 Nano Omni** (30B-A3B) adds native text/image/video/audio as a "multimodal perception sub-agent" (Verified — NVIDIA newsroom, developer docs; Super/Ultra were slated for H1 2026).

## Founders & origins
**Jensen Huang** (ex-LSI Logic, AMD; still CEO 33 years later), **Chris Malachowsky**, and **Curtis Priem** (both ex-Sun Microsystems engineers) founded NVIDIA in April 1993 to bet on graphics-accelerated computing (Verified — extensively documented). The pivot from gaming GPUs to general-purpose compute began with CUDA in 2006 — the reason the company owned the AI wave when it arrived.

## Funding
Public company — no private rounds to track. Early venture backing of ~$20M came from Sequoia Capital (Don Valentine) and Sutter Hill Ventures (Verified — widely documented). IPO January 1999 on Nasdaq at $12/share (Verified). Current scale as of 2026-07-02: FY2026 revenue (year ended Jan 25, 2026) of **$215.9B**, up 65% YoY; the April 2026 quarter alone posted ~$75B in data center revenue (~92% of sales); market cap ~$5T, the world's most valuable company (Reported — NVIDIA newsroom, CNBC, Futurum). Management claims $500B in Blackwell + Rubin revenue visibility through calendar 2026 (Reported — CFO commentary).

Notably, NVIDIA is now a major *investor* in its own customers: up to $100B pledged to OpenAI alongside a 10GW systems deployment deal (September 2025; later reportedly scaled back to ~$30B — the $30B figure matches OpenAI's Feb–Mar 2026 round in this repo's OpenAI profile), and a reported up-to-$10B commitment to Anthropic alongside Microsoft (Reported — CNBC, OpenAI/NVIDIA announcements; the circularity is a live analyst concern).

## Evidence of real-world use
The hardware is beyond question — every lab profiled in this repo trains and serves on NVIDIA. For the software layer specifically:
- **SAP** reports up to 20% inference performance gains using NIM over a popular open-source serving engine (Reported — SAP News, vendor-adjacent).
- **NTT DATA** launched NVIDIA-powered "enterprise AI factories" integrating NeMo and NIM (March 2026) (Reported — NTT DATA press release).
- NIM Agent Blueprints ship through Accenture, Cisco, Dell, Deloitte, HPE, Lenovo, SoftServe, WWT (Reported — NVIDIA newsroom; partner-list evidence, weaker than usage data).
- Dynamo and NeMo Agent Toolkit are active open-source repos with public docs and examples; independent vendors (e.g., Solo.io) publish integration guides for NIM — third-party ecosystem activity, a decent adoption signal.

## Relevance to agentic AI engineering
NVIDIA is the substrate for everything, but three pieces intersect this repo's research threads directly. Dynamo's agentic-inference work (priority routing, KV-cache reuse across multi-turn agent loops) is the serving-side answer to the long-horizon degradation problems *SlopCodeBench* and *SWE-EVO* measure, and its speculative/latency-aware serving connects to *Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling*. NeMo's evaluation/observability/Guardrails suite maps to *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering* and the governance thread (*Governance by Construction for Generalist Agents*, *ClawLess: A Security Model of AI Agents*). Nemotron 3 Nano Omni's native audio plus Riva speech services make NVIDIA a self-hosted option for the voice stacks benchmarked in *τ-Voice* and *LTS-VoiceAgent*.

## Use cases & considerations
Use cases: (1) self-hosted open-model inference via NIM containers when data can't leave your VPC; (2) Nemotron 3 Nano as a cheap, long-context agent workhorse on your own GPUs; (3) Dynamo for teams serving agents at scale who've outgrown single-node vLLM; (4) NeMo Agent Toolkit for framework-agnostic agent observability without buying a SaaS.

Considerations: NIM/AI Enterprise is per-GPU licensed software — you pay NVIDIA twice (silicon + license); CUDA lock-in is the industry's defining dependency (competitors: AMD MI-series/ROCm, Google TPU, AWS Trainium, Cerebras, Groq, Etched — see this repo's etched.md); Nemotron benchmark claims are vendor-reported; and the OpenAI/Anthropic investment circularity is the biggest open question hanging over the financials.

## Sources
- https://nvidianews.nvidia.com/news/nvidia-debuts-nemotron-3-family-of-open-models
- https://www.nvidia.com/en-us/ai-data-science/foundation-models/nemotron/
- https://www.nvidia.com/en-us/ai-data-science/products/nim-microservices/
- https://www.nvidia.com/en-us/ai-data-science/products/nemo/
- https://github.com/NVIDIA/NeMo-Agent-Toolkit
- https://github.com/ai-dynamo/dynamo
- https://developer.nvidia.com/blog/nvidia-dynamo-1-production-ready/
- https://developer.nvidia.com/blog/full-stack-optimizations-for-agentic-inference-with-nvidia-dynamo/
- https://nvidianews.nvidia.com/news/nvidia-announces-financial-results-for-second-quarter-fiscal-2026
- https://www.cnbc.com/2026/05/20/nvidia-nvda-earnings-report-q1-2027.html
- https://futurumgroup.com/insights/nvidia-q3-fy-2026-record-data-center-revenue-higher-q4-guide/
- https://theenergymag.com/news/market-news/nvidia-reports-215-9-billion-in-fy-2026-revenue-as-data-center-networking-surges-142
- https://openai.com/index/openai-nvidia-systems-partnership/
- https://www.cnbc.com/2025/09/22/nvidia-openai-data-center.html
- https://news.sap.com/2026/03/how-sap-nvidia-advance-ai-enterprise-transformation/
- https://www.nttdata.com/global/en/news/press-release/2026/march/031200
- https://nvidianews.nvidia.com/news/nvidia-and-global-partners-launch-nim-agent-blueprints-for-enterprises-to-make-their-own-ai
- https://www.solo.io/blog/llms-in-the-enterprise-overcoming-cost-security-and-observability-challenges-with-nvidia-nim-and-gloo-ai-gateway
- https://www.hpcwire.com/aiwire/2026/04/29/nvidia-launches-nemotron-3-nano-omni-model-unifying-vision-audio-and-language-for-ai-agents/
