# Models & Inference

Frontier labs and model companies, inference/fine-tuning platforms, model routing/gateways, AI accelerator hardware, and training-data curation. This is the supply side of the entire agent stack: every agent loop, coding harness, voice pipeline, and back-office workflow in this repo ultimately resolves to a model call, and this category is who trains that model, who serves it, who picks which one to call, what silicon it decodes on, and what data made it good. The real-world problem it exists to solve: frontier-quality intelligence is expensive, closed, and supply-constrained — so a whole industry has formed around making it cheaper (open weights + optimized serving), faster (custom silicon), better-targeted (routing, fine-tuning, curation), and ownable (air-gapped weights, VPC deployment).

**How to read this category.** Three profiles carry the most weight: [OpenAI](openai.md) (the reference implementation — the $852B default every other vendor positions against), [Together AI](together-ai.md) (the archetypal open-model inference platform, and the conference's platinum sponsor), and [OpenRouter](openrouter.md) (the neutral gateway whose public token telemetry is the closest thing to a census of what models developers actually run). The axis that differentiates the remaining ~30 is *where in the model lifecycle they sit*: labs that train frontier or open weights → platforms that serve them → routers that pick between them → silicon that accelerates them → data/post-training vendors that improve them. A second axis worth tracking: the 2026 wave of Chinese open-weight labs (MiniMax, Z.ai) and US "sovereign" counter-plays (Arcee, poolside) — jurisdiction is now a purchasing criterion, not a footnote.

## Start here

- [openai.md](openai.md) — the baseline everyone benchmarks against; Codex at 5M+ weekly users is the agentic-SWE story in production.
- [together-ai.md](together-ai.md) — how open-weights economics actually get delivered (serving + fine-tuning + GPU clusters); Cursor and Cognition run on it.
- [openrouter.ai profile](openrouter.md) — one API over 400+ models; read it to understand how model selection became infrastructure.
- [zai.md](zai.md) — the sharpest picture of the Chinese open-weight challenge: MIT-licensed GLM-5.x sold as a drop-in cheap backend *inside Claude Code*.
- [cerebras.md](cerebras.md) — why decode speed is the new battleground for serial agent loops (and a $5.55B IPO to prove the market believes it).

## The labs (frontier & open-weight model builders)

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [OpenAI](openai.md) | ChatGPT, GPT-5.x, and the Codex coding agent | labs | ~$180B+ raised; $852B post-money, IPO groundwork reported | 70% of sampled Codex users ran a request exceeding an hour of estimated human work (their own arXiv paper) |
| [Google DeepMind](google-deepmind.md) | Alphabet's frontier lab: Gemini, AlphaFold, Antigravity | labs | Alphabet-funded | ~8.5M developers building on Gemini monthly; killed Gemini CLI with ~30 days' notice — adoption *and* churn warning |
| [Google](google.md) | The Gemini API / Vertex AI / Antigravity commercial surface | supporting | Public company | Managed Agents: a sandboxed tool-using agent in one API call (shorter stub profile; details live in google-deepmind.md) |
| [Amazon AGI Labs](amazon-agi-labs.md) | Adept acqui-hire turned AWS Nova Act browser-agent lab | labs | Internal Amazon (Adept raised $415M pre-acqui-hire) | GA browser-agent service claims >90% workflow reliability — but zero named customers, and founder David Luan left Feb 2026 |
| [MiniMax](minimax.md) | Shanghai lab shipping MIT-licensed agentic M-series models + video/speech APIs | labs | ~$1B pre-IPO; HKEX-listed Jan 2026 (~$11.5B) | M2 was the first Chinese model to clear 50B tokens/day on OpenRouter; audited FY2025 revenue $79M |
| [zAI / Z.ai](zai.md) | Tsinghua spinout; open-weight GLM-5.x sold as a flat-fee Claude Code backend | labs | ~$1.2–1.5B pre-IPO; HKEX-listed Jan 2026 | On the US Commerce Entity List while its MIT weights top Hugging Face trending — the jurisdiction paradox in one company |
| [poolside](poolside.md) | Code-specialized foundation models you can own outright (air-gapped, IL5) | supporting | ~$626M; a ~$2B Series C failed to close | Sells full model weights to defense primes and banks — the strongest answer to "we can't send code to an API" |
| [Arcee AI](arcee-ai.md) | ~30-person team behind MergeKit and the Apache-2.0 Trinity model family | supporting | ~$50M | Trained a 400B-param MoE from scratch in ~6 months for ~$20M; IBM used its MergeKit in Granite 4.0 |
| [Prior Labs](prior-labs.md) | TabPFN — a foundation model for tabular data (predict from a table like an LLM completes a prompt) | silver | €9M pre-seed; SAP acquiring for €1B+ commitment | *Nature*-published research to €1B+ SAP acquisition in ~18 months |
| [Elorian](elorian.md) | Pre-product lab: native visual/spatial reasoning models | supporting | $55M seed at $300M | Ex-DeepMind founders, Jeff Dean angel — and no product, API, or customer yet |
| [Moonlake AI](moonlake-ai.md) | Generative world models: text/image → interactive 3D simulation | supporting | $28M seed | Closer to robotics/simulation than LLM inference — flagged in its own profile as a category edge-case |
| [TypeSafe AI](typesafe-ai.md) | "System1" models for no-human-in-the-loop machine-to-machine execution | supporting | Undisclosed; pre-launch waitlist | CEO co-invented InstructGPT/RLHF at OpenAI; everything else is still unverifiable |

## Inference platforms & serving stacks

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Together AI](together-ai.md) | Serverless open-model APIs + fine-tuning + rentable GPU clusters | platinum | ~$1.3B; $8.3B valuation (Jul 2026) | Chief scientist Tri Dao wrote FlashAttention; annualized bookings reported above $1.15B |
| [Fireworks](fireworks.md) | Speed-focused inference cloud (FireAttention) + managed RL fine-tuning | gold | ~$327M; $4B (reported $15B round in talks) | Cursor's Fast Apply runs on its speculative decoding; >10T tokens/day claimed |
| [Baseten](baseten.md) | "We are your inference team": dedicated deployments, Chains pipelines, 18-cloud capacity | gold | ~$2.1B; $13B (three rounds in ten months) | Bland AI's sub-400ms voice calls run on Chains; NVIDIA put in $150M |
| [FriendliAI](friendliai.md) | The team whose Orca paper invented continuous batching, selling the engine commercially | gold | ~$26M — 80x less than Baseten for the same category | Sued Hugging Face over its batching patent, settled, then became an official HF inference partner two weeks later |
| [Modular](modular.md) | Mojo language + MAX serving: hardware-agnostic inference across NVIDIA *and* AMD | gold | ~$380M; $1.6B | Chris Lattner (LLVM, Swift, MLIR) attacking CUDA lock-in; claims up to 53% over vLLM on AMD |
| [Venice](venice.md) | Privacy-first "uncensored" open-model API with a crypto payment rail | gold | $65M Series A at $1B — already profitable | Agents can pay for their own inference by staking VVV/DIEM tokens, no credit card |
| [Hugging Face](hugging-face.md) | The GitHub of ML: 2.4M-model Hub + Inference Providers routing layer | supporting | ~$400M; $4.5B (2023) | `transformers` is the industry's model interchange format; one API key fronts 15+ serving vendors |
| [Prime Intellect](prime-intellect.md) | Decentralized training: open INTELLECT model runs + an RL Environments Hub | supporting | ~$70M | Trained a 10B model across globally distributed, unreliable nodes — and open-sourced the whole pipeline |

