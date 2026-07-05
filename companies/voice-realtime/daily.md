# Daily

> Developer infrastructure for realtime voice and video (WebRTC APIs), and the company behind Pipecat, the most widely adopted open-source framework for building voice AI agents.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** 2016, San Francisco, CA (Verified — Tracxn, Crunchbase; originally incorporated as Pluot Communications, reflected in Crunchbase's `pluot` slug; Y Combinator participation Reported)
- **Website / GitHub:** https://www.daily.co · https://github.com/pipecat-ai/pipecat · https://docs.pipecat.ai

## What they do

Daily runs a global WebRTC infrastructure business: REST APIs and client SDKs that let developers embed low-latency, multi-party audio/video into web and mobile apps without operating SFUs, TURN servers, or codec pipelines themselves. The video API is mature — HIPAA-compliant options, call recording, PSTN/SIP dial-in, telemetry dashboards — and has historically sold into telehealth, edtech, and social products.

Since 2024 the center of gravity has shifted to voice AI. Daily created and maintains **Pipecat**, an open-source Python framework (BSD-2-Clause) for realtime voice and multimodal conversational agents. Pipecat's model is a composable pipeline: streaming STT → LLM → streaming TTS, with frame-level orchestration handling interruptions, turn-taking, and function calling at conversational latency (the project targets sub-second voice-to-voice response). It is deliberately vendor-neutral — integrations span roughly 80–100+ services including Anthropic, OpenAI, Gemini (including Gemini Live speech-to-speech), Deepgram, ElevenLabs, Cartesia, AWS, plus transports beyond Daily's own (LiveKit, WebSockets/telephony). The ecosystem includes client SDKs (JS, React, React Native, Swift, Kotlin, C++), Pipecat Flows for structured conversation paths, a Voice UI Kit, and debugging tools (Whisker, Tail).

The commercial wrapper is **Pipecat Cloud**: containerized deployment of Pipecat agents on Daily's infrastructure with autoscaling, multi-region hosting, integrated PSTN/SIP telephony, Krisp noise cancellation, recording/telemetry, and HIPAA/GDPR compliance. It has a public pricing page — a real, self-serve commercial product, not vaporware. The strategy is classic open-core: own the framework standard, monetize transport and hosting.

## Founders & origins

**Kwindla Hultman Kramer** (co-founder & CEO) — MIT Media Lab background in large-scale networked systems and realtime video; co-founded Oblong Industries (spatial/multi-screen computing, of *Minority Report* interface fame); previously CTO of AllAfrica (Verified across Crunchbase, The Org, Daily's own blog). **Nina Kuruvilla** is named as co-founder (Reported — Tracxn). The company began as Pluot Communications (video-conferencing hardware/software) before pivoting to the developer-API business as Daily.

## Funding

- Seed: ~$4.6M (Reported — TenOneTen portfolio page)
- Series A: $15M, announced March 2021, led by Lachy Groom with Tiger Global (Verified — PR Newswire, Crunchbase)
- Series B: $40M, November 2021, led by Renegade Partners; Heritage Group, Cendana Capital, Tiger Global, Slack Fund and others participating; total raised >$60M at that point (Verified — Daily blog, Crunchbase, The SaaS News)
- No post-2021 rounds found in public sources.

## Evidence of real-world use

- Pipecat GitHub: ~13.2k stars, ~2.3k forks, 114 releases (v1.5.0 current), active Discord — strong and current OSS adoption signal (Verified, checked 2026-07-02).
- NVIDIA maintains an official `voice-agent-examples` repo built on Pipecat; AWS published a two-part ML blog series on building voice agents with Pipecat + Bedrock; Google's Gemini Live documentation path includes Pipecat integration (Verified — first-party repos/blogs).
- Claims that Pipecat "powers voice AI for OpenAI and Google DeepMind" appear in interview/newsletter coverage of Kramer (Reported — not confirmed by those companies' own materials).
- Video API side: named telehealth users are thin in public sources (EasyEMDR, SimplyDoc migration write-up); most usage evidence is indirect (Reported).
- Kramer co-teaches a popular voice-agents course on Maven with swyx — notable community/mindshare signal.

## Relevance to agentic AI engineering

Daily sits squarely in the voice/realtime layer of the agent stack: transport, orchestration, turn-taking, and interruption handling — the engineering problems catalogued in this repo's voice-agent papers. Pipecat is effectively the reference implementation for the pipeline architectures discussed in "Building Enterprise Realtime Voice Agents from Scratch" and the listen-think-speak decomposition in "LTS-VoiceAgent"; its interruption/turn-taking machinery maps to "Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents" and full-duplex evaluation in "τ-Voice"; voice RAG latency tradeoffs ("VoiceAgentRAG") and voice tool-calling evaluation ("From Text to Voice") are exactly the problems a Pipecat pipeline forces you to confront. For a construction back-office thesis, this is the plumbing for phone-based agents: subcontractor call intake, scheduling callbacks, voicemail detection (Daily has a published cookbook for this).

## Use cases & considerations

Use cases: (1) inbound/outbound phone agents over PSTN/SIP with voicemail detection; (2) voice front-ends on existing agent backends via Pipecat's client SDKs; (3) HIPAA-compliant telehealth video with AI transcription/notes; (4) multi-agent voice systems with handoffs (Pipecat 1.5 supports distributed multi-agent composition).

Considerations: Pipecat itself is vendor-neutral, but the managed path (Pipecat Cloud + Daily transport + telephony) concentrates spend with Daily — moderate lock-in, mitigated by self-hosting being genuinely viable. Main competitors: **LiveKit** (Agents framework + cloud, arguably the sharpest rival), **Vapi** and **Retell** (higher-level voice-agent platforms), **Agora**, **Vonage**, **GetStream** on the video-API side, plus OpenAI/Google realtime APIs commoditizing the speech-to-speech layer. Open questions: no disclosed funding since 2021 (revenue-sustained or quietly raised?), and thin public case-study evidence for Pipecat Cloud specifically versus the framework's obvious OSS traction. Category note: filed under consumer-ai per assignment, but Daily is developer infrastructure, not a consumer product.

## Sources

- https://www.daily.co/
- https://github.com/pipecat-ai/pipecat
- https://www.daily.co/products/pipecat-cloud/
- https://www.daily.co/pricing/pipecat-cloud/
- https://www.crunchbase.com/organization/pluot
- https://www.crunchbase.com/person/kwindla-kramer
- https://tracxn.com/d/companies/daily/__2IpjUrg3r1I2LAsoj644u1TIGJr9pf-iNIbaDFDAhCE
- https://www.prnewswire.com/news-releases/daily-raises-15-million-from-lachy-groom-and-tiger-global-to-expand-video-and-audio-chat-apis-for-developers-301244748.html
- https://www.daily.co/blog/announcing-our-40m-series-b/
- https://www.thesaasnews.com/news/daily-raises-40-million-in-series-b
- https://www.tenoneten.com/latest/daily-seed
- https://github.com/NVIDIA/voice-agent-examples
- https://aws.amazon.com/blogs/machine-learning/building-intelligent-ai-voice-agents-with-pipecat-and-amazon-bedrock-part-1/
- https://docs.pipecat.ai/pipecat/features/gemini-live
- https://www.smartspeakers.fm/p/the-pipeline-for-voicekwindla-hultman
- https://maven.com/pipecat/voice-ai-and-voice-agents-a-technical-deep-dive
- https://www.daily.co/blog/building-a-voicemail-detection-agent-with-pipecat-and-daily/
- https://www.daily.co/use-cases/telehealth/
