# Stop AI Agent Hallucinations: 5 Techniques + Production Patterns

> Five code-level techniques against agent hallucination, each demoed with and without on a Strands Agents travel bot, then mapped to AWS production services.

- **Speaker:** Elizabeth Fuentes, AWS
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=vJukHCIv7Ck) (AI Engineer channel; ~55m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Elizabeth Fuentes, a developer advocate at AWS focused on agentic applications, works through five techniques for reducing hallucination and token waste, with the recurring refrain that each is a code change, not a prompt change. All demos run in Jupyter notebooks against a dummy travel agent built on Strands Agents, the open source framework AWS maintains, using OpenAI for inference and a shared public repo. For each technique she runs the agent without it and then with it.

Technique one is semantic tool selection. Her travel agent has 29 tools, and every tool schema costs roughly 200 tokens, so around 3,000 tokens of tool descriptions ride along on every call whether used or not, and with all 29 visible the model sometimes picks the wrong one. Her fix embeds tool descriptions into a local vector store using a sentence-transformers model that runs free on the laptop, retrieves the top three matches per query, and passes only those to the agent, dropping tool-description tokens from thousands to under 300 while accuracy improves. For multi-turn conversations she clears and swaps the tool registry inside the Strands agent loop on each invocation. In production, she notes, Amazon Bedrock AgentCore Gateway builds the tool index and does this routing automatically.

Technique two is GraphRAG for questions where vector retrieval structurally fails: averages, counts, and multi-hop queries. Vector search always returns something and only surfaces the top chunks, so the model computes aggregates from a sample and presents the estimate as fact. Her graph agent has one tool that writes a Cypher query against a local Neo4j knowledge graph, which Neo4j's library built automatically from raw text files using an LLM. The comparison lands hardest on "tell me about hotels in Antarctica": the RAG agent hedges verbosely while the graph agent's query returns zero rows and an honest "there are no hotels in Antarctica."

Technique three is multi-agent validation, because a single agent that hits a tool error can rationalize it and return a confident fabricated success the user never questions. Using the Strands Swarm class, she chains an executor, a validator, and a critic; when a booking targets a nonexistent hotel, the executor errors, the validator flags the hallucination, and the critic rejects, so the fabricated confirmation never reaches the user.

Technique four, neuro-symbolic guardians, treats prompt rules as suggestions the model reads as text and code as the only real constraint. Strands hooks fire before each tool call, and her Python rules, payment verified before confirmation, maximum ten guests, valid date ranges, cancel the call when parameters violate them. Same model, same tools, same prompt, different outcomes because the rules live in code. AgentCore's policy service, she says, is this pattern managed in production. Technique five softens it: hooks block unconditionally, but some rules are soft, so the agent-control open source library registers steering rules on a local server via API, no redeploy, and steers instead of stopping. A booking far over the guest cap gets split across rooms and the task completes without a hard stop.

The closing production map puts the Strands agent in AgentCore runtime with gateway, memory, and CloudWatch observability, steering rules in DynamoDB that go live on the next call, and Neo4j AuraDB for the graph, with notebooks, a deployable app, CDK templates, and AWS credits linked from the repo.

## Notable moments

- [0:05:07](https://www.youtube.com/watch?v=vJukHCIv7Ck&t=307s) The token math: 29 tool schemas cost about 3,000 tokens on every single call.
- [0:26:25](https://www.youtube.com/watch?v=vJukHCIv7Ck&t=1585s) Hotels in Antarctica: vector RAG waffles, the Cypher query returns an honest zero.
- [0:34:36](https://www.youtube.com/watch?v=vJukHCIv7Ck&t=2076s) The swarm's validator and critic catch a fabricated booking a single agent reported as success.
- [0:43:47](https://www.youtube.com/watch?v=vJukHCIv7Ck&t=2627s) Side-by-side scenarios: identical model, tools, and prompt, different outcomes because rules run in Python.

## Connections

- [AWS](../../companies/cloud-compute/aws.md): the speaker's employer; Strands Agents and Bedrock AgentCore are the stack throughout.
- [Neo4j](../../companies/memory-rag-search/neo4j.md): the graph database behind her GraphRAG demo, including its LLM-driven graph construction library.
- [Session recaps](../../notes/session-recaps.md): the AWS Builder Loft AgentCore session and Stephen Chin's GraphRAG talk cover the same two pillars in person.
