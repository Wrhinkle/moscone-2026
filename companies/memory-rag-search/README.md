# Memory, RAG & Search

**Category definition:** Vector/graph databases, agent memory layers, search APIs, web crawling/scraping and web data for LLM ingestion, embeddings.

This is the category that answers one question every agent system eventually hits: **how does the model get the right context at the right moment?** An LLM without retrieval hallucinates; an agent without memory starts every session from zero. The companies here supply the substrate: stores that hold embeddings and graphs, APIs that fetch the live web, layers that turn interaction history into durable memory, and the models that produce the embeddings in the first place. It is also the most crowded and commoditization-threatened category in this repo. The shared existential question is whether these stay durable independent layers or get absorbed into general-purpose databases and frontier-model providers' built-in search and memory.

## How to read this category

Nineteen profiles, but really **four distinct layers of one stack**, bottom to top: (1) **stores**: vector/hybrid databases (Qdrant, Turbopuffer, Pinecone, Elastic, LanceDB, TopK, Hornet) and graph databases (Neo4j, FalkorDB); (2) **memory layers** built on those stores (Zep, Cognee); (3) **live-web acquisition**: proxy/scraping giants (Bright Data, Oxylabs, Apify) and agent-native ingestion/search APIs (Firecrawl, Exa, Ref); (4) **enrichment primitives**: embeddings (Mixedbread) and metadata (Deasy Labs).

The three most load-bearing reads:

- **[Turbopuffer](turbopuffer.md)**: the architectural story of the moment. Object-storage-first economics, powers Cursor and Notion, ~$75–100M ARR estimates on under $1M of disclosed primary capital. Read it against [Pinecone](pinecone.md), which defined the managed-vector-DB category and is now navigating churn (Notion left *for* Turbopuffer-style economics), a CEO change, and reported sale exploration. The pair shows the commoditization question playing out inside a single rivalry.
- **[Neo4j](neo4j.md)**: the structured/symbolic side of retrieval. GraphRAG, Context Graph memory, an IPO-track incumbent betting that multi-hop explainable retrieval beats cosine similarity. It is the counterpoint to everything vector-shaped here.
- **[Bright Data](bright-data.md)**: the live-web layer at industrial scale ($300M ARR reported, litigation wins against Meta and X that define scraping law), with [Exa](exa.md) as the agent-native rethink of the same slot (own index, embeddings-first, $2.2B valuation).

The axes that differentiate the rest: **open vs. proprietary** (Qdrant/LanceDB/Cognee/Graphiti are Apache 2.0; Turbopuffer/Pinecone/Exa are closed and managed-only), **RAM-first vs. object-storage-first** economics (Qdrant/Pinecone vs. Turbopuffer/LanceDB/TopK), **vector vs. graph** memory shape (Elastic/Qdrant vs. Neo4j/FalkorDB, with Zep and Cognee betting on hybrid graph+vector), and **funding posture**: this category spans a $2.2B a16z-backed rocket (Exa), PE-owned and bootstrapped cash machines (Bright Data, Oxylabs, Apify), and sub-$10M seed companies you'd adopt mainly through their open source (Cognee, FalkorDB, Zep).

## All profiles

### Vector & hybrid search databases

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Elastic](elastic.md) | 15-year-old search engine repositioned as hybrid retrieval + agent-context layer (Agent Builder, GA 2026) | Gold | Public (NYSE: ESTC), $1.74B FY26 revenue | 3,000+ customers using its vector/AI features; BM25 + dense + sparse in one query DSL |
| [Qdrant](qdrant.md) | Open-source Rust vector DB; filterable HNSW makes metadata-scoped retrieval fast | Gold | ~$88M raised; $50M Series B (Mar 2026) | Powers Tripadvisor's AI Trip Planner and HubSpot's Breeze after a bake-off; ~29k GitHub stars |
| [Turbopuffer](turbopuffer.md) | Serverless vector + BM25 engine built on object storage, ~10x cheaper for cold, multi-tenant data | Gold | Deliberately under-raised; undisclosed Thrive seed; ~$75M ARR (est.) | Cursor runs 80M+ namespaces on it; Notion cut vector costs ~80% |
| [Pinecone](pinecone.md) | The original managed vector database, repositioning up-stack as an agent "knowledge layer" (Nexus) | Supporting | ~$138M raised, $750M valuation (2023); reported sale exploration | Defined the 2023 RAG-boom default; then flagship customer Notion churned on cost |
| [LanceDB](lancedb.md) | Embedded vector DB + the Lance columnar format: a "SQLite of vector search" on object storage | Bronze | ~$41M raised; Databricks Ventures in Series A | Midjourney, Runway, Character.AI in production; ships inside Continue.dev's codebase indexing |
| [TopK](topk.md) | Serverless object-storage-native search DB: vector + BM25 + filters in one query, Postgres wire-compatible | Bronze | ~$5.5M seed (2025) | Claims 17ms p99 on 10M docs; no named customers yet, the earliest-stage store here |
| [Hornet.dev](hornet-dev.md) | Pre-launch retrieval engine designed for agents as the querying user, from the core Vespa/Yahoo team | Supporting | Funding undisclosed; Norwegian holding structure suggests investment | Founders ran web-scale search for billions at Yahoo; the product is entirely unproven, so evaluate it before adopting |

