# Benchmarking semantic code retrieval on Claude Code

> Turbopuffer bolts a vector search tool onto Claude Code and measures on ContextBench whether semantic retrieval beats the agent's default grep behavior.

- **Speaker:** Kuba Rogut, Turbopuffer
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=zKk7sDMGDEQ) (AI Engineer channel; ~16m, released 2026-06-03)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Rogut starts from a known tension. Claude Code ships without semantic code search; Boris Cherny, its creator, has said early versions used a local vector DB but plain agentic grep worked better and simpler. Meanwhile Cursor, one of Turbopuffer's first customers, indexes codebases into Turbopuffer and publishes real gains from it: a 24% relative improvement in answer accuracy with its Composer model, roughly 12 to 13% across all models, and an online A/B test showing a 2.6% increase in code retention in large codebases and a 2.2% drop in dissatisfied requests. Rogut's framing for why this works is that embeddings are cached compute. Grep-style agentic search re-spends thousands of tokens rediscovering the same code structure in every session and every agent, while an index pays the chunk-embed-index cost once and lets later queries hit the cached semantic meaning.

To test whether Claude Code benefits, Turbopuffer built Turbogrep, a CLI that walks the file system, parses and chunks code with tree-sitter, embeds it with Voyage's code model (voyage-code-3), and uploads to Turbopuffer, exposed to Claude Code as a search tool. Evaluation uses ContextBench, a human-labeled benchmark that scores process rather than outcome: for each task, did the agent read the specific golden files, lines, and symbols needed to solve it. He runs three conditions across 50 tasks: stock Claude Code, Claude Code with reads windowed to 50 lines, and windowed reads plus the Turbopuffer search tool.

Precision moves the most. Baseline Claude Code hits about 65% file precision, which Rogut translates as one in every three file reads being wasted; windowed grep gets to one in five, and adding semantic search reaches about 87% file precision, one wasted read in eight. Recall is murkier. Stock Claude Code actually wins file recall because it reads everything it can, but its line recall drops sharply since much of that exploration lands in files without golden lines. Splitting the 50 tasks by winner shows the tools are complementary rather than one dominating: semantic search wins on behavior-adjacent code that shares no keywords, such as finding all the ORM handling spread across libraries, while grep wins on import-tracing tasks where the right keyword appears in the first tool call or two.

His honest caveat is that the numbers trail Cursor's because Claude Code is built and tuned for grepping. A bolted-on tool with a note saying you should probably use this sometimes cannot match a harness like Cursor's Composer that natively knows when and how to call retrieval. In Q&A he adds that semantic search performs best on well-commented code, since inline documentation gives the embedding model meaning to index, and notes Cursor is thought to generate synthetic comments before embedding. His closing claim is that long-term winners will provide lightweight tools for finding the right context in different ways, shrinking billion-token file systems into the right million.

## Notable moments

- [0:01:07](https://www.youtube.com/watch?v=zKk7sDMGDEQ&t=67s) Cursor's published numbers: 24% relative accuracy gain with Composer and the A/B retention results
- [0:06:07](https://www.youtube.com/watch?v=zKk7sDMGDEQ&t=367s) Precision results: 65% baseline file precision rising to about 87% with windowed grep plus semantic search
- [0:08:08](https://www.youtube.com/watch?v=zKk7sDMGDEQ&t=488s) Task-level breakdown showing where semantic search wins and where grep wins
- [0:11:09](https://www.youtube.com/watch?v=zKk7sDMGDEQ&t=669s) Q&A definition of the stack: vector search over Voyage code-3 embeddings in Turbopuffer

## Connections

- [Turbopuffer](../../companies/memory-rag-search/turbopuffer.md): the speaker's company; the talk is a first-party benchmark of its database as a coding-agent tool
- [Qdrant](../../companies/memory-rag-search/qdrant.md): competing vector database making its own case for agent retrieval workloads
- [Session recaps](../../notes/session-recaps.md): Stephen Chin's in-person session argued the limits of vector similarity from the GraphRAG side, a useful counterpoint
