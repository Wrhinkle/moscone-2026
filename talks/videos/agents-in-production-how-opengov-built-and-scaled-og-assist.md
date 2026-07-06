# Agents in Production: How OpenGov Built and Scaled OG Assist

> Gabe De Mesa walks through the production architecture of OG Assist, the agent embedded across OpenGov's government ERP suite, from its Effect-based agent loop to evals, sandboxing, and generative UI.

- **Speaker:** Gabe De Mesa, OpenGov
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=4uFVSLgD2Q4) (AI Engineer channel; ~18m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

De Mesa is an engineer on OpenGov's AI agents team. OpenGov, founded about 14 years ago, sells ERP software to governments: budgeting, procurement, asset management, permitting, utility billing. OG Assist is a button in the navigation bar of every product; each product team builds tools and skills that power it, so the same chat surface answers utility-billing rate-code questions in one suite and permitting questions in another. The agent can also see the page the user is on and highlight elements to click, which De Mesa demos by asking it to point out next steps on screen.

The architectural bet he spends the most time on is Effect, the open-source TypeScript library. The team started on LangGraph, then replaced it with their own Effect-native agent loop as use cases outgrew the framework, giving them full control over the loop. De Mesa says the payoff is that Effect's schema validation, error handling, structured concurrency, logging, and tracing now propagate through the whole loop. The core is the Effect AI package: instantiate a chat, stream text against a prompt, and swap language models via dependency injection. Tracing comes out of the box because Effect functions are tagged with spans automatically, so the team can profile where seconds go in a request chain and cross-reference failures across services and teams. His slogan for the observability section is "you can't scale what you can't see."

Several production mechanisms get concrete treatment. Agent routes follow Google's A2A protocol, with agent cards (name, description, capabilities) as the contract both front end and back end consume; De Mesa credits the rigor of the spec with driving alignment across teams. Evals run in CI against real completions, checking that a prompt hits the expected tools, and pair with a thumbs-up-thumbs-down feedback mechanism in the product. The loop deterministically interrupts when a tool call needs human approval, showing an accept-or-reject UI before any mutating operation proceeds, which De Mesa frames as keeping humans in the driver's seat. Code execution and file creation happen in ephemeral sandboxes the agent spins up on demand and tears down afterward; his demo has the agent build a downloadable PDF inside one. For long conversations, the team found rolling summarization more effective than stuffing recent messages: keep the last several messages verbatim, maintain a running summary of the rest, and do recall over the summary when a user asks about something a hundred messages back. A generative-UI primitive lets the agent render forms at runtime, so a vague request like "write me a long essay" comes back with a form offering topic options.

The talk closes with the internal side: the same team building customer-facing tools and skills uses Claude and Cursor heavily for reading, writing, and reviewing code. De Mesa's summary of the philosophy is that tools and skills are really all you need, and that shipping is the start of the work rather than the finish.

## Notable moments

- [0:02:03](https://www.youtube.com/watch?v=4uFVSLgD2Q4&t=123s) OG Assist in situ: one button across the whole ERP suite, powered by tools each product team contributes.
- [0:05:04](https://www.youtube.com/watch?v=4uFVSLgD2Q4&t=304s) Why the team left LangGraph for a hand-rolled Effect-native agent loop.
- [0:10:10](https://www.youtube.com/watch?v=4uFVSLgD2Q4&t=610s) Deterministic interrupts for human approval before mutating tool calls.
- [0:12:11](https://www.youtube.com/watch?v=4uFVSLgD2Q4&t=731s) Rolling summarization plus recall as the fix for long-context overload.

## Connections

- [LangChain](../../companies/agent-orchestration/langchain.md): OpenGov's migration off LangGraph is a data point on when teams outgrow orchestration frameworks.
- [E2B](../../companies/swe-infrastructure/e2b.md): sells the ephemeral agent sandboxes OpenGov built in-house for code execution and file creation.
- [CopilotKit](../../companies/agent-orchestration/copilotkit.md): productizes the in-app agent UX and generative-UI patterns OG Assist implements first-party.
