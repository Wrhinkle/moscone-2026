# Neo4j

> The dominant native graph database, now repositioning as the knowledge-graph and memory layer for GraphRAG and agentic AI systems.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** platinum
- **Founded:** 2007, Malmö, Sweden (as Neo Technology; the graph engine dates to ~2000–2003) — Verified. HQ now San Mateo, CA.
- **Website / GitHub:** https://neo4j.com — https://github.com/neo4j (core DB), https://github.com/neo4j/mcp, https://github.com/neo4j-contrib/mcp-neo4j

## What they do
Neo4j is a property-graph database: data is stored as nodes and relationships with properties, queried in Cypher (their declarative graph query language, now standardized alongside ISO GQL). Unlike a relational join or a vector lookup, multi-hop traversals ("who approved the invoice for the sub who worked the job connected to this claim") are index-free adjacency walks, so deep relationship queries stay fast. You integrate it as a server (self-hosted Community/Enterprise editions) or via **Aura**, the managed cloud service, with official drivers for Python, JS, Java, Go, and .NET.

The AI-era product line is what earns the platinum booth. Neo4j added native vector indexes so one database serves both semantic (embedding) search and symbolic graph traversal; **Cypher 25** (2025) exposes both in a single query surface. The **neo4j-graphrag** Python package ships retrievers (VectorRetriever, VectorCypherRetriever, Text2Cypher) plus knowledge-graph construction from unstructured documents. In 2025–2026 they layered on explicit agent-infrastructure products: AI memory / "Context Graph" capabilities positioning Neo4j as persistent structured memory for agents, **Aura Agent** (low-code environment for deploying multi-hop agents over a knowledge graph), **Aura Graph Analytics** (serverless, zero-ETL graph algorithms over any data source, May 2025), and official **MCP servers** (github.com/neo4j/mcp and the neo4j-contrib Labs servers) that let Claude, Cursor, or any MCP client inspect schema, run Cypher, and call GraphRAG retrievers as tools.

## Founders & origins
Emil Eifrem (CEO), Johan Svensson (CTO), and Peter Neubauer — Verified across Wikipedia, company sources, and press. Origin story (Reported, told consistently by Eifrem): the graph model was sketched on a napkin on a flight around 2000 while wrestling with relational-database mismatch at Swedish startup Windh; the engine was built in-house, open-sourced in 2007, and the company formed around it.

## Funding
Verified rounds: Series A $10.6M (Fidelity Growth Partners Europe, 2011); Series B $11M (Sunstone, 2012); Series C $20M (Creandum, Dawn Capital, 2015); Series D $36M (Greenbridge, 2016); Series E $80M (One Peak, Morgan Stanley Expansion Capital, 2018); Series F $325M led by Eurazeo and GV at a $2B+ valuation (June 2021) — at the time the largest funding round ever for a database company. A further $50M from Noteus Partners at the reaffirmed $2B valuation (late 2024) — Reported. Total raised: roughly $530M+ (Tracxn lists $581M; figures vary by source). Reported: >$200M ARR (company press release, late 2024), IPO preparations for Nasdaq underway per Bloomberg; secondary-market pricing suggests ~$1.5B — no IPO as of 2026-07-02.

## Evidence of real-world use
Unusually strong for this category — this is 15+ years of production deployment, not launch-week logos. Reported by company/press: 84 of the Fortune 100 and over half the Fortune 500 use Neo4j, including Adobe, Walmart, UBS, Citi, Uber, and Daimler Truck; PayPal (a fellow AIEWF platinum sponsor) uses it in real-time fraud detection; NASA credited Neo4j on Project Orion for mining Apollo-era lessons-learned data (Verified, 2017). Community signals: the core database has been open source since 2007 with a large GitHub presence, GraphAcademy courses (including a dedicated Neo4j MCP tools course), the NODES developer conference, and first-party integrations maintained in LangChain and LlamaIndex. Microsoft Agent Framework v1.0 (April 2026) ships Neo4j as a supported agent-memory provider alongside Mem0 and Redis — Reported, strong third-party validation.

## Relevance to agentic AI engineering
Neo4j sits at the memory/retrieval layer of the agent stack, on the "structured/symbolic" side of the RAG spectrum: GraphRAG for multi-hop, explainable retrieval where pure vector search fails, and durable graph-shaped memory for long-running agents. This maps directly onto this repo's agent-memory papers: **Graph-based Agent Memory: Taxonomy, Techniques, and Applications** and **GAM: Hierarchical Graph-based Agentic Memory for LLM Agents** describe exactly the architecture Neo4j is productizing; **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation**, **Towards Autonomous Memory Agents**, and **Are We Ready For An Agent-Native Memory System?** frame the open questions its AI-memory/Context Graph products claim to answer; **Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents** is an industrial proof-point for the same pattern. On the tool-use side, its MCP servers make the database an agent tool (cf. **The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration**), and Text2Cypher raises the governance questions in **Governance by Construction for Generalist Agents** — an agent writing arbitrary Cypher needs least-privilege scoping.

## Use cases & considerations
Use cases: (1) GraphRAG over entity-heavy corpora — contracts, claims, org/project data — where answers require joins across documents; (2) persistent agent memory (entities, episodes, relationships) instead of a flat vector store; (3) fraud/risk-style relationship analytics feeding agent decisions; (4) exposing an existing enterprise knowledge graph to coding/ops agents via MCP.

Considerations: knowledge-graph construction and schema design are real ongoing engineering cost — the "autonomous KG construction" pitch is young; Cypher skill is a hiring dependency; Aura pricing scales with instance size, and Enterprise self-hosted licensing is expensive; Community Edition (GPLv3) lacks clustering. Competitors: FalkorDB (AIEWF bronze sponsor), Memgraph, TigerGraph, AWS Neptune, Microsoft Cosmos DB (Gremlin), and — for the memory use case specifically — Zep/Graphiti, Mem0, and Cognee (also AIEWF sponsors). Open questions: whether GraphRAG's quality edge justifies its build cost versus improving long-context retrieval, and how the delayed IPO / softened secondary valuation affects roadmap pace.

## Sources
- https://en.wikipedia.org/wiki/Neo4j
- https://neo4j.com/news/in-conversation-with-emil-eifrem-founder-and-ceo-neo4j/
- https://tracxn.com/d/companies/neo4j/__nPBGtpp2oSzyOKZjZabZI40RgEha3i3AC51z6fAxZS4
- https://neo4j.com/press-releases/neo4j-revenue-milestone-2024/
- https://forgeglobal.com/insights/neo4j-upcoming-ipo-news/
- https://arcticstartup.com/neo4j-raises-50m/
- https://neo4j.com/blog/genai/what-is-graphrag/
- https://neo4j.com/blog/news/2025-ai-scalability/
- https://neo4j.com/press-releases/aura-graph-analytics/
- https://neo4j.com/blog/developer/building-an-ai-agent-with-memory-microsoft-agent-framework-neo4j/
- https://neo4j.com/blog/developer/neo4j-graphrag-retrievers-as-mcp-server/
- https://github.com/neo4j/mcp
- https://github.com/neo4j-contrib/mcp-neo4j
- https://neo4j.com/customer-stories/
- https://aws.amazon.com/blogs/apn/when-to-use-a-graph-database-like-neo4j-on-aws/
