# Temporal

> Open-source "durable execution" engine — write ordinary code as workflows that survive crashes, retries, and weeks-long waits — now positioning itself as the reliability substrate under production AI agents.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2019, Seattle/Bellevue, WA (Verified — GeekWire, company sources)
- **Website / GitHub:** https://temporal.io · https://github.com/temporalio/temporal

## What they do

Temporal's core is an MIT-licensed, Go-based orchestration service (21.4k stars / 1.7k forks) plus SDKs (Go, Java, TypeScript, Python, .NET, PHP, Ruby). You write a "workflow" as normal code in your language; the SDK intercepts every side effect ("activities": API calls, DB writes, LLM calls) and the server event-sources the execution history. If a worker dies mid-run, another worker deterministically replays the history and resumes exactly where it left off. The result: retries, timeouts, backoff, human-in-the-loop waits ("signals"), and month-long sleeps come for free, without you writing state machines or checkpoint tables. Workers poll task queues from your own infra, so code and data stay with you even when the orchestration plane is managed.

The commercial product is **Temporal Cloud**, a managed control plane with public consumption-based pricing (per "action" plus storage) — a real product, not a services wrapper. Recent platform additions target agentic workloads directly: **Nexus** (durable cross-team/cross-namespace service calls), large payload storage, task-queue priority/fairness, execution-history branching, serverless execution, and official integrations with the OpenAI Agents SDK, Vercel's AI SDK, and Pydantic (Verified — Series D announcement, Feb 2026).

## Founders & origins

**Maxim Fateev (co-founder, CTO)** and **Samar Abbas (co-founder, CEO)** built Uber's open-source orchestrator **Cadence** together; Temporal began as a fork of it (Verified — GitHub, Contrary Research, press). Fateev earlier worked on messaging/workflow infrastructure at Amazon (SQS/Simple Workflow lineage); Abbas worked on Microsoft's Durable Task Framework (Reported — Contrary Research, bios). They swapped roles in April 2024: Abbas took CEO, Fateev moved to CTO (Verified — TechCrunch).

## Funding

- **Seed, $6.75M (~2019):** Amplify Partners and Addition (Verified — company Series A announcement notes total raised of $25.5M).
- **Series A, $18.75M (Oct 2020):** led by Sequoia, with Madrona (Verified).
- **Series B, ~$100–103M (Feb 2022):** led by Index Ventures; valuation >$1.5B (Verified — company + Crunchbase; sources vary $100M vs $103M).
- **Series B extension, $75M (Feb 2023):** flat valuation (Verified — TechCrunch).
- **Series C, $146M (Mar 2025):** led by Tiger Global; $1.72B post-money (Verified — TechCrunch, Businesswire).
- **Secondary, $105M (Oct 2025)** (Reported — GeekWire).
- **Series D, $300M (Feb 2026):** led by Andreessen Horowitz, with Lightspeed and Sapphire; **$5B valuation** (Verified — company, GeekWire).
- **Total raised: ~$650M** (Reported — GeekWire).

## Evidence of real-world use

Unusually strong for this category. **OpenAI runs Codex on Temporal in production** at millions-of-requests scale (Reported — Temporal blog/Series D materials; repeatedly cited in press). Other named customers: **Replit, Lovable, ADP, Abridge, Washington Post, Block, Yum! Brands (Taco Bell/KFC)** (Series D announcement) and earlier **Box, Instacart, Snap, Stripe, Nvidia** (TechCrunch, Mar 2025). Documented case studies: **Gradient Labs** runs every AI support conversation for fintech clients as a Temporal workflow; **Grid Dynamics** deleted thousands of lines of custom retry code building a deep-research agent for a Fortune 500 manufacturer (Reported — vendor case studies). Scale metrics: 183k active OSS users and ~2,500 Cloud customers (Mar 2025, TechCrunch); at Series D the company claimed >380% YoY revenue growth, 20M+ monthly installs, and 9.1 trillion lifetime Cloud actions, 1.86T from AI-native companies (Reported — vendor figures).

## Relevance to agentic AI engineering

Temporal sits **below** frameworks like LangGraph: it doesn't decide what an agent does, it guarantees the loop survives reality — LLM rate limits, tool failures, day-long human approvals — without re-burning tokens on replay. That OpenAI's Codex runs on it connects directly to the repo's agentic-SWE-benchmark work: long-horizon coding agents are exactly the workloads where durable state and resumability dominate. Signals/updates and history auditability operationalize the tool-use/governance papers' concerns (approval gates, replayable traces of every tool call). The event-sourced workflow history is a complement — not a substitute — for the agent-memory line (MemGPT-style semantic memory): Temporal remembers *execution*, not *knowledge*. Voice-agent relevance is indirect (ambient/background agents, not the audio path).

## Use cases & considerations

Use cases: (1) production-hardening an existing agent loop — wrap LLM+tool calls as activities and get retries/resume for free; (2) long-running back-office automation with human-in-the-loop steps (invoice/job-packet style pipelines); (3) multi-agent systems where each agent is a child workflow; (4) classic infra orchestration (payments, provisioning) alongside AI.

Considerations: real operational cost — the deterministic-replay programming model has sharp edges (workflow code must be deterministic; versioning running workflows is a known pain), and self-hosting the server plus Cassandra/Postgres is nontrivial, which is the push toward Cloud. Lock-in is architectural more than contractual (MIT core, but code is structured around Temporal semantics). Competitors: **Orkes/Conductor, Inngest, Restate, DBOS, Hatchet, AWS Step Functions, Azure Durable Functions**; LangGraph's checkpointing overlaps at the framework layer. Open question: whether agent frameworks absorb "good-enough" durability, shrinking the case for a separate execution layer.

## Sources

- https://temporal.io/ and https://temporal.io/news/temporal-raises-300M-to-make-agentic-ai-real-for-companies
- https://github.com/temporalio/temporal
- https://www.geekwire.com/2026/temporal-raises-300m-hits-5b-valuation-as-seattle-infrastructure-startup-rides-ai-wave/
- https://techcrunch.com/2025/03/31/temporal-lands-146-million-at-a-flat-valuation-eyes-agentic-ai-expansion/
- https://techcrunch.com/2023/02/28/microservices-orchestration-platform-temporal-raises-75m-and-remains-a-unicorn/
- https://www.businesswire.com/news/home/20250330487137/en/Temporal-Technologies-Secures-$146M-at-$1.72B-Valuation-to-Fuel-Durable-Production-Agentic-Workloads-Globally
- https://temporal.io/news/temporal-raises-usd18-75m-series-a-increases-total-raised-to-usd25-5m
- https://temporal.io/news/temporal-io-raises-usd100-million-series-b-company-valuation-passes-usd1-5
- https://temporal.io/resources/case-studies/gradient-labs-uses-ai-agents-to-resolve-complex-customer-issues
- https://temporal.io/blog/prototype-to-prod-ready-agentic-ai-grid-dynamics
- https://research.contrary.com/company/temporal-technologies
