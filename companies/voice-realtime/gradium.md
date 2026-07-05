# Gradium

> Paris-based voice AI lab (spun out of Kyutai) selling ultra-low-latency streaming text-to-speech, speech-to-text, and voice cloning through a single developer API.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** September 2025, Paris, France (Verified — TechCrunch, Sifted)
- **Website / GitHub:** https://gradium.ai · docs at https://docs.gradium.ai · parent lab OSS at https://kyutai.org (Moshi and related models)

## What they do

Gradium is the commercial spinout of Kyutai, the Paris non-profit AI lab behind Moshi — the 7B-parameter full-duplex speech-to-speech model that could interrupt, backchannel, and respond in ~160 ms. Gradium productizes that research line: audio language models built for real-time voice, sold as an API rather than a consumer app.

Concretely, the platform exposes (Verified via their API docs and pricing page):

- **Streaming TTS and streaming STT over WebSocket**, with semantic voice-activity detection and multiplexing (multiple TTS/STT streams over one socket connection — relevant if you run many concurrent agent calls).
- **Voice cloning** at two levels; the instant tier builds a clone from ~10 seconds of audio via REST.
- **Speech translation** (STT-translation and speech-to-speech translation) as separate credit-metered endpoints.
- Five languages at launch: English, French, German, Spanish, Portuguese; more planned.
- Python and Rust SDKs, plus native integrations with **LiveKit and Pipecat** — the two dominant open voice-agent orchestration frameworks — and an AWS Marketplace listing for real-time TTS.

Pricing is public and credit-based (Verified): free tier (45k credits, non-commercial), paid tiers from $13/mo to $1,615/mo, enterprise custom. TTS is 1 credit/character (~45k characters ≈ 1 hour); STT is 3 credits/second. A public self-serve pricing page this granular signals a real commercial product, not vaporware.

## Founders & origins

Four co-founders (Verified — Sifted, TechCrunch, SiliconANGLE): **Neil Zeghidour** (CEO; Kyutai founding member, ex-Google DeepMind voice-model researcher), **Laurent Mazaré** (ex-Jane Street; Reported), **Alexandre Défossez** (ex-Meta; Reported), and **Olivier Teboul** (ex-Google; Reported). Press and the company's own material credit the team with foundational work on neural audio codecs and audio language models — Zeghidour and Défossez are known in the literature for SoundStream/AudioLM and EnCodec/Demucs respectively (Reported; consistent with their DeepMind/Meta affiliations but not itemized in launch coverage). The company was formed in September 2025 inside Kyutai's orbit; Kyutai remains a shareholder and the two collaborate, with Gradium as the "commercial arm" converting millions of monthly open-model downloads into a business.

## Funding

- **$70M seed, announced December 2, 2025** (Verified — TechCrunch, Sifted, Bloomberg, SiliconANGLE). All equity. Co-led by **FirstMark Capital** and **Eurazeo**; participation from DST Global, Korelya Capital, Amplify Partners, plus angels Xavier Niel, Rodolphe Saadé, and Eric Schmidt.
- Total raised: $70M. Valuation: not disclosed (Not found in public sources).

## Evidence of real-world use

- **A dozen paying customers** ~3 months after launch, spanning video-game character voices and medical-secretary applications (Reported — Sifted, citing the company; no named customers found in public sources as of 2026-07-02).
- Public pricing, self-serve API, startup-grant program ($2k+ credits), and an AWS Marketplace listing (Verified) — commercial infrastructure is real.
- Independent benchmark presence: Gradium TTS appears on Artificial Analysis's TTS quality/speed/price leaderboard (Verified).
- Strong inherited credibility via Kyutai's OSS: Moshi and related models see millions of downloads monthly (Reported — Amplify Partners blog). This is adjacent evidence — downloads accrue to Kyutai, not Gradium's paid API.
- Third-party technical coverage from Coval on Gradium/Kyutai's full-duplex approach (Verified as coverage).

Net: early-stage but genuinely used; customer evidence is thin and unnamed, typical for a company one quarter out of stealth.

## Relevance to agentic AI engineering

Gradium sits at the **voice I/O layer of the agent stack**: STT in, TTS out, with latency and turn-taking as the differentiators. It maps directly onto this repo's realtime-voice research cluster — full-duplex behavior and interruption handling are exactly what **τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains** and **Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents** measure; their semantic VAD + streaming pipeline is the infrastructure assumed by **LTS-VoiceAgent** and **VoiceAgentRAG** (latency budgets), and voice tool-calling evaluation (**From Text to Voice**) applies the moment you wire Gradium into a LiveKit/Pipecat agent that calls tools. For a back-office builder, it's the phone-channel layer for call agents (AR follow-up calls, sub scheduling) rather than a reasoning component.

## Use cases & considerations

Use cases: (1) low-latency voice front-end for a phone/web agent via LiveKit or Pipecat; (2) branded voice cloning for IVR or game characters; (3) real-time transcription with semantic VAD for meeting/call agents; (4) speech-to-speech translation for multilingual support lines.

Considerations: crowded market — **ElevenLabs, Cartesia, Deepgram, OpenAI Realtime**, plus AssemblyAI (also at AIEWF) on STT; only five languages today; no named customers yet; credit-based pricing needs modeling at call-center volume; EU-based lab may appeal for data-residency. Open question: how much of the Moshi-style speech-to-speech (vs. cascaded STT→LLM→TTS) capability is actually exposed in the paid API today.

## Sources

- https://techcrunch.com/2025/12/02/paris-based-ai-voice-startup-gradium-nabs-70m-seed/
- https://sifted.eu/articles/gradium-70m-seed-voice-ai
- https://siliconangle.com/2025/12/02/audio-language-model-startup-gradium-raises-70m-create-realistic-voice-ai-systems/
- https://www.bloomberg.com/news/articles/2025-12-02/eric-schmidt-xavier-niel-back-french-ai-voice-startup-gradium
- https://gradium.ai/ and https://gradium.ai/about/who-we-are
- https://gradium.ai/pricing
- https://gradium.ai/api_docs.html
- https://www.amplifypartners.com/blog-posts/arming-the-rebels-with-gpus-gradium-kyutai-and-audio-ai
- https://www.coval.ai/blog/the-future-of-speech-to-speech-ai-inside-gradium-and-kyutai-s-approach-to-full-duplex-conversation/
- https://artificialanalysis.ai/text-to-speech/models/gradium-default
- https://aws.amazon.com/marketplace/pp/prodview-vso5hhkq2eiww
- https://kyutai.org/
