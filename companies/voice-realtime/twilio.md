# Twilio

> The incumbent communications-API company (voice, SMS, email, WhatsApp) now selling the plumbing for phone-based AI agents — ConversationRelay pipes a live call's audio to any LLM you choose and speaks the answer back.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** March 2008, San Francisco (Verified — Wikipedia, founder posts, funding histories agree)
- **Website / GitHub:** https://www.twilio.com — https://github.com/twilio (plus community repos like pBread/twilio-agentic-voice-assistant)

## What they do

Twilio is the reference CPaaS: REST APIs and SDKs for programmable voice, SMS/MMS/WhatsApp, phone numbers, SIP trunking, Verify (OTP/2FA), email (SendGrid), a customer-data platform (Segment, acquired 2020), and the Flex contact-center platform. Unlike Telnyx, Twilio does not own the network — it orchestrates on top of partner carriers and public cloud — but it owns the developer mindshare: TwiML, webhooks, and Media Streams (raw call audio over WebSocket) are the de facto patterns most voice-agent tutorials assume.

The AIEWF-relevant layer is **ConversationRelay**: a TwiML `<Connect><ConversationRelay>` verb that handles telephony, streaming STT, interruption/barge-in handling, and streaming TTS, and hands you a WebSocket carrying text — you bring your own LLM and agent logic (any model, any framework). This is deliberately the opposite of an all-in-one bot builder: Twilio does the latency-sensitive audio pipeline; your server does reasoning and tool calls. Announced late 2024, GA in 2025, with 2026 additions including PCI-compliant and HIPAA-eligible configurations, a drag-and-drop Studio widget, and a native hook into **Conversational Intelligence** (transcript analytics/observability for AI-agent calls) (Reported — Twilio launch blogs). Separately, Twilio was OpenAI's launch partner for the **Realtime API** (October 1, 2024): speech-to-speech GPT models reachable from Twilio calls via Media Streams or an Elastic SIP Trunking connector (Verified — Twilio press release + OpenAI announcement).

## Founders & origins

**Jeff Lawson** (CEO 2008–January 2024; previously one of AWS's first product managers, CTO of StubHub, co-founder of Versity and NineStar), **Evan Cooke** (early CTO), and **John Wolthuis** (Verified — Wikipedia, Lawson's own posts, Forbes). Origin story: Lawson had repeatedly needed telephony at startups and found carrier integration miserable; Twilio Voice launched November 2008 as "phone calls via web API." Lawson stepped down in January 2024 under activist-investor pressure (Elliott, Legion, Anson); **Khozema Shipchandler**, former GE and Twilio CFO, is CEO since (Verified — widely reported).

## Funding

Public company — funding history is settled record: $600K seed (March 2009); $3.7M Series A led by Union Square Ventures (December 2009); $12M Series B led by Bessemer (November 2010); later rounds through a ~$130M Series E (2015, Fidelity/T. Rowe Price) for roughly ~$240M total private capital (Reported — funding databases). **IPO June 23, 2016, NYSE: TWLO** at $15/share, ~$150M raised, ~$1.23B valuation, +92% day one (Verified). FY2025 results: **$5.07B revenue, +14% YoY; Q4 2025 revenue $1.37B; GAAP operating income $158M; dollar-based net expansion 108%** (Verified — Q4 2025 earnings release, February 2026).

## Evidence of real-world use

Among the strongest in this repo. Twilio claimed **300,000+ active customer accounts and 10M+ registered developers** at the OpenAI partnership announcement (Reported — Twilio press release). Historic marquee usage (Uber, Airbnb, Lyft notifications) is well documented. AI-specific: **Philippine Airlines** runs Flex across voice/chat, cut contact-center wait times to under a minute and monthly service costs ~30%, targeting 80% automation of live-agent tasks by April 2026 (Reported — Computer Weekly); the same piece reports Twilio's **voice AI revenues grew 49% YoY in 2025**. Third-party voice-agent platforms (Retell, Vapi, LiveKit/Pipecat stacks) routinely use Twilio for PSTN ingress, meaning Twilio gets paid even when competitors win the agent layer. Public per-minute pricing, mature docs, and active community repos round out the picture.

## Relevance to agentic AI engineering

Twilio is the PSTN on-ramp for nearly every phone-based agent architecture this repo tracks. ConversationRelay implements, as managed service, the pipeline *Building Enterprise Realtime Voice Agents from Scratch* assembles by hand; its interruption handling is the production counterpart of *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents*; the bring-your-own-LLM WebSocket design is exactly the seam where *VoiceAgentRAG* and *LTS-VoiceAgent* latency architectures plug in. Conversational Intelligence is a first-party answer to voice-agent evals — compare *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*, *τ-Voice*, and *ProVoice-Bench* before trusting vendor dashboards. PCI/HIPAA-eligible modes connect to the tool-use/governance thread: regulated-workload guardrails are becoming table stakes for agents that take real actions on calls.

## Use cases & considerations

Use cases: (1) inbound AI phone agent (intake, scheduling, dispatch — e.g., a construction back office fielding sub/vendor calls) via ConversationRelay with your own agent server; (2) speech-to-speech agents on OpenAI Realtime over Twilio SIP; (3) adding SMS/WhatsApp/Verify channels to an existing agent product from one account; (4) Flex + AI for a full contact center.

Considerations: costs stack (Twilio per-minute + carrier + ConversationRelay + your LLM tokens) and Twilio is historically the premium-priced option — Telnyx undercuts on owned-network latency and price; Vonage, Sinch, Plivo, Bandwidth compete on CPaaS; LiveKit, Daily/Pipecat, Vapi, Retell compete for the agent layer above it. You still build and host the agent logic yourself — ConversationRelay is plumbing, not an agent. US messaging carries A2P 10DLC compliance overhead. Open questions: whether post-activist Twilio keeps shipping developer-first (vs. Flex/enterprise focus), and how aggressively OpenAI's own SIP ingress disintermediates the ConversationRelay layer.

## Sources

- https://www.twilio.com/en-us/products/conversational-ai/conversationrelay
- https://www.twilio.com/docs/voice/conversationrelay
- https://www.twilio.com/en-us/blog/products/launches/the-evolution-of-conversation-relay
- https://www.twilio.com/en-us/press/releases/openai-integration
- https://openai.com/index/introducing-the-realtime-api/
- https://investors.twilio.com/news-releases/news-release-details/twilio-announces-fourth-quarter-and-full-year-2025-results
- https://www.computerweekly.com/news/366641314/How-voice-AI-is-transforming-customer-service
- https://en.wikipedia.org/wiki/Twilio
- https://www.getpin.xyz/post/inside-the-deal-twilios-early-investors
- https://github.com/pBread/twilio-agentic-voice-assistant
- https://www.twilio.com/docs/conversational-intelligence/conversation-relay-integration
