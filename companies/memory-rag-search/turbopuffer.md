# Turbopuffer

> A serverless vector + full-text search engine built directly on object storage (S3/GCS), sold on being roughly 10x cheaper than RAM/SSD-first vector databases at large scale.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, Ottawa, Canada (Verified — BetaKit, Sacra, Globe and Mail agree)
- **Website / GitHub:** https://turbopuffer.com/ — no open-source core; proprietary managed service (client SDKs are the main public code)

## What they do
Turbopuffer is a search database whose storage engine treats object storage as the source of truth, with NVMe/memory used only as cache. Writes land durably on S3-class storage; hot namespaces get cached for fast queries (sub-10ms p50 claimed for cached vector queries). Because cold data costs object-storage prices instead of provisioned RAM/SSD, the economics invert for workloads with many tenants and skewed access patterns — exactly the shape of per-user AI features.

The query surface is: approximate nearest-neighbor vector search (claimed 90–100% recall@10), BM25 full-text search, hybrid combinations, and metadata filtering — over an HTTP API with namespaces as the isolation unit. Namespaces are cheap and numerous (Cursor reportedly runs 80M+), which is the key design decision for multi-tenant RAG: one namespace per user/workspace/repo rather than one big index with filters. Copy-on-write namespace branching was recently added. Scale claims on their homepage (2026-07-02): 4T+ documents, 15PB+, 10M+ writes/sec, 25k+ queries/sec across the fleet; per-namespace limits around 500M documents.

You integrate it as a managed API (multi-cloud regions on AWS/GCP); pricing is usage-based (storage + writes + queries) with a public cost calculator — a real, self-serve commercial product, not enterprise-only vaporware.

## Founders & origins
Simon Hørup Eskildsen (CEO) and Justin/Justine Li (CTO) — reported spellings vary; BetaKit uses "Justine" (Verified as co-founders; name spelling Reported). Both are ex-Shopify infrastructure engineers (~8 years, Eskildsen a principal engineer known for his resiliency/scaling writing), leaving around 2021. Origin story (Reported, multiple interviews): Eskildsen priced existing vector DBs for a side project circa 2023, found RAM-based pricing absurd for mostly-cold vectors, and built an object-storage-first engine; Li joined days after trying it. Team was ~22 people as of late 2025 (Reported — BetaKit), spread across Ottawa, Vancouver, and NYC.

## Funding
Deliberately under-raised — the anti-pattern for this category:
- Angel round, early 2024: under $1M from Lachy Groom (Reported — Sacra).
- Seed, December 2025: amount undisclosed; Thrive Capital new, Lachy Groom returning (Verified — BetaKit, Crunchbase, Sacra).
- Total raised: not computable from public sources; Sacra says "less than $1M in total primary capital" as of May 2026, which likely excludes the undisclosed seed (Unverified).
- Revenue: "tens of millions" ARR at the Dec 2025 raise (Reported — BetaKit); Sacra estimates ~$75M ARR end-2025 and ~$100M annualized by March 2026 (Reported — single-source estimate, treat cautiously).

## Evidence of real-world use
Unusually strong, documented rather than logo-wall:
- **Cursor** (Verified — turbopuffer's own case study plus independent coverage): powers codebase semantic indexing; migrated Nov 2023, ~95% cost reduction claimed, 1T+ documents, 80M+ namespaces.
- **Notion** (Verified — Google Cloud case study, AWS Startups piece, press): 10B+ vectors across millions of namespaces; ~80% cost reduction credited with enabling removal of per-user AI charges.
- Homepage/press also name Anthropic, Linear, Atlassian, Ramp, Cognition, Grammarly, Harvey, Superhuman; Sacra adds Bridgewater and TELUS (Reported). "500+ customers" (Reported — AWS Startups).
- Independent technical deep-dives exist (Jason Liu, Latent Space podcast, ANN v3 case study) — engineers analyze it unprompted, a good community signal.

## Relevance to agentic AI engineering
This is the retrieval/memory substrate layer of the agent stack. The economics of per-agent or per-user namespaces bear directly on the agent-memory question in **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** — cheap isolated namespaces make per-agent long-term semantic memory financially plausible (compare LinkedIn's approach in **Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents**). Hybrid search + metadata filtering is the mechanism interrogated in **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval**. Via Cursor, it's the retrieval backend behind the coding agents evaluated in the agentic-SWE benchmark line (**SWE-EVO**, **ProdCodeBench**). Latency claims matter for the voice-RAG bottleneck described in **VoiceAgentRAG**.

## Use cases & considerations
Use cases: (1) multi-tenant RAG with one namespace per customer/workspace; (2) codebase indexing for coding agents (the Cursor pattern); (3) long-term agent memory stores where most memories are cold; (4) hybrid BM25+vector retrieval replacing an Elasticsearch+vector-DB pair.

Considerations: closed-source and managed-only — real lock-in, no self-host escape hatch; cold-namespace first-query latency is inherently worse than RAM-resident DBs (warm-up matters for latency-critical paths); feature surface is deliberately narrower than Elastic/Qdrant/Weaviate (no aggregations-heavy analytics). Competitors: Pinecone, Qdrant, Weaviate, Milvus/Zilliz, pgvector, and S3 Vectors — AWS's 2025 native offering is the most direct architectural threat. Open questions: whether Sacra's ARR estimates hold, and how pricing evolves as hyperscalers copy the object-storage-first design.

## Sources
- https://turbopuffer.com/
- https://turbopuffer.com/customers/cursor
- https://betakit.com/ex-shopify-engineers-raise-fresh-financing-to-scale-turbopuffers-ai-search/
- https://sacra.com/c/turbopuffer/
- https://cloud.google.com/customers/turbopuffer
- https://aws.amazon.com/startups/learn/how-turbopuffer-is-refactoring-the-economics-of-search
- https://www.theglobeandmail.com/business/article-turbopuffer-fastest-growing-canadian-ai-startup-never-heard-of/
- https://www.crunchbase.com/organization/turbopuffer
- https://www.latent.space/p/turbopuffer
- https://jxnl.co/writing/2025/09/11/turbopuffer-object-storage-first-vector-database-architecture/
- https://www.pmf.show/blog/how-simon-eskildsen-built-turbopuffer-the-vector-db-powering-cursor-and-notion/
