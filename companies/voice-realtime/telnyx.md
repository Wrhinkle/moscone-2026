# Telnyx

> A telecom carrier that owns its own global network and GPUs, selling voice/messaging APIs and an all-in-one voice AI agent platform — the "Twilio competitor that owns the wires" now positioning as voice-agent infrastructure.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** 2009, Chicago (Verified — company history, Tracxn, TADSummit founder interview agree)
- **Website / GitHub:** https://telnyx.com — https://github.com/team-telnyx

## What they do

Telnyx is a CPaaS (communications platform as a service) with one structural difference from Twilio-style competitors: it is a **fully licensed carrier operating its own private IP network** (licensed in 40–45+ countries per their site), rather than reselling on top of AWS and partner carriers. Core products: Voice API ("Call Control" — programmatic call handling launched 2019), Elastic SIP trunking, SMS/MMS messaging, phone numbers, number lookup/Verify APIs, IoT SIMs, programmable networking, and — since ~2023–24 — **cloud storage and GPU inference** on hardware they own.

The AIEWF-relevant product is **Voice AI Agents**: a hosted STT→LLM→TTS pipeline you attach to any phone call via API (AI Assistant / AI Gather commands). It is deliberately multi-vendor at each layer: STT via Deepgram, Whisper, AssemblyAI, Speechmatics, or Soniox behind one API; 1,300+ TTS voices (their own "Telnyx Ultra" plus MiniMax, Rime, AWS, Azure, etc.); any OpenAI-compatible LLM endpoint, including open-weight models (Qwen3, Kimi K2.5, GLM) served on Telnyx's own co-located GPUs. Their latency pitch: because telephony PoPs and inference GPUs sit in the same data halls, they claim **sub-200ms audio round-trip** versus 500ms+ for stitched-together stacks (Reported — vendor benchmark). Pricing is public and unusually simple: **$0.05/min all-in** (STT + TTS + orchestration; LLM tokens billed separately when using hosted models). Pre-built connectors for Salesforce, HubSpot, Zendesk, ServiceNow, Shopify; "Agent Skills" packages for building against their API from Claude Code/Cursor.

## Founders & origins

**David Casem (CEO)** and **Ian Reither (COO)**, both still in role (Verified — TADSummit interview, The Org, Crunchbase). Started in 2009 as a consultancy installing Asterisk-based call-center systems; 2010–2013 pivoted to reselling voice minutes, became a licensed carrier, incorporated as Telnyx LLC in 2013, and built their own switching/routing software. Casem is a self-taught engineer; the origin is bootstrapping with open-source telephony plus an FCC license (Reported — founder accounts).

## Funding

Strikingly lean for its scale. PitchBook and Tracxn both list **~$11.1M total raised** (most recent activity 2023); Tracxn's round-level data shows even less ($2.2M across early rounds), a discrepancy typical of undisclosed rounds (Reported — databases conflict). Investors named across sources: **Founders Fund, Drive Capital, Glynn Capital**, plus early Chicago investors (Chicago Ventures, Corazon Capital, Pritzker Group, MATH Venture Partners) (Reported). A 2025 TADSummit interview calls Telnyx a "unicorn" — no valuation or large round is publicly documented, so treat as Unverified. Net: predominantly revenue-funded growth; ~270 employees (Reported — Prospeo/LeadIQ-type estimates).

## Evidence of real-world use

Solid and documented. Named case studies on their site: **Replicant** (built its automated contact center on the Telnyx Voice API), **UJET** (cloud contact center; switched from Twilio for private-network latency and cost), **Lightspeed Commerce** (SIP trunking), **Fetch** (messaging), **Ooma**; **PatientSync** CTO quoted for Voice AI Agents (Verified — first-party case studies; independent corroboration thinner). G2 named Telnyx **2025 best CPaaS provider** (Reported — Telnyx's own announcement of the G2 award). Public per-minute pricing, active docs/SDKs (Python, Node, Go, Java, Ruby), and 15+ years as a licensed carrier are strong commercial-reality signals. Counter-signal worth knowing: in **February 2025 the FCC proposed a $4.49M fine** against Telnyx over robocallers who used its network to impersonate an "FCC Fraud Team" — a first-of-its-kind know-your-customer enforcement; Telnyx self-reported, blocked the traffic within hours, and is contesting the penalty (Verified — FCC document + multiple law-firm analyses; outcome unresolved as of 2026-07-02).

## Relevance to agentic AI engineering

Telnyx is the **telephony + inference substrate** under the voice-agent stack this repo tracks — the layer that determines the latency budget every pipeline paper fights over. Directly relevant: *Building Enterprise Realtime Voice Agents from Scratch* (Telnyx collapses the STT/LLM/TTS pipeline it tutorializes into one co-located vendor), *VoiceAgentRAG* and *LTS-VoiceAgent* (their sub-200ms co-location claim attacks exactly the latency bottlenecks those papers architect around), *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents* (carrier-side audio quality and jitter feed turn-detection), *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation* (their CRM connectors are voice tool-calling in production), and *τ-Voice*/*ProVoice-Bench* for evaluating agents you'd deploy on it. The FCC KYC action also connects to the tool-use/governance thread: identity, STIR/SHAKEN attestation, and abuse controls are becoming hard requirements for outbound agent calling.

## Use cases & considerations

Use cases: (1) inbound phone agent (scheduling, intake, dispatch — e.g., a construction back office answering sub/vendor calls) at a predictable $0.05/min; (2) replacing a self-assembled LiveKit/Pipecat + Twilio + STT + TTS stack with one vendor when latency and telephony reliability matter more than composability; (3) SIP trunking + Call Control for adding AI to an existing PBX/contact center; (4) SMS/Verify alongside voice from one account.

Considerations: all-in-one convenience is lock-in — the agent logic, telephony, and inference live in Telnyx's cloud; lowest-latency path pushes you toward their hosted open-weight LLMs rather than frontier models; the agent orchestration layer is younger than pure-plays. Competitors: **Twilio** (incumbent CPaaS + ConversationRelay), **Vonage, Plivo, Bandwidth** (telephony), **Vapi, Retell, LiveKit, Daily/Pipecat** (voice-agent layer). Open questions: FCC fine outcome and reputational drag; whether vendor latency claims hold under third-party benchmarks; true funding/valuation picture.

## Sources

- https://blog.tadsummit.com/2025/05/01/david-casem-telnyx/
- https://telnyx.com/products/voice-ai-agents
- https://telnyx.com/pricing
- https://telnyx.com/customer-stories
- https://telnyx.com/resources/g2-cpaas-2025
- https://tracxn.com/d/companies/telnyx/__onaSxbt6b7xZEHxduRdPtb6IKilK-rekIfw5N-NOJmo
- https://pitchbook.com/profiles/company/97302-97
- https://www.fcc.gov/document/fcc-proposes-nearly-45m-fine-apparently-illegal-robocall-scheme
- https://broadbandbreakfast.com/telnyx-calls-fccs-4-5-million-penalty-mistaken/
- https://www.crunchbase.com/organization/telnyx
