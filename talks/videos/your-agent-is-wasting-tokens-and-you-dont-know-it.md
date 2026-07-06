# Your Agent Is Wasting Tokens and You Don't Know It

> Five concrete techniques for cutting agent token costs, demonstrated with AWS Strands Agents code.

- **Speaker:** Erik Hanchett, AWS
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=uiP88SpCi1Q) (AI Engineer channel; ~6m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Erik Hanchett, a senior developer advocate at AWS, packs five token-cost reductions into a lightning talk, each illustrated with code from AWS's Strands Agents framework. He notes the techniques work with any provider; Strands is just the vehicle.

The first technique is prompt caching. Adding a `cache_prompt` setting means the full system prompt goes over the wire once, and every subsequent agent call sends a much smaller cached reference. Hanchett points out the same applies to tool prompts and messages, which agents resend constantly.

Second is routing by difficulty. Hanchett argues against using the most expensive model for everything. His example routes hard tasks to a frontier model like Claude Sonnet and simple ones to Claude Haiku, with an if statement or even a very cheap model acting as the router. The principle is to match model cost to task difficulty per call rather than picking one model for the whole agent.

Third is offloading large tool results. When a tool returns a big payload, the naive path re-injects that payload into the context on every loop of the agent. Hanchett shows a manual pattern: store the result locally or in cloud storage, put a summary in the context instead, and let the agent fetch details only when needed. Strands offers APIs that automate this, but the summarization technique works anywhere.

Fourth is capping tool loops. Hanchett says he has often watched an agent call the same tool 10 or 20 times, and an uncapped loop can go infinite, which he calls very bad for token usage. He recommends always setting a max iterations limit, and running observability tooling before deployment to see how long each tool call takes and how many times each tool loops, so inefficient calls can be fixed rather than just capped.

Fifth is trimming conversation history. In a multi-turn agent the entire history goes back to the model on every call, which Hanchett says can eat hundreds or thousands of tokens per turn. Strands ships a sliding window conversation manager that sends only the last N messages, 10 by default and configurable. The trade-off is losing the early history, and his fix is to summarize the truncated portion and place that summary in the context window instead of the raw messages.

The talk closes with the five items as a checklist: cache the system prompt and tool prompts, route by difficulty, offload big tool results, cap tool loops with observability to back it up, and trim multi-turn history with summarization. It is a practical list rather than an argument, aimed at builders who have not yet looked at where their agent's tokens actually go.

## Notable moments

- [0:00:14](https://www.youtube.com/watch?v=uiP88SpCi1Q&t=14s) Prompt caching in Strands Agents: full system prompt on the first call, cached on every call after.
- [0:01:01](https://www.youtube.com/watch?v=uiP88SpCi1Q&t=61s) Routing by difficulty, with Claude Haiku for cheap tasks and Claude Sonnet for harder ones.
- [0:02:01](https://www.youtube.com/watch?v=uiP88SpCi1Q&t=121s) Offloading large tool results to storage and summarizing them so the agent loop stops resending them.
- [0:04:03](https://www.youtube.com/watch?v=uiP88SpCi1Q&t=243s) The sliding window conversation manager, and summarizing lost history to keep long conversations cheap.

## Connections

- [AWS](../../companies/cloud-compute/aws.md): Hanchett is an AWS developer advocate and the demos use AWS Strands Agents.
- [Session recaps](../../notes/session-recaps.md): the AWS Builder Loft session on Bedrock AgentCore covers the same AWS agent stack in person.
