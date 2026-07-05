# AssemblyAI

> Speech-to-text and speech-understanding API company: you send audio (files or live streams), you get back accurate transcripts plus structured extras (diarization, summaries, PII redaction) — the ASR layer under many voice agents and conversation-intelligence products.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** 2017, San Francisco (Verified — YC S17; founder accounts and Contrary Research agree)
- **Website / GitHub:** https://www.assemblyai.com — https://github.com/AssemblyAI

## What they do

AssemblyAI sells API access to its own speech models. Two integration shapes matter: **async (pre-recorded)** — POST an audio file/URL, poll or webhook for a JSON transcript with word-level timestamps, speaker diarization, punctuation/casing, and optional "audio intelligence" add-ons (summarization, sentiment, topic detection, PII redaction) — and **streaming** — a WebSocket that returns partial and final transcripts with low enough latency to sit inside a voice-agent loop (STT → LLM → TTS).

The model line has moved fast. **Universal-2** (Nov 2024) was their flagship general ASR model. **Slam-1** (2025) introduced a "promptable" speech language model — you pass key terms/context in the request to bias recognition toward domain vocabulary (since deprecated in favor of the Universal-3 line). **Universal-Streaming** (mid-2025) is a voice-agent-specific streaming model at $0.15/hr session-based pricing with unlimited concurrency. The current flagships are **Universal-3 Pro** (async, early 2026) and **Universal-3 Pro Streaming** (March 2026): promptable speech language models with keyterm prompting, disfluency control, code-switching, real-time diarization, and 99+ language claims. October 2025 also added multilingual streaming (ES/FR/DE/IT/PT), safety guardrails, and an LLM gateway (LeMUR lineage: run LLM tasks over transcripts through their API). A Speech-to-Speech API was announced in beta alongside Universal-3 Pro (Reported — announced, maturity unverified as of 2026-07-05).

Practically: it's a hosted, usage-priced ASR vendor with a public pricing page (~$0.15/hr streaming; async priced per hour with volume discounts), official SDKs (Python/JS/etc.), and integrations into voice-agent frameworks (LiveKit, Pipecat, Vapi).

## Founders & origins

**Dylan Fox**, solo founder and CEO (Verified). Previously a software/research engineer at Cisco working on AI features; left in 2017, applied to Y Combinator past the deadline with a video demo, and was accepted (YC S17). Origin story — betting that incumbents (Google/AWS speech APIs) had subpar developer experience and that new ML architectures would let a focused startup win on accuracy + DX — is consistently documented across interviews (Contrary Research, Voicebot, Accel podcast).

## Funding

- Seed rounds post-YC, 2017–2019 (Verified existence; amounts small, ~$1–9M range per databases).
- **Series A: $28M, March 2022, led by Accel** (Verified).
- **Series B: $30M, July 2022, led by Insight Partners**, with Accel, YC, Nat Friedman & Daniel Gross (Verified).
- **Series C: $50M, December 2023, led by Accel**, with Keith Block/Smith Point Capital, Insight Partners, Daniel Gross & Nat Friedman, YC (Verified — company blog + press).
- **Total: ~$115M** per the company's own Series C post (Verified); some databases (Tracxn/Signalbase) list ~$158M total — discrepancy unresolved, treat $115M as the floor. Valuation ~$300M at Series C (Reported — Getlatka/secondary-market sources). No post-2023 round found in public sources as of 2026-07-05.

## Evidence of real-world use

Strong. Named, documented customers with case-study detail — not just logos: **CallRail** (dedicated customer story: +23% transcription accuracy, doubled conversation-intelligence customers), **Fireflies.ai** (meeting notes), **Veed.io** (auto captions/subtitles), plus Typeform, Close, Loop Media; Spotify appears in customer lists (Reported). Company claims 25M+ inference calls and 10TB+ of audio processed daily (Reported — company figures). Public pricing page, active docs, official SDKs, and first-party integrations in the major voice-agent orchestration stacks (LiveKit Agents, Pipecat, Vapi) are all real commercial-traction signals. Frequently benchmarked head-to-head with Deepgram and Whisper in third-party comparisons — being the default comparison point is itself a usage signal.

## Relevance to agentic AI engineering

AssemblyAI is the **ears** of the voice-agent stack: the streaming-STT box in every realtime pipeline this repo's voice papers study. Directly relevant: *Building Enterprise Realtime Voice Agents from Scratch* (STT/LLM/TTS pipeline latency budgets), *LTS-VoiceAgent* and *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents* (endpointing/turn-detection depends on streaming-ASR finality semantics — exactly what Universal-Streaming's "immutable transcripts" target), *VoiceAgentRAG* (STT latency feeds the RAG bottleneck), and *From Text to Voice: ...Voice Tool-Calling Evaluation* (transcription errors on entities/key terms are a top cause of tool-call argument failures — the problem keyterm prompting in Universal-3 Pro addresses). Their promptable-ASR direction is effectively context engineering pushed into the speech layer.

## Use cases & considerations

Use cases: (1) STT layer for a phone/web voice agent via LiveKit or Pipecat; (2) batch transcription + LLM extraction over call recordings (e.g., a contractor back office mining customer/adjuster calls into CRM notes); (3) meeting/call intelligence features inside a SaaS product; (4) compliance workflows using PII redaction.

Considerations: hosted-only (no self-host/open weights — unlike Whisper); rapid model churn (Slam-1 already deprecated — pin versions and re-eval); real costs run above the $0.15/hr headline once add-ons stack (third-party analyses cite ~$0.35/hr effective); English-centric accuracy edge, multilingual streaming newer. Main competitors: **Deepgram, OpenAI (Whisper/Realtime), Google, ElevenLabs Scribe, Speechmatics, Gladia**. Open questions: no funding since Dec 2023 in a capital-hungry model race; whether end-to-end speech-to-speech models erode standalone STT.

## Sources

- https://www.assemblyai.com/blog/announcing-our-50m-series-c-to-build-superhuman-speech-ai-models
- https://research.contrary.com/company/assemblyai
- https://www.assemblyai.com/blog/introducing-universal-streaming
- https://www.assemblyai.com/blog/universal-3-pro-streaming
- https://www.assemblyai.com/blog/introducing-universal-3-pro
- https://www.assemblyai.com/blog/assemblyai-october-2025-releases
- https://www.assemblyai.com/blog/speech-language-model-and-improved-streaming-model
- https://www.assemblyai.com/customers/callrail-customer-story
- https://www.assemblyai.com/pricing
- https://voicebot.ai/2022/09/26/dylan-fox-ceo-of-the-assembly-ai-talks-ai-models-as-a-service-voicebot-podcast-ep-274/
- https://www.unite.ai/dylan-fox-ceo-founder-of-assemblyai-interview-series/
- https://brasstranscripts.com/blog/assemblyai-pricing-per-minute-2025-real-costs
- https://tracxn.com/d/companies/assemblyai/__Ka5MAyG7QWVq1ddyIfrErBH8kfGj0qmYFsILhdFtiIs
