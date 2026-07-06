# Why your agents need decision traces, not just documents
> Neo4j's Zach Blumenfeld defines context graphs, shows a financial-analyst agent retrieving past decision traces via graph embeddings, and demos a one-command scaffold for building your own.

- **Speaker:** Zach Blumenfeld, Neo4j
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=B9h9ovW5H9U) (AI Engineer channel; ~20m, released 2026-05-29)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Blumenfeld, recently moved from technical marketing back into a research engineering role at Neo4j, builds the talk around a distinction: a knowledge base helps an agent answer questions correctly, while a context graph carries the information needed to make better decisions. He credits Foundation Capital with popularizing the term around December and defines the data model as three layers: entities (things that exist), events (decisions, transactions, approvals), and context (policies plus recorded reasoning from both AI and past human decision makers).

The worked example is a financial analyst agent handling a credit increase request. With only systems-of-record context (customer info, transactions, policies), the agent can assign a risk score and recommend a review. With a context graph it also retrieves past decision traces and precedents, so it can answer whether to accept or reject and why, acting with something closer to subject matter expertise. The demo, built with Claude in the agent runtime, OpenAI embeddings, Neo4j with vector indexes, and a Next.js front end, shows the agent calling tools in sequence: pulling the customer's graph context, fetching decision traces, reaching a reject decision, then running a find-precedents step.

The technical idea Blumenfeld highlights is graph embeddings. Text embeddings give semantic similarity ("fraud rejection"); graph embeddings, computed with Neo4j's Graph Data Science library, embed the structure of connected decision-trace nodes into vectors, so structurally similar past decisions become retrievable by vector lookup. The precedent search is a hybrid of both, matching how past decisions were made rather than only what they were about, which he argues would be very hard to extract from documents alone.

The second half is tooling for getting started. Create-context-graph, built by product manager William Lyon and about a month old at the time, scaffolds a full-stack context graph application from a single uvx command, in the spirit of create-react-app: pick a name, a domain, and an agent framework (he chooses Pydantic AI; OpenAI, LangGraph, Crew, Strands, and Google ADK are among the options) and it generates the back end, front end, seeded demo data, Cypher-powered retrieval, an MCP server, and multi-turn conversation. It ships 22 built-in domains, including the healthcare one he demos and FinServ, supports custom domains with generated ontologies, and has data connectors for GitHub, Notion, Jira, and Slack. Underpinning it is the Neo4j agent memory package, a memory API covering short-term (conversation history and session context), long-term (entities extracted, deduplicated, and resolved over time), and reasoning (the traces themselves). Its entity extraction pipeline stages spaCy, GLiNER, and an LLM fallback, with separate merging, deduplication, and enrichment.

In Q&A he is candid about maturity: timestamps can link decision steps into causal chains, but automatic writing of new decision traces is still being worked out, and the current demo only stores decisions when prompted. Scoring decision quality is flagged as an open idea.

## Notable moments
- [0:02:14](https://www.youtube.com/watch?v=B9h9ovW5H9U&t=134s) The definition by contrast: knowledge bases answer questions, context graphs support decisions, shown through the credit-request example.
- [0:07:30](https://www.youtube.com/watch?v=B9h9ovW5H9U&t=450s) Graph embeddings explained: structurally similar decision traces become vector-searchable precedents.
- [0:08:31](https://www.youtube.com/watch?v=B9h9ovW5H9U&t=511s) Create-context-graph demo: a full context graph app from one uvx command.
- [0:12:32](https://www.youtube.com/watch?v=B9h9ovW5H9U&t=752s) The agent memory package: short-term, long-term, and reasoning memory with a staged extraction pipeline.

## Connections
- [Neo4j](../../companies/memory-rag-search/neo4j.md), the speaker's company; this talk is the practitioner view of the Context Graph products described in the profile.
- [Graph-based Agent Memory paper](../../papers/memory-research-agents/graph-based-agent-memory-taxonomy-techniques-and-applicat.md), a taxonomy of exactly the graph-shaped memory architecture productized here.
- [Session recaps](../../notes/session-recaps.md), where Stephen Chin's GraphRAG session made the matching in-person argument that auditable graph traversal beats vector similarity for agent decisions.
