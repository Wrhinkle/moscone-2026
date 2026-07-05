# LangChain

> The default open-source toolkit for building LLM agents (LangChain/LangGraph), monetized through LangSmith, a hosted observability/evals/deployment platform for those agents.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** OSS project late 2022; incorporated early 2023, San Francisco (Verified — TechCrunch, Fortune, company's own about page)
- **Website / GitHub:** https://www.langchain.com · https://github.com/langchain-ai/langchain · https://github.com/langchain-ai/langgraph

## What they do

Three layers, and it matters to keep them straight. **LangChain** (MIT-licensed, Python + JS) is the original framework: model-provider abstractions, tool/`create_agent` primitives, integrations. The 1.0 release (October 2025) re-centered it on agents rather than the old "chains" sprawl, and it now runs on the LangGraph runtime underneath. **LangGraph** (also OSS) is the lower-level orchestration runtime — agents as graphs/state machines with durable execution, checkpointing, streaming, human-in-the-loop interrupts, and persistence. It's usable without LangChain and is what serious production teams actually deploy on. **LangSmith** is the commercial product: tracing/observability, prompt management, evals and dataset runs, plus a deployment platform (formerly LangGraph Platform) for hosting long-running stateful agents. Public seat + usage pricing (free dev tier, ~$39/seat Plus, enterprise/self-hosted) — a real commercial product, not a logo page.

Newer: **deepagents**, an opinionated "batteries-included" agent harness on top of these primitives (planning, sub-agents, filesystem, context management) — LangChain's answer to Claude-Code-style deep agents as a library.

What you'd actually buy/integrate: OSS frameworks for free; LangSmith for traces + evals (works even if your agent isn't written in LangChain, via OTel-compatible SDKs); the deployment platform if you want managed infra for stateful agents.

## Founders & origins

**Harrison Chase (CEO)** — ML engineer at Robust Intelligence, previously Kensho (Reported); started LangChain as a side project in late October 2022, weeks before ChatGPT shipped (Verified — TechCrunch, Fortune). **Ankush Gola (co-founder)** — Princeton EE, four years at Facebook as senior SWE, met Chase at Robust Intelligence (Verified — Fortune, LinkedIn, Princeton AI talk). They incorporated in early 2023 after OSS traction exploded.

## Funding

- **Seed, $10M (April 2023):** led by Benchmark (Verified — TechCrunch, multiple sources).
- **Series A, $25M (announced Feb 2024, closed ~May 2023 per TechCrunch):** led by Sequoia, ~$200M valuation (Verified).
- **Series B, $125M (October 2025):** led by IVP, with CapitalG and Sapphire Ventures joining Sequoia, Benchmark, Amplify; **$1.25B valuation** (Verified — company blog, TechCrunch, Fortune).
- **Total raised: ~$260M** (Verified — consistent across Tracxn/press). Reported ~$12–16M ARR around 2025 (Reported — Sacra/Getlatka; treat as estimate).

## Evidence of real-world use

- **OSS scale:** langchain repo ~118k stars / ~19k forks; langgraph ~34k stars; deepagents ~24k stars (Verified — GitHub, Oct 2025–2026 figures). Among the most-downloaded AI packages on PyPI.
- **Named production customers with documented case studies** (vendor-published but specific): **Klarna** — AI assistant on LangGraph/LangSmith serving 85M users, ~80% faster resolution; **Replit** — its coding agent is built on LangGraph; **Uber, LinkedIn, Elastic** (threat-detection agents); **C.H. Robinson** — 5,500 orders/day automated; **AppFolio** (Realm-X copilot, 2x accuracy after moving to LangGraph); **Vizient, Dun & Bradstreet, Exa** (multi-agent web research) (Reported — vendor case studies; Klarna and Replit also independently covered in press).
- LangChain's State of AI Agents report claims 10x YoY growth in tokens traced through LangSmith (Reported — vendor data).

## Relevance to agentic AI engineering

This is the center of the **agent-orchestration** layer this category tracks: graph-based control flow, durable state, human-in-the-loop gates, and the eval/trace loop. LangSmith's eval tooling is the productized version of what the repo's agentic SWE benchmark work (SWE-bench-style harnesses) does offline — trajectory-level scoring against datasets. LangGraph's checkpointing/persistence and its memory store are a shipping counterpart to the agent-memory papers (MemGPT-lineage ideas of externalized, persistent state). Interrupt/approval nodes are where the tool-use/governance papers' concerns get operationalized. Voice-agent relevance is thinner — LangGraph is used as the brain behind voice stacks (e.g. with Daily/AssemblyAI-type pipelines) rather than doing audio itself.

## Use cases & considerations

Use cases: (1) long-running back-office agents needing durable state + human approval steps; (2) adding tracing/evals to an existing agent (LangSmith is framework-agnostic); (3) multi-agent research/support systems (the Exa/Klarna pattern); (4) fast prototyping via deepagents.

Considerations: the framework has a reputational hangover — pre-1.0 LangChain was widely criticized as over-abstracted, and some teams use LangGraph or raw SDKs while skipping LangChain proper. LangSmith is the lock-in surface (traces, datasets, deployments), not the MIT-licensed frameworks. Competitors: **OpenAI Agents SDK, Google ADK, CrewAI, Mastra, Temporal** (durable execution), and **Braintrust/Arize/Langfuse** on the observability side. Open question: whether the orchestration layer stays valuable as model providers absorb agent loops into their own SDKs/harnesses.

## Sources

- https://www.langchain.com/ and https://www.langchain.com/about
- https://www.langchain.com/blog/series-b
- https://techcrunch.com/2025/10/21/open-source-agentic-startup-langchain-hits-1-25b-valuation/
- https://fortune.com/2025/10/20/exclusive-early-ai-darling-langchain-is-now-a-unicorn-with-a-fresh-125-million-in-funding/
- https://github.com/langchain-ai/langchain · https://github.com/langchain-ai/langgraph · https://github.com/langchain-ai/deepagents
- https://www.langchain.com/customers and https://www.langchain.com/built-with-langgraph
- https://blog.langchain.com/exa/
- https://docs.langchain.com/oss/python/langgraph/case-studies
- https://www.ivp.com/content/langchain-the-platform-for-the-enterprise-ai-agent-era/
- https://tracxn.com/d/companies/langchain/__O9N2dOHcgRE9Nbcn5BFfkUHn-rVk6GTbq8oY-UJ0Ba4
- https://sacra.com/c/langchain/
- https://ai.princeton.edu/news/2026/watch-langchain-co-founder-cto-comes-campus-founders-talk-series
