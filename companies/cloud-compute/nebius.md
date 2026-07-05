# Nebius

> Nasdaq-listed "neocloud" built from the non-Russian remains of Yandex: owns and builds its own AI data centers, rents NVIDIA GPU clusters, and runs an OpenAI-compatible inference platform (Token Factory) for open-weight models.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** gold
- **Founded:** 2024 in current form (Amsterdam HQ); engineering lineage back to Yandex, founded 1997 (Verified — TechCrunch, company newsroom)
- **Website / GitHub:** https://nebius.com · https://docs.nebius.com · https://github.com/nebius

## What they do

Three layers, deliberately full-stack:

1. **Data centers.** Nebius builds/operates its own capacity rather than only leasing: Mäntsälä, Finland (its original site, with a new 310 MW "AI factory" announced), plus US builds in Kansas City and Vineland, NJ — the Vineland site anchors the Microsoft contract (Verified — company newsroom, Forbes, Redmondmag).
2. **Nebius AI Cloud.** The neocloud product competing with CoreWeave/Crusoe/Lambda: reserved and on-demand NVIDIA clusters (Hopper → Blackwell HGX B200/GB300, with an early Vera Rubin deployment promised under the Meta deal), InfiniBand fabric, managed Kubernetes/Slurm, object storage. Public self-serve pricing exists — a real commercial product, not just mega-deals (Verified — product docs, pricing pages).
3. **Nebius Token Factory** (launched Nov 2025, replacing "Nebius AI Studio"): a production inference platform serving 60+ open models (DeepSeek, GPT-OSS, Llama, Qwen, Nemotron) behind an OpenAI-compatible API, plus fine-tuning/post-training, dedicated endpoints, autoscaling, and fine-grained access management. Nebius agreed to acquire **Eigen AI** to strengthen the inference engine (Verified — Businesswire, company newsroom). This is the layer an application engineer integrates; the clusters are what a platform team buys.

The group also holds adjacent assets inherited from the Yandex split: **Toloka** (data labeling/human feedback; took outside investment led by Bezos Expeditions in 2025 — Reported), **Avride** (autonomous driving/robotics), **TripleTen** (edtech), and a stake in **ClickHouse** (Reported — investor materials, press).

## Founders & origins

**Arkady Volozh (founder/CEO)** co-founded Yandex — "Russia's Google," ~$30B at peak — and ran it for decades; earlier CompTek International and InfiNet Wireless (Verified — Crunchbase, Accel podcast, company bio). After Russia's invasion of Ukraine he was EU-sanctioned in 2022, resigned, publicly criticized the war, and was de-sanctioned in 2024 (Reported). In July 2024 Yandex N.V. sold all Russian assets to a Russian consortium for ~$5.4B — the largest post-invasion corporate exit — renamed itself Nebius Group, kept ~1,300 mostly ex-Yandex engineers, and resumed Nasdaq trading (NBIS) on October 21, 2024 (Verified — TechCrunch, US News/Reuters). So: a "startup" with 25 years of infrastructure engineering and billions of cash at day one.

## Funding

Public company (NBIS), so financing rather than venture rounds:

- **Dec 2024:** $700M oversubscribed private placement — Accel, NVIDIA, Orbis (Verified — company release).
- **2025:** convertible notes + Class A share offerings (June/Sept 2025) raising several billion (Verified — SEC filings, company newsroom).
- **March 2026:** closed a **$4.34B convertible debt** raise; separately **NVIDIA bought $2B of share warrants** (Reported — Yahoo Finance/Reuters, io-fund analysis).
- FY2026 capex guided to ~$20–25B; expect more debt/equity/prepayments (Reported — TIKR, Dealroom). "Total raised" isn't meaningful here; watch dilution and leverage instead.

## Evidence of real-world use

- **Microsoft:** ~$17.4B contract through 2031 (up to $19.4B), ~$7B upfront, dedicated capacity from Vineland, NJ (Verified — company release, Redmondmag, CNBC-adjacent coverage).
- **Meta:** $3B deal (Nov 2025) expanded March 2026 to **up to $27B** over five years — $12B dedicated capacity plus up to $15B optional, ~$30B combined (Verified — CNBC, company release).
- **Revolut** runs fraud prevention, support, and training on Nebius AI Cloud + Token Factory across 200+ H100s (Reported — customer story).
- **Hugging Face** uses Nebius as an inference provider for open models; **Prosus** reports up to 26x cost reduction vs proprietary models; **Higgsfield AI** (video), **Recraft** (B200 migration), **Chatfuel**, **xAID**, **SGLang** collaboration (2x DeepSeek-R1 throughput) (Reported — company/customer pages; vendor-published but named and quantified).
- Q3 2025 revenue $146.1M, +355% YoY; targets $7–9B ARR by end of 2026 (Verified — 6-K filing, Motley Fool).

