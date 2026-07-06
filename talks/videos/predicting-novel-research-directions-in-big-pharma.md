# Predicting Novel Research Directions in Big Pharma

> Cognee's founder describes a hypothesis-generation system built with Bayer that uses a graph memory layer to point drug-discovery scientists at promising research areas.

- **Speaker:** Vasilije Markovic, cognee
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=M7-KY0W-BPo) (AI Engineer channel; ~3m, released 2026-06-22)
- **Program:** Online Track 2026

## Summary

Markovic presents a project cognee built with Bayer: an agentic system for hypothesis generation in drug discovery. Bayer's team wanted to build on the corpus of research it already holds and predict where its scientists should focus next. Markovic stresses that this is more than a search problem. The team needed to know in which areas hypothesis generation and scientific discovery should continue and in which areas it should stop, which meant cognee had to learn the biomedical domain alongside Bayer, iterate, and validate before making predictions.

The scale argument is concrete. Markovic asks the audience to imagine reading 10,000 scientific papers, which is the kind of corpus the system ingests so that researchers do not browse it by hand. The architecture combines formal traditional ontologies with LLM-generated knowledge to structure that corpus, then layers cognee's memory system on top so Bayer's agents can query it. Predictions come from deep graph embeddings that surface interesting relationships and candidate research areas.

Markovic spends the middle of the talk on validation, which he calls the breakthrough of the project. The system is built to be fully explainable. The team validated on a synthetic dataset, cross-validated on real datasets, ran ingested, generated, and shuffled data cross-validation, and added cross-domain validation on top. He says the results were significant and that cognee and Bayer are co-authoring a paper, with a poster due out within days of the recording.

The business framing closes the talk. The system reduces the human time a team of researchers would spend browsing papers, automating parts of entity extraction and memory consolidation in a way Bayer's teams can run and iterate on themselves. Markovic says cognee has turned the engagement into a repeatable motion: the know-how for predicting relationship-level signals with deep graph embeddings transfers to other customers, and pieces of the work flowed back into cognee's open source project.

## Notable moments

- [0:00:03](https://www.youtube.com/watch?v=M7-KY0W-BPo&t=3s) The brief from Bayer: too much data, and a need for a memory system that locates promising research areas for agentic workflows.
- [0:01:03](https://www.youtube.com/watch?v=M7-KY0W-BPo&t=63s) The 10,000-paper framing and the ontology-plus-LLM knowledge structuring approach.
- [0:02:03](https://www.youtube.com/watch?v=M7-KY0W-BPo&t=123s) Validation methodology and the forthcoming joint paper with Bayer.

## Connections

- [Cognee](../../companies/memory-rag-search/cognee.md), the speaker's company; the profile covers the graph-plus-vector memory architecture this project runs on.
- [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](../../papers/memory-research-agents/graph-based-agent-memory-taxonomy-techniques-and-applicat.md) surveys the architecture class behind cognee's memory layer.
- [Session recaps](../../notes/session-recaps.md) include an in-person GraphRAG session that names Cognee among the tools for multi-hop queries beyond vector similarity.
