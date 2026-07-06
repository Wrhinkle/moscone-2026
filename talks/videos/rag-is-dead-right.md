# RAG is dead, right??

> Argues that retrieval never died, it just went agentic: hybrid, tool-rich search is replacing one-shot vector lookup.

- **Speaker:** Kuba Rogut, Turbopuffer
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=UM6sFg_jdlE) (AI Engineer channel; ~11m, released 2026-06-09)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Kuba Rogut, a deployed engineer at Turbopuffer, takes on the wave of "RAG is dead" posts that spread across X in late 2025 and early 2026. His counterevidence is Google search volume for the topic, which plateaued through 2024 and then hit a new inflection point mid-2025. Retrieval interest is rising, he argues; what is dying is a narrow definition of it.

Rogut first separates the terms. What Twitter calls RAG is usually one-shot vector search: embed a corpus, fetch nearest neighbors, stuff the context window. Turbopuffer's view is that retrieval spans vector search, full text search with BM25, grep, glob, regex, and plain filters. What people call agentic search, meanwhile, is usually just filesystem grep in the style of Claude Code or Codex. Rogut's preferred definition is broader: giving an agent a set of tools to progressively and iteratively find and reason over context, reading a file, deciding it is not enough, and searching again until the task can proceed.

The core case study is Cursor, one of Turbopuffer's first customers. When you open a codebase, Cursor parses, chunks, and embeds it for semantic search. Because a 100-engineer team mostly opens the same few repos, Cursor uses Merkle trees to detect similarity between codebases across the team, copies over existing index data, and re-embeds only changed files, with Turbopuffer handling the storage securely. Rogut cites Cursor's published numbers for why this effort pays: roughly a 12.5 to 13.5 percent average increase in answer accuracy across models on Cursor's internal context benchmark, and nearly 24 percent for their pre-Composer-2 model. An online A/B test showed about 2.6 percent better code retention in large codebases and a 2.2 percent drop in dissatisfied requests. He notes those percentages look small only because most queries never invoke the semantic search tool.

The contrast is Claude Code, which dropped its local vector DB early on, per Boris Cherny, and rediscovers a codebase by grep-read-assess loops every session. Rogut frames embeddings as cached compute: ten agents across ten developers asking how metadata filtering works will each burn about 6,000 tokens repeating the same discovery, while an indexed codebase pays the parsing and embedding cost once and answers the same question at runtime with a lightweight query. He says several Claude Code users at Turbopuffer have switched to Cursor for the speed this brings, especially with Composer 2.

The conclusion is that one-shot vector RAG worked in 2023 and early 2024, but Turbopuffer's sophisticated customers now run many retrieval calls per task, mixing semantic and full text search and fetching only what each step needs. Rogut closes with a Jeff Dean quote on long context: you do not need a trillion tokens at once, you need the right million, which is why staged retrieval matters even as context windows grow.

## Notable moments

- [0:01:07](https://www.youtube.com/watch?v=UM6sFg_jdlE&t=67s) Google search volume for RAG hits a new inflection point in mid-2025, contradicting the death notices.
- [0:03:08](https://www.youtube.com/watch?v=UM6sFg_jdlE&t=188s) How Cursor indexes codebases with Merkle trees so teams share index work and only changed files get re-embedded.
- [0:06:09](https://www.youtube.com/watch?v=UM6sFg_jdlE&t=369s) Embeddings as cached compute: the Claude Code grep loop versus the Cursor indexed trace, side by side.
- [0:09:11](https://www.youtube.com/watch?v=UM6sFg_jdlE&t=551s) Jeff Dean's line that you don't need a trillion tokens at once, you need the right million.

## Connections

- [Turbopuffer](../../companies/memory-rag-search/turbopuffer.md): Rogut's employer; the object-storage search database underneath Cursor's semantic index.
- [Pinecone](../../companies/memory-rag-search/pinecone.md): competing vector database facing the same shift from one-shot RAG to agentic retrieval.
- [Session recaps](../../notes/session-recaps.md): Stephen Chin's GraphRAG session made a parallel argument that retrieval has to move beyond plain vector similarity.
