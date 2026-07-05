# Yutori

> Ex-Meta AI researchers building browser-use agents end to end: their own computer-use model (n1/n1.5), an API for developers, and consumer agent products (Scouts, Delegate) that run on it.

- **Category:** browser-computer-use
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified — Parikh and Das left Meta in 2024; company emerged from stealth March 27, 2025)
- **Website / GitHub:** https://yutori.com · https://github.com/yutori-ai · https://docs.yutori.com

## What they do

Yutori is unusual in this category because it is vertically integrated: it trains its own browser-use foundation model rather than wrapping Claude/GPT/Gemini computer-use APIs. The core asset is **n1** (January 2026), a "pixels-to-actions" LLM initialized from Qwen3-VL and trained via mid-training, SFT, and RL — including RL against live websites, not just simulated environments. **Navigator n1.5** (the current `n1.5-latest`) adds hybrid vision + DOM interaction, JavaScript execution, and structured JSON output, exposed through an OpenAI Chat Completions–compatible **Navigator API** at $1.50/M input and $5.00/M output tokens, with a Python SDK, a hosted MCP server, and a Chrome extension for no-code trials.

On top of the model sit two products. **Scouts** (June 2025) are always-on monitoring agents: you describe what to watch (price drops, new papers, competitor changes), and agents autonomously browse — including logged-in sites, with credentials kept on-device — and deliver alerts via email digests or webhooks, each run backed by a transparent activity log. **Delegate** (April 23, 2026) is a proactive task agent that navigates sites, drafts replies, fills forms, and builds decks/dashboards, paired with **Yutori Local**, a macOS app for actions requiring local access (Windows "coming soon").

Benchmark posture is aggressive and public: Yutori claims 94.5% on Online-Mind2Web, 88.0% on Navi-Bench v2, and 93.0% on "Westworld"; at n1's launch they reported 91% on Navi-Bench v1 vs. Claude Opus 4.6 (88%) and GPT-5.4 (78%), at 2.5x the speed and 5.6x lower cost than Opus. Vendor-reported numbers — but Navi-Bench itself is open-sourced on GitHub, which is more falsifiable than most.

## Founders & origins

**Verified:** Co-CEOs **Devi Parikh** and **Abhishek Das**, with **Dhruv Batra** as Chief Scientist. Parikh led Meta's multimodal AI research; Batra headed embodied AI; Das was a research scientist at FAIR. Parikh and Batra earned CMU PhDs and were professors at Virginia Tech, then Georgia Tech, where all three ran labs together. Parikh and Das left Meta in 2024; Batra joined months later. "Yutori" is Japanese for mental spaciousness.

## Funding

- **Verified:** $15M Seed, announced March 27, 2025, led by Radical Ventures with Felicis; angels include Fei-Fei Li, Jeff Dean, Elad Gil, Sarah Guo, Amjad Masad (Replit), Guillermo Rauch (Vercel), Akshay Kothari (Notion), Logan Kilpatrick.
- **Series A:** Not found in public sources as of 2026-07-02; total raised stands at $15M.
- **Reported (single low-confidence source, GetLatka):** ~$2.3M ARR — treat as unverified.

## Evidence of real-world use

- **Verified:** Public, self-serve API with a published pricing page and $5 free credits — a real commercial product, not a waitlist.
- **Reported:** Anchor Browser (browser-infra company) publicly highlighted n1 for speed/cost gains in production — third-party developer adoption of the model.
- **Verified:** Open-source footprint: `navi-bench`, `yutori-mcp`, and `yutori-sdk-python` on GitHub (star counts not checked).
- **Reported:** Encord published a customer case study on Yutori's human-data pipeline (evidence Yutori buys tooling, not that customers use Yutori).
- Scouts launched with Fortune exclusive coverage and a Product Hunt listing; Delegate covered by SiliconANGLE. No named enterprise customers found — consumer/prosumer traction is not publicly quantified.

## Relevance to agentic AI engineering

Yutori sits at the action layer of the agent stack — the model that clicks, types, and reads pages — competing directly with Anthropic/OpenAI/Google computer-use models and complementing infra like Browserbase (see `companies/browser-computer-use/browserbase.md`). Its RL-on-live-websites training and open Navi-Bench connect to this repo's tool-use/computer-use papers: *Verifiable Software Worlds for Computer-Use Agents* (simulated vs. live environment tension), *AI Planning Framework for LLM-Based Web Agents* and *WebXSkill: Skill Learning for Autonomous Web Agents* (the planning/skill layer above n1), and *CaMeLs Can Use Computers Too* plus *Governance by Construction for Generalist Agents* (the security questions raised by agents operating logged-in sessions). Scouts' 24/7 monitoring pattern echoes *Agentic Search in the Wild* on autonomous web-search trajectories.

## Use cases & considerations

1. Swap n1.5 into an existing browser-automation agent via the OpenAI-compatible API for cheaper/faster steps than frontier computer-use models.
2. Webhook-driven Scouts for competitive/price monitoring (for Ridgeline: supplier pricing, permit-portal status changes) without building a scraper.
3. Delegate/Local as a prosumer back-office agent for form-heavy web workflows.

**Considerations:** benchmark claims are vendor-run (Navi-Bench is theirs); credential handling on logged-in sites deserves scrutiny (cf. the CaMeL-style security literature); startup risk on API dependency; consumer traction unquantified. Competitors: Anthropic computer use, OpenAI Operator/Atlas, Amazon Nova Act, Browserbase, Anchor Browser. Open question: whether a $15M-seed company can keep pace with frontier labs on model quality.

## Sources

- https://yutori.com/ and https://yutori.com/scouts, https://yutori.com/delegate
- https://yutori.com/blog/announcing-mission-and-seed-round
- https://yutori.com/blog/introducing-n1 · https://yutori.com/blog/introducing-n1-5 · https://yutori.com/blog/introducing-navigator
- https://fortune.com/2025/06/10/exclusive-ex-meta-ai-leaders-agent-web-yutori/
- https://www.globenewswire.com/news-release/2025/03/27/3050486/0/en/Yutori-Launches-from-Stealth-with-15M-Seed-Funding-to-Build-Consumer-AI-Assistants-Capable-of-Everyday-Tasks-on-the-Web.html
- https://siliconangle.com/2026/04/23/yutori-launches-delegate-turn-ai-agents-proactive-web-workers/
- https://radical.vc/building-the-best-web-agent-in-the-world/
- https://www.tipranks.com/news/private-companies/anchor-browser-highlights-purpose-built-browser-ai-model-n1-with-reported-speed-and-cost-gains
- https://encord.com/customers/yutori/
- https://github.com/yutori-ai (navi-bench, yutori-mcp, yutori-sdk-python)
- https://getlatka.com/companies/yutori (low confidence, ARR figure only)
