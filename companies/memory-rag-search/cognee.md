# Cognee

> Open-source memory engine for AI agents: it turns your documents and interaction history into a combined knowledge graph + vector index that agents can query, update, and prune across sessions.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** bronze
- **Founded:** 2024, Berlin, Germany (OSS project started ~2023 under the GitHub org "topoteretes"; German entity Topoteretes UG, US entity cognee inc) — Verified
- **Website / GitHub:** https://www.cognee.ai — https://github.com/topoteretes/cognee (Apache 2.0)

## What they do
Cognee is a Python-first memory layer that sits between your data and your agent. Its core operation, `cognify`, runs an ingestion pipeline over arbitrary documents: classify, chunk, use an LLM to extract entities and relationships, generate summaries, then embed everything into a vector store while committing typed edges to a graph store. The result is a hybrid graph+vector memory — searchable by meaning (embeddings) and traversable by relationship (graph) — rather than a flat chunk index. A second operation, `memify`, treats the graph as *evolving* memory: pruning stale nodes, reweighting edges from usage signals, and adding derived facts, which is the concrete difference between "RAG over documents" and "agent memory."

The developer surface is deliberately small — remember / recall / forget / improve — with ~14 retrieval modes underneath, from classic vector RAG to chain-of-thought graph traversal, plus auto-routing to pick a strategy per query. It defaults to a single Postgres instance with swappable backends (dedicated graph DBs like Neo4j/Kuzu, vector DBs like Qdrant), ships an MCP server (stdio/HTTP/SSE), a Claude Code plugin for persistent cross-session memory, and Rust/TypeScript clients. Commercial layer: **Cognee Cloud** (hosted, usage-based at ~$2.50/1M tokens with a free tier — a public pricing page, so a real commercial product) — Verified via GitHub README, docs, and cognee.ai.

## Founders & origins
**Vasilije Markovic** (CEO) and **Boris Arzentar** (CTO) — Verified across the company site, funding press, and Crunchbase. Markovic spent ~a decade in Berlin data engineering (Zalando, Omio, and first Data Product Manager at Taxfix); he later studied cognitive science/clinical psychology, and Cognee's "multilayered memory" framing comes directly from that — Reported (Heavybit podcast, LinkedIn, conference bios). Arzentar joined as co-founder/CTO in early 2024; public detail on his prior roles is thin beyond cloud/infrastructure engineering — Reported/partially Unverified.

## Funding
- Pre-seed: €1.5M (~$1.5–1.6M), announced November 2024 — Verified (company blog + Crunchbase)
- Seed: $7.5M led by **Pebblebed** (Pamela Vagata, ex-OpenAI founding team; Keith Adams, ex-FAIR), with 42CAP, Vermilion Ventures, and angels from Google DeepMind, n8n, and Snowplow — announced February 2026 — Verified (company blog, EU-Startups, Tech in Berlin, pulse2)
- Total raised: ~$9M — Verified (Tracxn: $9.09M over 2 rounds)

## Evidence of real-world use
Better than typical for a bronze-tier seed startup, though most case studies are company-published. Verified OSS signals: **~27.1k GitHub stars, ~2.5k forks, 121 releases (v1.2.2, June 2026)**, ~700k+ PyPI downloads (pepy.tech). Strong third-party validation: **Microsoft's `ai-agents-for-beginners` course uses Cognee as its agent-memory lesson (lesson 13)** — documented usage, not a logo wall. Company-reported: 70+ companies running Cognee in live environments (seed announcement); named case studies include **Dynamo.fyi** (gaming-user personalization agents over messenger — one of the first production deployments) and an unnamed Singapore construction-tech firm linking 3D building models to schedules and cost data — Reported. Cognee also publishes its own benchmarks (HotPotQA-based evals vs. Mem0, Zep/Graphiti, LightRAG, validated with DeepEval; README claims SOTA on the BEAM long-context benchmark at 100K–10M tokens) — Reported and self-published, treat as directional.

## Relevance to agentic AI engineering
Cognee is a direct commercial instantiation of this repo's agent-memory thread: **Graph-based Agent Memory: Taxonomy, Techniques, and Applications** and **GAM: Hierarchical Graph-based Agentic Memory for LLM Agents** describe exactly its architecture class; **Are We Ready For An Agent-Native Memory System?** and **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** frame the gap it claims to fill above raw vector stores (its self-run evals are the vendor version of that paper's evaluation problem). The `memify` maintenance loop maps to **Towards Autonomous Memory Agents**, and the metadata/graph-vs-vector retrieval question is the subject of **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval**. In the stack it sits one layer above Qdrant/Neo4j (both also profiled here) and competes with Mem0, Zep/Graphiti, and Letta.

## Use cases & considerations
Use cases: (1) persistent memory for a long-running back-office agent — e.g. a job-packet auditor that remembers subcontractors, permits, and prior claims across sessions; (2) graph-RAG over interlinked domain documents where multi-hop questions defeat chunked vector RAG; (3) cross-session memory for coding agents via the Claude Code plugin/MCP server; (4) personalization memory for customer-facing agents (the Dynamo pattern).

Considerations: LLM-driven graph extraction makes ingestion slower and more expensive than plain embedding, and extraction quality bounds graph quality; benchmarks favoring Cognee are self-published; the company is small (~10 people) and seed-stage, so weigh continuity risk for production dependencies — Apache 2.0 self-hosting mitigates lock-in. Competitors: Mem0, Zep (Graphiti), Letta, LightRAG, plus "just use pgvector + your own schema." Open question: whether standalone memory layers survive as frameworks (LangChain/LlamaIndex) and model providers absorb memory natively.

*Researched 2026-07-02.*

## Sources
- https://github.com/topoteretes/cognee
- https://www.cognee.ai/ and https://www.cognee.ai/about-us
- https://www.cognee.ai/blog/cognee-news/cognee-raises-seven-million-five-hundred-thousand-dollars-seed
- https://www.cognee.ai/blog/cognee-news/funding-and-web-site-launch
- https://www.crunchbase.com/organization/cognee-inc
- https://tracxn.com/d/companies/cognee/__XkSxgBzH5vOB59VwVuEQNwoDJxGMlvIPIq8cIV5WsJY
- https://www.eu-startups.com/2026/02/german-ai-infrastructure-startup-cognee-lands-e7-5-million-to-scale-enterprise-grade-memory-technology/
- https://pulse2.com/cognee-7-5-million-seed-funding-raised-for-building-enterprise-grade-memory-layer-for-ai-agents/
- https://www.heavybit.com/library/podcasts/open-source-ready/ep-20-exploring-ai-memory-with-vasilije-markovic-of-cognee
- https://www.cognee.ai/blog/case-studies/cognee-case-study-with-dynamo
- https://www.cognee.ai/blog/cognee-news/cognee-july-updates
- https://www.cognee.ai/blog/deep-dives/ai-memory-evals-0825
- https://deepeval.com/blog/use-case-cognee-ai-memory
- https://github.com/microsoft/ai-agents-for-beginners/blob/main/13-agent-memory/13-agent-memory-cognee.ipynb
- https://pepy.tech/projects/cognee
