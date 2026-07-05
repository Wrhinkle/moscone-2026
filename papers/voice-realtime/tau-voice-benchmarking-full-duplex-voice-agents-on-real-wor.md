# τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains

- **Status:** Located — [arXiv:2603.13686](https://arxiv.org/abs/2603.13686)
- **Area:** voice-realtime
- **Authors / venue / date:** Soham Ray, Keshav Dhandhania, Victor Barres, Karthik Narasimhan — arXiv preprint (cs.SD / cs.AI), submitted 2026-03-14

## Problem
Production voice agents are evaluated either on conversational dynamics (turn-taking, barge-in) or on task completion — never both together. Nobody has measured how much task-solving capability a full-duplex speech-to-speech agent actually loses relative to the same tasks in text, under realistic audio (noise, accents, interruptions).

## Approach
Extends τ²-bench into a voice benchmark: 278 verifiable customer-service tasks (Retail 114, Airline 50, Telecom 114) where success is checked against final database state (pass@1). A tick-based orchestrator exchanges exactly 200ms of audio per tick and decouples simulation time from wall-clock time, so the GPT-4.1-powered user simulator can make turn-taking decisions with no real-time latency constraint. Two conditions: **clean** (studio audio, American accents, no interruptions) and **realistic** (7 personas with diverse accents — Bengali, Mandarin, French- and Indian-influenced English — background noise, ~1/min burst sounds, ~2% frame drops, LLM-driven interruptions and backchanneling). Also scores voice-interaction quality: responsiveness, latency, interrupt rate, selectivity.

## Key findings
- Text baseline: GPT-5 (reasoning) hits **85%** pass@1 on identical tasks.
- Voice agents (gpt-realtime-1.5, gemini-live-2.5-flash-native-audio, grok-voice-agent): **31–51% clean**, **26–38% realistic** — retaining only **30–45% of text capability**.
- Provider trade-offs: xAI best completion (51%/38%) but 84% interrupt rate; OpenAI fastest (0.90s latency, 100% responsiveness) but 6% selectivity; Google most degradation-robust (−17% vs −24–28%), 21% interrupt rate.
- Ablations (Retail): accents −10pp on average (xAI loses 38%, Google nearly unaffected); turn-taking −7pp; noise −4pp.
- Error analysis of 91 failed simulations: **79–90% of failures are agent behavior** (logic errors, transcription failures during authentication, hallucinated completions), not simulator artifacts.

## Limitations & open questions
Authors concede: English-only, TTS rather than recorded speech (accent findings "indicative rather than definitive"); no naturalness/user-satisfaction/partial-credit scoring; the simulator is more patient than real users, with perfect memory and instant tool calls. A skeptic would add: only three proprietary speech-to-speech models tested — no cascaded STT→LLM→TTS pipeline baseline, which is what most production stacks actually run — and results may shift fast as realtime models iterate.

## Why builders should care
If your voice agent does anything transactional, assume roughly half-to-two-thirds capability loss versus the same model in text — and test with accents and interruptions, since degradation is provider-specific. Cascaded pipelines with a strong reasoning LLM may still beat native full-duplex models on task completion; benchmark before betting on speech-to-speech.

## Related companies in this landscape
- **Vapi, LiveKit, Daily, Telnyx, Twilio, Plivo** — voice-agent orchestration/transport platforms; the text-vs-voice gap is exactly the reliability problem their customers hit in production.
- **Deepgram, AssemblyAI, Gradium** — speech models/STT-TTS; validates cascaded pipelines as still competitive, and accent robustness as a differentiator.
- **Hamming AI** — voice-agent evaluation/testing; τ-Voice is the academic version of its product thesis.
- **OpenAI, Google DeepMind (Labs sponsors)** — their realtime models are the systems under test; the 26–51% scores are the headline.
- **Braintrust, Arize, Weights & Biases** — eval/observability platforms that would host this kind of grounded, pass@1-style voice eval.

## Sources
- https://arxiv.org/abs/2603.13686
- https://arxiv.org/html/2603.13686v1
- https://www.arunbaby.com/speech-tech/0066-tau-voice-benchmark-full-duplex-voice-agents/
