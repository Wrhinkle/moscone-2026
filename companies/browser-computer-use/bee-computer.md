# Bee Computer

> A $49 wearable (clip/bracelet) that always-listens to your conversations and turns them into notes, reminders, and to-do lists via LLM summarization.

- **Category:** browser-computer-use
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, San Francisco (Verified — TechCrunch)
- **Website / GitHub:** https://bee.computer (no public GitHub found; hardware/consumer product, not OSS)

## What they do
Bee makes a small ambient-audio wearable (a Fitbit-like bracelet or clip-on pin, plus an Apple Watch app) that continuously records conversations unless muted, transcribes them, and runs them through an LLM pipeline to auto-generate reminders, to-do lists, and "Daily Insights" (pattern/trend summaries of a user's life). Newer features include "Actions," which connects the assistant to email and calendar to act on what it hears. For engineers, it's a real-world example of ambient/always-on audio capture + streaming ASR + LLM summarization + agentic action-taking, deployed as a consumer device rather than a developer tool — relevant as a reference architecture for context-capture and proactive-agent products, not as an SDK you'd integrate.

## Founders & origins / Funding
Co-founded by CEO Maria de Lourdes Zollo and CTO Ethan Sutin, both ex-Twitter/Squad. Raised $7M seed in July 2024 (led by EXOR, with Greycroft, New Wave, Banana Capital) on top of $1.5M pre-seed — Verified via TechCrunch/Crunchbase. **Acquired by Amazon** (announced July 2025; as of Jan 2026 reporting the deal was signed but not yet closed) — Verified, multiple sources.

## Evidence of real-world use
Consumer hardware sold directly ($49.99 + $19/mo); shipped four feature updates post-acquisition and was shown at CES 2026. Amazon's interest signals a real, non-trivial acquisition rather than an acqui-hire for talent alone.

## Relevance to agentic AI engineering
Illustrative case study for ambient-context capture feeding an agent loop (always-on sensing → transcription → summarization → proactive action), a pattern relevant to memory/context and voice-agent tracks at AIEWF.

## Sources
- https://techcrunch.com/2024/07/29/former-squad-and-twitter-execs-raise-7m-to-build-a-hardware-ai-assistant/
- https://techcrunch.com/2025/07/22/amazon-acquires-bee-the-ai-wearable-that-records-everything-you-say/
- https://techcrunch.com/2026/01/12/why-amazon-bought-bee-an-ai-wearable/
- https://www.geekwire.com/2025/amazon-is-acquiring-bee-maker-of-a-wearable-ai-assistant-that-listens-to-conversations/
