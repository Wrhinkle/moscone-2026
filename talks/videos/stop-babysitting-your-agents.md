# Stop babysitting your agents...

> Why static context files and MCP access fail coding agents, and what a context engine does instead.

- **Speaker:** Brandon Waselnuk, Unblocked
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=BiG2ssibKGc) (AI Engineer channel; ~19m, released 2026-05-26)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Waselnuk's premise is that every agent spawns with zero organizational context, so the engineer ends up acting as the context engine, correcting the agent's guesses in a loop. He calls this babysitting. The talk walks through three myths about fixing it, three lessons Unblocked learned building a commercial context engine, and a demo of a social graph tool the company planned to open source the week of the event.

The myths. First, naive RAG over docs is not context. Waselnuk borrows "satisfaction of search" from radiology: once a scan turns up one finding, the radiologist stops looking. Agents do the same, treating the first retrieved pattern as the answer and never running exhaustively, so they miss the real root cause. Second, connecting more MCPs does not help, because MCPs are pipes that grant access without understanding; a new hire with badge access to every system still does not know what they do not know. Third, big context windows do not solve it. Unblocked found that stuffing a million-token window leaves the model unable to reason over the data except for needle-in-haystack lookups, and everything learned inside a session evaporates when the terminal closes.

His definition of a context engine: ingest static sources plus runtime signals across the corporate knowledge corpus, reason across them at query time, and return a token-optimized packet the agent can act on. Six requirements: unified system context, targeted retrieval, conflict resolution, a secure access model, personalized relevance, and token optimization. Two of these get concrete treatment. Conflict resolution means settling cases where the code in main says one thing and a Slack thread has the CTO saying it was implemented wrong; the engine should weigh the CTO's authority and surface both. The secure access model carries OAuth through the MCP delivery layer, so the engine will answer from your private Slack chats when you ask but never expose them to anyone else.

The evidence is a head-to-head test. The same integration prompt ran twice, once with MCP access to every needed SaaS tool and once with Unblocked's engine. The naive run compiled and passed code checks, but the senior reviewer said it would have broken the whole system if shipped; it missed that the team uses Bedrock as a fallback and broke custom callers. The engine-backed run got a nitpick and a merge approval.

The hard lessons: Unblocked first optimized for access and assumed the model would figure it out, and it did not, even after years. The agent silently picked a side when sources conflicted rather than resolving them. And caching good answers for latency backfired, because a correct answer cached today is probably a lie tomorrow once the system changes.

The demo shows a procedurally generated social graph of Unblocked's engineering org: node size by shipping volume, edges for who reviews whose code, expert labels per area of the codebase. The engine pivots on this graph to interpret a query by who is asking. A second demo has Claude call Unblocked's MCP research tool for a Zendesk integration; the returned research packet steers the agent's explore subagents to the right places, and the resulting plan captures the team's factory pattern and provider registration. His recommended pattern is engine for planning, plain execution, engine again at code review.

## Notable moments

- [0:05:19](https://www.youtube.com/watch?v=BiG2ssibKGc&t=319s) The naive MCP-only run compiles and passes checks, but the senior engineer says shipping it would have broken the entire system.
- [0:08:19](https://www.youtube.com/watch?v=BiG2ssibKGc&t=499s) The social graph as pivot point, and settling the fight between source code in main and a Slack thread where the CTO says it was implemented wrong.
- [0:12:22](https://www.youtube.com/watch?v=BiG2ssibKGc&t=742s) Three hard lessons, including why caching good answers turns them into lies within a day.
- [0:15:22](https://www.youtube.com/watch?v=BiG2ssibKGc&t=922s) Live demo of the soon-to-be-open-source social graph tool built from a code repo.

## Connections

- [Unblocked](../../companies/swe-infrastructure/unblocked.md), the speaker's company and the context engine described in the talk.
- [Sourcegraph](../../companies/coding-agents/sourcegraph.md), an adjacent vendor attacking code context through indexing and search rather than a cross-system knowledge engine.
- [Session recaps](../../notes/session-recaps.md), where Sonar's memory-injection hooks and Stephen Chin's GraphRAG session cover the same agent-context problem from other angles.
