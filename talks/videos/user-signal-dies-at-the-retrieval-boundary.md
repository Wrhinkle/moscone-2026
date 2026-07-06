# User Signal Dies at the Retrieval Boundary
> Why agent retrieval should be re-ranked by past task outcomes instead of embedding similarity alone, with a runtime memory layer and benchmark numbers.

- **Speaker:** Sonam Pankaj, StarlightSearch
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Jx4ZFEAq6bY) (AI Engineer channel; ~16m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Pankaj, CEO and co-founder of StarlightSearch, argues that agent pipelines fail at retrieval far more often than at generation, and that the standard ReAct loop is missing a learning step. She cites figures that 85% of AI projects fail to gain traction and that 73% of pipeline failures trace to retrieval rather than generation, and quotes a former Pinecone CTO saying the industry made wrong answers appear faster and cheaper while forgetting to make retrieval learn.

Her diagnosis is a missing layer between evals and action. Observability stacks capture every tool call, completion, and exception, and eval suites judge outputs pass or fail, but none of that signal flows back into the agent's context or skills. The eval signal dies in the dashboard, so an engineer has to sit down, read the traces, rewrite the prompt, and redeploy by hand. Existing memory products, she says, store user preferences and conversation history for chat personalization; they retrieve by embedding similarity and do not learn from outcomes.

StarlightSearch's answer is a runtime layer she calls AgentRx, the agent's runtime experience. Its core mechanism is a utility score: memories are retrieved by semantic similarity to the current task, weighted by whether each memory historically helped or hurt execution. Eval outcomes become a first-class signal in retrieval re-ranking. Pankaj also insists memory should hold reasoning rather than isolated facts. A customer support bot should not remember that the user prefers dark theme; it should remember that a refund request means checking the settlement first so the customer is not paid twice. Once roughly ten related memories accumulate, the system bakes the reasoning into a skill, which also lets stale instructions get retired. Her example is a SQL agent whose system prompt still references a dropped column; nothing in a static prompt ever removes it, but a continuously updated skill can.

On numbers, Pankaj reports tau-bench policy-following performance improving from 66% to 76% with the memory system, and to 80% once findings are baked into skills. On Humanity's Last Exam she reports a 35.7% baseline, 47.5% with RAG, 58.2% with another memory system, and 61.3% with her outcome-weighted system, with similar trends on other agentic benchmarks. She is candid about limitations: a cold start where retrieval is pure semantic search until enough reviews accumulate, utility drift among similar memories, noisy review labels contaminating the utility score, and a lambda hyperparameter governing credit assignment in re-ranking. She says the product mitigates all of these except cold start.

The demo is a product SQL agent asked to find a gaming mouse. With zero memories it fails, even though a wireless mouse exists in the database. She submits the failure through the dashboard, the system records the trajectory and the empty tool result, and on the next run the agent's tool-call trajectory changes and it finds the product. The memory that fixed it then keeps re-ranking itself as its utility score updates across future runs.

## Notable moments
- [0:02:02](https://www.youtube.com/watch?v=Jx4ZFEAq6bY&t=122s) The missing layer framing: observability has the traces, evals have the verdicts, and the agent sees neither.
- [0:06:06](https://www.youtube.com/watch?v=Jx4ZFEAq6bY&t=366s) Memory as reasoning: the refund example of what an outcome-aware memory should actually store.
- [0:09:07](https://www.youtube.com/watch?v=Jx4ZFEAq6bY&t=547s) Limitations listed openly: cold start, utility drift, noisy review labels, and the lambda hyperparameter.
- [0:13:11](https://www.youtube.com/watch?v=Jx4ZFEAq6bY&t=791s) Demo payoff: the tool-call trajectory changes after one submitted failure and the agent finds the mouse.

## Connections
- [Pinecone](../../companies/memory-rag-search/pinecone.md): Pankaj quotes a former Pinecone CTO on retrieval optimization going after the wrong target, and her utility score is a direct critique of similarity-only vector search.
- [Are We Ready for an Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): paper-side treatment of the same gap between chat personalization memory and memory that serves agent task execution.
- [Session recaps](../../notes/session-recaps.md): the Stephen Chin GraphRAG session made the parallel in-person argument that vector similarity alone is not enough for agent memory.
