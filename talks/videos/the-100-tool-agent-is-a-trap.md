# The 100-Tool Agent Is a Trap

> Benchmarks showing tool-selection accuracy collapses as tool catalogs grow, and a fix: semantic routing with just-in-time context injection.

- **Speakers:** Sohail Shaikh & Ankush Rastogi, Prosodica
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=vh2VGuQ3zhY) (AI Engineer channel; ~28m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Sohail Shaikh, a data scientist at Prosodica, and Ankush Rastogi, a senior data solutions engineer there, split this talk between routing behavior and production engineering. Their target is what they call the fat agent: giving a model every tool definition, name, description, and JSON schema on every request. It works in a demo with 10 tools. Their headline numbers show what happens after: a 741-tool catalog consumes about 127,000 tokens of prompt before the user's question is even considered, and tool selection accuracy falls from roughly 78 percent at 10 tools to about 40 percent at 100 and 13.6 percent at 741, roughly one correct call in eight. Shaikh attributes the collapse partly to the lost-in-the-middle problem: hundreds of schemas packed into mid-context get weak attention, so you pay for a huge prompt that makes the decision harder. Latency degrades too; past 500 tools, time to first token can exceed 5 seconds.

Their fix is semantic routing, which Shaikh summarizes as RAG for tools. Each tool description is embedded offline into a vector index. At runtime the user query is embedded with the same model, a nearest-neighbor search returns the top K tools, usually three to five, and only those schemas are injected into the model call. In their benchmarks the routed agent holds above 83 percent accuracy across the same catalog sizes, because from the model's view it always chooses from a handful of tools no matter how large the real catalog is, and time to first token stays nearly flat. The token math: three to five routed schemas run about 1,000 tokens against 127,000 for the full catalog, roughly a 99 percent reduction in tool context, which compounds at 100,000 requests a day.

Rastogi frames just-in-time context injection as the general principle: instead of loading everything before the query is understood, wait until the query is known and inject only what that request needs, the same idea as lazy loading and JIT compilation. He cites Anthropic's write-up on on-demand tool loading through MCP, which reported token usage dropping from 150,000 to 2,000, a 98.7 percent reduction, as external confirmation, along with the MCP-Zero project routing across thousands of tools.

The methodology and practice sections are unusually concrete for a talk like this. They evaluated on the Berkeley Function Calling Leaderboard, skills-bench-style scenarios, and synthetic tool pools scaled from 10 to 1,041 tools, running identical queries in fat and routed modes with the same model and answer key, sweeping K at 3, 5, and 10; K=5 is their recommended default. The implementation checklist covers cataloging tools with owners and versions, building the index with Chroma, Pinecone, or Qdrant, wiring the agent loop so the tool list comes from the router rather than a hard-coded catalog, and logging every selection so misses can be traced to weak descriptions. They are equally clear about limits: under 20 tools a router is unnecessary, and routing pays off past roughly 50 tools in production. Known risks include router misses (widen K or run a second retrieval pass), weak tool descriptions producing weak embeddings, and rare tools that never score high until their descriptions use the language users actually use.

## Notable moments

- [0:03:05](https://www.youtube.com/watch?v=vh2VGuQ3zhY&t=185s) The 741-tool catalog that costs 127,000 tokens before the user's question arrives.
- [0:04:06](https://www.youtube.com/watch?v=vh2VGuQ3zhY&t=246s) The accuracy collapse curve: 78 percent at 10 tools, 40 percent at 100, 13.6 percent at 741, versus the router holding above 83 percent.
- [0:12:16](https://www.youtube.com/watch?v=vh2VGuQ3zhY&t=736s) Anthropic's on-demand MCP tool loading as external validation: 150k tokens down to 2k.
- [0:20:22](https://www.youtube.com/watch?v=vh2VGuQ3zhY&t=1222s) The six-step production checklist, from cataloging tools to re-embedding when descriptions change.

## Connections

- [Pinecone](../../companies/memory-rag-search/pinecone.md): one of the vector stores the speakers recommend for the tool-description index.
- [Qdrant](../../companies/memory-rag-search/qdrant.md): the other named vector store option for running the semantic router locally before moving to managed infrastructure.
- [The evolution of tool use in LLM agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): research survey of the tool-calling progression this talk's routing pattern belongs to.
