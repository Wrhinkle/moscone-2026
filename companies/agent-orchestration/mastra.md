# Mastra

> Open-source TypeScript framework for building AI agents and workflows, from the team that built Gatsby, with a hosted cloud for deployment and observability.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified via YC company page and Mastra's own seed announcement; SF location Reported)
- **Website / GitHub:** https://mastra.ai · https://github.com/mastra-ai/mastra

## What they do

Mastra is an npm-installable TypeScript framework (`npm create mastra@latest`) for building agentic applications. The core primitives: **agents** (LLM + tools + memory), **graph-based workflows** with explicit control-flow syntax and suspend/resume for human-in-the-loop steps (state persists across the pause), **context management** (conversation history, RAG, and what they call "observational memory"), and **model routing** across 40+ providers behind one interface. It ships MCP support (both consuming MCP servers as tools and exposing agents as MCP servers), built-in evals ("scorers" — model-graded, rule-based, and statistical, returning 0–1 scores), and observability (traces, logs, and as of 2026 a metrics dashboard for token cost, latency percentiles, error rates, and eval scores). It embeds in Node, Next.js, and React apps.

The commercial layer is **Mastra Cloud** (one-command agent deployment; a CloudExporter ships traces there) and **Mastra Studio** (local dev playground plus the observability/eval UI). The repo is dual-licensed Apache 2.0 + a "Mastra Enterprise License" (Verified from the GitHub repo, checked 2026-07-02). Cloud pricing is "free to start" with paid tiers announced for Q1 2026 but exact prices not yet public as of this writing (Reported) — so the monetization posture is still settling.

## Founders & origins

**Verified:** Sam Bhagwat (CEO), Abhi Aiyer, and Shane Thomas — all ex-Gatsby, the open-source React site framework that scaled to ~$5M ARR and sold to Netlify. Bhagwat co-founded Gatsby; Aiyer led engineering on Gatsby Cloud; Thomas was staff engineer/head of product. Origin story (Reported, consistent across YC page and interviews): in October 2024 they set out to build an AI-powered CRM/sales agents, found TypeScript agent tooling lacking, and pivoted to building the framework instead. YC Winter 2025 batch.

## Funding

- **$13M seed, announced October 8, 2025** (Verified — Mastra's own blog plus independent press). Investors include Y Combinator, Paul Graham, Gradient Ventures (Google's AI fund), Guillermo Rauch (Vercel), Amjad Masad (Replit), Balaji Srinivasan, and 120+ others; no single lead is clearly stated, so treat "led by YC" claims as Reported.
- Prior YC standard-deal investment implied by W25 participation; amount not separately disclosed.
- **Total raised:** ~$13M publicly disclosed.

## Evidence of real-world use

Stronger than typical for a supporting-tier sponsor, though most case studies are Mastra-published:

- **OSS adoption (Verified, 2026-07-02):** 25.8k GitHub stars, 2.4k forks, ~1.9k dependent repos on GitHub's "Used by," and ~190k weekly npm downloads per the seed announcement. Mastra claims "third-fastest growing JavaScript framework ever" (Unverified marketing claim).
- **Replit:** Agent 3 reportedly runs thousands of Mastra sandboxes daily (Reported — Mastra's own materials).
- **Marsh McLennan:** "LenAI" agentic search used across a 75,000-employee workforce, powered by Mastra (Reported — seed blog).
- **Documented case studies:** Index (AI-first data analytics platform, supervisor-agent architecture) and MedusaJS (e-commerce agents on Mastra Cloud, validated with six customer companies) — both on mastra.ai/blog.
- **Landing-page logos** (weaker signal): PayPal, Adobe, Elastic, Docker, SoftBank.
- Their book *Principles of Building AI Agents* has shipped 70,000+ physical copies since March 2025 (Reported) — an unusual and effective distribution motion.

## Relevance to agentic AI engineering

Mastra sits squarely in the orchestration layer of the stack: tool-calling, durable workflows, memory, and evals in one TypeScript package. Its multi-tool/MCP surface maps to *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*; its suspend/resume workflow model is where questions raised in *From Plan to Action: How Well Do Agents Follow the Plan?* and *Governance by Construction for Generalist Agents* get answered in practice. The memory subsystem (conversation history + RAG + observational memory) is a production instantiation of the design space in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation* and *Are We Ready For An Agent-Native Memory System?*. Mastra also ships voice modules (STT/TTS/speech-to-speech), relevant to *Building Enterprise Realtime Voice Agents from Scratch*.

## Use cases & considerations

**Use cases:** (1) back-office document/workflow agents where human approval gates matter — suspend/resume fits invoice intake or job-packet auditing; (2) embedding agents in an existing Next.js/Node product without adding Python infrastructure; (3) standing up evals + tracing on day one instead of bolting them on.

**Considerations:** youngest of the major frameworks (vs. LangChain/LangGraph, LlamaIndex, Vercel AI SDK, OpenAI Agents SDK, Inngest AgentKit; Temporal for heavy durable execution). TypeScript-only — a plus or a dealbreaker by team. Cloud pricing still unpublished, and the enterprise dual license bears reading before deep adoption. Open question: whether the framework's breadth (voice, RAG, evals, cloud) holds up against best-of-breed point tools.

## Sources

- https://www.ycombinator.com/companies/mastra
- https://mastra.ai/blog/seed-round
- https://github.com/mastra-ai/mastra
- https://technews180.com/funding-news/mastra-raises-13m-seed-for-typescript-ai-framework/
- https://mastra.ai/blog/index-case-study
- https://mastra.ai/blog/medusa-ecommerce
- https://mastra.ai/pricing
- https://mastra.ai/docs/observability/metrics/overview
- https://scalingdevtools.com/podcast/episodes/sam-from-mastra-the-gatsby-founder-building-an-agents-framework
