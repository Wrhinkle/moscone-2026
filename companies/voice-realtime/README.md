# Voice & Realtime

Voice/video agents, STT/TTS, realtime media infrastructure, telephony APIs, avatars/conversational video, and video understanding. This category exists because talking to software is brutally latency-sensitive: a usable voice agent has roughly one second (often much less) to hear you, transcribe you, think, call a tool, and start speaking back, over networks and phone lines that were never designed for it. Every company here sells one or more layers of that pipeline: the wires (telephony/CPaaS), the transport (WebRTC), the ears and mouth (STT/TTS models), the orchestration loop (turn-taking, interruptions, tool calls), or the face (realtime avatars and generative video). A smaller sub-cluster (TwelveLabs, Reactor, uRun) is video rather than voice, meaning machines understanding or generating video in real time; it lives here because it shares the same streaming-inference engineering problem.

## How to read this category

The axis that organizes everything is **which layer of the voice-agent stack you're buying**, from wires up to face:

1. **Telephony/CPaaS** (Twilio, Telnyx, Plivo): gets a phone call's audio into your code.
2. **Transport + agent framework** (LiveKit, Daily/Pipecat): WebRTC rooms and the open-source orchestration loop your agent code runs in.
3. **Speech models** (Deepgram, AssemblyAI, Gradium): the STT/TTS APIs plugged into that loop.
4. **Managed orchestration** (Vapi): the "buy" option that wraps layers 1–3 behind one API.
5. **Face/video layer** (HeyGen, LemonSlice; Reactor and uRun for generative video; TwelveLabs for video understanding): what sits on top of, or adjacent to, the voice loop.

The most load-bearing profiles are **[LiveKit](./livekit.md)** and **[Daily](./daily.md)**, the two open-source frameworks (LiveKit Agents, Pipecat) that nearly everything else in the category integrates with, plus **[Twilio](./twilio.md)**, the PSTN on-ramp that even competing platforms pay for. The second big fault line is **compose vs. buy**: assemble Twilio/Telnyx + Deepgram/AssemblyAI + LiveKit/Pipecat yourself, or pay Vapi (or Telnyx's all-in agent, or Deepgram's Voice Agent API) $0.05/min-ish to own the pipeline for you. Watch for vertical integration in both directions: telcos adding hosted agents, model vendors adding orchestration, and speech-to-speech models threatening to collapse the cascaded pipeline everyone here monetizes.

**Start here:**
- [LiveKit](./livekit.md): the transport + agents framework ChatGPT's Advanced Voice Mode runs on; the clearest picture of the whole reference architecture.
- [Twilio](./twilio.md): the incumbent whose ConversationRelay defines the "we do audio, you bring the LLM" seam.
- [Deepgram](./deepgram.md): the speech-model vendor pushing furthest into the agent loop (Flux folds turn-taking into the recognizer itself).
- [Vapi](./vapi.md): what "just buy the whole voice agent" looks like at production scale (Amazon Ring routes 100% of inbound calls through it).

## Companies

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [AssemblyAI](./assemblyai.md) | Speech-to-text / speech-understanding API; the ears under many voice agents | Gold | ~$115M through Series C (Dec 2023); no round since | Universal-3 Pro makes ASR "promptable": keyterm prompting is context engineering pushed into the speech layer |
| [Daily](./daily.md) | WebRTC APIs + Pipecat, the most widely adopted open-source voice-agent framework | Gold | >$60M through Series B (2021); nothing disclosed since | NVIDIA, AWS, and Google all publish first-party guides/repos built on Pipecat |
| [Deepgram](./deepgram.md) | STT + TTS + managed Voice Agent API, cloud or self-hosted | Silver | $215M+; $130M Series C at $1.3B (Jan 2026); cashflow positive in 2025 | NASA uses it on ISS–Mission Control comms; self-host containers serve air-gapped deployments |
| [Gradium](./gradium.md) | Kyutai spinout selling ultra-low-latency streaming TTS/STT and voice cloning | Gold | $70M seed (Dec 2025), one of Europe's largest | Team behind Moshi, the full-duplex speech model that responds in ~160ms |
| [HeyGen](./heygen.md) | Talking-avatar video generation plus a realtime streaming-avatar API (LiveAvatar) | Supporting | ≥$75M verified (Series B at ~$2B reported); ~$95–100M ARR reported | Streaming avatar API is BYO-LLM over LiveKit-backed WebRTC: a face you bolt onto any agent |
| [LemonSlice](./lemonslice.md) | Turns a single still image into a live, talking two-way video call | Supporting | $10.5M seed (Matrix, YC) | One headshot or illustration becomes a real-time conversational avatar, with no footage-capture step |
| [LiveKit](./livekit.md) | Open-source WebRTC SFU + Agents framework + managed cloud | Gold | ~$183M; $100M Series C at $1B (Jan 2026) | OpenAI built ChatGPT's Advanced Voice Mode on LiveKit Cloud |
| [Plivo](./plivo.md) | Lower-cost Twilio-alternative CPaaS with WebSocket audio streaming for voice agents | Supporting | $1.75M seed; reportedly ~$100M ARR on minimal outside capital | Possibly the most capital-efficient company in the category |
| [Reactor](./reactor.md) | SDK/API for real-time generative video / interactive "world models" | Supporting | $59M Series A (Lightspeed, May 2026) | Ex-Apple Vision Pro founders; near-zero time-to-first-frame claim. The AIEWF sponsor link (reactorhq.com) is a parked domain, so the profile marks the identification as Reported, pending confirmation |
| [Telnyx](./telnyx.md) | CPaaS that owns its network and GPUs, plus an all-in-one $0.05/min voice-AI agent | Gold | ~$11M raised; essentially revenue-funded at carrier scale | Claims sub-200ms round-trip by co-locating telephony PoPs with inference GPUs; contesting a first-of-its-kind $4.49M FCC KYC fine |
| [TwelveLabs](./twelvelabs.md) | Video-native foundation models (search, analyze, embed) as APIs | Supporting | ~$207M; $100M Series B (Jul 2026) with Amazon | Cut MLSE's 16-hour highlight-retrieval job to ~9 minutes; first video-understanding models on Bedrock. Video understanding, not voice: a perception tool agents call |
| [Twilio](./twilio.md) | The incumbent CPaaS; ConversationRelay pipes live call audio to any LLM you bring | Gold | Public (NYSE: TWLO); $5.07B FY2025 revenue | Voice AI revenue grew 49% YoY in 2025; Twilio gets paid even when competitors win the agent layer |
| [uRun](./urun.md) | Early-stage "runtime for AI video": live-steerable, continuously generated interactive video | Supporting | Not found in public sources | Pre-launch posture ("the runtime is coming"); founders, funding, and customers all unverified as of Jul 2026 |
| [Vapi](./vapi.md) | Managed voice-agent platform: define an assistant, Vapi runs the whole pipeline | Silver | $72M; $50M Series B at ~$500M (May 2026) | Amazon Ring evaluated 40+ vendors and routes 100% of inbound calls through Vapi; 1B+ calls processed |

