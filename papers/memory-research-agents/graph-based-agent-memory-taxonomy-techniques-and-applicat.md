# Graph-based Agent Memory: Taxonomy, Techniques, and Applications

- **Status:** Located — [arXiv:2602.05665](https://arxiv.org/abs/2602.05665)
- **Area:** memory-research-agents
- **Authors / venue / date:** Chang Yang, Chuang Zhou, Yilin Xiao, et al. (18 authors, incl. Ninghao Liu, Jinsong Su, Xiao Huang); arXiv preprint, submitted 2026-02-05. Companion repo: [Awesome-GraphMemory](https://github.com/DEEP-PolyU/Awesome-GraphMemory).

## Problem
Agents on long-horizon tasks (multi-turn dialogue, game playing, scientific discovery) need memory that supports accumulation, iterative reasoning, and self-evolution — and flat vector stores don't capture relational dependencies, hierarchy, or temporal structure. The field's graph-memory work (Zep/Graphiti, Mem0, HippoRAG-style systems) is fragmented; this survey organizes it.

## Approach
A survey, not a system. Contributions: (1) a taxonomy of agent memory along three axes — short-term vs. long-term, knowledge vs. experience, non-structural vs. structural — with a graph implementation view; (2) a life-cycle analysis in four stages:

- **Extraction** — entity/relation and LLM triple extraction from text, event segmentation + timestamping from trajectories, VLM-based extraction from multimodal data.
- **Storage** — knowledge graphs (AriGraph, Mem0), hierarchical trees (MemTree, SGMEM), temporal graphs (Graphiti bi-temporal modeling, TReMu, MemoTime), hypergraphs (HyperGraphRAG), hybrids decoupling knowledge from experience (Optimus-1, KG-Agent).
- **Retrieval** — six operator families: similarity (vector top-k), rule-based filters, temporal (Zep time windows, decay functions), graph traversal (H-MEM, G-Memory), RL-based (PPO/GRPO policies), and agent-based self-planned traversal; plus multi-round and hybrid-source enhancement.
- **Evolution** — consolidation via graph merging, reorganization, and updating from environmental feedback.

It also catalogs libraries/benchmarks by scenario (interaction, personalization, web, long-context, continual) and nine application domains (conversational, code, financial, medical, game, robotics agents, etc.).

## Key findings
- Graphs earn their complexity in three cases: relational dependency modeling, hierarchical organization, efficient structured retrieval — the implicit claim is pure vector RAG underserves all three (inferred framing; the survey reports no benchmark numbers of its own).
- Temporal graph memory (bi-temporal: when a fact was true vs. when it was learned) is a distinct, maturing technique class — validating Zep/Graphiti's design.
- Retrieval is the widest design space (6 operator families); most production systems use only similarity retrieval.
- Seven open challenges: memory quality/consistency, scalability, privacy/security, dynamic schema learning, interpretability, theoretical foundations, multi-agent memory coordination.

## Limitations & open questions
As a survey it reports no head-to-head numbers, so it can't tell you whether graph memory beats a well-tuned vector store on your workload, or what the extraction cost (LLM calls per ingested document) does to unit economics. Dynamic schema learning and multi-agent memory sync are acknowledged as unsolved.

## Why builders should care
This is the current map of the graph-memory design space: if your agent only does top-k vector retrieval over chat history, you're using one of six retrieval families and no evolution stage. Steal the life-cycle framing (extract → store → retrieve → evolve) as an architecture checklist before adopting any memory vendor.

## Related companies in this landscape
- **Neo4j** (Platinum) — the graph database this whole technique class runs on; the survey is effectively its agent-era sales case.
- **FalkorDB** (Bronze) — low-latency graph DB positioned for GraphRAG/agent memory.
- **Zep AI** (Supporting) — Graphiti's bi-temporal graph memory is named as the exemplar temporal-storage technique.
- **Cognee** (Bronze) — open-source memory engine building knowledge graphs from agent data; direct implementation of the extraction/storage stages.
- **Qdrant, Pinecone, Turbopuffer, LanceDB** — vector stores the survey implicitly challenges: similarity search is one of six retrieval operators, not the whole answer.
- **LangChain / LlamaIndex** (Gold) — orchestration layers where these memory life-cycle stages get wired into agents.
- **SurrealDB** (Silver) — multi-model (graph + vector + document) DB matching the survey's hybrid-storage direction.

## Sources
- https://arxiv.org/abs/2602.05665
- https://arxiv.org/html/2602.05665v1
- https://www.themoonlight.io/en/review/graph-based-agent-memory-taxonomy-techniques-and-applications
- https://github.com/DEEP-PolyU/Awesome-GraphMemory
