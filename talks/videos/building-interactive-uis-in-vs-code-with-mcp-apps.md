# Building Interactive UIs in VS Code with MCP Apps

> GitHub developer advocates explain MCP Apps, which let MCP server tools return interactive UI components rendered in a sandboxed iframe inside the chat, with a live flame-graph profiler demo in VS Code.

- **Speaker:** Marlene Mhangami & Liam Hampton, GitHub
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=_xIwFcnHqp4) (AI Engineer channel; ~16m, released 2026-06-06)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Mhangami, a senior developer advocate at Microsoft and GitHub, opens with the MCP basics: hosts (programs like VS Code that want data from servers), clients (GitHub Copilot in their setup, maintaining one-to-one connections with servers), and servers (lightweight programs exposing tools, prompts, and resources). She recommends installing servers from the vetted list in the VS Code extensions tab rather than random ones from the internet, since unvetted servers can carry malicious code. The problem MCP Apps solves is that early MCP tools could only return text, which she illustrates with README ASCII art standing in for diagrams that could not be generated.

MCP Apps let server tools return rich interactive components that render directly in the chat. The flow she walks through: the user sends a prompt, the agent picks a tool, the server returns tool results plus a UI resource reference pointing to server-generated HTML, and then the host (VS Code, not the Copilot client) fetches that HTML and renders it inside a sandboxed iframe. The app can call back to the server so fresh data keeps flowing both ways. Her Excalidraw example makes the difference concrete: the same "draw a diagram explaining MCP" prompt that once produced text now yields a live diagram the user can drag and edit inside the chat. Use cases she cites include data exploration, where clicking chart elements beats typing follow-up questions, and e-commerce, where the whole checkout should happen in the chat rather than as returned links. Shopify is building MCP Apps with attention to keeping brand experience identical to its website, and Excalidraw and Figma are shipping them too.

Hampton's live demo shows the build path. He took an MCP Apps skill from Anthropic's Model Context Protocol repository, edited it, and ran it through GitHub Copilot CLI to generate several apps (markdown viewer, flight status, color picker, and the flame-graph profiler he demos). An MCP App has three parts: the tool, the bundled HTML UI (React, Vue, Svelte, or vanilla JS), and the link that tells the host a UI resource exists for a tool result. His server profiles a Go program containing bubble sort and Fibonacci functions over five seconds using Go's pprof, returns JSON, and VS Code renders a React flame-graph app in the chat with top functions and a summary. The payoff he stresses is eliminating the back-and-forth of pasting profiler output at a model and asking where the time goes. He closes with the sandbox rationale via a hamster analogy: the iframe is the cage, because you do not want the app touching VS Code settings, APIs, or anything external.

## Notable moments

- [0:04:17](https://www.youtube.com/watch?v=_xIwFcnHqp4&t=257s) Definition of MCP Apps and the Excalidraw diagram that replaces ASCII-art answers.
- [0:05:18](https://www.youtube.com/watch?v=_xIwFcnHqp4&t=318s) The architecture walk-through: tool result, UI resource reference, host-rendered sandboxed iframe.
- [0:13:23](https://www.youtube.com/watch?v=_xIwFcnHqp4&t=803s) The pprof flame graph renders live inside the Copilot chat window in VS Code.
- [0:14:23](https://www.youtube.com/watch?v=_xIwFcnHqp4&t=863s) Why the iframe: Hampton's hamster-in-a-cage explanation of the sandbox boundary.

## Connections

- [GitHub](../../companies/coding-agents/github.md): the speakers' company; the talk extends the Copilot and MCP Registry story in the profile to in-chat UI.
- [Microsoft](../../companies/cloud-compute/microsoft.md): VS Code is the host application doing the iframe rendering, and both speakers sit in Microsoft developer advocacy.
- [Figma](../../companies/enterprise-adopters/figma.md): named in the talk as a company shipping MCP Apps components.
