# Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents

- **Status:** Located — published as "Hierarchical Long-Term Semantic Memory for LinkedIn's Hiring Agent" ([arXiv:2604.26197](https://arxiv.org/abs/2604.26197))
- **Area:** memory-research-agents
- **Authors / venue / date:** Zhentao Xu, Shangjin Zhang, Emir Poyraz, Yvonne Li, Ye Jin, Xie Lu, Xiaoyang Gu, Karthik Ramgopal, Praveen Kumar Bodigutla, Xiaofeng Wang — KDD 2026 Applied Data Science track; arXiv v1 April 29, 2026 (v3 May 30, 2026)

## Problem
Production agents need long-term memory over noisy longitudinal behavioral data, but industrial deployment adds constraints academic memory papers skip: scalability, low-latency retrieval, hard privacy boundaries between tenants, adaptability as data changes, and observability. Flat RAG and graph-memory approaches either leak across tenants or blow up indexing cost.

## Approach
HLTM builds a **schema-aligned memory tree whose topology mirrors business ownership**, not semantic clusters: leaf = hiring project, middle = recruiter seat, root = org account. Each node stores a multi-view representation — (1) facet key-value pairs, (2) 5–10 self-contained QA pairs, (3) a paragraph + one-line summary — extracted by LLM agents at ingestion, then aggregated bottom-up (parents merge children's memories, dedupe, reconcile conflicts). Retrieval is identity-scoped: hard-filtered to the subtree the querying user owns, then ranked by three parallel retrievers (facet micro-queries, QA embedding match, summary cosine similarity), with top-k fused into LLM context.

## Key findings
- Answer correctness on 1,341 LinkedIn Hiring Assistant queries: **0.892 vs 0.833** for best baseline (HippoRAG), p < 10⁻⁷.
- Retrieval F1: **0.782 vs 0.617** for best baseline (ReadAgent); Cliff's δ = +0.328.
- LongMemEval-s (500 queries): **0.778 vs 0.716** (A-Mem), winning all six question types.
- Privacy: **0.0% query-wise and entity-wise leakage** vs 30–92% leakage in baselines — the ownership-tree scoping does this structurally.
- Latency: ~3.0s (summary) / ~3.5s (retrieval) queries; incremental indexing cut from ~7 days full rebuild to ~12 hours; ~50% token reduction vs graph-based baselines (~3.9–4.3k tokens/query).
- Ablation: removing tree aggregation drops summary correctness 4 points and retrieval F1 16 points.
- Fully deployed in LinkedIn's Hiring Assistant. Baselines spanned RAG, full-context, GraphRAG, HippoRAG, RAPTOR, A-Mem, SimpleMem, Mem0, ReadAgent.

## Limitations & open questions
No explicit limitations section. Evaluated on one domain (hiring) with a naturally tree-shaped ownership structure — unclear how it transfers when access patterns are graphs, not trees (matrixed orgs, shared documents). Multi-view extraction is LLM-heavy at ingestion; cost isn't fully characterized. Cross-entity reasoning and multimodal signals are explicitly deferred to future work.

## Why builders should care
Memory hierarchy should follow **who owns the data**, not what the embeddings cluster to — you get tenant isolation for free (0% leakage) and GDPR-clean deletion. Precompute multiple views (facets, QAs, summaries) at ingestion and aggregate bottom-up; that trades offline compute for 3-second online retrieval and halved token spend. If you're building a multi-tenant agent, structural scoping beats post-hoc filtering.

## Related companies in this landscape
- **LinkedIn** (supporting partner) — the paper's own production system; Hiring Assistant is the deployment vehicle.
- **Zep AI** — agent memory platform; HLTM validates the long-term-memory-as-a-layer thesis while challenging flat temporal-graph designs on tenant isolation.
- **Cognee** — memory/knowledge-graph pipelines for agents; the schema-aligned-tree result is directly comparable prior art.
- **Neo4j / FalkorDB** — graph memory backends; HLTM beat GraphRAG/HippoRAG-style graph baselines on both quality and token cost, a challenge to pure graph-RAG pitches.
- **Qdrant, Pinecone, LanceDB, Turbopuffer** — vector stores power the QA/summary embedding views, but the paper shows raw vector RAG alone underperforms hierarchical multi-view retrieval.
- **LlamaIndex / LangChain** — RAPTOR-style hierarchical indexing ships in these frameworks; HLTM's twist (ownership topology + multi-view nodes) is an implementable upgrade.

## Sources
- https://arxiv.org/abs/2604.26197
- https://arxiv.org/html/2604.26197v2
