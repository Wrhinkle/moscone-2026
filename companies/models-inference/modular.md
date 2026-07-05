# Modular

> Modular builds a hardware-agnostic AI inference stack — the Mojo language, the MAX serving framework, and the Mammoth cluster control plane — so you can run models fast on NVIDIA or AMD GPUs without writing CUDA.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** 2022, Silicon Valley (Los Altos/Palo Alto area), CA — **Verified**
- **Website / GitHub:** [modular.com](https://www.modular.com/) · [github.com/modular/modular](https://github.com/modular/modular)

## What they do

Modular is attacking the CUDA lock-in problem: the fact that most production inference is welded to NVIDIA's software stack. Their platform has three layers. **Mojo** is a Python-superset systems language (built on MLIR, which CEO Chris Lattner created at Google) for writing GPU/CPU kernels — you get Python-like syntax with C/Rust-level performance and direct GPU programmability. **MAX** is the inference framework and serving engine: an OpenAI-compatible endpoint that runs popular open-weight models with graph compilation and a streaming-aware scheduler, positioned head-to-head against vLLM, SGLang, and TensorRT-LLM. **Mammoth** (announced 2025, managed endpoints coming 2026) is a Kubernetes-native control plane for enterprise-scale deployments: disaggregated prefill/decode, intelligent routing, multi-model orchestration.

The practical pitch to an engineer: one container that serves the same model on NVIDIA and AMD GPUs with no code changes, letting you burn existing NVIDIA commitments and scale into cheaper AMD capacity. Modular claims MAX beats vLLM by up to 53% throughput on prefill-heavy and 32% on decode-heavy BF16 workloads on AMD MI-series hardware (**Reported** — Modular's own benchmarks). Deployment model: Modular runs the control plane, inference runs in your VPC on your hardware.

## Founders & origins

- **Chris Lattner (CEO)** — creator of LLVM, Clang, Swift, and MLIR; previously Apple, Tesla (Autopilot), Google (TPUs/MLIR), SiFive. **Verified**
- **Tim Davis (President)** — led ML product at Google (TensorFlow ecosystem). **Verified**

The two met at Google and founded Modular in 2022 out of frustration with AI's fragmented compute infrastructure — the "unified compute layer" thesis. **Verified** (company about page, press).

## Funding

- Seed: $30M, June 2022, GV among leads — **Verified**
- Series B: $100M, August 2023, led by General Catalyst, ~$600M valuation — **Verified**
- Series C: $250M, September 2025, led by U.S. Innovative Technology Fund, with DFJ Growth, GV, General Catalyst, Greylock; $1.6B post-money — **Verified** (multiple press sources)
- **Total raised: ~$380M** as of 2026-07-02.

## Evidence of real-world use

Strong and unusually concrete for an infra company:

- **Inworld AI**: co-engineered TTS pipeline on NVIDIA Blackwell in under 8 weeks; Inworld TTS 1 Max ranked #1 on the Artificial Analysis speech leaderboard, with ~70% faster time-to-first-audio and ~60% lower cost claimed. **Verified** (case study + leaderboard coverage).
- **TensorWave** (AMD-based GPU cloud): claims up to 70% cost savings serving on AMD via MAX. **Reported**.
- **Hippocratic AI** (healthcare voice agents) named as a customer. **Reported** (Modular customers page).
- Hardware-vendor case studies with **AMD**, **NVIDIA**, and **AWS** — genuine engineering partnerships, not just logos (SOTA results on AMD MI355X within two weeks of that GPU's launch).
- OSS traction: ~24k+ GitHub stars, Mojo stdlib and MAX Python API open-sourced (Apache 2.0 w/ LLVM exceptions), 450k+ lines of open Mojo kernel code, ~22k-member Discord. **Verified**.

Caveat: no public self-serve pricing page; commercial motion is enterprise/partner-led, so paying-customer breadth is hard to gauge from outside.

## Relevance to agentic AI engineering

Modular sits at the serving layer beneath agents: anyone running open-weight models for agent loops (high-QPS tool-calling, long-context planning, disaggregated prefill/decode for bursty agent traffic) is choosing between vLLM, SGLang, and MAX. Latency economics matter most where this repo's **voice-agent papers** live — the Inworld TTS result is directly about time-to-first-audio for conversational agents, the same constraint those papers analyze. Cheap, fast self-hosted inference also changes the cost calculus for the heavy sampling regimes in the **agentic SWE benchmark** literature (many-rollout eval and repair loops), and Mammoth's multi-model routing is the infra substrate for the multi-model orchestration patterns discussed in the **tool-use/governance** work. No direct connection to agent-memory research — Modular is below that layer.

## Use cases & considerations

Use cases: (1) self-hosting open-weight LLMs for agent backends with an OpenAI-compatible endpoint; (2) hedging NVIDIA supply/cost by making AMD capacity usable without a rewrite; (3) writing custom kernels or novel model architectures in Mojo instead of CUDA; (4) low-latency speech/voice pipelines (the proven case study).

Considerations: performance claims are mostly Modular-published — benchmark on your own workload. vLLM and SGLang are free, huge-community defaults; Modular's edge must be sustained perf plus AMD portability. Mojo is still maturing as a language (compiler not fully open source yet). Enterprise pricing is opaque. Betting on Mammoth before its 2026 GA is a roadmap bet — though Lattner's compiler-infrastructure track record (LLVM, MLIR became industry standards) is the strongest argument the platform endures.

## Sources

- https://www.modular.com/company/about
- https://www.modular.com/blog/modular-2025-year-in-review
- https://www.modular.com/customers
- https://www.modular.com/case-studies/amd
- https://www.modular.com/case-studies/inworld
- https://github.com/modular/modular
- https://www.sdxcentral.com/news/modular-raises-250m-for-ais-unified-compute-layer-at-16b-valuation/
- https://sacra.com/c/modular/
- https://finance.yahoo.com/news/modular-secures-250m-expand-unified-090144970.html
- https://en.wikipedia.org/wiki/Mojo_(programming_language)
- https://www.modular.com/blog/the-next-big-step-in-mojo-open-source
