# Elastic

> The company behind Elasticsearch — a 15-year-old search engine now repositioned as the hybrid retrieval, vector-database, and agent-context layer for enterprise AI.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2012, Amsterdam, Netherlands (Elasticsearch OSS first released Feb 2010; company distributed, now NYSE-listed) — Verified
- **Website / GitHub:** https://www.elastic.co — https://github.com/elastic/elasticsearch

## What they do
Elasticsearch is a distributed search and analytics engine built on Apache Lucene: JSON documents in, inverted-index (BM25) plus doc-value analytics out, scaled horizontally across shards, queried over a REST API. Kibana is the visualization/console layer. Around this core Elastic sells three product lines — Search, Observability (logs/metrics/APM), and Security (SIEM/endpoint) — self-managed or on **Elastic Cloud** (AWS/GCP/Azure, plus a "Serverless" tier).

The AI-relevant story is that Elasticsearch quietly became a serious vector database. It ships HNSW ANN indexes, **BBQ/DiskBBQ** quantization (company benchmarks claim up to 7x higher throughput than Qdrant at comparable recall on network-attached storage — Reported, vendor-run), a first-party sparse embedding model (**ELSER**) that gives semantic retrieval without picking an embedding model, and hybrid ranking (RRF combining BM25 + dense + sparse) in one query DSL. For agents specifically, **Agent Builder** went GA in 2026: a framework inside Elasticsearch for building context-driven agents whose tools are queries over your indices, with MCP support so external agents (Claude, Cursor, etc.) can use an Elastic deployment as a tool. Practically, what you'd buy/integrate: a single store that does lexical + vector + filterable-metadata retrieval with document-level security — the retrieval half of a RAG or agent-memory system — rather than a dedicated vector DB plus a separate keyword engine.

Licensing history matters for adopters: Apache 2.0 until 2021, then SSPL/Elastic License (triggering AWS's OpenSearch fork), then AGPLv3 added in August 2024, making Elasticsearch open source again — Verified.

## Founders & origins
Shay Banon, Steven Schuurman, Uri Boness, and Simon Willnauer — Verified (Wikipedia, press). Origin story (Verified, widely documented): Banon wrote a recipe-search app for his wife (a Le Cordon Bleu student) in 2004, which became the Compass library, rewritten as Elasticsearch in 2010. Company formed 2012 to commercialize it. Banon served as CEO twice; since January 2022, Ash Kulkarni (ex-CPO) is CEO and Banon returned to CTO — Verified.

## Funding
Verified: $10M Series A (Benchmark, Index Ventures, late 2012); $70M Series C led by NEA (June 2014), bringing pre-IPO total to ~$104M (a Series B from Index sits between; per-round amount not confirmed in sources used). IPO on NYSE as **ESTC**, October 2018, valuing the company around $5B — Verified. Now a public company: FY2026 (ended April 2026) revenue **$1.739B, +17% YoY** — Verified (SEC 8-K, company IR). FY27 guidance ~$1.985–2.0B — Reported.

## Evidence of real-world use
Among the strongest in this category — this is decades-scale production infrastructure, not launch-week logos. Named customers with documented use: **Booking.com** (security/fraud, Elastic case study), **Uber** (marketplace real-time data, 1,000+ QPS, presented at Elastic{ON}), **Cisco**, **Slack** — Verified/Reported via case studies and talks. Commercial scale: 1,720+ customers above $100K ACV, 240+ above $1M, and 3,000+ customers using its AI/vector features per the FY26 Q3 report — Reported (company figures). Third-party validation for the AI positioning: Elasticsearch is a recommended vector database in **NVIDIA's Enterprise AI Factory validated design**, and Microsoft published a customer case study using the Elasticsearch vector-store connector in Semantic Kernel / Agent Framework — both Verified. Elastic also dogfoods: its public support assistant runs RAG over 300K+ docs with ELSER, and internal "ElasticGPT" is documented. Community: elasticsearch GitHub repo is one of the most-starred Java projects (~70K+ stars); a $20K Agent Builder hackathon ran Jan–Feb 2026.

## Relevance to agentic AI engineering
Elastic sits at the retrieval/memory layer of the agent stack, on the "unstructured + hybrid" side (contrast Neo4j's graph-shaped memory, same category). Its pitch maps onto this repo's agent-memory literature — **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** frame exactly the question Agent Builder answers with "your search index is the memory"; unlike graph-memory systems (**GAM**, **Graph-based Agent Memory: Taxonomy, Techniques, and Applications**), Elastic bets on hybrid retrieval over episodic stores rather than explicit entity graphs. Agent Builder's tools-as-queries model is a concrete instance of the patterns in **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**, and its document-level security answers part of the least-privilege concern raised in **Governance by Construction for Generalist Agents**. Its Observability line is also where many teams will end up storing agent traces/logs.

## Use cases & considerations
Use cases: (1) hybrid RAG over large enterprise corpora where BM25 + vectors beats vectors alone; (2) agent memory/context store with per-document RBAC; (3) exposing existing Elastic data (logs, tickets, product catalogs) to agents via Agent Builder/MCP without a new datastore; (4) observability backend for agent telemetry.

Considerations: operational heaviness — cluster sizing, shard management, and JVM tuning are real costs versus managed vector DBs; Elastic Cloud pricing scales with hot storage and can surprise; AGPL is open source but copyleft, which some legal teams treat cautiously; Agent Builder is new (GA 2026) and unproven versus framework-native memory (Mem0, Zep, LangGraph stores). Competitors: OpenSearch (the AWS fork), Pinecone, Qdrant, Weaviate, Vespa, MongoDB Atlas Search, pgvector, Algolia. Open question: whether "AI customer count" growth converts into agents built *on* Elastic rather than Elastic being just one retriever behind them.

## Sources
- https://en.wikipedia.org/wiki/Elasticsearch
- https://en.wikipedia.org/wiki/Elastic_NV
- https://www.elastic.co/about/leadership
- https://www.elastic.co/blog/shay-banon-to-re-assume-the-role-of-cto-ash-kulkarni-promoted-to-ceo
- https://www.devclass.com/databases/2024/09/02/elasticsearch-will-be-open-source-again-as-cto-declares-changed-landscape/1618331
- https://www.sec.gov/Archives/edgar/data/0001707753/000170775326000008/a26q4erex991.htm
- https://ir.elastic.co/News--Events/news/news-details/2026/Elastic-Reports-Fourth-Quarter-and-Fiscal-2026-Financial-Results/default.aspx
- https://seekingalpha.com/news/4558542-elastic-raises-fy-2026-revenue-guidance-to-1_736b-as-ai-customer-count-tops-3000
- https://www.elastic.co/docs/explore-analyze/ai-features/elastic-agent-builder
- https://www.elastic.co/search-labs/blog/agent-builder-elastic-ga
- https://elasticsearch.devpost.com/
- https://www.elastic.co/customers/booking
- https://www.elastic.co/elasticon/conf/2017/sf/powering-uber-marketplace-real-time-data-needs-with-elasticsearch
- https://www.elastic.co/blog/elasticsearch-vector-database-nvidia-enterprise-ai-factory-validated-design
- https://devblogs.microsoft.com/agent-framework/customer-case-study-how-to-use-elasticsearch-vector-store-connector-for-microsoft-semantic-kernel-for-ai-agent-development/
- https://www.zenml.io/llmops-database/building-a-production-rag-based-customer-support-assistant-with-elasticsearch
- https://www.indexventures.com/perspectives/elastic-the-evolution-of-open-source/
