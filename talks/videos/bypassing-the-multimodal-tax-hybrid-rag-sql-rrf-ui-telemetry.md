# Bypassing the Multimodal Tax: Hybrid RAG, SQL RRF & UI Telemetry
> A framework-free, fully local RAG stack: Docling-to-markdown ingestion, four chunking strategies, hybrid BM25-plus-vector retrieval in Postgres, and guardrails written as Python code instead of prompts.

- **Speaker:** Abed Matini, Ogilvy
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Akm1sqvWG4A) (AI Engineer channel; ~46m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Matini, a senior backend developer at Ogilvy, demos an HR FAQ chatbot built without any paid framework and walks through every layer live. His two starting problems: dragging a PDF into a chat UI burns tokens before a single question is asked, and production chatbots accumulate too many tools to manage. His answer is to do the heavy document work locally on CPU before the LLM ever sees a query. The stack is Python and FastAPI, React, PostgreSQL with vectors, Docker, Ollama running small local models, and Langfuse for telemetry; the whole codebase runs from one command in GitHub Codespaces, no GPU required.

Ingestion converts raw PDFs, Word files, PowerPoint, and images to markdown with Docling, then chunks into Postgres. Matini spends a long section on why chunking strategy decides answer quality. Uploading a whole 28-page handbook produces meaningless chunks (signature lines, acknowledgements) that slow retrieval and increase hallucination. He demos four strategies from his admin dashboard: heading-based chunking, which pairs each heading with its answer and gives clean, traceable references, ideal for FAQ content authored as question-and-answer; paragraph chunking; fixed 512-character chunks with 64-character overlap for messy unstructured data; and sentence-based grouping. A practical touch: a screenshot of a maintenance email can be dropped in, OCRed to text, chunked by sentence group, and immediately answerable ("is there any maintenance plan for this weekend?") with the screenshot as the cited reference.

Retrieval is hybrid on purpose. Vector search with cosine distance finds semantically near chunks, but Matini argues product names, SKUs, medication names, and numbers need exact keyword matching, so BM25 runs alongside and the results are fused into a ranked top-k. He keeps the window at top two for FAQ use and explains tuning it by domain: retrieve more for product catalogs so items are not permanently buried, retrieve less for medical content where liability demands precision.

A distinctive position in the talk: his "agents" are plain Python functions, not LLM calls. Running locally on Ollama, he cannot afford three or four agent loops adding 20 to 30 seconds. Anything a function can do (current date, product lookups) is done in code, which is testable and cannot hallucinate. The same logic drives his guardrails: medical escalation, off-topic rejection, and prompt injection filtering all happen in code with intent regexes, term dictionaries, and an LLM classifier before anything reaches the model, so the system prompt stays a few sentences long and behavior is covered by a rigid test suite. He contrasts this with prompt-based instructions the model sometimes ignores.

His most quotable finding concerns model size. He started with a 7B model, found it slow and wordy, and settled on Qwen 2.5 0.5B instruct, roughly 400 MB, plus one small embedding model. If the data is vetted before it reaches the LLM, he argues, the smallest model answers well and hallucinates less, simply saying it lacks information rather than inventing it. Langfuse traces every conversation locally with model, latency, retrieved chunks, and per-session tracking, and supports cost estimation when external models are used.

## Notable moments
- [0:13:18](https://www.youtube.com/watch?v=Akm1sqvWG4A&t=798s) Live demo of heading-based chunking: each heading-plus-answer becomes a clean, referenceable chunk.
- [0:22:29](https://www.youtube.com/watch?v=Akm1sqvWG4A&t=1349s) A maintenance-email screenshot is OCRed, chunked, and answering employee questions minutes later.
- [0:37:35](https://www.youtube.com/watch?v=Akm1sqvWG4A&t=2255s) Guardrails as code: medical questions are blocked before the query ever reaches the LLM.
- [0:42:39](https://www.youtube.com/watch?v=Akm1sqvWG4A&t=2559s) The model-size finding: a 0.5B Qwen model beats bigger ones here because the data is vetted first.

## Connections
- [Elastic](../../companies/memory-rag-search/elastic.md), whose core pitch is the same hybrid keyword-plus-vector retrieval Matini hand-builds on Postgres.
- [Memory, RAG and search vendors](../../companies/memory-rag-search/README.md), the managed alternatives this framework-free local stack positions itself against.
