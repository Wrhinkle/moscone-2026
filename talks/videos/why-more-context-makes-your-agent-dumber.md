# Why More Context Makes Your Agent Dumber and What to Do About It

> Qodo's Nupur Sharma catalogs the ways agents fail as context grows and lays out the context-optimization and multi-agent patterns Qodo uses in its code review product.

- **Speaker:** Nupur Sharma, Qodo
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=EcqMYoIV57A) (AI Engineer channel; ~26m, released 2026-06-08)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Sharma comes to agents from DevSecOps, where pipelines either run or crash, and frames the talk as lessons from watching non-deterministic agents fail. She traces the evolution from static 4K-context prompts, where humans picked what the model saw, to tool-using agent loops that never know when to stop searching, to multi-agent setups where agents clash over conflicting interpretations. Her core claim: bigger context windows do not make agents smarter. Models attend to the start and end of a prompt and purge the middle, a U-curve where instructions like "I have Jira, I have MCPs, look into those" get dropped. Qodo sees this directly because it benchmarks whether the context it feeds an agent actually shows up in the result.

The answer she proposes is strategic context optimization instead of dumping everything on the model. She compares four approaches by cost and payoff. A context engine acts like a bouncer with search and ranking logic, but indexing slows down and gets unpredictable at 600 to 700 repositories. Hierarchical summarization keeps per-file and per-folder summaries agents can skim, at the price of heavy LLM processing on every file change. Knowledge graphs work well for logical dependencies that span repositories but demand a lot of upfront developer effort. For teams building agents for their own processes rather than a product, she recommends iterative retrieval, a library-card style index that lets agents drill into code on demand with low developer input, optionally paired with a critic node that checks results against the original goal and triggers retries.

Sharma then names a failure she calls the orchestration paradox: strong reasoning models spend their tokens researching how to solve a problem, hopping between methods instead of solving it. Qodo's counter is an 80/20 hybrid. High-reasoning models get 80 percent of the task, the free-flowing discovery, planning, and tool selection. The remaining 20 percent, validation and summarization, runs as deterministic hard gates on cheaper models that do not need to research anything. Runaway loops in the 80 percent get capped by retry counters (work with the last result after four or five attempts) or timeouts (take the last decision after 5 minutes).

The last failure mode is the do-everything agent: give one agent four tasks and it silently drops two. Qodo's production architecture instead uses a mixture of specialized agents. A context collector gathers PR context from the codebase, tools, and the context engine, then routes only the relevant slice to each expert agent (security, code diffs, Jira). A judge agent merges their findings and re-checks them against the PR context, filtering perhaps 15 raw recommendations down to what matters. In Q&A Sharma says the agents communicate through LangChain, with an intermediate agent that collects results and writes a refined prompt for the next agent. Calibration comes from indexed PR history and acceptance feedback: suggestions developers accept gain weight, ones the reviewer ignores ten times lose it, and explicit rules always surface regardless.

## Notable moments

- [0:02:16](https://www.youtube.com/watch?v=EcqMYoIV57A&t=136s) The U-curve claim: models keep the start and end of context and purge the middle.
- [0:08:21](https://www.youtube.com/watch?v=EcqMYoIV57A&t=501s) The orchestration paradox, where Opus-class models loop on choosing a method instead of executing.
- [0:09:23](https://www.youtube.com/watch?v=EcqMYoIV57A&t=563s) The 80/20 hybrid: research models for discovery, deterministic hard gates for validation.
- [0:15:31](https://www.youtube.com/watch?v=EcqMYoIV57A&t=931s) Qodo's architecture: context collector, specialized agents, and a judge agent that re-grounds findings in PR history.

## Connections

- [Qodo](../../companies/coding-agents/qodo.md): the speaker's company; the talk describes the multi-agent review and Context Engine architecture the profile covers.
- [LangChain](../../companies/agent-orchestration/langchain.md): Sharma names LangChain as the framework carrying inter-agent communication under Qodo's review system.
- [Greptile](../../companies/coding-agents/greptile.md): competing AI code review vendor solving the same codebase-context problem.
