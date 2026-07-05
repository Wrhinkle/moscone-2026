# Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval

- **Status:** Located — [arXiv:2605.28787](https://arxiv.org/abs/2605.28787)
- **Area:** memory-research-agents
- **Authors / venue / date:** Shiyu Chen, Tarfah Alrashed, Alon Halevy, Natasha Noy — arXiv (cs.IR, cs.AI), submitted 2026-05-27

## Problem
LLM agents are increasingly asked to find *data* — not answers — on the open web. The question: can an agent reliably retrieve actionable, machine-readable datasets from raw web search alone, or does it still need the structured semantic metadata layer (schema.org markup) that dataset registries publish? This is the "does RAG-over-everything obsolete curation?" question, tested empirically.

## Approach
Two agents built on the same stack (Agent Development Kit, Gemini 2.5 Pro, temperature 0), differing only in corpus: a **Baseline Agent** over Google Search (billions of pages) vs. a **Semantic Agent** over Google Dataset Search (90M schema.org-annotated dataset records). Evaluated on 58 keyword queries from the NTCIR-16 Data Search benchmark using an LLM-as-judge framework mapped to FAIR principles: relevance (Findable), a six-level accessibility rubric (Accessible), and page-type classification (Interoperable/Reusable). ~31% of pages the scraper couldn't process went to human review (Kappa 0.70–0.95; autorater alignment 0.73–0.78).

## Key findings
- **FAIR-compliance precision:** Semantic Agent 46.4% (52/112) vs. Baseline 28.0% (46/164) — 65.7% relative improvement.
- **Machine-readable data on retrieved pages:** 71.4% vs. 48.7% (46.6% relative gain).
- **Data-registry precision:** Semantic Agent hit DATA_REGISTRY pages 88.4% of the time (44.9% improvement); 86.6% fewer narrative pages, zero discovery portals.
- **Coverage trade-off:** Baseline answered 56/58 queries vs. 40/58 — 40% more coverage, but with "Last-Mile Utility" failures: 20.1% prose-heavy pages, 8.5% portal landing pages that name the topic but yield no downloadable data.
- **Relevance was a wash:** ~60.4% vs. ~60.7% highly relevant — the metadata advantage is in *actionability*, not topical matching.

## Limitations & open questions
Authors concede: single-corpus dependence on Google Dataset Search, proprietary black-box ranking on both sides, 31% of pages unevaluable by automated scraping, and only 58 English keyword queries. A skeptic would add: results may reflect Dataset Search's curation quality rather than schema.org per se, and stronger browsing agents (multi-hop navigation to the download link) might close the last-mile gap.

## Why builders should care
An agent's retrieval corpus matters more than its model: same LLM, same framework, 65.7% precision swing. If your agent must *act on* retrieved data (download, parse, compute), route it to structured/annotated sources first and fall back to open web only for coverage. Publishing machine-readable metadata on your own data is now agent-UX, not just SEO.

## Related companies in this landscape
- **Exa** — agentic search engine; this paper quantifies exactly the precision-vs-coverage trade-off Exa's structured retrieval pitch rests on.
- **Deasy Labs** — sells metadata generation for unstructured data; the paper is direct validation that metadata quality drives agent retrieval precision.
- **Bright Data / Apify / Oxylabs / Firecrawl** — web crawling for LLM ingestion; the 31%-unscrapeable and "last-mile" failures are the problem they monetize.
- **Neo4j / Cognee / FalkorDB** — graph/knowledge-graph memory vendors; supports the thesis that structured semantics beat raw text for agent-grade retrieval.
- **Qdrant / Turbopuffer / LanceDB / Pinecone** — vector DBs; challenged slightly: pure semantic similarity gave no relevance edge — actionability metadata did.
- **LlamaIndex** — retrieval routing across structured and unstructured sources is the paper's practical prescription.

## Sources
- https://arxiv.org/abs/2605.28787
- https://arxiv.org/html/2605.28787
