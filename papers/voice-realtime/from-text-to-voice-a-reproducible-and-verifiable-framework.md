# From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation

- **Status:** Located — [arXiv:2605.15104](https://arxiv.org/abs/2605.15104) (published title: "...for Evaluating Tool Calling LLM Agents")
- **Area:** voice-realtime
- **Authors / venue / date:** Md Tahmid Rahman Laskar, Xue-Yong Fu, Seyyed Saeed Sarfjoo, Quinten McNamara, Jonas Robertson, Shashi Bhushan TN. arXiv preprint, v1 May 14 2026, v2 May 20 2026.

## Problem
Voice agents need reliable tool calling, but nearly all tool-calling benchmarks are text-only, and building audio benchmarks from scratch means expensive re-annotation. Teams shipping voice agents also face an unresolved architectural question — ASR→text cascade vs. end-to-end omni-modal ("speech-native") models — with little controlled evidence either way.

## Approach
A dataset-agnostic pipeline that converts verified text tool-calling benchmarks into paired audio versions while preserving the original tool schemas, gold labels, and scoring, so text-vs-voice gaps are directly measurable. Mechanics: three TTS engines (Gemini-2.5-Flash, Gemini-2.5-Pro, GPT-4o-Mini), male/female speaker variation, and DEMAND environmental noise at 5–20 dB SNR; output is 16 kHz mono PCM WAV. Applied to two benchmarks: **Confetti** (313 instances; function selection + argument extraction in multi-turn conversation, AST-based soft accuracy) and **When2Call** (300 instances; call-vs-don't-call decisions, F1). Human validation: 97.7% of clean and 94.3% of noisy samples stayed faithful to source text. Includes an LLM-as-judge track where open-source judges substitute for proprietary ones (privacy-preserving eval).

## Key findings
- Seven omni-modal models evaluated. Best on Confetti (audio): Gemini-3.1-Flash-Live 70.4; best on When2Call: GPT-Realtime-1.5 71.9 — no single model wins both.
- Huge spread: Confetti audio scores run 70.4 down to 23.1 (Gemini-2.5-Flash-Live) / 23.3 (Phi-4-Multimodal).
- Text→voice gap is modest for top models: −1.8 (Qwen3-Omni), −2.6 (Gemini-3.1-Flash-Live), −4.8 (GPT-Realtime-1.5) points on Confetti.
- Cascade vs. direct voice is a wash: cascade +0.9 for Gemini-3.1-Flash-Live, direct +0.4 for GPT-Realtime-1.5, direct +1.5 for Qwen3-Omni.
- Dominant failure mode is **misheard/misinterpreted argument values**, not tool selection: 54–57% of paired failures for the GPT/Gemini leaders.
- Ambiguous-query stress test hurts far more than noise: Qwen3-Omni drops −24.6 points (62.2→37.6); noise degradation across SNR levels is comparatively modest.
- Open-source Qwen3-32B judge reaches >85% agreement with proprietary judges (Qwen3-8B: 80%).

## Limitations & open questions
Authors concede: only two datasets (no BFCL, τ-Bench, MCP coverage yet); TTS audio is a controlled proxy, not spontaneous speech with disfluencies, accents, barge-in; no cost/latency analysis. A skeptic would add: results use Gemini/GPT TTS to test Gemini/GPT listeners (possible same-family acoustic bias), and real telephony audio (8 kHz, codec artifacts) is harsher than 16 kHz WAV.

## Why builders should care
You don't need a bespoke audio benchmark — convert the text evals you already trust and measure the gap directly. Budget engineering effort for argument-value robustness (confirmation/read-back of names, numbers, IDs) rather than tool-selection prompting, since that's where voice failures concentrate; and don't assume speech-native beats a cascade — measure, because the difference is within ~1.5 points either way.

## Related companies in this landscape
- **Vapi, Daily, LiveKit** — voice-agent platforms/transport whose customers face exactly this cascade-vs-realtime-model choice; the paper says test both, per task.
- **Deepgram, AssemblyAI, Gradium** — STT/speech vendors; the near-parity cascade result keeps ASR-first architectures competitive for tool-calling agents.
- **Hamming AI** — voice-agent testing/evals; this framework is essentially a reproducible open-method version of what such products sell.
- **Braintrust, Arize, Weights & Biases** — eval/observability platforms that could host paired text-audio suites and the text-to-voice gap as a tracked metric.
- **Twilio, Telnyx** — telephony rails; the untested 8 kHz phone-audio condition is the obvious next stress test for their traffic.
- **OpenAI, Google DeepMind, Microsoft** — their realtime/omni models are the systems under test (GPT-Realtime, Gemini Live, Phi-4-Multimodal).

## Sources
- https://arxiv.org/abs/2605.15104
- https://arxiv.org/html/2605.15104v2
