# LanceDB

> Open-source embedded vector database plus a columnar storage format (Lance) built for multimodal AI — positioning itself as the "lakehouse" where AI teams keep vectors, images, video, and training data in one place.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** bronze
- **Founded:** 2022, San Francisco (Y Combinator W22) — Verified
- **Website / GitHub:** https://lancedb.com — https://github.com/lancedb/lancedb (~10.8k stars) and https://github.com/lance-format/lance

## What they do
Two layers, both open source. The foundation is **Lance**, a Rust-implemented columnar format positioned as a Parquet successor for AI data: ~100x faster random access, built-in vector indexing, data versioning, and the ability to append columns without rewriting the dataset — designed for the mixed random-read/scan patterns of embedding search and model training rather than pure analytics scans. It interoperates with Pandas, DuckDB, Polars, PyArrow, and PyTorch.

On top sits **LanceDB**, an embedded retrieval library (the "SQLite of vector search" pattern): it runs in-process with native Python, TypeScript/JavaScript, and Rust APIs, stores data on local disk or directly on object storage like S3, and does vector + full-text + hybrid search with metadata filtering. No server to run for the OSS version. Commercially there's **LanceDB Cloud** (serverless, usage-based) and **LanceDB Enterprise** (BYOC/VPC deployments). In June 2025, alongside the Series A, they launched the **Multimodal Lakehouse**: one platform on the Lance format serving search, feature engineering, and model-training workloads without separate infrastructure per workload — the pitch is compute/storage separation on cheap object storage instead of RAM-resident vector clusters.

## Founders & origins
**Chang She** (CEO) — one of the original major contributors to Pandas, ex-CTO/co-founder of DataPad, former VP Engineering at Tubi where he built the ML stack; earlier a quant at AQR and Barclays — Verified (YC, conference bios, TechCrunch). **Lei Xu** (CTO) — led ML infrastructure at Cruise (2018–2021), previously HDFS engineer at Cloudera, Apache Hadoop committer/PMC, PhD in CS (University of Nebraska–Lincoln) — Verified (LinkedIn/The Org, consistent across sources). Origin story: both hit the same wall — data infrastructure built for tabular analytics is a poor fit for ML engineers working with embeddings and multimodal data — and started with the format itself rather than a database — Reported (TechCrunch interview).

## Funding
- Seed: $8M, May 2024, led by CRV with Essence VC and Swift Ventures; total raised $11M at that point including earlier YC-era money — Verified (TechCrunch, company)
- Series A: $30M, announced June 24, 2025, led by Theory Ventures with CRV, Y Combinator, Databricks Ventures, RunwayML, Zero Prime, and Swift — Verified (company blog, Crunchbase, press)
- Total raised: ~$41M — Verified (YC/CRV profiles corroborate)

Databricks Ventures and Runway participating is notable signal: a data-platform incumbent and a marquee customer both invested.

## Evidence of real-world use
Unusually strong for a bronze-tier sponsor. Named production customers: **Midjourney** (vector search at "high-traffic, large scale" — TechCrunch covered this independently in 2024), **Character.AI**, **Runway** (uses Lance in its model-training pipeline; testimonial cites append-columns-without-rewrite and fast random access), **WeRide** (autonomous driving), and **Airtable** — Verified (TechCrunch + company customer page). Series A materials claim petabytes of training data and searches across tens of billions of vectors at these customers — Reported (company). OSS signals: 20M+ Lance package downloads as of June 2025 — Reported (company); ~600k monthly downloads as of May 2024 per TechCrunch. Strong ecosystem evidence: **Continue.dev** ships LanceDB as the embedded store behind its codebase indexing (documented in Continue's own docs/architecture, with real bug traffic in their issue tracker — a sign of actual use), and LanceDB is a supported backend in LangChain and LlamaIndex.

## Relevance to agentic AI engineering
LanceDB is a memory/retrieval substrate for agents, with a distinctive angle: embedded and file-based, so an agent's memory can live in-process or on object storage with no service dependency. That maps directly onto the repo's memory papers — **Are We Ready For An Agent-Native Memory System?** and **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** frame the gap between raw vector stores and agent memory that LanceDB's hybrid search + versioned tables would sit under; **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval** speaks to its metadata filtering. The Continue.dev integration ties it to the coding-agent thread (codebase retrieval underlies the systems evaluated in **OmniCode** and **ProdCodeBench**), and the embedded/low-latency story is relevant to **VoiceAgentRAG**'s RAG-latency bottleneck for voice agents.

## Use cases & considerations
Use cases: (1) local-first agent memory or codebase index shipped inside a desktop/CLI tool (the Continue pattern — no server for end users); (2) RAG over object storage where you'd rather pay S3 prices than RAM-cluster prices; (3) multimodal datasets (images/video + embeddings + metadata) shared between search and training; (4) versioned, reproducible retrieval corpora for agent evals.

Considerations: crowded category — Qdrant, Pinecone, Weaviate, Chroma, Turbopuffer (closest architecturally: also object-storage-first), plus pgvector for teams that just want Postgres. The lakehouse expansion pits them against far bigger data-platform players, and Databricks' investment cuts both ways (validation vs. absorption). OSS is Apache 2.0 so lock-in is low; Cloud/Enterprise pricing is usage-based but Enterprise terms are opaque. Open question: whether the Lance format wins broad ecosystem adoption beyond LanceDB itself — that's the real bet.

## Sources
- https://lancedb.com and https://www.lancedb.com/customers
- https://www.lancedb.com/blog/series-a-funding
- https://techcrunch.com/2024/05/15/lancedb-which-counts-midjourney-as-a-customer-is-building-databases-for-multimodal-ai/
- https://www.ycombinator.com/companies/lancedb
- https://github.com/lancedb/lancedb and https://github.com/lance-format/lance
- https://www.crunchbase.com/funding_round/lancedb-series-a--4ac9a0b2
- https://theorg.com/org/lancedb/org-chart/lei-xu and https://theorg.com/org/lancedb/org-chart/chang-she
- https://www.crv.com/companies/lancedb
- https://docs.continue.dev/guides/custom-code-rag and https://deepwiki.com/continuedev/continue/3.4-codebase-indexing
- https://blog.lancedb.com/lancedb-x-continue/
