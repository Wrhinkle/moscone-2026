# Building Enterprise Realtime Voice Agents from Scratch: A Technical Tutorial

- **Status:** Located — [arXiv:2603.05413](https://arxiv.org/abs/2603.05413)
- **Area:** voice-realtime
- **Authors / venue / date:** Jielin Qiu, Zixiang Chen, Liangwei Yang, Ming Zhu, Zhiwei Liu, Juntao Tan, Wenting Zhao, Rithesh Murthy, Roshan Ram, Akshara Prabhakar, Shelby Heinecke, Caiming Xiong, Silvio Savarese, Huan Wang (Salesforce AI Research). arXiv cs.SD, v1 2026-03-05, v2 2026-03-17.

## Problem
25+ speech-to-speech models exist, but there is no public codebase that builds a complete streaming enterprise voice agent from scratch — production frameworks (LiveKit, Pipecat-style stacks) are opaque, and fully self-hosted realtime end-to-end speech models effectively don't exist. Builders can't see where latency actually comes from or how the pieces compose.

## Approach
A 9-chapter progressive tutorial (with tested code) building a cascaded streaming pipeline: Silero VAD (2MB, CPU) → Deepgram Nova-3 streaming STT → vLLM-served Qwen2.5-7B with OpenAI-protocol function calling → ElevenLabs streaming TTS, over WebSockets with browser AudioWorklet clients. Core thesis: **realtime = streaming + pipelining**, not one fast model — a sentence buffer bridges the LLM token stream to TTS so components overlap. Turn-taking is a VAD state machine (IDLE → LISTENING → PROCESSING at 700ms silence → SPEAKING, with a SPEAKING → INTERRUPTED barge-in path plus echo gating). Demo: hospital receptionist with five tools (check/schedule/cancel appointments, patient/doctor info) and multi-step tool chains.

## Key findings
- End-to-end time-to-first-audio: **~755ms measured** (best case 729ms) for the full self-hosted cascaded pipeline.
- Latency budget (P50): STT 337–402ms; LLM TTFT 337ms (Qwen2.5-7B, vLLM 0.8.5, H200, 34ms inter-token); TTS TTFB 219–221ms (eleven_turbo_v2_5, 0.05–0.10x RTF).
- Native speech-to-speech comparison: Qwen2.5-Omni local ~13.2s TTFA (unusable realtime); Qwen3-Omni via DashScope cloud ~702ms but not self-hostable and only partial function calling; local Qwen3-Omni runs Thinker-only (no audio out). Transformers backend is 4.6 vs 168 tok/s on vLLM.
- Audio plumbing: 20ms PCM int16 chunks at 16kHz in (640 bytes), 24kHz out.

## Limitations & open questions
Authors concede no self-hosted realtime end-to-end model exists yet, LLM TTFT variance is high (278–784ms on cloud APIs), and this is a teaching resource, not a benchmark suite. A skeptical builder would ask: no telephony (PSTN/WebRTC) transport, no multi-party or overlapping-speech handling, fixed 700ms silence threshold is crude turn-taking, and no task-success evaluation at scale.

## Why builders should care
If you're building a voice agent, cascaded still beats end-to-end for self-hosted enterprise deployment — spend your effort on pipelining and sentence-boundary buffering, not model hunting. The ~755ms TTFA figure is a concrete, reproducible latency budget to hold vendors and your own stack against.

## Related companies in this landscape
- **Deepgram** (Silver) — its Nova-3 streaming STT is the paper's chosen transcription layer; the tutorial is effectively a reference integration.
- **AssemblyAI** (Gold) — direct competitor STT; the published latency budget (337–402ms P50) is the bar to beat.
- **LiveKit** (Gold) / **Daily** (Gold) — the "opaque framework" alternative the paper contrasts; validates their transport/orchestration value while demystifying it.
- **Vapi** (Silver) — hosted voice-agent platform; this paper is the build-vs-buy counterargument, and its numbers frame Vapi's pricing conversation.
- **Twilio / Telnyx / Plivo** — telephony transports the tutorial omits; the missing chapter for real call-center deployment.
- **Baseten / Fireworks / Together AI / Modal / RunPod** — self-hosted vLLM serving (the LLM leg of the 755ms budget) is exactly their product.
- **Hamming AI** — voice-agent evaluation; the paper's admitted lack of a benchmark suite is Hamming's opening.

## Sources
- https://arxiv.org/abs/2603.05413
- https://arxiv.org/html/2603.05413v2
- https://www.alphaxiv.org/overview/2603.05413v2