### Graph databases

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Neo4j](neo4j.md) | Dominant property-graph DB, now the knowledge-graph/GraphRAG and agent-memory incumbent | Platinum | ~$530M+ raised, $2B valuation; IPO prep reported | 84 of the Fortune 100 reported as customers; >$200M ARR; Cypher 25 unifies vector + graph queries |
| [FalkorDB](falkordb.md) | Low-latency graph DB (RedisGraph's continuation) via GraphBLAS sparse matrices; multi-tenant agent memory | Bronze | ~$3M seed | Securin case study: 7-hop agent queries, 1.5s → 0.3s; official backend for Zep's Graphiti |

### Agent memory layers

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Zep AI](zep-ai.md) | Temporal knowledge-graph memory as a service: facts get invalidated, not deleted, with full provenance | Supporting | ~$2.3M raised (YC W24); the traction lives in its open source rather than its war chest | Graphiti at 28.4k GitHub stars; vendor paper claims 94.8% on Deep Memory Retrieval |
| [Cognee](cognee.md) | Open-source memory engine: `cognify` turns documents into hybrid graph+vector memory, `memify` keeps it evolving | Bronze | ~$9M raised; $7.5M Pebblebed seed (Feb 2026) | Microsoft's ai-agents-for-beginners course uses it as *the* agent-memory lesson; ~27k stars |

### Web data, crawling & live-web search

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Bright Data](bright-data.md) | Industrial-scale proxies, unblocking, datasets, and The Web MCP for live agent web access | Platinum | PE-owned (EMK); $300M ARR reported, no VC | Won *Meta v. Bright Data*, where discovery showed Meta was its customer; MCP claims 100M+ daily agent interactions |
| [Oxylabs](oxylabs.md) | Bright Data's arch-rival: 177M-IP proxy network, Scraper APIs, and a young AI Studio/MCP layer | Gold | Bootstrapped, zero VC; acquires instead (Webshare, ScrapingBee) | A years-long patent war with Bright Data, the kind of sustained legal attention a market leader reserves for its closest competitor |
| [Apify](apify.md) | Marketplace of ~48,000 ready-made scrapers ("Actors") exposed to agents via MCP with runtime tool discovery | Gold | ~$3.5M total raised; profitable ($7.5M rev 2023) | Two-sided marketplace where top scraper devs earn $10k+/mo; Crawlee at ~24k stars; Intercom's Fin ingests via Apify |
| [Firecrawl](firecrawl.md) | Any website → clean LLM-ready markdown/JSON; the default scraping MCP server for coding agents | Silver | $16.2M raised (Nexus-led Series A), lean next to Exa's $357M | ~145k GitHub stars, among the most-starred AI-infra repos anywhere; Zapier and Replit in production |
| [Exa](exa.md) | Search engine built from scratch for AI agents: own crawl + embeddings index, Websets structured entity search | Gold | ~$357M raised; $2.2B valuation (a16z Series C, May 2026) | Cursor, Cognition, HubSpot as customers; monday.com cites 2.7M CRM enrichments via Websets |
| [Ref](ref.md) | MCP server giving coding agents token-efficient, deduplicated documentation search | Silver | Founders/funding not found in public sources (Unverified) | Screens fetched docs for prompt-injection payloads before returning them to the agent |

### Embeddings & metadata enrichment

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Mixedbread Inc.](mixedbread-inc.md) | Open embedding/reranker lab (mxbai-embed-large) grown into a hosted multimodal search API | Supporting | ~$6.4M raised | ~5.45M monthly HF downloads + 12.2M Ollama pulls make it a default local-embedding choice |
| [Deasy Labs](deasy-labs.md) | LLM-driven metadata auto-tagging for unstructured data so RAG can retrieve by filter instead of leaning on cosine similarity alone | Gold | ~$2.9M seed, then acquired by Collibra (Jul 2025) | The category's first exit, now "Unstructured by Collibra"; may exhibit under either brand |

**Expected-but-missing check:** every company on the expected list (Bright Data, Neo4j, Apify, Deasy Labs, Elastic, Exa, Oxylabs, Qdrant, Turbopuffer, Firecrawl, Cognee, FalkorDB, LanceDB, TOPK, Hornet.dev, Mixedbread, Pinecone, Zep AI) has a profile in this folder; none is missing. One profile is present beyond the expected list: **Ref** (ref.md), a docs-search MCP server that fits the search-API side of the category definition.

## Related papers

The [`papers/memory-research-agents/`](../../papers/memory-research-agents/) area is effectively this category's research syllabus; tool-use/governance and voice papers supply the integration and latency constraints.