## Routing & gateways

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [OpenRouter](openrouter.md) | One OpenAI-compatible endpoint over 400+ models from 60+ providers | supporting | ~$153M; $1.3B (May 2026) | ~25–29T tokens routed weekly; its public data underpins the "State of AI: 100 Trillion Token Study" |
| [Not Diamond](not-diamond.md) | Per-request meta-model that predicts which LLM will answer best/cheapest | supporting | $2.3M seed + undisclosed follow-on (SAP, IBM) | Middleware, not a gateway — it never sees your payloads; SAP built a prompt-optimization service on it |
| [Neurometric](neurometric.md) | "Automated token engineering": route agent sub-tasks to specialist SLMs, auto-generate one if none fits | bronze | $4M pre-seed | Claims one customer went from $40K/yr to $250/mo — company-sourced, zero named customers |

## Accelerator hardware

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [NVIDIA](nvidia.md) | The substrate under everything — plus Dynamo serving, NIM containers, and Nemotron open models | supporting | Public; ~$5T market cap, FY2026 revenue $215.9B | Now a major investor in its own customers (up to $30B into OpenAI) — the circularity is a live analyst concern |
| [Cerebras](cerebras.md) | Wafer-scale chips serving open models at ~1,000–3,000 tokens/sec | supporting | ~$3.1B private + $5.55B IPO (May 2026) | OpenAI signed a >$10B / 750MW deal for latency-sensitive agentic inference |
| [Etched](etched.md) | Sohu: inference-only ASIC sold as rack-scale systems | silver | ~$800M; ~$5B | Claims $1B+ in signed contracts before shipping a single production rack — all customers unnamed |

