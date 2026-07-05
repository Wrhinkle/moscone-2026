# FalkorDB

> Low-latency property graph database (the continuation of RedisGraph) positioning itself as the knowledge-graph backend for GraphRAG and agent memory.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** bronze
- **Founded:** 2023, Petah Tikva, Israel (Verified — company site, Startup Nation Finder, Tracxn; the codebase itself dates to RedisGraph, which is years older)
- **Website / GitHub:** https://www.falkordb.com/ · https://github.com/FalkorDB/FalkorDB

## What they do
FalkorDB is a property graph database that runs as a Redis module and answers openCypher queries. Its distinguishing technical bet, inherited from RedisGraph: graphs are stored as GraphBLAS sparse adjacency matrices, and traversals compile down to linear-algebra operations (sparse matrix multiplication) instead of pointer-chasing. That is what its sub-10ms / multi-hop latency claims rest on. It requires Redis 7.4+, is written mostly in C, and is licensed SSPLv1 (source-available, not OSI open source — same posture as MongoDB/Elastic).

The company was formed when Redis EOL'd RedisGraph (announced July 2023; support ended January 2025). The original RedisGraph author forked the module and kept building — so FalkorDB is less a startup building a database from scratch than the maintainers of an existing engine spinning out around it. Since the fork they've added multi-graph/multi-tenancy (thousands of isolated graphs per instance — relevant for per-agent or per-customer memory), graph access control, and vector similarity alongside graph queries.

What you'd actually buy or integrate: (1) the database itself, self-hosted via Docker or through FalkorDB Cloud (public pricing: free tier with 100MB, Startup from ~$73/mo at $0.10/GB-hour, Pro from ~$350/mo with HA/clustering; Azure via BYOC for enterprise); (2) **GraphRAG-SDK**, an LLM-agnostic Python framework that builds knowledge graphs from documents and does retrieval over them — they claim it ranked #1 on GraphRAG-Bench Novel and Medical datasets (Reported — their own blog, not independently verified); (3) as a backend for **Graphiti**, Zep's temporal knowledge-graph agent-memory framework, which added official FalkorDB support for multi-agent isolation and performance.

## Founders & origins
Verified across company site, Calcalist, and Tracxn: **Guy Korland** (CEO, PhD, database background), **Roi Lipman** (CTO — the engineer behind RedisGraph at Redis; the sparse-matrix approach is his), and **Avi Avni** (Chief Architect; prior contributions to C#/F# ecosystems, had independently built a similar database before joining forces). Origin story is unusually legible: Redis killed RedisGraph, its creator forked it, and the fork became the company (Show HN, August 2023: "FalkorDB fork from RedisGraph bringing it back to life").

## Funding
- **Seed, ~$3M, June 2024** — led by Angular Ventures with K5 Global, plus angels including Jerry Dischler (Google) and Firebolt co-founders Eldad Farkash and Saar Bitner (Verified — Crunchbase, Tracxn, StartupHub agree on round and lead; amount consistently reported as $3M).
- Total raised: ~$3M. No later rounds found in public sources as of 2026-07-02. This is a very lean company relative to Neo4j.

## Evidence of real-world use
- **Securin case study** (vendor-published, but with concrete numbers): cybersecurity intelligence firm replaced "a leading graph database vendor" with FalkorDB for its CVE/threat-actor knowledge graph queried by AI copilot agents — query latency 1.5s → 0.3s, agent responses ~15s → ~3s, enabling 7-hop traversals within a 5s SLO. This is the strongest production signal and it is exactly the agent-retrieval use case.
- **GitHub:** ~4.7k stars, ~400 forks, 76 releases, active through June 2026 (Verified). Real but modest OSS traction; some of that community is inherited RedisGraph users, since Redis's EOL left them needing a migration path.
- **Graphiti backend support** (Verified — both projects document it) puts FalkorDB inside a widely-used agent-memory framework rather than only selling direct.
- Public pricing page and GCP Marketplace listing = real commercial product. No large named-logo customer list found beyond Securin (stated explicitly rather than guessed).

## Relevance to agentic AI engineering
FalkorDB sits at the memory/retrieval layer, same slot as Neo4j (see companion profile) but optimized for latency and multi-tenant agent workloads rather than enterprise analytics. The Graphiti integration makes it a concrete substrate for the architectures in this repo's agent-memory papers — **Graph-based Agent Memory: Taxonomy, Techniques, and Applications** and **GAM: Hierarchical Graph-based Agentic Memory for LLM Agents** describe the graph-shaped memory it hosts, while **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** frame the open questions (multi-tenancy per agent is FalkorDB's specific answer to isolation). The Securin pattern — agents translating natural language into multi-hop Cypher — raises the same least-privilege concerns as **Governance by Construction for Generalist Agents**: an agent emitting arbitrary Cypher needs scoped graph ACLs, which FalkorDB does ship.

## Use cases & considerations
Use cases: (1) per-agent or per-user isolated memory graphs (multi-tenancy is the differentiator vs. one big enterprise graph); (2) latency-sensitive GraphRAG behind interactive agents where a 1–2s graph query blows the response budget; (3) drop-in RedisGraph migration; (4) Graphiti/Zep-style temporal agent memory without running Neo4j.

Considerations: tiny company (~$3M raised) — vendor-viability risk for long-lived deployments, mitigated by source-available code you can self-host forever. SSPL licensing constrains offering it as a service. Ecosystem, tooling, and hiring pool are far smaller than Neo4j's (main competitor; also Memgraph, Kuzu, Amazon Neptune, and increasingly Postgres+pgvector-plus-graph approaches). Benchmark claims are largely self-published — validate on your own workload. Open question: whether GraphRAG-SDK gets independent adoption or remains a funnel into the database.

## Sources
- https://www.falkordb.com/ and https://www.falkordb.com/company/
- https://github.com/FalkorDB/FalkorDB
- https://www.falkordb.com/blog/redisgraph-eol-migration-guide/
- https://news.ycombinator.com/item?id=37104193
- https://www.crunchbase.com/funding_round/falkordb-seed--663ce4f6
- https://tracxn.com/d/companies/falkordb/__PJxFm_FWv6LlUi5sobdRovUnRjmKZkmxjbgryRNDj4M
- https://www.calcalistech.com/ctechnews/article/rju0kvhb0
- https://www.falkordb.com/case-studies/securin-falkordb-graph-case-study/
- https://www.falkordb.com/blog/graphiti-falkordb-multi-agent-performance/
- https://www.falkordb.com/blog/graphrag-sdk-knowledge-graph/
- https://www.falkordb.com/plans/ and https://docs.falkordb.com/cloud/
- https://dbdb.io/db/falkordb
