# ProVoice-Bench: Assessing the Proactivity of Voice Agents

- **Status:** Located — [arXiv:2604.15037](https://arxiv.org/abs/2604.15037) (full title: "From Reactive to Proactive: Assessing the Proactivity of Voice Agents via ProVoice-Bench")
- **Area:** voice-realtime
- **Authors / venue / date:** Ke Xu, Yuhao Wang, Yu Wang; Interspeech 2026; submitted 2026-04-16 (v3 2026-05-02)

## Problem
Voice-agent benchmarks measure how well a model answers when spoken to. Nobody had measured the harder skill: knowing when to speak at all. A proactive agent must stay dormant through ambient conversation, then intervene at exactly the right trigger — hesitation, an alarm sound, a factual error — without butting in constantly. Existing evals overlook this intervention/dormancy decision entirely.

## Approach
First benchmark for proactive voice agents: 1,182 multimodal samples, balanced positive/negative, across four tasks:

- **Proactive Intent Capture (PIC):** infer implicit intent from cues (hesitation, action items) and initiate a tool request with confirmation
- **Latent Topic Monitor (LTM):** stay silent during ambient talk; intervene only on a user-specified semantic trigger
- **Environment Sound Sensing (ESS):** react to predefined acoustic events (alarms etc.)
- **Context Fact Checking (CFC):** interrupt when speech contradicts on-device digital context

Data comes from a five-stage synthesis pipeline: LLM-generated app states and scenes → speech via CosyVoice3 → acoustic simulation (−20 dBFS normalization, far-field filtering, room impulse responses) → assembly with Gaussian-sampled turn gaps and CochlScene ambient noise. Scored on accuracy, false-positive rate (FPR), recall, plus response accuracy via LLM-as-judge (Qwen3-80B).

## Key findings
- Over-triggering is the dominant failure. Best-model FPRs: PIC 0.934 (Step-Audio-R1), ESS 0.533, LTM 0.392 — models fire constantly rather than wait. Step-Audio-R1 hit 0.961 FPR on CFC.
- Best accuracies by task: CFC 0.838 (Qwen3-Omni, thinking), LTM 0.804, ESS 0.644, PIC 0.531 — barely above chance on intent capture.
- A "decision-to-execution" gap: even when models correctly decide to speak, response accuracy is only 0.484–0.759, with semantic drift and hallucinated tool calls.
- Chain-of-thought substantially helps analysis-heavy tasks (CFC, LTM, PIC); digital context is essential — removing it degrades both recall and accuracy.
- Evaluated: Mimo-Audio (7B), Qwen3-Omni (30B), Step-Audio-R1 (33B), Qwen2.5-Omni (7B), each ± CoT.

## Limitations & open questions
All audio is synthetic (TTS + simulated acoustics) — real-world barge-in, overlap, and codec artifacts untested. Judge is a single LLM (Qwen3-80B). Frontier closed models (GPT-4o Realtime, Gemini Live) appear absent from the evaluated set — I did not see them in the results (inferred). No latency measurement, which matters as much as decision quality in production proactivity.

## Why builders should care
If you're building an always-listening or meeting-resident agent, assume your model will over-trigger badly out of the box — the interruption-suppression logic has to live in your application layer (explicit trigger schemas, confidence gating, confirm-before-act). Also budget CoT-style reasoning before intervention decisions and pipe in digital context; both measurably move the needle.

## Related companies in this landscape
- **LiveKit / Daily** — realtime infra where proactive (full-duplex, always-on) agents run; this paper says the hard part is the decision layer above their transport.
- **Vapi** — voice-agent platform; proactivity failures (interrupting, hallucinated tool calls) are exactly its customers' production complaints.
- **Deepgram / AssemblyAI / Gradium** — streaming STT/speech stacks feeding the ambient-listening pipelines these tasks assume.
- **Hamming AI** — voice-agent evaluation; ProVoice-Bench's FPR/recall framing is a template for proactive-scenario test suites.
- **Twilio / Telnyx / Plivo** — telephony rails where over-triggering agents directly burn customer goodwill on live calls.

## Sources
- https://arxiv.org/abs/2604.15037
- https://arxiv.org/html/2604.15037
