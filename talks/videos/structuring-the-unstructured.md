# Structuring the Unstructured
> Cedric Clyburn demos Docling, an open-source local tool that turns PDFs, tables, and images into LLM-ready markdown, JSON, and Pydantic structures.

- **Speaker:** Cedric Clyburn, Red Hat
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=-x5GEVnkuRw) (AI Engineer channel; ~21m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Cedric Clyburn, an open-source engineer at Red Hat, makes the case that context is the most important input to any AI application, yet most enterprise data sits in unstructured formats an LLM cannot use: PDFs, presentations, contracts, technical docs, meeting notes, scanned documents, diagrams, tables, and images. His goal for the session is to show how to extract structure from raw documents and feed it into downstream RAG and agent systems, using Docling, an open-source tool under the Linux Foundation. He cites Jensen Huang's keynote framing that unstructured data is becoming the new context layer, and notes the practical problem that PDFs are scattered across dozens of systems and that proprietary solutions often require sending private data to someone else's server.

Clyburn grounds the stakes with a viral example: about 20 scientific papers now cite a nonsensical term that never existed, because an AI misread an old scanned PDF and merged two words from adjacent columns, then researchers propagated it. His point is that processing accuracy determines whether an answer is correct. He compares three approaches to a PDF containing a table, an image, and captioned sections. A simple PDF parser is fast and cheap on CPU but truncates and merges text, flattens the table linearly, and drops the image content entirely. A frontier model produces good markdown but is expensive, around 30 dollars per million output tokens, and non-deterministic, so it is risky at the scale of thousands of PDFs. Docling is his middle ground: a fast, cheap, local CLI and library, installable with `pip install docling`, that converts inputs to markdown, JSON, and a Pydantic document type using a pipeline of OCR, layout analysis, and vision models. He cites a Hugging Face use case from Leandro where Docling cleaned common-crawl PDFs into the FinePDFs training export at roughly 50x cost savings versus naive VLM and OCR, done on CPU without a GPU.

The live demos build up capability. Docling converts an eight-page PDF (its own research paper) to markdown while preserving layout, exposes the result as a Pydantic type so you can inspect pages, extracts eight tables into data frames, and pulls images with captions and embedded text. A layout visualizer draws bounding boxes over section headers, text, and figures, useful for stripping personally identifiable information before extraction. Vision language models, run locally through Ollama with a Granite model, enrich images with detailed descriptions. Structured output pulls specific fields like an invoice's bill number and total into a Pydantic schema. Clyburn then shows "chunkless" or agentic RAG using Docling: instead of a vector database, the retrieval index is the document's markdown outline, and an LLM iterates in a loop to pick the relevant section and pull its full text, demonstrated on a small doc and on IBM's 2025 annual report with 418 sections. For scale he shows Docling Serve as a REST microservice deployable via containers or Kubernetes, and a Docling MCP server exposing conversion, generation, and manipulation tools to agents like Claude Code, Cursor, or Codex. His closing pitch is that everything runs locally, no GPU required, fast, cheap, and open-source.

## Notable moments
- [0:03:00](https://www.youtube.com/watch?v=-x5GEVnkuRw&t=180s) The invented scientific term that spread through 20 papers because a scanned PDF merged two columns.
- [0:07:04](https://www.youtube.com/watch?v=-x5GEVnkuRw&t=424s) The Hugging Face FinePDFs case showing roughly 50x cost savings using Docling on CPU.
- [0:13:04](https://www.youtube.com/watch?v=-x5GEVnkuRw&t=784s) Enriching document images with a local Granite vision model through Ollama.
- [0:14:05](https://www.youtube.com/watch?v=-x5GEVnkuRw&t=845s) Chunkless agentic RAG where the markdown outline is the entire retrieval index.

## Connections
- [Red Hat](../../companies/cloud-compute/red-hat.md) is the speaker's employer and the source of the Granite models used in the vision demos.
- [Reducto](../../companies/back-office-automation/reducto.md) is a document-parsing vendor solving the same PDF-to-structure problem from a proprietary angle.
- [Session recaps](../../notes/session-recaps.md) note the in-person invoice and tax extraction pipelines that overlap with this document-processing topic.
