# Modal

> Serverless Python-native cloud for AI: decorate a function, and Modal runs it in the cloud on autoscaling CPUs/GPUs with sub-second cold starts — plus Sandboxes for safely executing agent-generated code at scale.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** silver
- **Founded:** 2021, New York City (Verified — company site, TechCrunch, AlleyWatch)
- **Website / GitHub:** https://modal.com · https://modal.com/docs · https://github.com/modal-labs

## What they do

Modal is a serverless compute platform where the unit of deployment is a Python function, not a container spec or a Kubernetes manifest. You decorate a function with the `modal` SDK, declare its image, GPU type, and secrets in code, and `modal deploy` gives you an autoscaling cloud function — web endpoint, scheduled job, queue-driven batch worker, or fine-tuning run. Billing is per-second for exactly the compute used, scaling to zero when idle (Verified — docs, pricing page).

The differentiator is that Modal rebuilt the stack rather than wrapping AWS primitives: a custom Rust container runtime, its own image builder, a distributed file system, and a scheduler, all optimized so containers (including multi-GB ML images) cold-start in seconds or less and can fan out to thousands of GPUs (Verified — company engineering material, independent interviews). Public GPU pricing (July 2026): H100 ~$3.95/hr equivalent billed per-second, A100-80GB ~$2.50/hr, down to T4-class cards; a free tier includes $30/mo of credit, Team plan is $250/mo (Verified — pricing page, third-party pricing comparisons).

The second product line, **Sandboxes**, targets agents: dynamically spawned, gVisor-isolated containers for running untrusted (typically LLM-generated) code, with claimed scale of tens of thousands to 100k+ concurrent sandboxes, sub-second scheduling, `modal.Volume` for durable filesystems across runs, tunnels for exposing ports, and secret injection (Verified — product page, independent sandbox comparisons by Northflank, Beam, Superagent). Uniquely among sandbox vendors, GPU workloads run natively inside the same platform. Python-first; a TypeScript SDK exists but was still beta-grade as of early 2026 (Reported — third-party comparisons).

## Founders & origins

**Erik Bernhardsson (CEO)** — built Spotify's music recommendations (Discover Weekly lineage) and open-sourced Annoy and Luigi; then ran the ~300-person tech org at Better.com from 2015–2021 (Verified — his own site, multiple interviews). **Akshat Bubna (co-founder/CTO)** — previously an engineer at Scale AI (Reported — company page, press profiles). The origin story is Bernhardsson's long-running blog thesis that data/ML teams have miserable infrastructure feedback loops; Modal was founded in 2021 to make cloud iteration feel like local iteration (Verified — his blog, podcast interviews).

## Funding

- **Seed, early 2022:** $7M led by **Amplify Partners** (Verified — TechCrunch, AlleyWatch).
- **Series A, Oct 2023:** $16M led by **Redpoint Ventures**, with Amplify, Lux, Definition; total then $23M (Verified — TechCrunch, company press release).
- **Series B, Sep 2025:** $87M led by **Lux Capital** at **$1.1B post-money** (Verified — company blog, Built In; note SiliconANGLE reported $80M — figures conflict slightly).
- **Series C, May 2026:** $355M co-led by **General Catalyst and Redpoint** at **$4.65B post-money**, two tranches (first at $2.5B), new investors Menlo, Bain Capital Ventures, Accel (Verified — company blog, DCD, multiple press).
- **Total raised:** ~$465M. Company-reported: >$300M annualized revenue, ~5x growth since Sep 2025 (Reported — press coverage of Series C).

## Evidence of real-world use

- **Suno** runs music-generation inference and batch pre-processing on thousands of Modal GPUs; case study claims Modal cut ~4 months off launch (Verified as published case study; metrics vendor-reported).
- **Ramp** fine-tuned LLMs on Modal for receipt extraction (34% fewer manual interventions, ~79% cheaper than API LLMs; PII-stripping 25K invoices from 3 days to 20 minutes) (Reported — vendor case study).
- **Meta and Scale AI** named as customers in Series B press (Reported — SiliconANGLE).
- Public per-second pricing, a large docs/examples library, active `modal-labs` GitHub org, and constant presence in independent 2026 sandbox benchmarks (Superagent, Northflank, Beam) — Modal is treated as a default option in that category, not a logo wall (Verified).

## Relevance to agentic AI engineering

Modal sits at two points in the agent stack. First, **agent code execution**: Sandboxes are exactly the isolated, resettable execution environments assumed by long-horizon coding-agent benchmarks like *SWE-EVO*, *FeatureBench*, and *ProdCodeBench*, and by *Verifiable Software Worlds for Computer-Use Agents*; `modal.Volume` gives the durable cross-episode filesystem that agent-memory work (*Memory for Autonomous LLM Agents*) argues agents need. gVisor isolation is a practical answer to the containment concerns in *ClawLess* and *Governance by Construction for Generalist Agents*. Second, **model serving for agents**: scale-to-zero GPU endpoints fit self-hosted STT/TTS/LLM pipelines, though cold-start behavior must be validated against the latency budgets in *LTS-VoiceAgent* and *VoiceAgentRAG*. Sandboxes are also the substrate for RL rollouts when training agentic models.

## Use cases & considerations

**Use cases:** (1) sandboxed execution of LLM-generated code inside a coding-agent or notebook product; (2) bursty GPU inference (open-weight LLMs, diffusion, audio) without managing endpoints; (3) fine-tuning/batch jobs (the Ramp pattern) with per-second billing; (4) RL environment fan-out at thousands of concurrent containers.

**Considerations:** Python-first — TypeScript support lags; it's a proprietary runtime, so the decorator-based programming model is real lock-in (code is portable, deployment topology isn't); premium unit pricing vs. raw GPU clouds at sustained utilization; revenue/growth figures are company-reported. Competitors: **E2B, Daytona, Runloop** (sandboxes); **Baseten, Replicate, RunPod, Together AI, Fireworks** (serverless GPU inference). Open question: whether the $4.65B valuation survives hyperscalers adding first-party agent-sandbox primitives.

## Sources

- https://modal.com/company
- https://modal.com/products/sandboxes
- https://modal.com/blog/announcing-our-series-b
- https://modal.com/blog/modal-series-c
- https://modal.com/blog/general-availability-and-series-a-press-release
- https://modal.com/blog/suno-case-study
- https://modal.com/blog/ramp-case-study
- https://techcrunch.com/2023/10/10/modal-labs-lands-16m-to-abstract-away-big-data-workload-infrastructure/
- https://techcrunch.com/2026/02/11/ai-inference-startup-modal-labs-in-talks-to-raise-at-2-5b-valuation-sources-say/
- https://www.alleywatch.com/2023/10/modal-labs-serveless-data-infrastructure-cloud-generative-ai-platform-erik-bernhardsson/
- https://siliconangle.com/2025/09/29/modal-labs-raises-80m-simplify-cloud-ai-infrastructure-programmable-building-blocks/
- https://www.builtinnyc.com/articles/modal-raises-87m-series-b-1b-valuation-20251001
- https://www.datacenterdynamics.com/en/news/modal-labs-secures-funding/
- https://erikbern.com/about.html
- https://www.superagent.sh/blog/ai-code-sandbox-benchmark-2026
- https://northflank.com/blog/ai-sandbox-pricing
- https://dev.to/thedailyagent/top-5-code-sandboxes-for-ai-agents-2026-58id

*Profile written 2026-07-02.*
