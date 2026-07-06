# A Song of Types and Agents

> An argument that TypeScript has taken the AI application layer from Python, and that agents should be built in it even while models keep training in Python.

- **Speaker:** Roberto Stagi, Ratel
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=UlFB6efYN5Q) (AI Engineer channel; ~14m, released 2026-06-22)
- **Program:** Online Track 2026

## Summary

Roberto Stagi, CTO and co-founder of Ratel, a context layer for AI agents, frames the last few years as a war of languages for the AI throne. Python was the unquestioned choice when AI meant training models, and GitHub's 2024 report crowned it the most popular language on the platform, crediting AI for the climb. Then in August 2025, by GitHub's own report and for the same stated reason, TypeScript passed Python as the most used language. Stagi's explanation for the reversal is coding agents. Between 2024 and 2025, tools like Claude Code, Cursor, and Codex became the default way to build applications, and the default language those agents build in is TypeScript. With one new developer joining GitHub every second in 2025, the newcomers reached for TypeScript where a year earlier they reached for Python.

Stagi is careful about the boundary of the claim. Training, research, and GPU serving remain Python's and will for a long time, he says. What changed is that AI stopped being something you train and became something you ship inside applications, and the application layer has belonged to TypeScript for years. Every new app now wants agentic capability, so the integration demand falls on TypeScript rather than Python. He cites Anthropic's acquisition of the Bun JavaScript runtime the previous December as a signal of where the labs think the application layer lives.

The middle of the talk answers the fair question of whether popularity alone justifies following. His reasons to build agents in TypeScript: coding agents will keep getting better at it because more TypeScript applications feed the next generation's training and integrations; npm is the deepest package ecosystem for the things agents must touch, authentication, payments, UI, and infrastructure; and one language can cover the agent loop, tools, backend, and UI in a single codebase. The Python alternative splits into at least two services, a FastAPI and Pydantic AI backend plus a separate React application, with a contract to maintain between them. In TypeScript a single Zod schema can define a type once and check it in the backend, at the model boundary, and in the UI. He also points to ecosystem velocity: the Vercel AI SDK went from 1.6 million to 15.1 million weekly downloads in one year, between 9x and 10x.

Stagi closes by claiming none of this was unpredictable, quoting Jeff Atwood's law that any application that can be written in JavaScript eventually will be, plus the corollary that it will eventually be written in TypeScript. His projection is that the gap between the two languages at the application layer widens from here: models still ship on pip, but agents, the new application, ship on npm. The recommendation is to keep training in Python and build the agents in TypeScript, because overlooking it now means falling behind.

## Notable moments

- [0:05:12](https://www.youtube.com/watch?v=UlFB6efYN5Q&t=312s) What changed between the 2024 and 2025 GitHub reports: coding agents became the default way to build.
- [0:06:14](https://www.youtube.com/watch?v=UlFB6efYN5Q&t=374s) Anthropic's acquisition of Bun as evidence the labs are moving to the application layer.
- [0:10:14](https://www.youtube.com/watch?v=UlFB6efYN5Q&t=614s) One Zod schema spanning backend, model, and UI versus the split Python stack.
- [0:11:14](https://www.youtube.com/watch?v=UlFB6efYN5Q&t=674s) Vercel AI SDK downloads up roughly 9-10x in a year, 1.6M to 15.1M per week.

## Connections

- [Vercel](../../companies/cloud-compute/vercel.md): the AI SDK whose download curve is Stagi's ecosystem evidence, with current usage numbers in the profile.
- [Pydantic](../../companies/agent-orchestration/pydantic.md): the Python-side agent stack Stagi contrasts against.
- [Session recaps](../../notes/session-recaps.md): Vercel's in-person session on eve, "Next.js for agents," is the same TypeScript-agent thesis from the vendor side.
