# Voice & Realtime — Paper Notes

Nine papers (Jan–Jun 2026, all located and verified on arXiv) on the hard problems of production voice agents: getting first audio out in under a second, deciding *when* to speak at all, grounding speech in tools and knowledge without blowing the latency budget, and measuring how much capability voice actually costs versus text. The through-line: realtime voice is an **architecture problem, not a model problem**. Every paper here either overlaps pipeline stages that naive stacks run serially, or benchmarks the failure modes that emerge when you don't.

## How to read this area

Start with three load-bearing entries:

1. **[Building Enterprise Realtime Voice Agents from Scratch](building-enterprise-realtime-voice-agents-from-scratch-a-te.md)** (Salesforce): the reference architecture. A full open cascaded pipeline (VAD → Deepgram STT → vLLM LLM → ElevenLabs TTS) hitting ~755ms time-to-first-audio, with a component-by-component latency budget you can hold any vendor against.
2. **[τ-Voice](tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md)**: the reality check. Full-duplex speech-to-speech models retain only **30–45% of their text-mode task capability** on real customer-service tasks; cascaded pipelines with a strong reasoning LLM may still win.
3. **[Building Interactive Real-Time Agents with Asynchronous I/O](building-interactive-real-time-agents-with-asynchronous-i-o.md)** (Berkeley): the most copyable design pattern. Speculate read-only tool calls on partial utterances and gate side-effecting calls on the final one, for 1.3–2.2× speedups.

The rest split along one axis: **latency engineering** (LTS-VoiceAgent, VoiceAgentRAG, RASST; each hides a different slow stage behind speculation or prefetching) versus **evaluation and turn policy** (τ-Voice, ProVoice-Bench, From Text to Voice, Adaptive Turn-Taking; each measures a decision the model gets wrong: when to speak, whether to intervene, whether it heard the arguments right).

Two convergent findings worth internalizing across the set: (a) speculation-with-rollback beats serial waiting everywhere it's tried, but always at a bounded accuracy or wasted-compute tax you must budget for; (b) models systematically **over-trigger** (false interruptions in multi-party calls, 0.9+ false-positive rates on proactive tasks), so suppression logic belongs in your application layer rather than in the model.

## Papers at a glance

| Paper | What it is | Headline finding |
|---|---|---|
| [Enterprise Realtime Voice Agents from Scratch](building-enterprise-realtime-voice-agents-from-scratch-a-te.md) | Salesforce's open 9-chapter tutorial building a cascaded pipeline | ~755ms end-to-end time-to-first-audio, self-hosted; realtime comes from streaming plus pipelining rather than one fast model |
| [τ-Voice](tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md) | Task-completion benchmark for full-duplex voice agents (τ²-bench in audio) | Voice agents keep only 30–45% of text capability; 79–90% of failures trace to agent behavior rather than simulator artifacts |
| [Async I/O + Speculative Tool Calling](building-interactive-real-time-agents-with-asynchronous-i-o.md) | Berkeley architecture: never block on user or tools | 1.3–1.7× cloud speedup at near-zero accuracy cost; safe/unsafe tool split as a side-effect firewall |
| [LTS-VoiceAgent](lts-voiceagent-a-listen-think-speak-framework-for-real-time.md) | Listen-Think-Speak cascade with a learned "when to start reasoning" trigger | 332–415ms first speech (vs 43–212s serial) at ~2 forward passes per query, but with a real accuracy tax on hard reasoning |
| [VoiceAgentRAG](voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md) | Salesforce dual-agent memory router: prefetch RAG chunks during pauses | 316× retrieval speedup (110ms → 0.35ms) at 75% cache hit rate; caveat: tiny 12-doc synthetic KB |
| [From Text to Voice](from-text-to-voice-a-reproducible-and-verifiable-framework.md) | Pipeline converting text tool-calling benchmarks into paired audio versions | Text→voice gap is only 2–5 points for top models and cascade-vs-native is a wash; failures concentrate in misheard argument values (54–57%) |
| [ProVoice-Bench](provoice-bench-assessing-the-proactivity-of-voice-agents.md) | First benchmark for *proactive* agents: when to speak unprompted | Over-triggering dominates: best-model false-positive rates up to 0.93; intent capture barely above chance |
| [Adaptive Turn-Taking (ModeratorLM)](adaptive-turn-taking-for-real-time-multi-party-voice-agents.md) | Amazon's role-conditioned speech LLM for multi-party turn-taking | Role conditioning gives >40% better precision / >70% better recall vs baselines; 0.01 false-interruption rate on real meetings |
| [RASST](rasst-retrieval-augmented-simultaneous-speech-translation.md) | Streaming cross-modal retrieval for simultaneous speech translation | ~40% relative terminology-accuracy gain at ≤16% decode overhead; trains the model to ignore bad retrievals |

## Maps to company categories

- **[Voice & realtime platforms](../../companies/voice-realtime/)**: the whole area is these companies' product surface. LiveKit, Daily, and Vapi are named in nearly every note (transport/orchestration these patterns run on); Deepgram, AssemblyAI, and Gradium get direct validation from the cascade-vs-native parity results and the transcript-dependence ablations; Twilio, Telnyx, and Plivo are the telephony rails where the latency and over-triggering findings bite hardest.
- **[Evals & observability](../../companies/evals-observability/)**: τ-Voice, ProVoice-Bench, and From Text to Voice are the academic versions of what Hamming AI sells, and paired text/audio suites are hostable metrics for Braintrust, Arize, and Weights & Biases.
- **[Models & inference](../../companies/models-inference/)**: OpenAI's Realtime API and Google's Gemini Live are the systems under test in τ-Voice and From Text to Voice; Amazon AGI Labs authored the turn-taking paper; Baseten, Fireworks, Together AI, and Cerebras own the fast-inference leg that every latency win here depends on.
- **[Memory, RAG & search](../../companies/memory-rag-search/)**: VoiceAgentRAG and RASST push vector stores (Qdrant, Pinecone, Turbopuffer, LanceDB) off the voice hot path: remote search must be prefetched or embedded to survive a 200ms budget.
- **[Agent orchestration](../../companies/agent-orchestration/)**: speculative tool-call DAGs with cancellation semantics (Berkeley paper) map onto Temporal's and Inngest's durable-execution models.

## Open questions the area hasn't answered

- **No cascaded baseline in the flagship benchmark.** τ-Voice tests only native speech-to-speech models; the stack most production teams actually run (STT→LLM→TTS) is unmeasured on the same tasks.
- **Synthetic audio everywhere.** Every benchmark here uses TTS-generated speech; real disfluencies, accents, barge-in, and 8kHz telephony codecs are consistently deferred, and the one naturalistic-speech test (Berkeley's "Human Instructions") cratered small-model accuracy.
- **The cost of speculation is unpriced.** Speculative tool calls, 5×10 prefetch retrievals per turn, dual Thinker/Speaker model streams: nobody reports the token/API spend these architectures add at scale.
- **Proactivity is unsolved.** Best models fire falsely up to 93% of the time on proactive-intent tasks; no paper yet combines the decision-quality work with latency measurement in one system.