## Training data, fine-tuning & post-training

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [DatologyAI](datology-ai.md) | Automated pretraining-data curation: same model quality at a fraction of the compute | gold | ~$58M | Arcee's AFM-4.5B trained on its curated 8T tokens matched models trained on ~4x more data |
| [Datacurve](datacurve.md) | Frontier coding training data via Shipd, a gamified bounty platform for expert engineers | supporting | ~$17.5M | $1M+ paid out in bounties; founders were 19-year-old Waterloo students at YC W24 |
| [Unsloth](unsloth.md) | Two brothers' OSS library: ~2x faster fine-tuning at 70% less VRAM, plus the default GGUF quants | supporting | ~$500K — the leverage is OSS, not capital | 67.8K GitHub stars and 10M+ monthly Hugging Face downloads on roughly a seed round |
| [Trajectory](trajectory.md) | Continual learning: turns production corrections into weekly post-training updates | supporting | $15M seed (Conviction; Jeff Dean, Fei-Fei Li angels) | Runs 10,000+ concurrent microVM sandboxes for training/eval — real scale weeks after launch |
| [Applied Compute](applied-compute.md) | Train/serve/improve custom "Specific Intelligence" models on proprietary data | supporting | ~$160M at ~$1.3B (round details conflict across sources) | Ex-OpenAI founders (Codex, o1-era RL) at unicorn valuation within a year of founding |
| [Emissary](emissary.md) | Enterprise fine-tuning and eval service ("AI for the 99%") | bronze | ~$1.2M note (single-source) | Thinnest profile in the category: founders undisclosed, logos unconfirmed |
| [Veris](veris.md) | Simulation + RL environments to train and certify enterprise agents pre-production | bronze | $8.5M seed | "Train agents like employees" — arguably an evals company filed here for its RL-training angle |
| [AIDAChip](aidachip.md) | AI copilots with shared team context for semiconductor design | supporting | Undisclosed | Flagged in its own profile as a category misfit — it's EDA tooling, not model infrastructure |

## Related papers

The category's profiles keep citing the same research threads — these are the load-bearing ones:

