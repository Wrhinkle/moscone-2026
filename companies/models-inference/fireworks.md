# Fireworks

> High-speed inference and fine-tuning cloud for open models — the platform Cursor, Notion, Uber, and DoorDash use to run customized open-weight LLMs in production instead of calling closed frontier APIs.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** 2022, Redwood City / San Francisco Bay Area, CA (Verified)
- **Website / GitHub:** https://fireworks.ai · https://docs.fireworks.ai · https://github.com/fw-ai

## What they do

Fireworks is an inference cloud for open-weight models (DeepSeek, Llama, Qwen, Kimi, Mixtral, plus image/audio models) exposed through an OpenAI-compatible API. Three consumption modes: serverless per-token endpoints, on-demand GPU deployments, and dedicated enterprise capacity (including BYO-cloud/VPC). The differentiation is a custom serving stack — the FireAttention engine (now V4, using FP4 precision on NVIDIA B200s to push >250 tokens/sec) plus speculative decoding and disaggregated serving — rather than stock vLLM. Verified scale claims from the Series C announcement (Oct 2025): 10,000+ customers, >10 trillion tokens processed per day, ~$280M annualized revenue.

The second product line is post-training. FireOptimizer covers LoRA and full-parameter SFT, DPO, and — since 2025 — Reinforcement Fine-Tuning (RFT), a managed RL service for tuning open models against your own reward functions. Fine-tuned LoRA models serve at the same per-token price as the base model, which materially changes the economics of maintaining many task-specific models. Alongside RFT they ship Eval Protocol, an open-source, language-agnostic framework for running RL on production agents using a trace-first evaluation approach (Reported — Fireworks' own blog/docs; the GitHub project exists).

Practically, what you'd buy: an OpenAI-drop-in endpoint for open models when latency/cost matters, or a pipeline where you distill/fine-tune a small open model on your traces and serve it 4–15x faster and cheaper than a frontier API.

## Founders & origins

Seven co-founders, mostly ex-Meta PyTorch (Verified across Sequoia, press, company site): **Lin Qiao** (CEO; co-creator and head of PyTorch at Meta, PhD UC Santa Barbara), **Dmytro Dzhulgakov** (CTO; PyTorch core maintainer), **Benny Chen** (Meta ads infra), **Chenyu Zhao** (Google Vertex AI), **Dmytro Ivchenko** (PyTorch for ranking at Meta), **James Reed** (PyTorch compiler), **Pawel Garbacki** (Meta Newsfeed core ML). Origin story: the team that ran PyTorch's production infrastructure at Meta rebuilt that serving expertise as a commercial inference platform.

## Funding

- **Series A:** $25M, early 2024, led by Benchmark, with Sequoia and Databricks Ventures (Verified).
- **Series B:** $52M, July 2024, led by Sequoia at a ~$552M valuation; participation from NVIDIA, AMD, Databricks Ventures, MongoDB Ventures (Verified).
- **Series C:** $250M, October 2025, at a $4B valuation, co-led by Lightspeed, Index Ventures, and Evantic; total raised ~$327M (Verified).
- **Reported (June–July 2026, unconfirmed):** in talks to raise at a ~$15B valuation; deal not closed as of 2026-07-02.

## Evidence of real-world use

Strong, documented usage — not just logos:

- **Cursor:** Fast Apply (instant code-edit application) runs on Fireworks' speculative decoding; publicly documented case study claiming it outperformed GPT-4 on speed for that task (Verified — Fireworks case study, widely cited).
- **Notion:** fine-tuned models on Fireworks, cutting a feature's latency from ~2s to ~350ms for 100M+ users (Reported — Fireworks/investor material).
- **Uber, DoorDash, Quora, Upwork, Verizon:** named production customers in Series B/C coverage (Reported).
- **Harvey (legal AI):** joint case study on RFT-tuned open agents beating closed models on cost + quality (Reported — Fireworks blog).
- Public pricing page, self-serve signup, and active docs — a real commercial product, not enterprise-only vaporware.

## Relevance to agentic AI engineering

Fireworks sits at the model-serving layer of the agent stack, but is pushing hard into the agent-training loop: RFT + Eval Protocol is essentially "turn your agent traces into a reward signal and RL-tune a small open model" — directly relevant to the trace-based evaluation ideas in *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering* and the cost/latency concerns behind *SlopCodeBench* (long-horizon agents burn tokens; cheap fast inference changes what's viable). The Cursor Fast Apply work is a concrete instance of the specialized-small-model pattern for coding agents benchmarked in *FeatureBench* and *ProdCodeBench* territory. Low-latency serving also matters for the voice-agent stack (*LTS-VoiceAgent*, *Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling* — speculative execution is literally Fireworks' serving trick applied at the agent layer).

## Use cases & considerations

Use cases: (1) drop-in cheap/fast open-model endpoint behind an agent router; (2) distill a frontier-model workflow into a fine-tuned small model once traces accumulate; (3) RFT a tool-calling agent against programmatic rewards; (4) dedicated VPC deployment where data can't leave.

Considerations: open-model-only (no OpenAI/Anthropic frontier models — you'll run multi-provider anyway); serving-stack lock-in is low (OpenAI-compatible API) but fine-tuning artifacts and RFT pipelines are stickier. Competitors: Together AI (closest, also in this repo), Baseten (also profiled here), Groq, Cerebras, DeepInfra, and hyperscaler offerings (Bedrock, Vertex). Open questions: margin durability as inference commoditizes, and whether the reported $15B round closes.

## Sources

- https://fireworks.ai/blog/series-c
- https://www.businesswire.com/news/home/20251028604819/en/Fireworks-AI-Raises-$250M-Series-C-to-Lead-the-AI-Inference-Market
- https://sequoiacap.com/podcast/training-data-lin-qiao/
- https://fireworks.ai/team
- https://siliconangle.com/2024/07/11/fireworks-ai-raises-52m-led-sequoia-522m-valuation/
- https://techfundingnews.com/nvidia-sequoia-invest-in-genai-startup-fireworks-ais-52m-round/
- https://sacra.com/c/fireworks-ai/
- https://fireworks.ai/blog/fireattention-v4-fp4-b200
- https://fireworks.ai/blog/fireworks-rft
- https://fireworks.ai/blog/eval-protocol-rl-on-your-agents
- https://fireworks.ai/blog/open-source-agents-frontier-advisors
- https://fireworks.ai/customers
- https://fireworks.ai/pricing
- https://docs.fireworks.ai/fine-tuning/fine-tuning-models
- https://www.indexventures.com/perspectives/inference-is-the-new-runtime-our-investment-in-fireworks/
- https://aiweekly.co/alerts/fireworks-ai-targets-15b-valuation-in-new-round
