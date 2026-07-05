# Vapi

> API platform for building phone/web voice agents: you define an assistant (prompt + model choices + tools), Vapi orchestrates the STT→LLM→TTS pipeline and telephony so you never touch the audio plumbing.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** silver
- **Founded:** 2020 as Superpowered Labs (YC W21), San Francisco; pivoted to Vapi in 2023, public launch 2024 (Verified — YC profile, TechCrunch Nov 2023 pivot story, TechCrunch May 2026)
- **Website / GitHub:** https://vapi.ai — https://github.com/VapiAI (SDK org)

## What they do

Vapi is a voice-agent orchestration layer, one abstraction level above LiveKit/Daily. You create an **Assistant** — a system prompt, a choice of STT/LLM/TTS providers (OpenAI, Anthropic, Google, Deepgram, Gladia, ElevenLabs, and "dozens" more), and tool definitions — via dashboard, REST API, CLI, or SDKs. Vapi handles the realtime loop: streaming transcription, model inference, speech synthesis, turn-taking/interruption handling, with claimed sub-600ms response times (Reported — company docs).

Key surfaces: **tool calling** against your APIs/databases mid-call (webhooks with structured outputs); **Squads** — multi-assistant orchestration with context-preserving transfers between specialized agents (e.g., triage → billing → scheduling); **telephony** — inbound/outbound PSTN calls on numbers Vapi provisions or via your own Twilio/Telnyx SIP trunk; and a **web SDK** to embed voice conversations in apps. Practically, you'd integrate it as: buy a number (or bring a trunk), POST an assistant config, point tools at your backend, and handle webhook events for call transcripts and function calls.

Pricing is public and usage-based: **$0.05/min platform fee** for orchestration, with STT/LLM/TTS/telephony provider costs passed through on top — third-party analyses put realistic all-in cost at ~$0.15–0.40/min; concurrency beyond 10 lines is ~$10/line/month, and HIPAA compliance is a paid add-on (Verified for the $0.05 platform fee — vapi.ai/pricing plus multiple independent breakdowns; per-minute all-in ranges Reported).

## Founders & origins

**Jordan Dearsley (CEO)** and **Nikhil Gupta**, University of Waterloo classmates (Verified — TechCrunch, YC). They went through YC W21 with **Superpowered**, an AI meeting notetaker, then pivoted in November 2023 after Dearsley built an AI phone companion/therapist for himself in 2023 and found that startups wanted the low-latency voice infrastructure underneath it more than the product on top (Verified — TechCrunch Nov 2023 and May 2026).

## Funding

- **Series A: $20M, December 2024, led by Bessemer Venture Partners**, with Abstract Ventures, AI Grant, Y Combinator, Saga Ventures, Michael Ovitz (Verified — GlobeNewswire release + company blog).
- **Series B: $50M, May 2026, led by Peak XV**, with M12 (Microsoft), Kleiner Perkins, Bessemer; **~$500M valuation** (Verified — TechCrunch, GlobeNewswire, SiliconANGLE).
- **Total raised: $72M** (Verified — stated in Series B coverage).

## Evidence of real-world use

Strong for a silver sponsor. **Amazon Ring** evaluated 40+ voice vendors and now routes **100% of its inbound calls** through Vapi, going zero-to-production in two weeks with improved CSAT (Verified — TechCrunch reporting, not just a logo). **Instawork's** VP Engineering is quoted scaling "to millions of calls" on the platform (Reported — company/press). Other named enterprise customers: Kavak, New York Life, UnityAI, Cherry, Intuit (Reported — Series B coverage). Scale metrics: **1B+ calls processed, 1–5M calls/day, 1M+ registered developers, 2.7M agents created, eight-figure ARR, 10x enterprise revenue growth**, ~100 employees (Reported — company Series B announcement, partially echoed by TechCrunch). Public self-serve pricing and active SDK repos confirm a real commercial developer product; strongest verticals are financial services, healthcare, insurance, automotive, and workforce management (Reported).

## Relevance to agentic AI engineering

Vapi is the "buy" option for the exact system this repo's voice papers describe building: the pipeline in *Building Enterprise Realtime Voice Agents from Scratch* and the listen-think-speak loop of *LTS-VoiceAgent* are what the $0.05/min buys. Its tool-calling-over-voice surface is precisely what *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation* evaluates, and its latency posture is the problem *VoiceAgentRAG* and *Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling* attack. Squads' multi-assistant transfers map to the turn-taking/orchestration questions in *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents*; benchmarking a Vapi deployment would look like *τ-Voice* or *ProVoice-Bench*. In the stack, it sits above transport (LiveKit, Daily), STT (AssemblyAI, Deepgram), and telco (Twilio, Telnyx) — all also in this landscape.

## Use cases & considerations

Use cases: (1) inbound call answering/triage for a back office — a Vapi number that qualifies leads, checks job status via tool calls, and books appointments; (2) outbound AR follow-up or appointment-reminder campaigns; (3) voice front-end on an existing agent backend, with Vapi as telephony+speech and your service handling logic via webhooks; (4) fast prototyping — dashboard-only assistants are demoable in an afternoon.

Considerations: real cost is 3–8x the headline $0.05/min once providers are added, and cost attribution across 4–6 vendors gets messy; it's a closed managed platform (no self-host), so latency, uptime, and provider routing are Vapi's, not yours; assistant configs are portable in spirit but the Squads/webhook model is Vapi-shaped lock-in. Competitors: **Retell AI** and **Bland** (direct), **Sierra/Decagon/PolyAI** (enterprise CX agents), **ElevenLabs Agents**, and DIY on **LiveKit/Pipecat**. Open questions: durability of the Ring win as Amazon builds in-house voice AI, and margin as model providers ship speech-to-speech APIs that collapse the pipeline Vapi orchestrates.

## Sources

- https://techcrunch.com/2026/05/12/vapi-hits-500m-valuation-as-amazon-ring-chose-its-ai-platform-over-40-rivals/
- https://www.globenewswire.com/news-release/2026/05/12/3292882/0/en/vapi-raises-50m-series-b-as-it-reaches-1-billion-calls-powering-the-next-generation-of-enterprise-voice-ai.html
- https://www.globenewswire.com/news-release/2024/12/12/2996317/0/en/Vapi-Dials-in-20M-in-Series-A-Led-by-Bessemer-to-Bring-AI-Voice-Agents-to-Enterprise.html
- https://techcrunch.com/2023/11/10/yc-backed-productivity-app-superpowered-pivots-to-become-a-voice-api-platform-for-bots/
- https://www.ycombinator.com/companies/vapi
- https://docs.vapi.ai/quickstart/introduction
- https://vapi.ai/pricing
- https://vapi.ai/blog/vapi-secures-20m-to-start-the-voice-revolution-2
- https://siliconangle.com/2026/05/12/vapi-nabs-50m-make-voice-ai-human/
- https://www.citybiz.co/article/844939/vapi-raises-50m-series-b-after-surpassing-1-billion-ai-voice-calls/
- https://pxlpeak.com/blog/ai-tools/vapi-pricing-breakdown
- https://telnyx.com/resources/vapi-pricing
