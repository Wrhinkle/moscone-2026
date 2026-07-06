# Context Graphs for Explainable, Decision-Aware AI Agents

> Neo4j's Zaid Zaim and Andreas Kollegger argue that agents need graphs that store rules and policies alongside knowledge, and walk through a decision-making workflow agents can run over such a graph.

- **Speaker:** Andreas Kollegger & Zaid Zaim, Neo4j
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=abvQEhvRI_c) (AI Engineer channel; ~17m, released 2026-05-28)
- **Program:** AI Engineer 2026 release, program placement unconfirmed. It is billed as "context graph session number two" following a talk by Stephen Chin, and an aside places the room in the UK, which suggests the AI Engineer Europe Summit.

## Summary

Zaim opens with Neo4j's framing: agents are strong at language, reasoning, and creativity, and knowledge graphs fill in the missing piece, knowledge. He splits agent memory into short-term (the conversation and state history), long-term (generalized context about organizations, people, and things), and reasoning memory. Context graphs, he says, sit inside context engineering but make a specific shift: beyond giving agents the right knowledge, they capture the rules and policies that govern behavior, what he calls the missing why. A context graph records why an agent should do something, so it can drive decisions rather than only answer questions. He sketches the memory graph (short-term in one region, long-term and reasoning in another) and the runtime loop: a user query goes to the agent, which checks its own knowledge, falls back to the graph database, translates language to Cypher via text2cypher tools, traverses the graph, and returns grounded content.

Kollegger's half is a decision-making workflow to run over that graph. His motivating example is OpenClaw-style autonomous agents, which he says exaggerate the need for good decisions: give an agent a credit card and an instruction to keep the fridge stocked with Red Bull, and it will happily order Red Bull the week rent is due, because nobody anticipated that circumstance in the prompt. Rather than patching instructions case by case, he proposes a general framework, the kind business schools teach, made explicit for agents. It starts with framing: the objective, the causality that led here, and the environment, since ordering Red Bull and prescribing medication are different worlds. Framing feeds a global context of precedent (what was done before in this situation) balanced against hard and soft business rules, which may overrule precedent. Then comes risk-value analysis, where he says agents should spend most of their time on serious decisions. He highlights reference class validation with a medical example: a drug correct for 99 percent of patients can be fatal for the other 1 percent, so knowing which population the case belongs to matters more than the statistics. The analysis also weighs whether the decision is reversible and the cost of being wrong, and forces the value side to be explicit, since maximizing savings and maximizing Red Bull availability point different directions.

A design choice he stresses: the analysis agent's output is a proposal of alternatives with pros and cons, and a separate agent decides whether it has the authority and certainty to act, escalating to a higher-privilege agent or a human when it does not. Deferring is a valid outcome. Finally, the entire reasoning chain, considered and rejected options included, gets written back into the graph with the decision and actions, giving future agents precedent and giving the organization traceability. He cautions that every step is domain-specific in practice, invites people to bring domains Neo4j has not cataloged yet, and points to free Graph Academy courses.

## Notable moments

- [0:03:10](https://www.youtube.com/watch?v=abvQEhvRI_c&t=190s) The context graph pitch: capture rules and policies, the missing why, alongside knowledge.
- [0:07:19](https://www.youtube.com/watch?v=abvQEhvRI_c&t=439s) The Red Bull example: an autonomous agent orders Red Bull the week rent is due.
- [0:11:21](https://www.youtube.com/watch?v=abvQEhvRI_c&t=681s) Reference class validation: right for 99 percent of patients, fatal for 1 percent.
- [0:14:23](https://www.youtube.com/watch?v=abvQEhvRI_c&t=863s) Writing the full reasoning chain back into the graph as precedent for future agents.

## Connections

- [Neo4j](../../companies/memory-rag-search/neo4j.md): the speakers' company; its Context Graph and agent-memory products are what this talk demonstrates.
- [Session recaps](../../notes/session-recaps.md): Stephen Chin's in-person GraphRAG session made the companion argument, auditable graph traversal beating vector similarity, and this talk explicitly follows a Chin talk.
- [Graph-based Agent Memory: Taxonomy, Techniques, and Applications](../../papers/memory-research-agents/graph-based-agent-memory-taxonomy-techniques-and-applicat.md): surveys the short-term, long-term, and reasoning memory structures Zaim sketches.
- [FalkorDB](../../companies/memory-rag-search/falkordb.md): a competing graph database chasing the same agent-memory positioning.
