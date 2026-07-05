# LlamaIndex

> Open-source framework for connecting LLMs to your data (RAG, agents, workflows), monetized through LlamaCloud — a document parsing/extraction platform and, in 2026, hosted "document agents."

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** OSS project (as "GPT Index") November 2022; company incorporated 2023, San Francisco (Verified — company blog, press, Tracxn)
- **Website / GitHub:** https://www.llamaindex.ai · https://github.com/run-llama/llama_index · https://github.com/run-llama/llama-agents

## What they do

Two distinct layers. **LlamaIndex the framework** (MIT, Python + TypeScript) is the data-to-LLM plumbing: document loaders, chunking/indexing, retrievers, query engines, and agent abstractions, with 300+ integration packages on LlamaHub for vector stores, embedding models, and LLM providers. It was *the* RAG framework of 2023–24; since then the center of gravity moved to **Workflows** (spun out as `llama-agents`/Workflows 1.0), an event-driven, async-first orchestration library where steps are plain Python/TS functions emitting and consuming events — their answer to LangGraph's graph runtime, deliberately lighter-weight. `llama-agents-server` wraps any workflow as a REST API with streaming, persistence, and human-in-the-loop.

**LlamaCloud** is the commercial product, anchored by **LlamaParse**: parsing/OCR/extraction for ugly enterprise documents (scanned PDFs, nested tables, charts), with "agentic" parsing modes that use VLMs for layout-aware extraction. SaaS or on-prem, SOC 2 Type 2. In 2025–26 they repositioned from "RAG framework" to "document agent platform": **LlamaAgents** (open preview) gives templated, one-command-deployable agents for invoice processing, contract review, and claims handling. They also shipped **LiteParse** (open-source local parser) and **ParseBench**, a ~2,000-page human-verified parsing benchmark on which they score their own LlamaParse Agentic at 84.9% (vendor-run — treat accordingly).

What you'd buy: framework and Workflows free; LlamaCloud on public credit-based pricing (Free 10K credits; Starter $50/mo; Pro $500/mo; ~$1.25 per 1,000 credits, basic parsing from 1 credit/page) — a real self-serve commercial product, not just enterprise sales.

## Founders & origins

**Jerry Liu (CEO)** — Princeton CS; research scientist at Uber ATG, then ML lead at Robust Intelligence (Reported — LinkedIn, interviews). Built GPT Index as a side project in November 2022 to let LLMs use data beyond their training set; it exploded alongside ChatGPT. **Simon Suo (co-founder)** — also ex-Uber ATG (Verified for name/role — Tracxn, press; background details Reported). Incorporated in 2023 after OSS traction.

## Funding

- **Seed, $8.5M (June 2023):** led by Greylock (Verified — multiple databases/press).
- **Series A, $19M (March 2025):** led by Norwest Venture Partners, Greylock participating (Verified — company blog, PRNewswire).
- **Strategic minority investments from Databricks Ventures and KPMG Ventures (May 2025):** amounts undisclosed (Verified — company/Jerry Liu announcements).
- **Total raised: ~$27.5M** disclosed (Verified — Tracxn, company blog). Notably small vs. LangChain's ~$260M. Post-money valuation ~$93M (Reported — secondary-market sources; unconfirmed).

## Evidence of real-world use

- **OSS scale:** ~50.7k GitHub stars, 7.7k forks, 495 releases (Verified — GitHub, July 2026); company cited 3M monthly downloads at Series A, ~5M+ monthly by 2026 (Reported — vendor figures).
- **Named enterprise users:** Rakuten, Carlyle (Applied AI lead quote calling LlamaParse "the best technology I have seen for parsing complex document structures for Enterprise RAG"), Salesforce (Agentforce team uses LlamaParse in RAG pipelines), KPMG — the latter two doubled as investors (Reported — vendor blog, but specific and consistent).
- **Case studies with numbers:** Pursuit parsed 4M pages in a weekend, +25–30% accuracy; Pathwork went from 5K to 40K insurance pages/week; StackAI processed 1M+ documents on LlamaParse; Scaleport ~50–60% fewer dev hours (Reported — vendor case studies).
- LlamaParse claimed "hundreds of millions of documents" processed for tens of thousands of users (Reported — vendor).

## Relevance to agentic AI engineering

Sits at the intersection of **agent orchestration** and **memory/RAG**: Workflows is a direct LangGraph competitor for event-driven multi-agent control flow with human-in-the-loop gates — where the repo's tool-use/governance papers' approval-and-audit concerns get operationalized. Their retrieval/indexing layer is the shipping counterpart to the agent-memory line of work (externalized state, long-horizon context); their own "Long Horizon Document Agents" writing engages the same problem. ParseBench is a domain-specific analogue to the agentic SWE benchmark pattern — task-grounded, human-verified eval sets rather than vibes. Recent Agent Client Protocol integration (filesystem/bash tools, MCP servers, persistent memory) connects to the tool-use standardization work. Voice-agent relevance is minimal — this stack is documents-first.

## Use cases & considerations

Use cases: (1) parsing messy back-office documents (invoices, claims, contracts, decades-old scans) into agent-usable structure — directly relevant to construction job-packet-style workflows; (2) production RAG over heterogeneous enterprise corpora; (3) lightweight multi-agent orchestration via Workflows without adopting a heavy framework; (4) fast-deploy templated document agents via LlamaAgents.

Considerations: the framework's abstractions drew the same over-wrapping criticism as pre-1.0 LangChain; many teams use only LlamaParse and skip the framework. LlamaCloud is the lock-in surface. Parsing competitors are strong and cheaper at volume: **Reducto** (also in this repo), **Unstructured**, **Chunkr**, and increasingly raw VLM calls (Gemini/GPT-4o-class models doing native PDF understanding) — the existential question is whether standalone parsing survives model-native document understanding. Orchestration competitors: **LangGraph, OpenAI Agents SDK, CrewAI, Mastra**. Funding is modest for the category — capital efficiency or ceiling, unclear which.

## Sources

- https://www.llamaindex.ai/ and https://www.llamaindex.ai/pricing
- https://www.llamaindex.ai/blog/announcing-our-series-a-and-llamacloud-general-availability
- https://www.prnewswire.com/news-releases/llamaindex-secures-19-million-series-a-to-power-enterprise-grade-knowledge-agents-302390936.html
- https://github.com/run-llama/llama_index · https://github.com/run-llama/llama-agents
- https://tracxn.com/d/companies/llamaindex/__U3EoO86v47zgZGnpR8N_TwMcdPI5GXVFL6PMeMT0sSU
- https://www.llamaindex.ai/blog/pursuit-transforms-public-sector-insights-with-llamaparse
- https://www.llamaindex.ai/customers/stackai-uses-llamacloud-to-power-high-accuracy-retrieval-for-its-enterprise-document-agents
- https://www.llamaindex.ai/customers/how-scaleport-ai-accelerated-development-and-improved-sales-with-llamacloud
- https://www.llamaindex.ai/blog/llamaagents-build-serve-and-deploy-document-agents
- https://www.llamaindex.ai/blog/announcing-workflows-1-0-a-lightweight-framework-for-agentic-systems
- https://www.llamaindex.ai/blog/llamaindex-is-more-than-a-rag-framework
- https://www.linkedin.com/posts/jerry-liu-64390071_today-were-excited-to-announce-that-llamaindex-activity-7323735973463228416-w5SE
- https://www.clay.com/dossier/llamaindex-funding
