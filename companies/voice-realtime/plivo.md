# Plivo

> Cloud communications platform (CPaaS) providing voice, SMS, and — increasingly — voice-AI-agent infrastructure via APIs and WebSocket audio streaming.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** supporting
- **Founded:** 2011, San Francisco, CA (YC S12) — Verified
- **Website / GitHub:** https://www.plivo.com

## What they do
Plivo is a telephony/CPaaS provider: programmable Voice and SMS APIs, SIP trunking, and a browser calling SDK, positioned as a lower-cost alternative to Twilio. Its newer Voice AI Agents product adds an **Audio Streaming** layer — a `<Stream>` XML verb plus WebSocket protocol — that pipes live call audio to a developer's own STT/LLM/TTS stack (or a no-code agent builder) so callers can have real-time conversations with an AI agent; it also ships an omnichannel AI chat product. This is squarely infrastructure a builder would integrate rather than buy the whole conversation stack from a single vendor.

## Founders & funding
Founded by Mike Ricordeau and Venky Balasubramanian, who met via GitHub. Raised $1.75M seed (a16z, Battery Ventures, Qualcomm, SV Angel) in 2012; reported to have since scaled to ~$100M ARR on minimal outside capital (Reported, single-source growth-newsletter claim).

## Evidence of real-world use
Named enterprise customers include Uber and Zomato in case-study/press coverage; 21 published case studies on FeaturedCustomers; HIPAA/PCI DSS compliance and enterprise support tiers indicate real production traffic, not just a landing page.

## Relevance to agentic AI engineering
Core plumbing for **voice-agent architectures** — audio streaming, low-latency WebSocket transport, telephony integration — directly relevant to the voice-realtime track alongside STT/TTS/LLM orchestration choices builders must make.

## Sources
- https://www.plivo.com/voice/overview/
- https://www.plivo.com/docs/voice-agents/audio-streaming/overview
- https://www.ycombinator.com/blog/plivo-yc-s12-raises-175m-from-andreessen-horo
- https://www.featuredcustomers.com/vendor/plivo/case-studies
