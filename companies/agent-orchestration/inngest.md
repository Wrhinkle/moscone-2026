# Inngest

> Durable execution engine for background workflows and AI agents: write step functions in your own codebase, and Inngest handles queues, retries, state, and orchestration over plain HTTP.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2021–2022 (sources conflict: company about page says 2022; third-party profiles say 2021 — Reported), San Francisco, remote-first (Verified)
- **Website / GitHub:** [inngest.com](https://www.inngest.com) · [github.com/inngest/inngest](https://github.com/inngest/inngest) · [github.com/inngest/agent-kit](https://github.com/inngest/agent-kit)

## What they do

Inngest is a workflow orchestration platform built around "durable functions." Instead of standing up queues, cron infrastructure, and state machines, you write functions in your app (TypeScript, Python, Go SDKs) composed of `step.run()` calls; each step's result is checkpointed, failed steps retry automatically, and workflows can pause for hours or days (e.g., `waitForEvent()` for human-in-the-loop) and resume after crashes. Triggers are events or schedules; flow control (concurrency limits, throttling, debounce, batching) is declarative. The distinctive architectural choice is HTTP as transport: Inngest calls your functions over HTTP, so the same code runs on serverless (Vercel/Lambda), containers, or long-lived servers, and the Dev Server gives a local runtime with full run traces (Verified from docs and GitHub README).

The core server/CLI is open source-ish — Go, Server Side Public License with delayed Apache 2.0 publication; SDKs are Apache 2.0 — and can be self-hosted, with Inngest Cloud as the managed offering (Verified). A public pricing page exists, indicating a real commercial product.

For AI specifically: `step.ai` wraps inference calls with retries and result caching, and **AgentKit** is their TypeScript framework for multi-agent systems — agents composed into "networks" with a deterministic router, shared network state as memory, and tool integration via MCP; it supports OpenAI, Anthropic, Gemini, and OpenAI-compatible models. AgentKit rides on the same durable-execution engine, so agent steps are fault-tolerant in production (Verified from agentkit.inngest.com and GitHub).

## Founders & origins

Tony Holdstock-Brown (CEO; formerly Head of Engineering at Uniform Teeth) and Dan Farrelly (CTO; formerly CTO at Buffer). Reported: the two met in a NYC co-working space; the product came out of repeatedly rebuilding queue/retry plumbing as engineers (Verified names/roles via company site and multiple profiles; backgrounds Reported).

## Funding

- **Seed:** ~$3M, ~2022, with GGV (now Notable Capital), Afore Capital, and Guillermo Rauch (Reported — TechCrunch retrospective mention).
- **Round led by a16z:** $6.1M, announced Jan 30, 2024, with follow-on from GGV/Notable, Afore, Guillermo Rauch (Verified — TechCrunch + company blog).
- **Series A:** $21M (Tracxn lists $20.5M), announced Sept 16, 2025, led by Altimeter, with a16z, Notable, Afore, Guillermo Rauch (Verified — company blog; amount discrepancy noted).
- **Total raised:** ~$30M by summation; Tracxn reports $34M (Reported). Angels include Tom Preston-Werner, Tristan Handy, Jake Cooper (Reported — company about page).

## Evidence of real-world use

- Documented case studies (not just logos): **SoundCloud** (dynamic video-generation workflows defined fully in code) and **Resend** (domain-verification and high-volume batch workflows) on inngest.com/customers (Verified).
- **TripAdvisor, Contentful, Day.ai** named as customers by investor Notable Capital and in the Series A post (Reported — company/investor sources).
- OSS traction: inngest/inngest at ~5.6k GitHub stars, 325 forks as of 2026-07-02 (Verified).
- Vercel's CEO is a repeat investor and Inngest is a common recommendation in the Vercel/Next.js ecosystem for background jobs (Reported).

## Relevance to agentic AI engineering

Inngest sits at the orchestration/runtime layer of the agent stack: durable step execution, retries around non-deterministic LLM calls, human-in-the-loop pauses, and observability of runs. AgentKit's MCP-based tooling and deterministic routing connect directly to this repo's tool-use/governance research thread (constraining what agents may invoke and when); its network-state design is a practical instance of the agent-memory literature's shared-state approaches. Their flagship examples — E2B and Daytona coding agents replicating Cursor-style agent mode — map onto the agentic SWE benchmark papers in this repo's landscape (long-horizon, multi-step code tasks needing checkpointed recovery). Less relevant to the voice-agent papers, which need low-latency streaming rather than durable checkpointing.

## Use cases & considerations

Use cases: (1) productionizing a multi-step LLM pipeline (extract → enrich → validate) without building queue infrastructure; (2) agent workflows requiring human approval mid-run via `waitForEvent`; (3) fan-out batch processing (embeddings, document ingestion) with concurrency/throttle controls; (4) replacing cron + queue sprawl in a back-office automation stack.

Considerations: SSPL core license limits some self-hosting/embedding scenarios; the HTTP-invocation model adds per-step latency (fine for workflows, wrong for real-time voice); managed-cloud pricing scales with runs/steps. Competitors: Temporal (heavier, code-first durable execution), Restate, Trigger.dev, Hatchet, AWS Step Functions; on the agent-framework side, LangGraph and OpenAI's (unrelated, identically named) AgentKit. Open question: how much AgentKit adoption exists independent of the core workflow product.

## Sources

- https://www.inngest.com/about
- https://github.com/inngest/inngest
- https://github.com/inngest/agent-kit
- https://agentkit.inngest.com/
- https://www.inngest.com/blog/announcing-inngest-series-a
- https://techcrunch.com/2024/01/30/inngest-raises-6-1m-as-it-expands-its-workflow-engine/
- https://www.notablecap.com/blog/inngests-21m-series-a-and-the-ai-workflow-revolution
- https://www.inngest.com/customers/soundcloud
- https://www.inngest.com/customers/resend
- https://tracxn.com/d/companies/inngest/__bR2Hk25CjytxEbFOu-0ElfrYa83f0lBJ_EqeMtipOPk
