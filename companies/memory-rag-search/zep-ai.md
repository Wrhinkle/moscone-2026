# Zep AI

> Managed memory/context layer for AI agents: it turns chat history and business data into a temporal knowledge graph (open-source Graphiti) and hands your agent back relevant, current context in under 200ms.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, San Francisco, CA (YC W24) — Verified (YC profile, Crunchbase)
- **Website / GitHub:** https://www.getzep.com — https://github.com/getzep/graphiti (Apache 2.0)

*Disambiguation note: not Zep Inc., the Atlanta cleaning-chemicals company — some data aggregators (e.g. Extruct's "$795M revenue") conflate the two. This profile is the YC W24 agent-memory startup at getzep.com.*

## What they do
Zep is agent memory as a service. The workflow is ingest → build → assemble: you send episodes (chat messages, JSON business records, documents) via API; the engine extracts entities, relationships, and facts into a **temporal knowledge graph**; at inference time your agent calls Zep to retrieve an assembled context block instead of stuffing raw chat history into the prompt. The temporal part is the differentiator: facts carry validity windows, and when new information contradicts an old fact, the old fact is *invalidated* rather than deleted — current state stays accurate while history and provenance (every fact traces back to its source episode) are preserved. Retrieval is hybrid: semantic embeddings + BM25 keyword search + graph traversal.

The engine is **Graphiti**, their open-source Python framework (28.4k GitHub stars, 2.8k forks as of 2026-07 — Verified via GitHub). Graphiti runs against Neo4j, FalkorDB, or Amazon Neptune, supports Pydantic-defined ontologies, builds graphs incrementally without batch recomputation, and ships an MCP server so Claude and other assistants can use it directly. The commercial platform layers on what they call a "Context Lake": millions of per-user/per-tenant graphs managed as one system, with attribute-based access control, policy-driven retention, legal hold, and audit logging built in. Deployment: managed cloud, cloud + BYOK, or BYOC in your VPC; SOC 2 Type II and HIPAA BAA — Verified (company site). SDKs in Python, TypeScript, and Go.

Their arXiv paper (Zep: A Temporal Knowledge Graph Architecture for Agent Memory, arXiv:2501.13956, Jan 2025) reports beating MemGPT on the Deep Memory Retrieval benchmark (94.8% vs 93.4%) and up to 18.5% accuracy gains with ~90% latency reduction on LongMemEval — Reported (vendor-authored paper).

## Founders & origins
**Daniel Chalef**, solo founder/CEO — Verified (YC profile, Crunchbase). Engineer-turned-founder; previously at KnowledgeTree (document management) and a late-stage operator at SparkPost (email infra, acquired by MessageBird), where he led product-focused ML/engineering plus marketing and corp-dev groups — Reported (YC profile, interviews). Zep began in 2023 as an open-source LLM memory server and pivoted up-stack into the knowledge-graph platform after Graphiti took off. One aggregator lists additional "founders" (Paul, Preston) — these appear to be early team, not co-founders; public primary sources name only Chalef — Unverified.

## Funding
- Pre-seed: $500K from Y Combinator, March 2024 (W24 batch) — Verified (Crunchbase, YC)
- Total raised: ~$2.3M, with Engineering Capital and Step Function (Boston) as additional investors — Reported (Tracxn; round breakdown/dates not public)
- No Series A found in public sources as of 2026-07-02. Revenue claims ($1M in 2024, per Getlatka) — Reported, single source.

Notably under-capitalized relative to direct competitor Mem0 (~$24M raised); Zep's traction case rests on OSS adoption and enterprise features, not war chest.

## Evidence of real-world use
- **Graphiti OSS adoption is the strongest signal:** 28.4k stars, 2.8k forks, 881 commits, active releases (v0.29.2, June 2026), 250+ open issues, active Discord — Verified via GitHub. YC notes it hit 20k stars within 12 months.
- **Named customers:** Twin Health, Praktika.ai (language-tutor app), Thrive AI Health, HoneyBook, plus Samsung, AWS, and an unnamed Fortune 500 tech company — Reported (company site logo wall; independent case-study detail is thin, so treat Samsung/AWS as logos rather than documented deployments).
- **Public self-serve pricing** (free tier; Flex $125/mo; Flex Plus $375/mo; credit-based metering) = real commercial product with real usage-based economics — Verified.
- Ecosystem integrations documented by third parties: Microsoft's AutoGen docs include a Zep agent-memory notebook; MCP server for Claude — Verified.

## Relevance to agentic AI engineering
Zep sits squarely in the agent-memory layer, one level above vector stores like Qdrant/turbopuffer and adjacent to Neo4j (a Graphiti backend, also in this repo's memory-rag-search category). The repo's memory papers are almost a syllabus for Zep's design space: **Graph-based Agent Memory: Taxonomy, Techniques, and Applications** and **GAM: Hierarchical Graph-based Agentic Memory for LLM Agents** cover exactly the graph-structured-memory approach Graphiti implements; **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation** and **Are We Ready For An Agent-Native Memory System?** frame the build-vs-buy question Zep answers commercially; **Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents** is the in-house alternative pattern. The governance/audit substrate (ABAC, provenance, retention) connects to **Governance by Construction for Generalist Agents**. For latency-sensitive stacks, the sub-200ms P95 retrieval claim is the same constraint **VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents** attacks.

## Use cases & considerations
Use cases: (1) persistent user memory for consumer/health assistants across sessions (the Praktika/Twin Health pattern); (2) fusing CRM/business records with conversation history so a support or back-office agent knows current account state — directly relevant to a Ridgeline-style job-packet/AR agent that must track facts that change (claim status, sub bills); (3) self-hosted Graphiti as a free temporal-KG memory when you control the graph DB; (4) audit-friendly memory in regulated settings (HIPAA, provenance, legal hold).

Considerations: LLM-driven graph construction means ingest costs tokens and adds write latency — fine for conversational memory, worth benchmarking for high-volume ingestion; credit-based pricing (per 350-byte episode chunk) needs modeling at scale; hosted platform is proprietary lock-in, though Graphiti + your own Neo4j/FalkorDB is a real exit path; small team (~5) and thin funding are a vendor-risk factor for enterprise commitments. Competitors: Mem0, Letta (MemGPT), Cognee, LangMem, plus DIY on vector stores. Open question: whether graph-shaped memory wins over simpler summarize-and-embed approaches outside fact-heavy domains — the benchmark evidence is largely vendor-authored.

## Sources
- https://www.getzep.com/ and https://www.getzep.com/pricing
- https://www.getzep.com/product/agent-memory/
- https://github.com/getzep/graphiti
- https://www.ycombinator.com/companies/zep-ai
- https://arxiv.org/abs/2501.13956
- https://www.crunchbase.com/organization/zep-ai and https://www.crunchbase.com/funding_round/zep-ai-pre-seed--91375980
- https://tracxn.com/d/companies/zep/__poSadJnSfLWHjz05Xi3U5KwnpCMWSU3aDrihLX_8FLs
- https://microsoft.github.io/autogen/0.2/docs/ecosystem/agent-memory-with-zep/
- https://www.generational.pub/p/building-ai-products-with-zep
