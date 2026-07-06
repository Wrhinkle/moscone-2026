# Semantic Blindness: 500,000 Sensors Confused an LLM

> How Phaidra made data center agents scale from 64 to 460,000 GPUs at flat token cost by letting the LLM plan while a deterministic resolver does the searching.

- **Speaker:** Raahul Singh & Van Levstik, Phaidra
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=EUsPvBeIx70) (AI Engineer channel; ~16m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Singh (staff AI research engineer) and Levstik (senior engineering manager) build agents at Phaidra that let data center operators query their AI factories in plain language: which chiller is running hot, analyze temperature distribution across data halls, are any GPUs having problems. The problem they call semantic blindness appeared when they handed an LLM 500,000 sensor names. The industry has no common naming convention, so equipment names range from readable to strings like CH3-something-6, and a 1 gigawatt facility holds 400,000-plus GPUs along with the chillers, pumps, and power meters that support them. A demo works at small scale because a model can read every name in context; at production scale the context window saturates. Singh's line: a product works for all scenarios and does not fail silently, a demo only has to work for one.

The obvious alternatives fail too. Vector embedding search collapses because 20-character names differing by one character (Chiller 6 versus Chiller 7) are nearly identical vectors, wrecking recall. Listing many near-identical names also trips LLM repetition penalties, which can shut off output mid-list. Sharding the equipment across parallel LLM calls produced horrible recall, phantom equipment that does not exist, and silently dropped equipment that does, unacceptable in mission-critical systems where misses cascade.

Their answer is to grow with tree depth instead of instance count. AI factories are hierarchical (data center, hall, aisle, row, rack, GPU; chiller plants, rooms, pumps), and the tree's depth grows very slowly while its width explodes. Four insights structure the system. First, a linearizer gives the LLM a summarized graph of paths from root to leaf rather than nodes: a million-node facility reduces to a short list of path types, so a 64 GPU system and a 460,000 GPU system produce roughly the same size summary. Second, LLMs are good at planning and bad at searching, so the planner LLM emits a structured plan (collect GPUs, scope to the data hall 11 subtree, filter to running hot) instead of sifting names. Third, a deterministic resolver executes the plan over pre-indexed subtrees using set operations, which guarantees perfect recall regardless of query fuzziness. Fourth, for vague queries the LLM emits name patterns to search for rather than reading name lists. The whole pipeline is a two or three step process instead of an open-ended agentic loop, keeping cost flat.

Levstik's production numbers: head-to-head with the same model and data over three runs per case, the old approach scored 80 percent correctness at 64 GPUs and fell to about 30 percent at 460,000, while the new system held 100 percent across all tests, including 66 cases on six real production systems with zero failures. A single validation pass at 1 gigawatt scale burned 116 million tokens under the old approach versus 390,000 tokens now, roughly 300 times fewer, and query cost stays at about 9,000 tokens whether the system has 64 or 460,000 GPUs. He frames the lesson through Karpathy's software 1.0 versus 3.0: legacy software drifts from deterministic code toward prompts, but AI-native systems should run that trend backwards, prototyping in pure 3.0 to find what is worth building, then moving everything with writable structure or rules (retrieval, set logic, counting, dedup) into 1.0 code, keeping the LLM for ambiguity, judgment, and synthesis. Every deterministic function added is firmer ground for the model to stand on.

## Notable moments

- [0:02:01](https://www.youtube.com/watch?v=EUsPvBeIx70&t=121s) Why RAG fails here: Chiller 6 and Chiller 7 embed nearly identically, and repetition penalties cut off long name lists.
- [0:05:30](https://www.youtube.com/watch?v=EUsPvBeIx70&t=330s) The tree-depth insight: path summaries stay the same size from 64 to 460,000 GPUs.
- [0:11:08](https://www.youtube.com/watch?v=EUsPvBeIx70&t=668s) Correctness results: old approach drops from 80 to 30 percent with scale; the new one holds 100 percent, zero failures on six production systems.
- [0:12:09](https://www.youtube.com/watch?v=EUsPvBeIx70&t=729s) Token accounting: 116 million tokens per validation pass becomes 390,000, and per-query cost stays flat at about 9,000 tokens.

## Connections

- [Session recaps](../../notes/session-recaps.md) includes Stephen Chin's in-person GraphRAG session, the same argument that structure beats vector similarity for retrieval.
- [Neo4j](../../companies/memory-rag-search/neo4j.md) sells graph-structured retrieval, the family of approach Phaidra's pre-indexed subtree resolver belongs to.
- [Do Agents Need Semantic Metadata?](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md) studies the adjacent question of what structured metadata agentic search actually needs.
