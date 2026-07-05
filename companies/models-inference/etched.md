# Etched

> Builds Sohu, an inference-only ASIC (originally transformer-specialized) sold as rack-scale systems, claiming order-of-magnitude throughput gains over NVIDIA GPUs for LLM serving.

- **Category:** models-inference
- **AIEWF 2026 tier:** silver
- **Founded:** 2022, by Harvard dropouts; HQ San Jose, CA (Verified — TechCrunch, company press release)
- **Website / GitHub:** https://www.etched.com · no public GitHub/SDK found as of 2026-07-02

## What they do
Etched makes **Sohu**, an application-specific chip for LLM inference, fabbed on TSMC's N4P (4nm) process, and sells it as complete rack-scale systems ("frontier inference clusters") rather than individual cards. The original 2024 pitch was radical specialization: burn the transformer architecture into silicon, give up the ability to run CNNs/other workloads, and reclaim the die area GPUs spend on general-purpose flexibility. Headline claims: one 8-Sohu server replaces ~160 H100s; ~500,000 tokens/sec on Llama-70B vs ~25k for a comparable H100 setup (Reported — company benchmarks, echoed by press; no independent MLPerf-style verification found).

By the June 30, 2026 stealth-exit announcement, the positioning had visibly widened: the press release describes systems for "models of all shapes and arbitrarily large numbers of parameters," with customers running **DeepSeek, Qwen, Llama — and Mamba**, a state-space (non-transformer) model (Verified — GlobeNewswire release). Two disclosed architectural bets: **Low Voltage Inference** (math blocks at under half typical voltage, claiming 80%+ peak FLOPs on trillion-parameter sparse MoEs without thermal throttling) and **Cluster Scale Memory** (hybrid HBM/SRAM with proprietary low-latency interconnects for "SRAM-level decode speeds") (Reported — company site only). What you'd actually buy: reserved rack capacity, not a self-serve API — the site has a "Get Access" form, no pricing page, no public developer docs.

## Founders & origins
**Gavin Uberti** (CEO) and **Chris Zhu**, Harvard dropouts, founded the company in 2022; **Robert Wachen** (COO) is the third co-founder (Verified — TechCrunch 2024, company release; the 2026 release names Uberti and Wachen). Origin: a 2022 bet that transformers would remain the dominant architecture long enough to justify architecture-specific silicon — "the biggest bet in AI," per their own framing. Team is now 400+ engineers drawn from NVIDIA, Broadcom, Google TPU, SK Hynix, and HFT firms (Reported — company release).

## Funding
Total raised: **~$800M** across four financings (Verified — company release, multiple outlets).
- 2023 seed: ~$5.4M (Reported — funding trackers).
- Jun 2024 Series A: **$120M**, led by Primary Venture Partners and Positive Sum, Peter Thiel participating (Verified — CNBC, TechCrunch).
- Early–mid 2025: ~$85M at reported $1.5B valuation, later reports of a $2.5B mark (Reported — secondary trackers/social sources only; treat with caution).
- Dec 2025 round (announced Jan 2026): **$500M at ~$5B post-money**, investors incl. Stripes, Peter Thiel, Ribbit Capital, Jane Street, Hudson River Trading, Jump, Two Sigma, Radical Ventures, VentureTech Alliance, plus angels Andrej Karpathy, Geoffrey Hinton, Fei-Fei Li, Arthur Mensch, Scott Wu (Verified — press release, Yahoo Finance/Bloomberg, DCD).

## Evidence of real-world use
- **Over $1B in signed customer contracts** claimed at stealth exit, before first production racks ship — customers unnamed (Reported — company press release; no named customer has publicly confirmed).
- **First-pass A0 silicon back from TSMC and working**; first racks slated to ship summer 2026; Taiwan factory operational; stated path to "gigawatt-scale in 2027" (Reported — company release).
- The strongest earlier public demo is **Oasis** (Oct 2024), the playable real-time AI-generated Minecraft-like world model built with **Decart** — it went viral and Decart shipped it publicly, but it ran on GPUs at launch; the Sohu speedup (">10x") was a projection (Verified demo / Reported speedup — Wikipedia, Decrypt, chipstrat.com analysis).
- Net: real silicon and serious contracted demand, but as of 2026-07-02 there is **no independently verifiable production deployment** — this is pre-revenue-shipment hardware.

## Relevance to agentic AI engineering
Agents are token-hungry: multi-step SWE agents of the kind benchmarked in **SWE-EVO**, **FeatureBench**, and **ProdCodeBench** burn orders of magnitude more inference than chat, and tree-search/multi-sample strategies compound it. If Sohu's throughput/cost claims hold, it changes the economics of exactly those loops. Ultra-low decode latency also matters for the voice stacks covered by **LTS-VoiceAgent** and **VoiceAgentRAG**, where time-to-first-token dominates UX, and for cheap summarization/compaction passes in **Memory for Autonomous LLM Agents**-style architectures. The risk cuts the other way, too: the tool-use trajectory surveyed in **The Evolution of Tool Use in LLM Agents** shows workloads shifting fast, and architecture-specialized silicon is the least flexible layer in the stack — the quiet addition of Mamba support suggests Etched knows it.

## Use cases & considerations
Use cases: (1) reserved high-volume inference for a mature agent product with stable model choice (support agents, coding agents at scale); (2) real-time interactive workloads — voice, world models, game NPCs — where decode latency is the product; (3) hedging inference cost against NVIDIA pricing for open-weight models (DeepSeek/Qwen/Llama).

Considerations: rack-scale sales only — irrelevant to most builders until a cloud partner resells capacity; deep lock-in to Etched's supported model architectures and software stack (no public docs to evaluate); all benchmarks are vendor-supplied; execution risk between working A0 silicon and gigawatt scale is large. Competitors: NVIDIA (Blackwell/Rubin), Groq, Cerebras, SambaNova, and hyperscaler silicon (TPU, Trainium/Inferentia, Maia). Open questions: who the $1B of contracts is with; whether a public API/cloud tier ever appears; how Sohu handles next year's architecture.

## Sources
- https://www.etched.com/
- https://www.globenewswire.com/news-release/2026/06/30/3319922/0/en/etched-emerges-from-stealth-with-working-chip-800m-raised-and-over-1b-in-customer-contracts.html
- https://techcrunch.com/2024/06/25/etched-is-building-an-ai-chip-that-only-runs-transformer-models/
- https://www.cnbc.com/2024/06/25/etched-raises-120-million-to-build-chip-to-take-on-nvidia-in-ai.html
- https://finance.yahoo.com/news/ai-chip-startup-etched-raises-160625909.html
- https://www.datacenterdynamics.com/en/news/etchedai-raises-500m-for-a-5bn-valuation-report/
- https://www.techtimes.com/articles/319393/20260630/transformer-chip-startup-etched-exits-stealth-800m-raised-1b-contracts.htm
- https://en.wikipedia.org/wiki/Oasis_(Minecraft_clone)
- https://www.chipstrat.com/p/etcheds-oasis-creating-a-market-for
- https://decrypt.co/289706/minecraft-clone-generated-ai-real-time
