# HeyGen

> AI video platform that generates photorealistic talking-avatar video from a script — plus a real-time streaming-avatar API for putting a live, LLM-driven face on conversational agents.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** supporting
- **Founded:** 2020 (as Surreal, later Movio; rebranded HeyGen in 2023) — **Verified**. Founded with early backing in China, relocated HQ to Los Angeles in 2022 — **Verified** (Wikipedia, SCMP).
- **Website / GitHub:** https://www.heygen.com · https://developers.heygen.com · npm: `@heygen/streaming-avatar`

## What they do

HeyGen's core product is async avatar video generation: paste a script, pick an avatar (stock, or a "digital twin" cloned from your own footage) and a voice, and get back a rendered video with synced lip movement, gestures, and intonation — in ~175 languages via built-in translation/dubbing. The current engines are Avatar IV (mid-2025) and Avatar V (reported April 2026), the latter claimed to build a photoreal twin from a ~15-second phone clip — **Reported** (third-party reviews; treat specific benchmark numbers as vendor-derived).

For engineers, the more interesting surface is the **Interactive Avatar / Streaming Avatar API** (recently spun out under the LiveAvatar brand — heygen.com/interactive-avatar now 301-redirects to liveavatar.com, **Verified**). It streams a live avatar over WebRTC using LiveKit-backed infrastructure: you open a session, pipe in text or audio, and get low-latency talking-head video back, with events like `AVATAR_START_TALKING`/`AVATAR_STOP_TALKING` for turn management. The design is deliberately LLM-agnostic — you bring your own brain (OpenAI Realtime, Claude, whatever) and HeyGen renders the face and voice. There's a TypeScript SDK (`@heygen/streaming-avatar`), REST video-generation APIs, and community React Native/LiveKit demos. API pricing moved to pay-as-you-go credits in early 2026 — **Reported** (single review source).

## Founders & origins

**Joshua Xu** (CEO, ex-Snap engineer/data scientist) and **Wayne Liang** (CPO, ex-ByteDance product designer) — **Verified**. They met at Tongji University in Shanghai and again at Carnegie Mellon for master's degrees — **Reported**. Founded in Shenzhen-adjacent Chinese VC ecosystem in 2020; after relocating to LA in 2022 the company had Chinese investors (IDG Capital, Baidu Ventures, HongShan, ZhenFund) sell their stakes to US investors amid Congressional scrutiny — **Verified** (SCMP).

## Funding

- Early rounds from Sequoia China/HongShan and ZhenFund — **Verified**.
- Nov 2023: $5.6M led by Conviction (Sarah Guo) — **Verified** (Forbes, Wikipedia).
- Jun 2024: $60M Series A led by Benchmark at a $500M valuation; Thrive, BOND, Conviction, Dylan Field, Elad Gil participating — **Verified** (Bloomberg, company blog, SCMP).
- Mid-2025: $150M Series B at ~$2.0B post-money — **Reported** (Sacra; not confirmed in a second primary source I found).
- Total raised: ≥$215M if the Series B holds; ~$75M **Verified** floor.

## Evidence of real-world use

Strong. Profitable by Q2 2023 with ARR climbing $1M → $35M (Jun 2024) → ~$95–100M (late 2025) — **Reported** (Sacra/Forbes; trajectory consistent across sources). 40,000+ paying business customers as of mid-2024 — **Verified**. Documented (not just logo-wall) usage: **trivago** localized TV ads across 30 markets and cut months of post-production; **Komatsu** multilingual training videos with ~90% completion rates; **Pyne** builds AI demo/onboarding agents on the API; McDonald's "Grandma McFlurry" campaign (2024); Javier Milei's Davos speech translation went viral in Jan 2024. G2 named it a fastest-growing product of 2026 — **Reported**. Counterweight: security researchers have repeatedly documented HeyGen output in deepfake scams and propaganda — a real reputational/governance consideration.

## Relevance to agentic AI engineering

HeyGen is the "face layer" for voice agents: the streaming API sits downstream of exactly the full-duplex/turn-taking problems covered in this repo's voice-agent papers — pair it with the latency and interruption-handling findings there, since avatar rendering adds a hop on top of ASR→LLM→TTS. Its BYO-LLM design makes it a tool-use integration target rather than an agent framework; session/event APIs map cleanly onto the tool-use/governance work in the landscape (identity, consent, and deepfake provenance are live governance questions here). Not relevant to agentic SWE benchmarks or agent-memory research except as a presentation layer an agent might call.

## Use cases & considerations

1. Put a live avatar on an existing voice/support agent (WebRTC session + your LLM + their events API).
2. Auto-generate multilingual training or product-update videos from docs as part of an agent pipeline.
3. Localize marketing/ad video across markets (the trivago pattern).
4. Interactive onboarding/demo agents embedded in-product (the Pyne pattern).

Considerations: closed SaaS, per-credit pricing that can get expensive at scale; latency of rendered video vs. pure-voice agents; brand/abuse risk given the deepfake track record (vet their consent-verification flow); platform churn (interactive product just rebranded to LiveAvatar). Competitors: Synthesia (enterprise async video), Tavus and Soul Machines (real-time conversational avatars), D-ID, Argil. Open questions: unconfirmed Series B terms; how sub-second latency claims hold up in production.

## Sources

- https://en.wikipedia.org/wiki/HeyGen
- https://www.scmp.com/tech/tech-trends/article/3267861/ai-start-heygen-raises-us60-million-after-pivoting-away-mainland-china-investors
- https://www.bloomberg.com/news/articles/2024-06-20/ai-video-startup-heygen-valued-at-500-million-in-funding-round
- https://www.forbes.com/sites/kenrickcai/2023/11/29/ai-video-startup-heygen-launches-near-instant-avatar-generator-adds-56-million-in-funding/
- https://www.heygen.com/blog/announcing-our-series-a
- https://sacra.com/c/heygen/
- https://developers.heygen.com/ and https://docs.heygen.com/docs/streaming-avatar-sdk-reference
- https://www.npmjs.com/package/@heygen/streaming-avatar
- https://www.heygen.com/customer-stories (trivago, Komatsu, Pyne case studies)
- https://www.heygen.com/interactive-avatar (301 → liveavatar.com)
- https://www.forbes.com/sites/annatong/2025/11/06/heygen-rides-the-ai-video-boom-rocket/

*Profile compiled 2026-07-02.*
