# Deepgram

> Voice AI infrastructure company: speech-to-text, text-to-speech, and a managed voice-agent API, sold as low-latency usage-priced APIs (cloud or self-hosted) — one of the two default STT choices under today's voice-agent stacks.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** silver
- **Founded:** 2015, San Francisco (Verified — YC W16; company and press agree)
- **Website / GitHub:** https://deepgram.com — https://github.com/deepgram

## What they do

Deepgram trains and serves its own end-to-end deep-learning speech models behind APIs. The core pieces as of mid-2026:

- **Nova-3** (Feb 2025) — flagship STT for both pre-recorded (REST) and streaming (WebSocket) audio, with word timestamps, diarization, multilingual/code-switching, and **keyterm prompting** to bias recognition toward domain vocabulary. Public pricing ~$0.0048/min streaming, ~$0.0077/min pre-recorded (Verified — pricing page).
- **Aura-2** (Apr 2025) — low-latency TTS voices tuned for conversational agents rather than long-form narration.
- **Voice Agent API** — a single WebSocket that orchestrates the full listen–think–speak loop (STT + your LLM + TTS) with barge-in/interruption handling, so you skip wiring the pipeline yourself.
- **Flux** (late 2025) — a "conversational speech recognition" model that folds turn-taking/endpointing decisions into the recognizer itself instead of leaving them to VAD heuristics; positioned specifically for voice agents, used alongside or instead of Nova-3 streaming.

A real differentiator vs. most rivals: **self-hosted deployment** (on-prem or VPC containers) for regulated/air-gapped environments — consistent with In-Q-Tel being an investor and NASA being a documented user. Practically, you integrate via official SDKs, pay per minute with $200 free credits to start, and it's already a first-class option inside voice-agent frameworks (LiveKit Agents, Pipecat, Vapi, Twilio).

## Founders & origins

**Scott Stephenson** (CEO) and **Noah Shutty**, University of Michigan particle physicists — Stephenson has a PhD and worked on a dark-matter detector two miles underground; the waveform-analysis ML from that work became the seed of Deepgram (Verified — multiple interviews, YC profile). **Adam Sypniewski** is also named as a third co-founder/founding CTO in several accounts (Reported). They wanted an API to search/analyze audio, found none good enough, and built it; YC batch 2016.

## Funding

- Seed/early rounds 2016–2020 (Verified existence; ~$12M Series A era per databases).
- **Series B: $72M total** — $25M (Feb 2021, Tiger Global) plus **$47M extension (Nov 2022, led by Madrona**, with Alkeon) (Verified — company blog, PitchBook).
- **Series C: $130M, Jan 13 2026, at $1.3B valuation, led by AVP**, with Alkeon, In-Q-Tel, Madrona, Tiger, Wing, Y Combinator, BlackRock-managed funds; new strategic investors Twilio, ServiceNow Ventures, SAP, Citi Ventures, plus university endowments (Michigan, Columbia, joining Stanford) (Verified — TechCrunch + company press release).
- **Total raised: $215M+** (TechCrunch); Tracxn lists ~$229M — treat $215M as the floor. TechCrunch reports the company was **cashflow positive** in 2025 (Reported — company statement via press).
- Acquired **OfOne**, a YC-backed voice-ordering startup for quick-service restaurants, alongside the Series C (Verified).

## Evidence of real-world use

Strong and specific. **NASA** uses Deepgram on ISS–Mission Control space-to-ground comms (documented, with an 89.6% word-recognition figure against an 80% requirement). **Five9** processes billions of call minutes annually through it (case study with accuracy/authentication metrics). Other named users: **Twilio, Spotify, Citi, TIAA, Talkdesk, Observe.AI, Vapi, Granola, Vida Health, Abby Connect** — several with real case-study detail, not just logos. Company/press figures: 1,300+ organizations, 200k+ developers, 10,000+ years of audio processed (Reported — company numbers). Public pricing page, active docs, SDKs, and default-option status in LiveKit/Pipecat/Vapi stacks are all independent traction signals; like AssemblyAI, it's the perennial benchmark comparison target in third-party STT shootouts.

## Relevance to agentic AI engineering

Deepgram is the ears (and increasingly the whole mouth-and-ears loop) of the voice-agent stack this repo's voice papers study. *Building Enterprise Realtime Voice Agents from Scratch* maps directly onto the Nova-3 + Aura-2 + Voice Agent API pipeline and its latency budget. Flux is a productized answer to the endpointing/turn-taking problem in *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents* and *LTS-VoiceAgent*. Keyterm prompting addresses the entity-transcription failure mode behind bad tool-call arguments in *From Text to Voice: ...Voice Tool-Calling Evaluation*, and streaming-STT latency is the input constraint in *VoiceAgentRAG*. The self-host option matters for tool-use/governance-sensitive deployments where audio can't leave the tenant.

## Use cases & considerations

Use cases: (1) STT/TTS under a phone-based agent (e.g., a contractor back office answering/qualifying inbound calls — pairs with the Twilio/Vapi/LiveKit route); (2) batch transcription of job-site or adjuster calls into structured CRM notes; (3) fully managed voice agent via the Voice Agent API when you don't want to own the pipeline; (4) on-prem transcription for compliance-bound audio.

Considerations: proprietary models (no open weights — self-host is licensed containers, not freedom); Voice Agent API convenience trades against pipeline lock-in; accuracy leadership flips model-to-model — benchmark on *your* audio vs. **AssemblyAI, OpenAI (Whisper/Realtime), ElevenLabs, Speechmatics, Gladia, Cartesia**, and the hyperscalers. Open questions: whether end-to-end speech-to-speech models commoditize the STT/TTS split, and how far the OfOne acquisition signals a move up-stack into vertical voice agents that compete with its own customers.

## Sources

- https://techcrunch.com/2026/01/13/deepgram-raises-130m-at-1-3b-valuation-and-buys-a-yc-ai-startup/
- https://deepgram.com/learn/press-release-deepgram-raises-series-c
- https://deepgram.com/learn/deepgram-72-million-series-b-defines-future-of-AI-speech-understanding
- https://pitchbook.com/newsletter/deepgram-extends-series-b-with-47m
- https://www.ycombinator.com/companies/deepgram
- https://www.madrona.com/founded-funded-deepgram-scott-stephenson/
- https://deepgram.com/learn/introducing-nova-3-speech-to-text-api
- https://deepgram.com/learn/introducing-ai-voice-agent-api
- https://developers.deepgram.com/docs/flux/flux-nova-3-comparison
- https://deepgram.com/pricing
- https://deepgram.com/enterprise
- https://www.businesswire.com/news/home/20240312857580/en/Deepgram-Launches-Aura-a-Text-to-Speech-API-for-Real-Time-Conversational-Voice-AI-Agents
- https://tracxn.com/d/companies/deepgram/__ThWYvD43I1HgSdguaRgcoZ1dLjXMEMfCv1tzktOKL2k/funding-and-investors
- https://brasstranscripts.com/blog/deepgram-pricing-per-minute-2025-real-time-vs-batch
