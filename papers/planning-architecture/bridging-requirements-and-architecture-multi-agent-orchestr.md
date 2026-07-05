# Bridging Requirements and Architecture: Multi-Agent Orchestration with External Knowledge and Hierarchical Memory

- **Status:** Located — arXiv: https://arxiv.org/abs/2606.01385
- **Area:** planning-architecture
- **Authors / venue / date:** Ruiyin Li, Yiran Zhang, Xiyu Zhou, Yangxiao Cai, Peng Liang, Weisong Sun, Jifeng Xuan, Zhi Jin, Yang Liu. Submitted May 31, 2026 (39 pages, journal submission).

## Problem
Turning a requirements document into a sound software architecture is still slow, architect-bottlenecked work, and teams rarely explore alternative decompositions or styles under agile time pressure. LLM agents have been applied heavily to coding and issue resolution, but the requirements-to-architecture step — the stage that determines whether downstream coding agents build the right thing — has seen little systematic agent work.

## Approach
The paper proposes MAAD (Multi-Agent Architecture Design): four specialized agents — Analyst (parses requirements), Modeler (builds "4+1" view models), Designer (synthesizes architecture documentation), Evaluator (produces structured quality assessments) — orchestrated in a revision loop. Two mechanisms distinguish it:

- **External knowledge via RAG:** a vector database of architectural standards (ISO/IEC/IEEE 42010:2022, 42020:2019) and authoritative textbooks (Bass et al., Martin, Richards & Ford), organized by architectural theme, top-3 segments retrieved per query, injected into the Modeler and Designer.
- **Hierarchical memory:** working memory (current revision round, artifacts, Evaluator feedback), episodic memory (per-task decisions, interactions, lessons learned with confidence levels), and semantic memory (generalized design principles distilled from episodes after task completion) — a closed loop that lets architecture experience compound across tasks.

## Key findings
- On 10 case studies scored with seven architecture-level metrics (coupling degree, cohesion, interface complexity, structural/state complexity, component coupling density, state-machine cyclomatic complexity), MAAD produced more complete, modular, and traceable architectures than the MetaGPT baseline. (Exact per-metric numbers were not extractable from the HTML version I fetched.)
- The Evaluator agent autonomously generates structured quality reports, which the authors report significantly reduces manual validation effort.
- Backbone model matters a lot: of GPT-5.2, Qwen 3.5 (397B MoE), DeepSeek-R1 (671B), and Llama 3.3 70B, GPT-5.2 and Qwen 3.5 led across most settings.
- Validation on 10 real-world specifications included feedback interviews with practicing architects.

## Limitations & open questions
Authors concede output quality is capped by the base LLM's reasoning capacity, and the practitioner validation involved only six architects. A skeptical builder would add: MetaGPT is a soft baseline (it wasn't designed as an architecture specialist); the structural metrics measure the models produced, not whether the resulting system would actually meet its quality attributes in production; and it's untested how the semantic-memory distillation behaves at scale (does accumulated "knowledge" drift or contaminate later tasks?). Effectiveness in novel or highly specialized domains is unexplored.

## Why builders should care
If you're building coding agents, this argues the leverage is upstream: a dedicated architecture stage with role-specialized agents, grounded in real standards via RAG, produces artifacts that downstream code agents can be held compliant to. The three-tier memory design (working/episodic/semantic with post-task distillation) is a concrete, copyable pattern for any agent that should get better across engagements rather than starting cold. And the finding that an Evaluator agent can replace much manual review suggests putting a critic-with-rubric inside every generation loop.

## Related companies in this landscape
- **Factory** — sells requirements-to-code agentic SDLC; MAAD validates inserting an explicit architecture stage between requirements and code.
- **Cognition / Qodo / Sourcegraph** — coding and code-review agents whose "plan compliance" story depends on exactly the traceable architecture artifacts MAAD produces.
- **Tessl** — spec-driven development; MAAD is the academic case that specs/architecture, not code, should be the durable artifact agents work from.
- **Zep AI / Cognee** — agent-memory vendors; MAAD's working/episodic/semantic hierarchy with post-task distillation mirrors their product architecture.
- **Qdrant / Neo4j / LlamaIndex** — the RAG-over-standards knowledge layer MAAD relies on is built from these components (vector DB, graph/knowledge store, retrieval orchestration).
- **LangChain / Orkes / Temporal** — multi-agent orchestration with revision loops is the workflow pattern these platforms operationalize.

## Sources
- https://arxiv.org/abs/2606.01385
- https://arxiv.org/html/2606.01385v1
- https://www.researchgate.net/publication/405682629_Bridging_Requirements_and_Architecture_Multi-Agent_Orchestration_with_External_Knowledge_and_Hierarchical_Memory