**Agentic-SWE benchmarks** (the labs' headline numbers are SWE-bench/Terminal-Bench scores; these papers are how to read them):
- [Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) — the standing caveat on every vendor-reported score in the tables above (OpenAI, zAI, MiniMax, poolside, Not Diamond all cite-worthy).
- [SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md) and [SlopCodeBench: How Coding Agents Degrade Over Long Horizons](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) — the long-horizon regime that Codex, GLM-5.2, M2.7, and Trinity-Large-Thinking all claim; also why fast inference (Cerebras, Etched) matters: more repair iterations per wall-clock budget.
- [FeatureBench](../../papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md) and [ProdCodeBench](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md) — production-derived evaluation; Datacurve's DeepSWE benchmark is a commercial response to the same realism critique.
- [Reproducible, Explainable, and Effective Evaluations of Agentic AI for SWE](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md) — the trace-first eval stance Fireworks' Eval Protocol and Trajectory's instrument-then-train loop productize.

**Tool use & governance** (routing, structured output, and computer-use vendors live here):
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — the multi-tool orchestration framing cited by more profiles in this folder than any other paper.
- [Verifiable Software Worlds for Computer-Use Agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md) — the verifiability problem Amazon Nova Act's atomic `act()` + assertion design answers.
- [CaMeLs Can Use Computers Too](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) — DeepMind originated the CaMeL defense this extends; relevant to Nova Act, Operator, Project Mariner.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — the control-plane argument behind FriendliAI's engine-level structured output, OpenRouter's spend caps, and Trajectory's approval-gated updates.

**Voice/realtime** (inference latency is the product for a chunk of this category):
- [LTS-VoiceAgent](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md), [VoiceAgentRAG](../../papers/voice-realtime/voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md), and [τ-Voice](../../papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md) — the latency budgets that Baseten Chains, Cerebras wafer-scale decode, Modular's Inworld TTS work, and Etched's pitch all attack from different layers.
- [Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling](../../papers/voice-realtime/building-interactive-real-time-agents-with-asynchronous-i-o.md) — speculative execution at the agent layer; Fireworks' serving trick generalized.

**Memory** (fine-tuned small models are the standard substrate for memory/summarization components):
- [Memory for Autonomous LLM Agents](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) — cited by Together, Baseten, Unsloth, and Trajectory profiles; Trajectory's continual post-training is a weights-level alternative to this paper's memory-layer approaches.

## Open questions the category hasn't answered

1. **Margin durability as inference commoditizes.** Together, Fireworks, Baseten, and FriendliAI all sell OpenAI-compatible endpoints over the same open weights; the profiles' own "considerations" sections flag price undercutting in every direction. Who keeps margin when the API surface is identical?
2. **Does routing survive as an independent layer?** OpenRouter, Not Diamond, and Neurometric all bet yes — but frontier labs are absorbing model selection into their own products, and the null hypothesis (labs' in-product auto-selection wins) is unresolved.
3. **Vendor-reported benchmarks vs. reality.** Nearly every headline number in this folder — SWE-bench scores, tokens/sec, cost savings — is company-sourced. The category has no MLPerf-for-agents; the swe-agents papers above are the closest thing to an antidote.
4. **The jurisdiction split.** Chinese open weights (GLM, MiniMax M-series) lead on price-performance while sitting under Entity List and compliance clouds; US "sovereign" alternatives (Arcee Trinity, poolside Laguna) trail on capability. Which constraint binds first for enterprise buyers?
5. **Specialized silicon vs. shifting workloads.** Etched burned the transformer into silicon, then quietly added Mamba support; Cerebras is demand-constrained with 86% revenue concentration in UAE-linked entities. Both are giant bets that today's architecture and demand curve hold.
6. **Circular financing.** NVIDIA invests in OpenAI, Baseten, Fireworks, and Together while selling them all GPUs; OpenAI anchors Cerebras' order book. How much category revenue is real end-demand versus capital recycling is the question analysts keep asking and nobody has answered.

---
*Category curated 2026-07-05 from the 34 profiles in this folder. All 32 companies expected for this category are present; Venice (gold) and Prior Labs (silver) are additional profiles filed here. Placement flags noted in individual profiles: AIDAChip (EDA tooling), Moonlake AI (world models/simulation), Veris (agent evals/RL environments), and Datacurve (training-data supplier, trains no models) sit at the category's edges.*
