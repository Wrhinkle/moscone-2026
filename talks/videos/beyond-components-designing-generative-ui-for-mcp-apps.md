# Beyond Components: Designing Generative UI for MCP Apps

> Postman's Ruben Casas maps three levels of agent-generated UI, static, declarative, and fully generative, and argues MCP apps are the sandboxed delivery mechanism the last level needs.

- **Speaker:** Ruben Casas, Postman
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=hCMrEfPG2Yg) (AI Engineer channel; ~17m, released 2026-06-03)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Casas, a staff engineer at Postman who has spent the past year on generative UI and MCP apps, opens with the distance traveled since November 2022, when building UI with ChatGPT meant copy-pasting code blocks, what he calls the poor man's vibe coding. He marks late 2025 as the inflection: GPT 5.2 and Opus 4.5 were the first models good at high-fidelity UI generation, and when he asked one to rewrite his blog it added an unrequested search box with a blur animation and accessibility out of the box. His framing question follows: if models write front-end code this well, why is the industry still shipping mostly static UI? Borrowing Karpathy, he says we have a new computer whose GUI has not been invented yet; chat everywhere and the super app (ChatGPT, Claude, or Gemini rendering third-party UI via MCP apps) are both transitional answers to where UI runs, but the more interesting question is what the model generates.

He sorts that into three levels. In the static model, the agent is an orchestrator: a tool call passes data and props to predefined developer-built components the client renders, as in the AG-UI protocol's SDK mapping tool calls to React components, or Goose's auto visualizer matching arbitrary data to a fixed component set. Declarative UI goes further: the agent emits a JSON, YAML, or Python descriptor that a rendering engine translates into design-system components, the same personalization pattern Netflix has run for years with server-driven UI, and now productized by Vercel's JSON Render. Casas judges declarative the best balance available today on flexibility, consistency, predictability, speed, and token cost.

The third level is generative components: let the model write HTML, CSS, and JavaScript at runtime, via recursive sampling or a second model call. His Postman experiment is a weather agent that, in one tool call, hits the weather API, writes a joke, and generates the full interface with no predefined components. The obvious problem is trust: if we sandbox third-party code, we cannot ship raw LLM-generated code to users either. That is his case for MCP apps as the distribution model, since they provide authentication, tool calling, message passing between UI and agent, and a double-iframe sandbox by default. He reads Anthropic's choice to build its first-party visualizer feature on MCP apps rather than a proprietary rendering path as strategic confirmation.

For the future, Casas thinks floating Jarvis-style windows are the failure-of-imagination answer, like early TV shows that were radio programs with cameras. His bet is collaboration over rendering: the Excalidraw MCP app's shared canvas, where human and agent edit the same artifact back and forth, previews generative UI that is personalized and collaborative rather than a one-way visualization feed.

## Notable moments

- [0:01:07](https://www.youtube.com/watch?v=hCMrEfPG2Yg&t=67s) The late-2025 inflection: GPT 5.2 and Opus 4.5 make high-fidelity UI generation routine.
- [0:07:09](https://www.youtube.com/watch?v=hCMrEfPG2Yg&t=429s) Static and declarative patterns: AG-UI, Goose's auto visualizer, Netflix-style server-driven UI, and Vercel's JSON Render.
- [0:10:11](https://www.youtube.com/watch?v=hCMrEfPG2Yg&t=611s) The weather agent experiment: API call, joke, and complete UI generated in a single tool call.
- [0:11:11](https://www.youtube.com/watch?v=hCMrEfPG2Yg&t=671s) Why runtime-generated code needs a sandbox, and why MCP apps' double iframe is the delivery mechanism.

## Connections

- [Postman](../../companies/api-platforms/postman.md): the speaker's company and the home of the generative weather-agent experiment.
- [Vercel](../../companies/cloud-compute/vercel.md): builds JSON Render, the descriptor-to-component engine Casas holds up as today's best declarative option.
- [CopilotKit](../../companies/agent-orchestration/copilotkit.md): maintains the AG-UI protocol Casas cites as the canonical static-components pattern.
