# Character.ai

> Consumer chat platform for talking with AI "characters" — persona-driven LLM chat at massive scale, not a developer/API business.

- **Category:** consumer-ai
- **AIEWF 2026 tier:** supporting
- **Founded:** 2021, Menlo Park, CA (Verified)
- **Website / GitHub:** https://character.ai — no public GitHub (closed-source consumer product)

## What they do
Character.ai lets users create and chat with custom AI personas (fictional characters, roleplay companions, coaching bots) built on the company's own fine-tuned LLMs, with voice and long-running memory/context features layered on top of a standard chat-app UI. There is **no public developer API or enterprise tier** (Verified via multiple 2026 pricing/review sources) — it is a pure B2C subscription product ($9.99/mo "c.ai+"), not something engineers integrate into their own stacks. Internally it is notable for serving inference at extreme scale (reportedly ~50,000 requests/sec at peak, Reported/single-source) on custom-trained models rather than solely reselling frontier-lab APIs, which made it an early proof point for cost-efficient, high-QPS LLM serving infrastructure.

## Founders & funding
Founded by ex-Google engineers Noam Shazeer (co-author of the Transformer paper) and Daniel De Freitas (lead on Google's Meena/LaMDA). Raised ~$193M total ($43M seed 2021, $150M Series A led by a16z in 2023) at a $1B valuation (Verified, Crunchbase/CNBC). In August 2024, Google hired back Shazeer and De Freitas and took a non-exclusive license to Character.ai's tech in a ~$2.7B-equivalent deal (Verified, TechCrunch).

## Evidence of real-world use
~20M monthly active users in 2026 per third-party trackers (down from a mid-2024 peak of ~28M as free frontier chatbots improved) — Reported, single-source-class trackers, treat as directional. No named enterprise customers since there is no B2B product.

## Relevance to agentic AI engineering
Limited direct relevance to agent/tool-building stacks given the absence of an API — its value to an AI engineer audience is as a case study in inference-serving economics and retention-driven consumer LLM product design, not as an integratable tool.

## Sources
- https://en.wikipedia.org/wiki/Character.ai
- https://www.cnbc.com/2023/03/23/characterai-valued-at-1-billion-after-150-million-round-from-a16z.html
- https://techcrunch.com/2024/08/02/character-ai-ceo-noam-shazeer-returns-to-google/
- https://www.demandsage.com/character-ai-statistics/
- https://www.eesel.ai/blog/character-ai-pricing
