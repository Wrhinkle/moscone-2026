# Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation

- **Status:** Located (arXiv: https://arxiv.org/abs/2603.07670) — published under the slightly different title "Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers"; the conference-notes title appears to be a minor misremembering of the same survey.
- **Area:** memory-research-agents
- **Authors / venue / date:** Pengfei Du; arXiv (cs.AI), v1 submitted 2026-03-08. No peer-reviewed venue verified.

## Problem
Agents that work fine in one session fall apart across many: context windows overflow, summaries drift, and nothing learned in task N survives to task N+1. The field has produced dozens of ad-hoc memory bolt-ons but lacked a shared vocabulary for what memory *is* in an agent loop and how to tell whether a given design actually works. Extending context to 100k+ tokens "delays the problem but cannot eliminate" it.

## Approach
A survey (2022–early 2026) that formalizes agent memory as a write–manage–read loop coupled to perception and action, plus a three-dimensional taxonomy: temporal scope, representational substrate, and control policy. It organizes systems into five mechanism families — context-resident compression (Self-Controlled Memory), retrieval-augmented stores (RAG, RETRO), reflective self-improvement (Reflexion, Generative Agents, ExpeL), hierarchical virtual context (MemGPT's OS-style paging across main context / recall DB / archival vector store), and policy-learned management (memory ops as RL-optimized tool actions). It then analyzes four benchmarks: LoCoMo, MemBench, MemoryAgentBench, MemoryArena.

## Key findings
- Models near-perfect on LoCoMo passive recall drop to **40–60% completion** on MemoryArena's interdependent multi-session tasks — recall is not the same skill as using memory to decide.
- Active-memory agents hit **>80%** on those interdependent tasks vs. **~45%** for a long-context-only baseline.
- Reflexion: **91% pass@1 on HumanEval vs. 80%** GPT-4 baseline; Voyager: **15.3× faster** Minecraft tech-tree progression.
- Removing reflection from Generative Agents degenerated behavior "within 48 simulated hours."
- Retrieval adds **200–500ms latency** per pipeline call — real cost for interactive/voice agents.
- On MemoryAgentBench, no system masters all four competencies; selective forgetting is the near-universal failure.

## Limitations & open questions
Single-author survey, not yet peer reviewed; the numbers above are collated from cited papers, not new experiments. Author-conceded open problems: episodic→semantic consolidation without losing rare critical facts, causally grounded retrieval ("what caused this?" vs. "what looks like this?"), trustworthy reflection (self-assessed beliefs entrench mistakes), learned forgetting beyond time-based expiry, and multi-agent memory governance (access control, concurrent writes). A skeptical builder would also ask whether MemoryArena's task design favors the "active memory" systems its framing celebrates.

## Why builders should care
Stop benchmarking memory with recall QA — test whether the agent *acts correctly* on information from ten sessions ago, because that's where near-perfect systems collapse to 40–60%. Budget the 200–500ms retrieval tax in latency-sensitive paths, and treat forgetting/contradiction-handling as unsolved: ship expiration and human-visible memory audits rather than trusting self-reflection.

## Related companies in this landscape
- **Zep AI** — temporal knowledge-graph agent memory; this survey is effectively the taxonomy its product competes within (retrieval-augmented + graph substrate).
- **Cognee** — agent memory layer built on knowledge graphs; validated by the survey's push beyond flat vector stores.
- **Neo4j / FalkorDB** — graph databases underpinning the "representational substrate" dimension and graph RAG.
- **Qdrant / Turbopuffer / LanceDB / Pinecone** — vector stores powering retrieval-augmented memory; the 200–500ms retrieval latency finding is their optimization target.
- **LangChain / LlamaIndex / Mastra** — frameworks shipping the write–manage–read loop as developer primitives.
- **Letta-style hierarchical designs (MemGPT lineage)** — the paper's hierarchical-virtual-context family; not a sponsor, but the pattern LangChain/Mastra memory modules copy.

## Sources
- https://arxiv.org/abs/2603.07670
- https://arxiv.org/html/2603.07670v1
