# SurrealDB

> Open-source (BSL), Rust-built multi-model database — document, graph, relational, vector, full-text, time-series, and geospatial in one engine — now positioning itself as the memory layer for AI agents.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** silver
- **Founded:** 2021, London, UK (SURREALDB LTD incorporated Sept 2021; project open-sourced 2022) — Verified (Companies House, Tracxn, press)
- **Website / GitHub:** https://surrealdb.com — https://github.com/surrealdb/surrealdb (~32.6k stars, BSL 1.1)

## What they do
SurrealDB is a single Rust engine that unifies data models most stacks split across several systems: schemaless documents, graph edges with recursive traversal, SQL-like relational queries, vector similarity search with HNSW indexing, full-text search, time-series, and key-value — all queried through **SurrealQL**, a SQL-flavored language with graph-traversal and vector operators. It runs three ways: embedded as a library (in-process, including WASM in the browser), as a single-node server, or as a distributed cluster over a pluggable KV backend (TiKV, FoundationDB). It also ships live queries over WebSockets and row/field-level permissions in the database itself, which lets thin clients query it directly.

**SurrealDB 3.0** (GA February 17, 2026) is an explicit pivot to agentic AI: hybrid search combining vector similarity, keyword search, and structured filters in one query; "context graphs" tracking entities, relationships, and timelines for agent memory; and **Surrealism**, an open-source plugin system for running Rust-defined logic inside the database rather than in middleware. The pitch to engineers: an agent's episodic memory (time-series), semantic memory (vectors + full-text), and relationship/world model (graph) live in one transactional store instead of a vector DB + graph DB + Postgres sandwich.

Commercially: the core database is Business Source License 1.1 (free to use, embed, and self-host at any scale; you can't resell it as a DBaaS; each release converts to Apache 2.0 after four years). **Surreal Cloud** is the managed offering with usage-based pricing; an Enterprise edition requires a commercial agreement.

## Founders & origins
Brothers **Tobie Morgan Hitchcock** (CEO) and **Jaime Morgan Hitchcock** (COO) — Verified across company site, LinkedIn, TechCrunch, and interviews. They began sketching the design around 2015 after years of building SaaS systems and juggling multiple database types per project; the database was open-sourced in 2022 and grew from ~180 to 1,500 GitHub stars in 48 hours at launch, which catalyzed the company — Reported (founder interviews, LinkedIn posts).

## Funding
- Seed: $6M led by FirstMark Capital, closed Nov 2022 / announced Jan 2023 — Verified (TechCrunch, company)
- Series A: announced June 2024 as "$20M raised to date," led by FirstMark and Georgian with Crew Capital and Alumni Ventures — Verified (note: that figure appears to include the seed)
- Series A extension: $23M, announced Feb 17, 2026, alongside 3.0 GA; Chalfen Ventures and Begin Capital joined FirstMark and Georgian; Mike Chalfen joined the board — Verified (company, SiliconANGLE, TechTarget)
- Total raised: $44M (company-stated; total Series A $38M + $6M seed). Tracxn lists $49M — the discrepancy traces to whether the 2024 "$20M" is read as inclusive of seed. Flagged rather than resolved.

## Evidence of real-world use
Better than logo-wall — several case studies have concrete numbers: **Samsung Ads** runs a knowledge graph for audience targeting (company-reported: query times from hours to seconds, ~30% cost reduction); **Verizon** powers a gen-AI assistant for ~10,000 field technicians (reported 40% faster responses); **Tencent** consolidated nine backend monitoring tools onto it; **Saks Fifth Avenue** serves ~1.5M weekly product recommendations from a single node; **PolyAI** uses it for low-latency customer-controlled RAG behind voice agents; **Permit.io** runs recursive permission-graph queries across millions of files — all Reported (company case studies; not independently audited, but detailed and named). OSS signals — Verified via GitHub: ~32.6k stars, 135 releases (v3.1.5 June 2026), SDKs in Rust/JS/Python/Go/Java/.NET, active Discord/community.

## Relevance to agentic AI engineering
SurrealDB is a direct bet on the agent-memory layer this repo tracks: the gap described in **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** — between raw vector stores and memory that carries entities, relations, and time — is precisely what 3.0's context graphs claim to close, in-database rather than via middleware like Mem0/Cognee. Its metadata-rich hybrid retrieval maps onto **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval**; the PolyAI voice deployment is a live instance of the tail-latency problem in **VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents**. In-database row/field permissions are also relevant to tool-use governance: an agent given DB access inherits enforceable scoping without a proxy layer.

## Use cases & considerations
Use cases: (1) single-store agent memory — embeddings, entity graph, and event log in one transactional engine; (2) knowledge graphs with hybrid graph+vector retrieval for RAG (the Samsung/Permit.io pattern); (3) embedded local-first apps (in-process or WASM) needing sync and live queries; (4) collapsing a Postgres + vector DB + graph DB stack in early-stage products.

Considerations: "does everything" databases carry maturity risk per model — a dedicated engine (Postgres, Neo4j, Qdrant) is likely deeper on any single axis; benchmark for your workload. BSL 1.1 is not OSI open source (self-hosting is fine, reselling isn't). Competitors on multiple fronts: Postgres+pgvector+AGE, Neo4j, MongoDB Atlas, Qdrant/Weaviate, EdgeDB/Convex. Open questions: distributed-mode production maturity at scale, and whether agent memory consolidates into general databases or stays a specialized layer — SurrealDB and the vector DBs are betting opposite ways.

## Sources
- https://surrealdb.com/ and https://surrealdb.com/blog/introducing-surrealdb-3-0--the-future-of-ai-agent-memory
- https://github.com/surrealdb/surrealdb and https://github.com/surrealdb/license
- https://surrealdb.com/blog/surrealdb-raises-23m-series-a-extension-to-power-the-ai-native-database-era
- https://surrealdb.com/blog/surrealdb-raises-20m-to-disrupt-database-tech-introduces-new-cloud-beta-access
- https://techcrunch.com/2023/01/04/surrealdb-raises-6m-startup-funding-database-as-a-service/
- https://siliconangle.com/2026/02/17/surrealdb-raises-23m-expand-ai-native-multi-model-database/
- https://www.techtarget.com/searchdatamanagement/news/366639042/SurrealDB-raises-23M-launches-update-to-fuel-agentic-AI
- https://thenewstack.io/surrealdb-3-ai-agents/
- https://surrealdb.com/casestudies (Samsung, Verizon, Tencent, PolyAI, Permit.io, GameScript pages)
- https://surrealdb.com/license and https://surrealdb.com/pricing
- https://find-and-update.company-information.service.gov.uk/company/13615201
- https://tracxn.com/d/companies/surrealdb/__BT2Y89TLe1oD9nDEcJ1L4Z5kn5B5oQCUXTPFJ5kJTz8
- https://techround.co.uk/interviews/meet-tobie-morgan-hitchcock-ceo-co-founder-of-surrealdb/