**Agent memory (the store + memory-layer companies):**
- [Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md): frames the gap between raw vector stores (Qdrant, Pinecone, Turbopuffer) and true agent memory (Zep, Cognee) that nearly every profile here cites.
- [Are We Ready For An Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): the build-vs-buy question this whole category is a commercial answer to.
- [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](../../papers/memory-research-agents/graph-based-agent-memory-taxonomy-techniques-and-applicat.md): the architecture class Neo4j, FalkorDB, Zep/Graphiti, and Cognee productize.
- [GAM: Hierarchical Graph-based Agentic Memory for LLM Agents](../../papers/memory-research-agents/gam-hierarchical-graph-based-agentic-memory-for-llm-agents.md): companion to the above.
- [Towards Autonomous Memory Agents](../../papers/memory-research-agents/towards-autonomous-memory-agents.md): maps to Cognee's `memify` self-maintaining memory loop.
- [Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents](../../papers/memory-research-agents/hierarchical-long-term-semantic-memory-for-linkedin-s-ai-age.md): the in-house alternative to buying Zep/Cognee; per-tenant economics connect to Turbopuffer's namespace model.

**Agentic search and retrieval (the web-data + search-API companies):**
- [Agentic Search in the Wild: Intents and Trajectory Characteristics of Autonomous Web-Search Agents](../../papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md): agent-issued queries differ from human ones, which is the founding premise of Exa and Hornet and the traffic Bright Data/Oxylabs MCP tools serve.
- [Deep Researcher Agent: An Autonomous Framework for 24/7 Deep Research](../../papers/memory-research-agents/deep-researcher-agent-an-autonomous-framework-for-24-7-deep.md): the pattern Exa's Research API commercializes, with Firecrawl/Bright Data/Oxylabs competing as the fetch backend.
- [Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md): Deasy Labs is a company-sized bet that the answer is yes; also maps to Qdrant's payload filtering, Firecrawl's Extract, and Exa's Websets.

**Tool use & governance (how retrieval plugs into agents, and what can go wrong):**
- [The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): the MCP tool-tier designs of Bright Data, Apify (runtime Actor discovery), Exa, and Elastic Agent Builder are live instances.
- [CaMeLs Can Use Computers Too: System-Level Security for Computer-Use Agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md): scraped/searched web content entering an agent's context is a prompt-injection surface; this applies verbatim to every web-data vendor here (Ref is notable for screening for it).
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md): least-privilege scoping for agents writing arbitrary Cypher (Neo4j, FalkorDB) or pulling arbitrary tools (Apify); Deasy's PII gating and Zep's ABAC/audit are governance applied at the data layer.
- [AI Planning Framework for LLM-Based Web Agents](../../papers/tool-use-governance/ai-planning-framework-for-llm-based-web-agents.md) and [WebXSkill: Skill Learning for Autonomous Web Agents](../../papers/tool-use-governance/webxskill-skill-learning-for-autonomous-web-agents.md): the browser/unblocked-page environment Bright Data, Oxylabs, and Apify sell is what these papers assume exists.

**Latency constraint:**
- [VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents](../../papers/voice-realtime/voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md): the tail-latency budget behind Qdrant's Rust/quantization story, Turbopuffer's cache warm-up caveat, Pinecone's Dedicated Read Nodes, Exa's 180ms fast mode, and Mixedbread's sub-200ms claim.

## Open questions this category hasn't answered

1. **Does the standalone vector database survive?** Postgres (pgvector), Elasticsearch, MongoDB, and AWS S3 Vectors all now ship "good enough" vector search inside infrastructure teams already run. Pinecone's churn and reported sale exploration suggest the raw layer is commoditizing; Qdrant (composable primitives), Turbopuffer (object-storage economics), and Pinecone itself (Nexus) are each betting on a different escape route up-stack.
2. **Does model-provider-native search kill the retrieval APIs?** OpenAI, Anthropic, and Google all ship built-in web search. Exa, Firecrawl, Bright Data, and Oxylabs are betting that agent-first indexes, unblocking-at-scale, and structured extraction stay defensible; nobody knows yet.
3. **Graph vs. vector for agent memory:** does GraphRAG/temporal-KG quality (Neo4j, Zep, Cognee, FalkorDB) justify its LLM-driven construction cost over summarize-and-embed on a cheap store, outside fact-heavy domains? Nearly all supporting benchmarks are vendor-authored.
4. **Do standalone memory layers survive** as LangChain/LlamaIndex and the model providers absorb memory natively? Zep and Cognee's Apache-2.0 cores hedge against that outcome without settling it.
5. **Benchmark trust deficit:** virtually every performance claim in this category (Exa's FRAMES numbers, Elastic's 7x-vs-Qdrant, Cognee's memory evals, TopK's recall, Mixedbread's BrowseComp-Plus) is self-published. There is no neutral, agent-workload retrieval benchmark the industry accepts.
6. **The injection surface is unpriced:** every live-web vendor here pipes untrusted content into agent contexts, and only Ref's profile documents active prompt-injection screening. Who owns sanitization (the data vendor, the framework, or the model) is unresolved.
