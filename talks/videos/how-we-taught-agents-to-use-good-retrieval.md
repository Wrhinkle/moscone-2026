# How We Taught Agents to Use Good Retrieval

> Mixedbread on the oracle gap between LLM reasoning and retrieval quality, and the harness plus SFT-and-RL training recipe behind their search agent.

- **Speaker:** Hanna Lichtenberg & Aamir Shakir, Mixedbread
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=1IdzkRVmWAA) (AI Engineer channel; ~15m; release date not captured in our metadata)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Shakir, Mixedbread's co-founder, opens with the gap the talk is named for: model reasoning has improved exponentially while search has improved slowly for twenty years, and retrieval tools are the main access pattern reasoning has to knowledge in legal and finance work. He quantifies it with oracle performance, the ceiling a model hits when handed exactly the right documents. On BrowseComp-Plus (a fixed-corpus variant of OpenAI's browsing benchmark over 100,000 documents) the oracle is 93 percent; on OfficeQA Pro (Databricks' benchmark over a century of US treasury documents) it is 64 percent. Codex with default tools drops nine and eight points below those ceilings, so the bottleneck is access to the right documents rather than reasoning. Swapping in Mixedbread search closes the BrowseComp-Plus gap to three points for GPT-5 and nearly eliminates it on OfficeQA Pro. The diagnosis for why agents underuse semantic search is specific: they emit keyword-mash queries (his example from benchmarking is essentially gibberish) because they are trained on grep-style codebase exploration, mimic human web queries, and face benchmark bias, since suites like BEIR use entity-heavy queries that structurally favor BM25.

Lichtenberg, who leads agentic search at Mixedbread, describes the search agent they built to fix this. The harness runs on the Mixedbread platform with four tools: an overview search returning summaries of up to 50 chunks for corpus reconnaissance, a semantic search returning full payloads of the top 10 chunks, a metadata-facet filter, and grep for exact keyword matching. The loop is deliberately short, at most four search rounds, but each round can fire parallel searches. The agent starts with the user query, results from an initial semantic search, and hints about available metadata facets, then splits its intent into up to four queries covering separate aspects and picks a tool per query, with chunks deduplicated across rounds. One prompting detail does heavy lifting: instead of asking the model to write a search query, which triggers the old BM25 keyword habit, they instruct it to write one concise sentence describing what it wants to find.

Training uses a small LLM for speed: supervised fine-tuning from a larger teacher, then on-policy reinforcement learning with a composite search reward. The retrieval reward combines NDCG on the agent's final ranked list with an LLM judge scoring rubrics such as whether all chunks are relevant and the ranking plausible. The trajectory reward uses an LLM judge on query naturalness and whether exploration was sufficient. The trained agent is unreleased, but Lichtenberg reports an NDCG@10 of 0.4 on a congressional-documents benchmark (rendered as "Oblique Congress" in the captions) versus 0.18 for the best model in that benchmark's paper, a GPT multi-hop agent. The beta agent already in production is top one on Snowflake's MADQA benchmark at 93.4 percent accuracy with Gemini 3.5 Flash using their agentic search as its tool, at lower cost than comparable setups.

## Notable moments

- [0:02:02](https://www.youtube.com/watch?v=1IdzkRVmWAA&t=122s) Oracle-gap numbers: 93 and 64 percent ceilings, with Codex default tools dropping nine and eight points.
- [0:03:04](https://www.youtube.com/watch?v=1IdzkRVmWAA&t=184s) The gibberish keyword query example and the three reasons agents write queries that way.
- [0:10:08](https://www.youtube.com/watch?v=1IdzkRVmWAA&t=608s) The training recipe: SFT from a teacher, then on-policy RL with retrieval and trajectory rewards.
- [0:13:09](https://www.youtube.com/watch?v=1IdzkRVmWAA&t=789s) Results: NDCG@10 of 0.4 versus 0.18, and top spot on Snowflake's MADQA at 93.4 percent.

## Connections

- [Mixedbread Inc.](../../companies/memory-rag-search/mixedbread-inc.md): the speakers' company; this talk is the technical story behind the BrowseComp-Plus claim in the profile.
- [Exa](../../companies/memory-rag-search/exa.md): competing agent-first search vendor making the same argument that retrieval built for models beats retrieval built for humans.
- [Agentic Search in the Wild](../../papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md): paper note on autonomous agent search behavior, the query-pattern problem this talk trains against.
