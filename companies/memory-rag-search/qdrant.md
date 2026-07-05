# Qdrant

> Open-source, Rust-based vector database and hybrid search engine — one of the default choices for the retrieval/memory layer under RAG and agent systems.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, Berlin, Germany (OSS project started ~2020) — Verified
- **Website / GitHub:** https://qdrant.tech — https://github.com/qdrant/qdrant (Apache 2.0)

## What they do
Qdrant is a vector similarity search engine and database written in Rust. Core engine: HNSW-based approximate nearest neighbor search over dense vectors, with a *filterable* HNSW implementation so metadata ("payload") filters are applied during graph traversal rather than as slow pre-/post-filtering — a genuine differentiator for multi-tenant and access-controlled retrieval. Beyond dense vectors it supports sparse vectors (SPLADE/BM25-style, plus their own miniCOIL model), multivector/ColBERT-style late interaction, and a Query API that composes dense + sparse + filters + rescoring into multi-stage retrieval pipelines in a single request. Scalar, product, and binary quantization plus memmap/on-disk storage keep large collections affordable; recent releases added GPU-accelerated indexing.

You integrate it via REST/gRPC with official Python/JS/Go/Java/Rust clients, or through first-party integrations in LangChain, LlamaIndex, Haystack, and most agent frameworks. Deployment options: self-hosted (single binary or Kubernetes/Helm, including distributed clusters with sharding and replication), **Qdrant Cloud** (managed on AWS/GCP/Azure, free 1GB tier, hybrid/private-cloud options for BYOC), **Qdrant Cloud Inference** (managed embedding inference colocated with the DB), and **Qdrant Edge** (beta, announced with the Series B) targeting on-device retrieval with cloud sync. The Series B framing is "composable vector search": retrieval primitives (dense, sparse, filters, custom scoring) you recombine per query rather than a fixed RAG pipeline.

## Founders & origins
**Andre Zayarni** (CEO) and **Andrey Vasnetsov** (CTO) — Verified across company site, TechCrunch, and press. Both worked at Berlin HR-matching startup MoBerries (Zayarni as CTO/CPO, Vasnetsov as lead data scientist), where they built a neural-search candidate–vacancy matching engine; Vasnetsov taught himself Rust and started the qdrant open-source project, which they spun into a company in 2021 — Reported (consistent across German press and founder interviews). Zayarni's earlier career includes StudiVZ, Bigpoint, and technical co-founder roles; Vasnetsov was previously ML tech lead in Tinkoff's search department — Reported.

## Funding
- Pre-seed: ~€2M (IBB Ventures among investors), announced 2022 — Verified
- Seed: $7.5M led by Unusual Ventures, April 2023 — Verified
- Series A: $28M led by Spark Capital, with Unusual Ventures and 42CAP, January 2024 — Verified
- Series B: $50M led by AVP, with Bosch Ventures, Unusual Ventures, Spark Capital, and 42CAP, announced March 12, 2026 — Verified
- Total raised: ~$87.8M — Verified (multiple press sources)

## Evidence of real-world use
Strong for the category, and mostly documented rather than logo-wall. Company-published case studies with concrete detail: **Tripadvisor** uses Qdrant for its AI Trip Planner and a user-engagement graph, reporting 2–3x revenue from travelers using the AI experience; **HubSpot** picked Qdrant after a bake-off to power retrieval for its Breeze AI assistant. Series B materials name **Canva, Bazaarvoice, Roche, Bosch, OpenTable**, and agent-platform **Lyzr** in production — Reported (company/press); Bosch Ventures joining the Series B is corroborating skin-in-the-game. OSS signals (Verified via GitHub): ~29k stars, 250M+ downloads claimed across packages, active contributor community; Qdrant is a supported backend in effectively every major RAG/agent framework, which is the strongest ecosystem evidence.

## Relevance to agentic AI engineering
Qdrant sits at the retrieval/memory layer of the agent stack — the substrate under both RAG and long-term agent memory (memory products like Mem0 and Cognee can use vector stores such as Qdrant underneath). The repo's memory papers frame what gets built on top: **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** describe the gap between raw vector stores and agent-native memory that Qdrant's "agents make retrieval a tight inner loop" positioning targets. **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval** maps directly onto Qdrant's payload-filtering strength. For voice, **VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents** is exactly the tail-latency problem Qdrant's Rust/quantization story (and Edge) claims to address.

## Use cases & considerations
Use cases: (1) hybrid dense+sparse retrieval for production RAG with per-tenant filtering; (2) semantic/episodic memory store for long-running agents; (3) recommendation and discovery over user-behavior vectors (the Tripadvisor pattern); (4) on-device or air-gapped retrieval via Edge/self-hosting.

Considerations: crowded market — Pinecone, Weaviate, Milvus/Zilliz, Chroma, Turbopuffer, plus pgvector/Elasticsearch/MongoDB adding "good enough" vector search inside databases teams already run; embedding models are largely BYO (Cloud Inference is new); scaling self-hosted clusters and choosing quantization settings is real ops work; single-store licensing is permissive (Apache 2.0) so lock-in is low, but Cloud-only features create some. Open question: whether standalone vector databases remain a durable layer or get absorbed into general-purpose databases — Qdrant's composable-primitives and agent-memory bet is its answer.

## Sources
- https://qdrant.tech/ and https://qdrant.tech/about-us/
- https://github.com/qdrant/qdrant
- https://techcrunch.com/2024/01/23/qdrant-open-source-vector-database/
- https://techcrunch.com/2023/04/19/qdrant-an-open-source-vector-database-startup-wants-to-help-ai-developers-leverage-unstructured-data/
- https://qdrant.tech/blog/series-b-announcement/
- https://www.businesswire.com/news/home/20260312313902/en/Qdrant-Raises-$50-Million-Series-B-to-Define-Composable-Vector-Search-as-Core-Infrastructure-for-Production-AI
- https://siliconangle.com/2026/03/12/qdrant-raises-50m-bring-flexible-vector-search-production-ai-systems/
- https://qdrant.tech/blog/case-study-tripadvisor/
- https://qdrant.tech/blog/case-study-hubspot/
- https://www.ibbventures.de/de/news/qdrant-financing and https://www.ibbventures.de/en/news/qdrant-seed
- https://blog.vasnetsov.com/andrey_vasnetsov_cv.pdf
- https://www.future-of-computing.com/andre-zayarni-powering-generative-ai-with-qdrants-scalable-vector-database/
