# Pinecone

> The original fully managed vector database — closed-source, serverless similarity search as an API, now repositioning as a "knowledge layer" for agents while navigating a brutally commoditized market.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** supporting
- **Founded:** 2019, New York, NY (Israeli-founded; offices in NYC, SF, Tel Aviv) — Verified
- **Website / GitHub:** https://www.pinecone.io — https://github.com/pinecone-io (clients/examples only; core DB is proprietary)

## What they do
Pinecone is a proprietary, fully managed vector database: you upsert embeddings with metadata into namespaced indexes and query by approximate nearest neighbor over REST/gRPC or Python/TS/Java/Go clients. There is nothing to self-host — that's the product. The 2024 serverless re-architecture (second generation rolled out in 2025) separates storage from compute, priced per read/write/storage rather than per provisioned pod, which is what made the Gong-scale "billions of vectors" workloads economically viable.

The surface has expanded well beyond raw ANN: **integrated inference** (hosted embedding + reranking models so you skip a separate embedding pipeline), **hybrid retrieval** (dense + sparse indexes with "cascading retrieval" and reranking), **full-text search** (public preview), **Pinecone Assistant** (a managed RAG/knowledge API — upload documents, get grounded chat completions with citations), **Dedicated Read Nodes** (public preview Dec 2025, predictable latency/cost for read-heavy workloads), and BYOC deployment. A 2026 launch week added **Nexus** (a "knowledge engine for agents," public preview) and **KnowQL** in early access — Reported (company announcements; too new to judge). Pinecone ships first-party MCP servers for the DB and Assistant, and it's a supported backend in LangChain, LlamaIndex, and essentially every agent framework. New Builder tier is $20/month flat (2026), between the free Starter and usage-based Standard/Enterprise — Verified (pricing page).

## Founders & origins
**Edo Liberty**, sole founder — Verified. PhD in computer science (Yale), previously research scientist/director at Yahoo, then Director of Research at AWS heading Amazon AI Labs, where he worked on SageMaker; he left AWS in April 2019 to build managed vector search before "vector database" was a category — Verified across company bio, press, and interviews. In **September 2025 Liberty moved to Chief Scientist and named Ash Ashutosh (three-time infrastructure founder: Serano, AppIQ, Actifio; ex-Greylock, ex-HP storage CTO, most recently at Google) as CEO** — Verified (company newsroom, VentureBeat, TechTarget).

## Funding
- Seed: $10M led by Wing Venture Capital, announced January 2021 — Verified
- Series A: $28M led by Menlo Ventures, March 2022 — Verified
- Series B: $100M led by Andreessen Horowitz at a $750M valuation, with ICONIQ Growth, Menlo, Wing — April 2023 — Verified (TechCrunch, company)
- Total raised: ~$138M — Verified. No round since 2023 found in public sources.
- Context that matters: The Information reported (Aug 2025) that Pinecone hired bankers to explore strategic options including a sale, with Oracle, IBM, MongoDB, and Snowflake floated as buyers; new CEO Ashutosh publicly said acquisition is not the goal — Reported. No transaction as of 2026-07-02.

## Evidence of real-world use
Real but mixed. **Gong** is the strongest documented case study: Pinecone serverless powers Smart Trackers over billions of embeddings with a claimed 10x cost reduction — Reported (company case study with technical detail). Site claims **9,000+ customers** and names ZoomInfo, Vanguard, TaskUs, DISCO, Aquant, Chipper Cash, CustomGPT.ai among case studies — Reported. The counter-signal is loud: flagship customer **Notion migrated off Pinecone** (churn reportedly cost-driven), which precipitated the sale exploration coverage — Reported (The Information, Calcalist). Pinecone was the default vector store of the 2023 RAG boom and remains one of the most-integrated backends across frameworks; the open question is retention as pgvector, Elasticsearch, MongoDB, and Turbopuffer undercut it.

## Relevance to agentic AI engineering
Pinecone is a candidate substrate for the agent memory layer — the raw store under episodic/semantic memory systems. The repo's memory papers frame the gap it's trying to close with Assistant and Nexus: **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** both argue plain vector stores are necessary-but-insufficient for agent memory — Nexus is Pinecone's explicit answer. Its metadata filtering and hybrid retrieval map onto **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval**; serverless tail latency is exactly the constraint in **VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents** (serverless cold reads are a real consideration there — Dedicated Read Nodes exist partly for this).

## Use cases & considerations
Use cases: (1) zero-ops production RAG when you don't want to run retrieval infrastructure; (2) Assistant as a shortcut to grounded Q&A over documents without building a pipeline; (3) billion-scale semantic search with usage-based cost (the Gong pattern); (4) agent long-term memory store via frameworks or MCP.

Considerations: fully proprietary and hosted-only — highest lock-in in the category (contrast Qdrant/Weaviate/Milvus, all OSS); usage-based pricing is hard to predict and cost was reportedly why Notion left; corporate uncertainty (sale exploration, CEO change) is a real vendor-risk factor for multi-year bets; competitors include Qdrant, Weaviate, Zilliz/Milvus, Chroma, Turbopuffer, and "good enough" vector search inside Postgres/Elastic/Mongo you may already run. Open question: whether Nexus/Assistant successfully move Pinecone up-stack before the raw vector layer fully commoditizes.

## Sources
- https://www.pinecone.io/ and https://www.pinecone.io/customers/
- https://www.pinecone.io/newsroom/next-chapter/
- https://venturebeat.com/data-infrastructure/pinecone-founder-edo-liberty-appoints-googler-ash-as-ceo
- https://techcrunch.com/2023/04/27/pinecone-drops-100m-investment-on-750m-valuation-as-vector-database-demand-grows/
- https://www.pinecone.io/newsroom/pinecone-raises-usd100m-in-series-b-funding-to-provide-long-term-memory-for-ai/
- https://www.pinecone.io/customers/gong/
- https://www.theinformation.com/articles/top-funded-ai-database-startup-pinecone-considers-sale
- https://www.calcalistech.com/ctechnews/article/rz31q82b5
- https://www.techtarget.com/searchdatamanagement/news/366631366/Vector-database-vendor-Pinecone-eyes-future-under-new-CEO
- https://www.infoq.com/news/2025/12/pinecone-drn-vector-workloads/
- https://www.runtime.news/pinecones-new-serverless-architecture-hopes-to-make-the-vector-database-more-versatile/
- https://research.contrary.com/company/pinecone
