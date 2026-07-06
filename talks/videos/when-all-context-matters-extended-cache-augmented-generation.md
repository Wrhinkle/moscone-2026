# When All Context Matters: Extended Cache Augmented Generation

> A six minute walkthrough of retrieval options for document collections where every document is relevant and the data is replaced constantly, ending in a parallel cache-augmented design.

- **Speaker:** Luis Romero-Sevilla, Orbis
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=XovaGv4f39A) (AI Engineer channel; ~6m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Romero-Sevilla, VP of AI at Orbis, frames the talk around one specific scenario: a collection of documents describing an event, where every document in the collection is relevant to the user's questions, and the whole collection goes stale and gets replaced frequently. He walks through why the two standard retrieval patterns each fail one half of that constraint.

Plain RAG handles the churn well. Embedding documents and inserting vectors into a database is fast, so a stale collection can simply be swapped for a new one. What it cannot do is answer questions that depend on all the documents at once, since similarity search only retrieves the chunks nearest the query. GraphRAG solves the opposite problem. An LLM reads every document, extracts entities and relationships, and builds a knowledge graph the system can traverse to synthesize answers that draw across the entire collection. Romero-Sevilla calls it an excellent approach when the corpus is stable, but recomputing the graph every time the data is replaced is computationally expensive and slow, which disqualifies it for his scenario.

His observation is that GraphRAG already pushes every document through an LLM anyway, so why not just load the documents into context directly. That is cache augmented generation (CAG): use a long-context model, load the documents, and cache the computed KV state so the prefill cost is paid once. The catch he cites is quality degradation as the context window fills up. The extension that gives the talk its title is running multiple CAG instances in parallel, distributing the documents across separate context buckets, each of which can answer questions about its own contents. A smarter supervisor model interrogates the buckets and synthesizes a final answer.

The distribution detail is the most counterintuitive part. Romero-Sevilla says the tempting move is to organize buckets by domain and tell the supervisor what each category holds, but in practice, with densely interrelated documents, the supervisor ignores domains that look irrelevant at first glance. So documents are distributed in no particular order, balanced only to minimize the bucket count. The supervisor explores the buckets, builds its internal understanding progressively, and asks specific buckets follow-up questions when it finds something interesting. Because all caches load in parallel, he says knowledge building is significantly faster than GraphRAG while giving more accurate answers than simple RAG.

He closes with the honest caveats: KV cache is expensive, though cost can be managed by tuning how long each cache lives, and no retrieval strategy wins on compute, cost, and speed at once. The design is fitted to this one problem shape, not offered as a general replacement for RAG or GraphRAG.

## Notable moments

- [0:02:04](https://www.youtube.com/watch?v=XovaGv4f39A&t=124s) GraphRAG explained, and why graph recomputation rules it out for fast-changing data
- [0:03:04](https://www.youtube.com/watch?v=XovaGv4f39A&t=184s) Cache augmented generation introduced, with the context-quality degradation problem
- [0:04:05](https://www.youtube.com/watch?v=XovaGv4f39A&t=245s) Why documents are distributed across buckets in no particular order, and how the supervisor explores them

## Connections

- [Neo4j](../../companies/memory-rag-search/neo4j.md): the GraphRAG vendor whose approach this talk positions as too slow for frequently replaced data
- [Qdrant](../../companies/memory-rag-search/qdrant.md): representative of the vector database layer in the simple RAG baseline he starts from
- [Session recaps](../../notes/session-recaps.md): Stephen Chin's in-person GraphRAG session covered the same vector-similarity-versus-relationships tradeoff from the graph side
