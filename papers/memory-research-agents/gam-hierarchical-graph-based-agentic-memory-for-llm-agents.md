# GAM: Hierarchical Graph-based Agentic Memory for LLM Agents

- **Status:** Located — [arXiv:2604.12285](https://arxiv.org/abs/2604.12285)
- **Area:** memory-research-agents
- **Authors / venue / date:** Zhaofen Wu, Hanrong Zhang, Fulin Lin, Wujiang Xu, Xinran Xu, Yankai Chen, Henry Peng Zou, Shaowen Chen, Weizhi Zhang, Xue Liu, Philip S. Yu, Hongwei Wang — arXiv (cs.AI), submitted April 14, 2026

## Problem
Long-running agents face a stability–plasticity conflict: stream-based memories (append everything, summarize later) update fast but let transient chatter corrupt stored knowledge, while structured/graph memories retain knowledge robustly but adapt poorly as the conversation's narrative evolves. Most systems couple encoding and consolidation into one step, so noise gets written into long-term memory immediately.

## Approach
GAM decouples encoding from consolidation with a two-level hierarchical graph:

- **Event Progression Graph (local):** ongoing dialogue is buffered as atomic interaction units linked by temporal/causal edges — cheap, append-only writes.
- **Topic Associative Network (global):** abstract theme nodes with LLM-scored semantic edges; the local graph is consolidated into it only when a **semantic-shift detector** fires (LLM-judged topic boundary, session end, pause, or 2048-token buffer overflow).
- **Graph-guided multi-factor retrieval:** top-down traversal from themes to episodes, re-weighted by temporal (β=1.4), speaker-role (β=1.4), and self-consistency confidence (β=1.2) signals.

Backbones: Llama-3.2-3B, Qwen2.5-7B/14B, GPT-4o-mini — no fine-tuning; MiniLM embeddings plus a cross-encoder re-ranker.

## Key findings
- **LoCoMo (Qwen2.5-7B):** GAM 40.00 avg F1 vs Mem0 35.38, MemoryOS 28.86, A-Mem 24.20 (~13% over the strongest baseline).
- **LongDialQA:** GAM 12.55 F1 vs Mem0 10.27, MemoryOS 6.76 (~22% over Mem0) — note the low absolute scores; the benchmark is far from solved.
- **Efficiency:** lowest token cost at 1,370 tokens/query (Mem0 1,534, A-Mem 4,221); latency 0.80s vs Mem0's 0.51s (GAM trades a bit of latency for accuracy; MemoryOS is 154s).
- **Ablations:** removing the Event Progression Graph costs −37.4% F1 — the biggest hit; removing state-based switching −18.6%; the topic network −12.3%; multi-factor retrieval −10.2%.

## Limitations & open questions
Authors concede text-only scope (no multimodal nodes). A skeptic would add: gains shown mostly on small open models (does the margin survive frontier backbones?); consolidation depends on an LLM topic-boundary judge whose failure modes are unquantified; retrieval weights (β values) look hand-tuned per benchmark; LoCoMo is dialogue QA, not tool-using agent workloads.

## Why builders should care
The ablation is the actionable result: a cheap, ordered short-term buffer that consolidates into structured memory only at topic boundaries beats both write-through graph memory and pure streams — and cuts tokens. If you're building agent memory, don't write to the knowledge graph on every turn; batch at detected semantic shifts, and add temporal/role/confidence re-weighting to retrieval.

## Related companies in this landscape
- **Zep AI** — temporal knowledge-graph agent memory; GAM validates the graph approach but challenges write-per-turn consolidation timing.
- **Neo4j / FalkorDB** — graph databases positioning for graph RAG and agent memory; this is direct evidence for their workload.
- **Cognee** — memory-graph pipelines for agents; GAM's hierarchy (episode vs. topic layers) is a design pattern to borrow.
- **LangChain / LlamaIndex** — ship memory abstractions; multi-factor (time/role/confidence) retrieval is a concrete upgrade path over plain vector recall.
- **Qdrant / Turbopuffer / LanceDB / Pinecone** — pure vector memory is the baseline GAM beats; pressure toward hybrid graph+vector retrieval.

## Sources
- https://arxiv.org/abs/2604.12285
- https://arxiv.org/html/2604.12285v1
