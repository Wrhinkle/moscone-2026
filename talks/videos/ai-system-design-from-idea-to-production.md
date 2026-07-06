# AI System Design: From Idea to Production

> Apoorva Joshi walks a four-phase design framework end to end through a health insurance claims review system, from product requirements to production optimization.

- **Speaker:** Apoorva Joshi, MongoDB
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=T0HhO4YtTfE) (AI Engineer channel; ~29m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Joshi, a data scientist turned developer advocate at MongoDB, opens against the "just vibe code it and ship it" instinct. That works when stakes are low and you can eyeball outputs, she argues, but for anything people depend on it is dangerous, and she cites Anthropic and OpenAI speakers saying the same: specs are the new code, and the art now lives in product requirements, system design, and evaluation criteria. Her framework has four phases: product requirements, system design, evaluation and monitoring, and optimization for cost, latency, and reliability. Rather than staying abstract she applies each phase to a fictional health insurance claims review system for MDB Health.

The requirements phase starts with a quantified, solution-agnostic business problem: medical reviewers spend an average of 2 days processing claim reviews, four times the industry standard for non-urgent cases and twelve times for urgent ones. Constraints come next, patient data stays in the approved cloud, only approved-cloud models may be used, complex cases need a senior physician, and every denial needs human review, which caps the system at semi-autonomous. She positions AI's role along three dimensions (complementary versus critical, reactive versus proactive, level of autonomy) and sets one success metric: cut urgent claim processing from 2 days to 1 hour within 90 days of launch.

System design begins with data strategy. Clinical guidelines and coverage policies live as PDFs in Confluence and update annually and quarterly; patient claims history sits in MongoDB and must refresh hourly to hit the 1-hour target. Guidelines get chunked, embedded, and enriched with metadata like procedure codes, because medical terminology such as diagnosis codes slips past vector search, so she prescribes vector search with metadata pre-filtering or hybrid search, while patient history needs only PII removal and an exact-match lookup. On architecture, Joshi warns against jumping straight to an agent or letting a coding agent pick the design, which risks over-engineering. Mapping the claim flow yields a RAG component, a control flow where escalation rules are predetermined, and human in the loop, rather than a fully autonomous agent. She also designs the feedback surface up front: reviewers can override verdicts with a logged reason and flag hallucinated or irrelevant citations.

Evaluation gets split from monitoring: evaluation is before you ship, monitoring after, and you need both. Guardrails reject irrelevant inputs ("write me a poem") and treat any response lacking citations as invalid. Her metric set covers guardrail compliance (claim rejection rate, missing citation rate), response quality (faithfulness to the retrieved guidelines), one domain metric (claim processing time, the North Star), and system health (cost per recommendation). In production she adds implicit signals: the human override rate, which should stay low, and how long reviewers spend on each AI recommendation, where drift upward suggests verbose or confusing outputs.

The final phase covers the gap between "accuracy looks good" and production. For accuracy she recommends prompt engineering, reranking retrieved passages, and persisting more than patient history as memory. For cost and latency, semantic caching keyed on similar past claims and batch processing. For reliability, structured outputs so every response carries both the decision and its citations. Her closing takeaways: the product spec is the hard part now, design the simplest system that meets the need and iterate from evaluation, and build evaluation in from the start because you cannot improve what you cannot measure.

## Notable moments

- [0:01:02](https://www.youtube.com/watch?v=T0HhO4YtTfE&t=62s) "Specs are the new code": Joshi quotes Anthropic and OpenAI talks to frame the whole framework.
- [0:04:03](https://www.youtube.com/watch?v=T0HhO4YtTfE&t=243s) The quantified business problem: 2-day claim reviews, 12 times the industry standard for urgent cases.
- [0:12:12](https://www.youtube.com/watch?v=T0HhO4YtTfE&t=732s) Why not to jump straight to an agent, mapping the claim flow to RAG plus control flow plus human in the loop instead.
- [0:24:26](https://www.youtube.com/watch?v=T0HhO4YtTfE&t=1466s) Production monitoring via implicit signals: human override rate and time spent reviewing each AI verdict.

## Connections

- [Pinecone](../../companies/memory-rag-search/pinecone.md), a competing vector search vendor for the retrieval layer Joshi builds on MongoDB's own vector search.
- [Qdrant](../../companies/memory-rag-search/qdrant.md), another vector database alternative for the hybrid search plus metadata filtering pattern she recommends.
- [LangChain](../../companies/agent-orchestration/langchain.md), representative of the orchestration framework choice she flags in the stack-selection step.