**Coverage note:** all 12 companies expected in this category are present, plus two more: **Daily** (gold sponsor; its profile's closing note says "filed under consumer-ai per assignment," but the file lives here and voice-realtime is clearly the right home) and **Gradium** (gold sponsor, Kyutai spinout). Nothing expected is missing.

## Related papers

The repo's [voice-realtime paper notes](../../papers/voice-realtime/) are effectively the research shadow of this category; every profile above cites them. The mapping:

- [Building Enterprise Realtime Voice Agents from Scratch](../../papers/voice-realtime/building-enterprise-realtime-voice-agents-from-scratch-a-te.md): the tutorial that hand-builds the exact cascaded pipeline (VAD → streaming STT → LLM → streaming TTS) that LiveKit/Pipecat package and Vapi/Telnyx/Deepgram sell as a service. Read first to understand what everyone here abstracts.
- [Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md): moves the "is it my turn?" decision out of VAD heuristics and into the model itself; the research counterpart of Deepgram Flux, LiveKit's turn detector, and Twilio's barge-in handling.
- [LTS-VoiceAgent](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md): incremental reasoning on partial transcripts to cut time-to-first-speech; the latency problem every vendor's sub-second claim is about.
- [VoiceAgentRAG](../../papers/voice-realtime/voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md): retrieval eats the ~200ms budget; speculative pre-fetching to fix it. Relevant to any knowledge-grounded agent on Vapi/LiveKit/Pipecat.
- [Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling](../../papers/voice-realtime/building-interactive-real-time-agents-with-asynchronous-i-o.md): overlapping reasoning and tool round-trips with speech; the same latency attack from the tool-calling side.
- [From Text to Voice: Voice Tool-Calling Evaluation](../../papers/voice-realtime/from-text-to-voice-a-reproducible-and-verifiable-framework.md): measures how much tool-calling accuracy voice costs vs. text; directly tests the failure mode (mis-transcribed entities → bad tool arguments) that AssemblyAI's and Deepgram's keyterm prompting target.
- [τ-Voice](../../papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md): task completion + conversational dynamics under realistic audio; how you'd benchmark a Gradium/Moshi-style full-duplex agent or a Vapi deployment before trusting vendor dashboards.
- [ProVoice-Bench](../../papers/voice-realtime/provoice-bench-assessing-the-proactivity-of-voice-agents.md): measures knowing *when* to speak at all (dormancy vs. intervention); the frontier past barge-in handling.
- [RASST](../../papers/voice-realtime/rasst-retrieval-augmented-simultaneous-speech-translation.md): retrieval-augmented simultaneous speech translation for rare terminology; maps to Gradium's speech-translation endpoints and multilingual support lines.

For the video-understanding corner (TwelveLabs as an agent's perception tool), see also [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md), [Do Agents Need Semantic Metadata?](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md), and [Memory for Autonomous LLM Agents](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md).

## Open questions

1. **Does speech-to-speech collapse the cascade?** Nearly every business model here monetizes a layer of the STT→LLM→TTS pipeline. If end-to-end speech models (OpenAI Realtime, Moshi-lineage) reach production quality, standalone STT/TTS vendors and pipeline orchestrators both get squeezed; Gradium is the hedge, since it owns the research either way.
2. **Who owns the agent layer vs. the plumbing?** Twilio, Telnyx, Deepgram, and LiveKit are all climbing up-stack toward Vapi's territory while remaining Vapi's suppliers. Several profiles in this folder flag that dynamic: a platform dependency today can turn into a direct competitor (yours or your vendor's) within a product cycle.
3. **Do vendor latency claims survive third-party measurement?** Telnyx's sub-200ms, Vapi's sub-600ms, and HeyGen's sub-second avatar claims are all vendor-reported. τ-Voice/ProVoice-Bench-style independent benchmarks for commercial stacks barely exist yet.
4. **What does governance look like for agents that place calls?** The FCC's $4.49M KYC action against Telnyx and HeyGen's deepfake track record point the same direction: identity, consent, STIR/SHAKEN attestation, and provenance are becoming hard requirements, and no one in the category has a complete answer.
5. **Capital structure whiplash.** The category spans a public company at $5B revenue, a $1.3B unicorn, an ~$11M-raised carrier, an ARR-rich bootstrap (Plivo), and a pre-launch site with no verifiable founders (uRun). Sponsor tier at AIEWF is a poor proxy for substance here; read the funding-posture column skeptically in both directions.
