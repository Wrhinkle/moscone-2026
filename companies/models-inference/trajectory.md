# Trajectory

> A research-lab/product startup building a "continual learning" platform: it turns the corrections, retries, and edits users make inside AI products into ongoing post-training, so a company's deployed agent models keep improving after launch instead of staying frozen.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2025–2026 (Reported — press describes it as "founded in 2026"; public launch and seed announcement May 2026). HQ location not stated in public sources; team and investor base suggest San Francisco (Unverified).
- **Website / GitHub:** https://trajectory.ai — training code open-sourced via the NovaSky-AI/SkyRL repository (Reported)

**Disambiguation note:** several AI companies share this name. This profile covers Trajectory (trajectory.ai), the continual-learning startup founded by Ronak Malde — the one listed as an AIEWF 2026 supporting partner. It is *not* "Trajectory Labs" (a stealth startup by Peter McIntyre) and not Elorian AI (Andrew Dai's ex-DeepMind startup, a separate AIEWF supporting partner that some press coverage conflates with this company).

## What they do

Trajectory's pitch, in engineer terms: your agent product already generates dense training signal — re-prompts, human edits to agent output, escalations, corrections — and almost nobody closes the loop. Trajectory sells the loop. Their platform has four parts (per their own site): **Instrument**, a lightweight SDK that captures traces and correction events from your product; **Understand**, analytics over where the model succeeds/fails in production; **Steer**, tooling to set optimization priorities; and **Learn**, the continuous post-training and deployment layer that ships updated models, prompts, and adapters back into production. Reported cadence at launch was weekly model updates on top of open-weight models customized per customer.

Technically, two named pieces stand out. **Continuous LoRA** is an open-source concurrent multi-LoRA training stack (built with SkyRL/Anyscale collaboration) that splits sampling and training pools and runs many fine-tuning jobs at once — MarkTechPost reports a 2.81x experiment-throughput gain, mostly from vLLM multi-LoRA inference. **SDPO** is their proprietary RL-ish post-training algorithm that uses "privileged hints" instead of a larger teacher model, reported to converge faster than GRPO on their benchmarks. Governance is built in: customers choose what data trains models, updates require approval before production, and changes are audit-trailed.

Infrastructure-wise, a June 10, 2026 Runloop announcement says Trajectory runs 10,000+ concurrent isolated microVM sandboxes ("Devboxes," <500ms launch) for training/eval workloads with per-customer credential isolation — real operational scale, not a demo.

## Founders & origins

**Verified across multiple sources:** CEO **Ronak Malde** — previously an AI researcher at Windsurf, then Google DeepMind via the 2024 ~$2.4B Windsurf deal; press notes he walked away from unvested Google equity. **Michael Elabd** — formerly Google DeepMind robotics. **Arjun Karanam** — former Apple researcher (Vision Pro). Broader team drawn from DeepMind, OpenAI, Apple, Meta Superintelligence Labs, Amazon AGI, and Scale AI, with product folks from Stripe and Figma (Reported).

## Funding

- **Seed, $15M at a $115M valuation, announced May 27, 2026** — led by **Conviction**, with Bessemer Venture Partners, Radical Ventures, BoxGroup; angels include Jeff Dean and Fei-Fei Li, plus founders of Notion, Dropbox, Hugging Face, and Braintrust. (Verified — multiple independent outlets agree.)
- Total raised: $15M (Verified).

## Evidence of real-world use

Early but stronger than logo-collecting: design partners named on Trajectory's own site *with described engagements* — **Clay** (models that learn from user corrections in GTM workflows), **Decagon** (steerable specialized support models), **Harvey** (legal agents capturing evolving domain expertise); press adds **Mercor** and **Rogo**, with Pulse2 reporting some partner deployments "already running in production environments" (Reported). The Runloop case study (10k+ concurrent sandboxes) is independent third-party evidence of real workloads. Open-source contribution via SkyRL is public. No public pricing page; this is design-partner-stage enterprise sales targeting AI-native companies and Fortune 500 support/sales/legal use cases. Paying-customer revenue: Not found in public sources.

## Relevance to agentic AI engineering

Trajectory sits at the post-training/model-improvement layer of the agent stack — the answer to the question raised by this repo's long-horizon benchmark papers: agents degrade or plateau in production (*SlopCodeBench: Benchmarking How Coding Agents Degrade Over Long-Horizon Iterative Tasks*, *SWE-EVO*), and static benchmarks don't capture deployed behavior (*Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering*, *ProdCodeBench*). Their instrument-then-train loop is essentially production-derived eval data turned into weights. The approval-gated, audit-trailed update flow rhymes with *Governance by Construction for Generalist Agents*. And continual post-training is a weights-level alternative to the memory-layer approaches surveyed in *Memory for Autonomous LLM Agents* and *Towards Autonomous Memory Agents* — same problem (agents that learn from experience), different layer.

## Use cases & considerations

**Use cases:** (1) a vertical-agent company (support, legal, GTM) fine-tuning open-weight models weekly from its own correction data instead of prompt-patching a frontier API; (2) replacing an eval-only feedback loop with one that actually updates the model; (3) cost/latency arbitrage — small continually-tuned models beating a frozen frontier model on your distribution.

**Considerations:** very young (weeks-old public launch as of 2026-07-02) — expect design-partner economics, no self-serve, no public pricing. The approach requires owning open-weight model deployment, a real commitment if you're currently API-only. Lock-in risk is at the data-flywheel layer. Competitors/adjacent: OpenPipe, Predibase, Together AI fine-tuning, Anyscale, and frontier labs' own RFT offerings; also every memory-layer startup solving "learning from usage" without touching weights. Open questions: whether weekly LoRA updates measurably beat prompt+memory iteration for most teams, and how catastrophic-forgetting risk is managed across continual updates.

## Sources

- https://trajectory.ai
- https://trajectory.ai/field-notes/multi-lora-training-for-continual-learning
- https://www.welcome.ai/content/trajectory-secures-15m-to-advance-continuous-learning-in-ai
- https://pulse2.com/trajectory-raises-15-million-to-build-a-platform-for-continual-learning/
- https://runtimewire.com/article/trajectory-raises-15m-continual-learning-agents-ronak-malde
- https://www.marktechpost.com/2026/05/30/trajectory-releases-a-concurrent-multi-lora-training-stack-for-continual-learning-reporting-a-2-81x-experiment-throughput-gain/
- https://finance.yahoo.com/sectors/technology/articles/trajectory-uses-runloop-scale-continual-163700538.html
- https://www.startuphub.ai/ai-news/artificial-intelligence/2026/every-product-a-living-system-trajectory-ai
- https://www.finsmes.com/2026/05/trajectory-raises-15m-in-seed-funding.html (403 on fetch; via search snippet)
