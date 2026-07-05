# Neurometric

> An "automated token engineering" platform: it watches every model call inside your agentic workflows, routes each task to the cheapest model that clears your accuracy/latency bar, and auto-generates a task-specific small language model (SLM) when no existing model fits.

- **Category:** models-inference
- **AIEWF 2026 tier:** bronze
- **Founded:** 2024, New York, NY (Reported — Dealroom and AlleyWatch funding coverage; company pages don't state a year)
- **Website / GitHub:** https://www.neurometric.ai · https://marketplace.neurometric.ai · public GitHub org: Not found in public sources

## What they do
Neurometric's core bet is that every model call inside an agent workflow is a pricing decision, and most teams default every call to a frontier model. The platform decomposes agent workloads into individual tasks, continuously evaluates model-task performance on real traffic (not static benchmarks), and routes each call to the most cost-effective model that meets the required accuracy/speed/quality threshold (Verified — company interviews, funding press). Named components: a **Task Endpoint Manager** (analytics/management layer), an **SLM Marketplace** (~121–125 pre-built models under 20B parameters across 14+ domains — document intelligence, support, legal/compliance, sales, developer tools — all API-accessible and OpenAI-SDK compatible), and an **Auto-SLM Generator**: describe a task, get a purpose-built small model without ML expertise (Verified — marketplace site, company Substack, AlleyWatch).

The distribution wedge is **ClawPack**, an OpenAI-compatible inference orchestration layer for OpenClaw (the open-source agent platform with ~346k GitHub stars / 3.2M users, per the PR). ClawPack intercepts routine sub-tasks — classification, extraction, formatting, summarization — and routes them to specialist SLMs instead of frontier APIs; a classifier model routes each prompt to the matching specialist. Free tier: 100M tokens/month (Verified — PRNewswire, marketplace docs). Business model is usage-based pricing on SLMs plus platform fees (Reported — AlleyWatch). Origin note: the product started as a leaderboard comparing "thinking algorithms"/reasoning strategies before pivoting into orchestration (Reported — Everywhere Ventures profile, Dec 2025).

## Founders & origins
- **Rob May** (CEO) — serial founder: Backupify (cloud backup, exited) and AI startup Talla; Managing Director at HalfCourt Ventures (100+ investments) and long-time author of the *Investing in AI* newsletter. Neurometric is his fifth startup (Verified — Unite.AI interview, AlleyWatch, Everywhere Ventures).
- **Byron Galbraith** — PhD (reinforcement learning), former Talla colleague of May (Verified — Everywhere Ventures, LinkedIn).
- **Calvin Cooper** — co-founder; LinkedIn bills him as serial VC-backed entrepreneur and PE advisor (Reported — LinkedIn).
- **Dave Rauchwerk** — started as a freelancer, became co-founder (Reported — Everywhere Ventures).
Origin story: May dug into OpenAI's o1 in late 2024 and concluded inference-time strategy and multi-model composition was underexplored relative to training bigger models (Reported — Everywhere Ventures).

## Funding
- **$4M pre-seed**, announced June 2026 (raised spring 2026): Betaworks, ex/ante, Everywhere Ventures, Encoded Ventures, Vermillion, Abstraction, Mu Ventures; angels include Jason Calacanis and Dharmesh Shah (HubSpot CTO) (Verified — PRNewswire, AlleyWatch, Everywhere Ventures).
Total raised: $4M. No later rounds found in public sources.

## Evidence of real-world use
Thin but nonzero — this is a months-old pre-seed company:
- Flagship traction claim: one (unnamed) customer cut a workflow from $40,000/yr to $250/mo while accuracy improved from 70% to 96% (company-sourced, unverified).
- May cites a 4B-parameter model beating frontier models on a specific CRM task, and composite multi-model systems hitting 72.7% vs 58% frontier accuracy on CRM tasks (company-sourced — Unite.AI interview).
- LumaDock partnership (June 4, 2026) ships an OpenClaw VPS template with ClawPack; "users report" 60–90% reduction in frontier calls (company PR, no named users).
- Live, self-serve marketplace with a free tier and playground = a real product you can touch today, but no named customers or case studies exist publicly (Verified absence as of 2026-07-02).

## Relevance to agentic AI engineering
This sits at the routing/cost-governance layer of an agent stack — between your orchestrator and model APIs. It's a productized answer to the sub-task decomposition question in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and its "evaluate on real traffic, not benchmarks" stance echoes *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* and *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*. A routing layer that enforces cost/quality thresholds per call is also a natural enforcement point in the spirit of *Governance by Construction for Generalist Agents*.

## Use cases & considerations
Use cases: (1) cutting inference spend on high-volume narrow tasks (classification, extraction, intent routing) inside back-office agent pipelines; (2) cheap always-on OpenClaw-style personal/ops agents via ClawPack; (3) commissioning a task-specific SLM without an ML team.
Considerations: pre-seed risk — small team, $4M, could pivot or die; all performance numbers are company-sourced with zero named customers; routing adds a dependency and a quality-evaluation trust question (who grades the router?); OpenAI-compatible endpoints limit lock-in. Competitors: OpenRouter and Martian/NotDiamond (routing), OpenPipe and Predibase (distillation/fine-tuned SLMs), Fireworks/Together (serving small models yourself). Open question: whether Auto-SLM quality holds outside demo-friendly tasks.

## Sources
- https://www.alleywatch.com/2026/06/neurometric-token-engineering-agentic-ai-cost-optimization-model-routing-automation-platform-rob-may/
- https://www.prnewswire.com/news-releases/neurometric-raises-4-million-and-introduces-automated-token-engineering-platform-for-agentic-ai-302809740.html
- https://www.prnewswire.com/news-releases/neurometric-ai-and-lumadock-partner-to-cut-openclaw-inference-costs-by-up-to-90-302791671.html
- https://www.unite.ai/rob-may-ceo-and-co-founder-of-neurometric-interview-series/
- https://ideas.everywhere.vc/p/neurometric-rob-may-founders-everywhere
- https://marketplace.neurometric.ai/
- https://marketplace.neurometric.ai/clawpack
- https://neurometric.substack.com/p/introducing-the-neurometric-slm-marketplace
- https://app.dealroom.co/companies/neurometric
- https://www.linkedin.com/in/coopernyc/