## Relevance to agentic AI engineering

Nebius is substrate plus a serving layer. Token Factory is a plausible backend for agent stacks that want open-weight models with an OpenAI-compatible API — relevant to serving the coding agents evaluated in *SWE-EVO*, *FeatureBench*, and *ProdCodeBench*-style benchmarks, where token volume (not chat) dominates cost. Its fine-grained access management and governed model lifecycle echo the concerns of *Governance by Construction for Generalist Agents* and *The Evolution of Tool Use in LLM Agents* (least-privilege access for tool-calling systems). Autoscaling low-latency inference matters for the latency budgets in *LTS-VoiceAgent* and *VoiceAgentRAG*. Toloka connects to eval/data pipelines behind agent benchmarks.

## Use cases & considerations

**Use cases:** (1) OpenAI-compatible inference on open models (DeepSeek/Qwen/Llama) for agent backends at aggressive per-token pricing; (2) fine-tuning + hosted dedicated endpoints for custom agent models; (3) reserved GPU clusters for training/RL at neocloud rates; (4) EU-domiciled capacity for data-residency-sensitive workloads.

**Considerations:** extreme revenue concentration (Microsoft + Meta dwarf everything); $20–25B capex funded by debt/dilution amid "circular financing" scrutiny with NVIDIA; Token Factory is young (Nov 2025) and the Eigen AI integration unproven; Yandex lineage may matter to some procurement/security reviews despite the clean split. Competitors: CoreWeave, Crusoe, Lambda, RunPod (GPU cloud); Together AI, Fireworks, Baseten (inference). Open question: whether the self-serve business becomes material or the company is effectively a two-customer data-center developer.

## Sources

- https://techcrunch.com/2024/10/18/nebius-to-resume-nasdaq-trading-after-severing-ties-with-russia-and-yandex/
- https://money.usnews.com/investing/news/articles/2024-10-21/investors-expect-volatile-nasdaq-return-for-ai-firm-split-from-russias-yandex
- https://www.crunchbase.com/person/arkady-volozh
- https://www.accel.com/podcast-episodes/nebiuss-arkady-volozh-on-what-it-takes-to-build-infrastructure-needed-for-the-ai-era
- https://nebius.com/newsroom/nebius-announces-oversubscribed-strategic-equity-financing-of-usd-700-million-to-accelerate-roll-out-of-full-stack-ai-infrastructure
- https://nebius.com/newsroom/nebius-announces-multi-billion-dollar-agreement-with-microsoft-for-ai-infrastructure
- https://redmondmag.com/articles/2025/09/10/microsoft-strikes-billion-deal-with-nebius.aspx
- https://www.cnbc.com/2026/03/16/meta-nebius-ai-infrastructure.html
- https://nebius.com/newsroom/nebius-signs-new-ai-infrastructure-agreement-with-meta
- https://finance.yahoo.com/sectors/technology/articles/nebius-says-well-funded-ai-125730023.html
- https://io-fund.com/ai-stocks/nvidia-coreweave-nebius-circular-financing-gpu-boom
- https://nebius.com/newsroom/nebius-launches-nebius-token-factory-to-deliver-production-ai-inference-at-scale
- https://nebius.com/newsroom/nebius-agrees-to-acquire-eigen-ai-strengthening-nebius-token-factory-as-a-frontier-inference-platform
- https://nebius.com/services/token-factory
- https://nebius.com/customer-stories
- https://nebius.com/newsroom/nebius-to-construct-310-mw-ai-factory-in-finland
- https://www.sec.gov/Archives/edgar/data/0001513845/000110465925088312/tm2525580d1_ex99-1.htm
- https://www.fool.com/investing/2026/04/02/nebius-just-signed-46-billion-in-ai-cloud-deals-wi/
- https://docs.nebius.com/overview/services

*Profile written 2026-07-02.*
