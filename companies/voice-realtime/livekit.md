# LiveKit

> Open-source WebRTC infrastructure plus an agents framework: the realtime transport and orchestration layer that lets a voice/video AI agent join a "room" with a human — the stack ChatGPT's Advanced Voice Mode runs on.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, San Jose, CA (Verified — Forbes, Crunchbase, company blog agree on 2021; HQ San Jose per databases)
- **Website / GitHub:** https://livekit.com — https://github.com/livekit

## What they do

Three layers. (1) **LiveKit server** — an open-source (Apache 2.0, Go, ~19.6k GitHub stars) WebRTC SFU: clients join "rooms" and exchange low-latency audio/video/data tracks; you can self-host it with no license fees. (2) **LiveKit Cloud** — the managed version: a globally distributed mesh network with usage pricing (free Build tier with 1,000 agent minutes/mo; Ship $50/mo; Scale $500/mo; agent session minutes around $0.01/min). (3) **LiveKit Agents** — an open-source Python framework (Apache 2.0, ~11.2k stars; Node.js port `agents-js`) where an agent is a program that joins a room as a participant. It handles the voice pipeline (streaming STT → LLM → TTS, or speech-to-speech models like OpenAI's Realtime API), turn detection/endpointing, interruption handling, and tool calling, with plugins for Deepgram, OpenAI, Anthropic, Google, Cartesia, ElevenLabs, etc., plus MCP support for tools. The company claims 1M+ monthly downloads of the framework (Reported — Series C post).

Around that core: SIP/telephony integration so agents answer phone calls (PSTN), **LiveKit Inference** (routes model requests across providers, colocated models), a no-code Agent Builder, serverless agent deployment, observability/session replay, and eval partnerships (Bluejay, Hamming, Roark). Practically, you'd integrate it as: client SDK in your app or a phone number in, LiveKit room in the middle, your agent worker (your code, their framework) on the other side.

## Founders & origins

**Russ d'Sa (CEO)** and **David Zhao (CTO)** (Verified). They met at Y Combinator in 2007 running separate video-streaming startups; d'Sa later worked at Twitter, Zhao at Motorola. They teamed up in 2012, eventually building Evie Labs (ML news recommendation), **sold to Medium in 2019 for $30M** (Verified — Forbes). LiveKit started in 2021 during the pandemic after they found no good open-source end-to-end WebRTC stack for a side project (Verified — Forbes, company accounts).

## Funding

- Early rounds bringing pre-Series-B total to ~$38M, incl. a Series A led by Altimeter; ~$110M valuation as of mid-2024 (Verified — Forbes June 2024).
- **Series B: $45M, April 2025, $345M valuation, led by Altimeter** with Redpoint and Hanabi Capital; total then $83M (Verified — FinSMEs, company blog).
- **Series C: $100M, January 22, 2026, $1B valuation, led by Index Ventures** with Salesforce Ventures, Hanabi, Altimeter, Redpoint (Verified — company blog + press).
- **Total: ~$183M** (computed from the above).

## Evidence of real-world use

Unusually strong for the category. **OpenAI built ChatGPT's Advanced Voice Mode on LiveKit Cloud** — a formal, documented partnership, not a logo (Verified — joint announcement). The Series C post names **Tesla** (voice AI for sales, support, insurance, roadside assistance) and **Salesforce Agentforce** voice agents (Reported — company post; Salesforce Ventures investing is corroborating). Other named users: **Character.AI, Retell AI, Speak, Podium, Hello Patient, Salient** (Reported — company case studies). OSS signals are real: ~30k stars across the two main repos, 108 repos in the org, an active examples org, and the fact that competitor frameworks (Pipecat) treat LiveKit as a supported transport. Public pricing page and PyPI distribution confirm a working commercial product.

## Relevance to agentic AI engineering

LiveKit is the **transport + runtime** box in the voice-agent reference architecture this repo's voice papers assume: *Building Enterprise Realtime Voice Agents from Scratch* (the STT→LLM→TTS latency budget lives inside LiveKit Agents), *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents* and *LTS-VoiceAgent* (turn detection/interruption is a first-class framework feature — LiveKit ships its own turn-detector model), *VoiceAgentRAG* (retrieval inside the agent worker loop), and *From Text to Voice: Voice Tool-Calling Evaluation* (function calling over voice is exactly the Agents API surface; MCP support connects it to this repo's tool-use/governance work). If AssemblyAI is the ears, LiveKit is the nervous system the ears plug into.

## Use cases & considerations

Use cases: (1) phone-answering agent for a back office — SIP trunk in, agent worker qualifies calls, writes to CRM; (2) in-app voice copilot via web/mobile SDKs; (3) multimodal agents that see video (inspections, telehealth); (4) self-hosted realtime infra when compliance forbids third-party media servers.

Considerations: the framework nudges you toward LiveKit Cloud (self-hosting the server is easy; self-hosting the full agents deployment story is more work); Cloud is cheaper below ~500 concurrent sessions, self-hosting wins at scale (Reported — third-party analyses). Competitors: **Daily/Pipecat** (vendor-neutral pipeline framework), **Agora**, **Twilio**, **Vapi/Retell** (higher-level, some built *on* LiveKit), and partial disintermediation risk from **OpenAI Realtime API over WebRTC** direct. Open questions: how much of the new surface (Inference, Agent Builder, evals) is mature vs. announced at Series C, and margin pressure from bundling model inference.

## Sources

- https://livekit.com/blog/livekit-series-c
- https://www.forbes.com/sites/rashishrivastava/2024/06/04/this-110-million-startup-is-building-a-nervous-system-for-ai/
- https://www.finsmes.com/2025/04/livekit-raises-45m-in-series-b-at-a-345m-valuation.html
- https://blog.livekit.io/livekits-series-b/
- https://livekit.com/blog/openai-livekit-partnership-advanced-voice-realtime-api
- https://github.com/livekit/livekit
- https://github.com/livekit/agents
- https://docs.livekit.io/agents/
- https://livekit.com/pricing
- https://www.crunchbase.com/organization/livekit
- https://datainnovation.org/2024/09/5-qs-for-russell-dsa-co-founder-and-ceo-of-livekit/
