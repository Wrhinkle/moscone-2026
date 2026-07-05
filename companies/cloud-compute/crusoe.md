# Crusoe

> Vertically integrated "energy-first" AI cloud: builds its own power-adjacent data centers (including OpenAI's Stargate Abilene campus) and sells GPU clusters and managed inference on top of them.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** gold
- **Founded:** 2018, Denver, CO (Verified — Contrary Research, company site)
- **Website / GitHub:** https://www.crusoe.ai · https://github.com/crusoecloud

## What they do

Crusoe operates at three layers, which is the whole pitch — "vertically integrated down to the electron":

1. **Energy + data centers.** Crusoe develops power generation and builds AI-optimized data centers where energy is cheap or stranded, claiming a 45+ GW power pipeline (Reported, company Series E release). Its flagship build is the **Stargate campus in Abilene, TX** for Oracle/OpenAI — roughly 1.2 GW across eight buildings running NVIDIA Blackwell (GB200) racks, the most complete Stargate site to date (Verified — Epoch AI, DCD, Forbes). Financed partly via a multi-billion-dollar JV with Blue Owl Capital and Primary Digital Infrastructure (Reported). In March 2026, after Oracle/OpenAI scrapped a planned 600 MW Abilene expansion, **Microsoft agreed to lease Crusoe's adjacent ~900 MW development** (Verified — Bloomberg, Fortune, DCD).
2. **Crusoe Cloud.** A GPU cloud (a "neocloud" competing with CoreWeave, Lambda, Nebius): reserved and on-demand clusters of NVIDIA H100/H200/GB200 and L40S, InfiniBand networking, managed Kubernetes, and "AutoClusters" with automated node health-checks/remediation. Aimed at training, fine-tuning, and large-scale inference rather than general-purpose compute (Verified — product pages, NVIDIA Cloud Partner listing).
3. **Crusoe Managed Inference.** OpenAI-compatible serverless endpoints for open-weight models, built on a proprietary engine with **MemoryAlloy** — a cluster-wide distributed KV cache that fetches prefix caches from local and remote nodes to cut time-to-first-token on long, repetitive contexts (Reported — company blog, Techstrong coverage). This is the piece an application engineer would actually integrate; the GPU clusters are what a platform/ML team would buy.

Origin worth knowing: Crusoe started in **Digital Flare Mitigation** — capturing flared natural gas at oil wells to power modular Bitcoin-mining data centers. In March 2025 it **sold the entire Bitcoin/DFM operation to NYDIG** (270 MW generation, 425+ modular data centers, 135 employees) to focus purely on AI infrastructure (Verified — company newsroom, DCD, Structure Research). The "climate-aligned compute" branding survives, but the flare-gas business itself is gone.

## Founders & origins

**Chase Lochmiller (CEO)** — MIT math/physics, Stanford MS in CS (AI); previously quant trading (Jump Trading, GETCO) — and **Cully Cavness (President/COO)** — Middlebury geology, energy finance and geothermal background (Verified — company leadership page, Bain Capital Ventures profile, Forbes). Childhood friends from Denver; the idea reportedly formed around a 2017 climbing trip and Lochmiller's crypto-mining exposure meeting Cavness's knowledge of flared gas economics. Named after Robinson Crusoe (resourcefulness with stranded assets).

## Funding

- **Series C, April 2022:** $350M led by G2 Venture Partners, ~$1.75B valuation (Verified).
- **Series D, December 2024:** $600M led by Founders Fund (Fidelity, Mubadala, NVIDIA, Ribbit, Valor participating), $2.8B valuation (Verified — GlobeNewswire, company).
- **Series E, October 2025:** $1.375B co-led by Valor Equity Partners and Mubadala Capital, valuation above $10B; investors include NVIDIA, Founders Fund, Fidelity, T. Rowe Price, Tiger Global, Salesforce Ventures (Verified — company release, Cooley, FinSMEs).
- **Total equity raised: ~$2.7–2.8B** (Reported — Tracxn/Sacra), plus separate multi-billion project-finance/JV debt for data center builds (Reported).

## Evidence of real-world use

- **OpenAI/Oracle Stargate Abilene is live** with multiple operational buildings — the strongest possible "someone bet the farm on their construction" signal (Verified). Microsoft leasing the follow-on site is a second anchor tenant (Verified).
- **Windsurf** (coding-agent company) runs H100 clusters on Crusoe, citing 99.98% cluster uptime (Reported — Crusoe customer page; vendor-published but named and quantified).
- **Neuralwatt** case study: +33% inference throughput, −40% GPU idle power on Crusoe Cloud (Reported — vendor blog).
- **Linum** benchmarked providers and found Crusoe's uplink fastest, avoiding data-loading costs (Reported — vendor case study).
- Crusoe Cloud bookings reportedly grew ~5x in the first three quarters of 2025 YoY (Reported — Series E release). NVIDIA is both investor and NVIDIA Cloud Partner listing (Verified).

## Relevance to agentic AI engineering

Crusoe is substrate, not agent tooling — but two hooks matter. First, agentic workloads are inference-heavy with long shared prefixes (system prompts, tool schemas, conversation history); MemoryAlloy's cluster-wide KV-cache reuse is the infrastructure mirror of what *Memory for Autonomous LLM Agents* and *GAM: Hierarchical Graph-based Agentic Memory* address at the application layer, and it directly cuts latency/cost for multi-turn agents. Second, coding-agent companies like Windsurf training and serving on Crusoe ties it to the agentic-SWE-benchmark work in this repo (*FeatureBench*-style evaluation demand is what drives these training clusters). Low-latency managed inference also matters for the voice-agent latency budgets studied in *LTS-VoiceAgent* and *τ-Voice*.

## Use cases & considerations

**Use cases:** (1) reserved H100/H200/GB200 clusters for training or RL fine-tuning at neocloud pricing; (2) OpenAI-compatible managed inference for open-weight models serving agent backends; (3) burst inference capacity with public pricing (a real, self-serve commercial product); (4) large dedicated builds if you are an AI lab needing hundreds of MW.

**Considerations:** revenue is concentrated in mega-deals (Oracle/OpenAI, now Microsoft) — the March 2026 Abilene expansion cancellation shows counterparty churn risk even when capacity gets re-leased. The Stargate association is construction/leasing, not proof the *cloud* product dominates. Managed inference is new and vendor-benchmarked. Competitors: CoreWeave, Lambda, Nebius, Together AI on GPU cloud; hyperscalers above; Fireworks/Baseten/Together on managed inference. Open question: post-flare-gas divestiture, how much of the "clean energy" positioning is pipeline vs. operating reality.

## Sources

- https://www.crusoe.ai/about/leadership
- https://research.contrary.com/company/crusoe
- https://baincapitalventures.com/insight/crusoe-climb-betting-on-power-before-ai-was-cool/
- https://www.forbes.com/sites/christopherhelman/2025/04/10/meet-the-tiny-startup-building-stargate-openais-500-billion-data-center-moonshot/
- https://www.crusoe.ai/resources/newsroom/crusoe-announces-series-e-funding
- https://www.finsmes.com/2025/10/crusoe-raises-1-375-billion-in-series-e-funding-at-above-10-billion-valuation.html
- https://www.globenewswire.com/news-release/2024/12/12/2996138/0/en/Crusoe-Closes-600M-in-Series-D-Round-at-2-8-Billion-Valuation-to-Power-AI.html
- https://www.crusoe.ai/resources/newsroom/nydig-to-acquire-crusoes-bitcoin-mining-operation-crusoe-to-scale-vertically
- https://www.datacenterdynamics.com/en/news/crusoe-exits-crypto-operations-to-focus-on-ai-sell-business-to-nydig/
- https://epoch.ai/publications/openai-stargate-where-the-us-sites-stand
- https://www.datacenterdynamics.com/en/news/oracleopenai-drop-plans-to-expand-flagship-abilene-stargate-site-meta-in-talks-to-pick-up-crusoe-capacity-with-nvidias-help/
- https://fortune.com/2026/03/27/microsoft-texas-data-center-open-ai-former-partner-cloud-provider/
- https://www.crusoe.ai/cloud
- https://www.crusoe.ai/cloud/managed-inference
- https://www.crusoe.ai/resources/customers
- https://www.crusoe.ai/resources/blog/neuralwatt-increases-ai-inference-throughput-by-33-on-crusoe-cloud
- https://techstrong.ai/features/crusoe-adds-managed-inference-service-to-optimize-ai-model-performance/
- https://tracxn.com/d/companies/crusoe/__yyRkgaJgxamAgI3lijDZiChhfKCvnkFGTnaMcmtbFiM

*Profile written 2026-07-02.*
