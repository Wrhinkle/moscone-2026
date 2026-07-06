# MCP Apps: Primitives, discovery, and the Future of Software

> A walkthrough of the MCP apps extension, the widget and state primitives it adds to MCP servers, and why the newly opened ChatGPT, Claude, and Cursor stores are the distribution channel to care about.

- **Speaker:** Pietro Zullo, Manufact, Inc
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=sAOBXCDiDOs) (AI Engineer channel; ~29m, released 2026-07-05)
- **Program:** Online Track 2026

## Summary

Zullo co-founded Manufact, which builds the open-source MCP-Use SDKs, 8 million-plus downloads and 10k GitHub stars, an open-source inspector, and a cloud for shipping MCP servers. His history of the space: MCP launched in 2024, MCP-UI emerged in May 2025 as a way for servers to return UI components, OpenAI's Apps SDK followed, and in January 2026 MCP-UI became MCP apps, the official protocol extension. He flags two shifts as the ones that matter. Servers now return rich UI instead of only JSON, and the stores opened: ChatGPT, Claude, and Cursor all moved from gated design-partner programs to self-serve submission, which Zullo argues most builders still have not noticed.

The primitives section is the technical core. An MCP app declares UI resources at initialization; when the model calls a tool, the tool populates the resource's arguments and the client renders a widget in a sandboxed iframe with a bidirectional channel to the host. From there Zullo enumerates what the channel enables. A set-state primitive keeps the model informed about what the user did inside the widget, so a follow-up message knows what is selected. Widgets can send follow-up messages to the chat, with client differences: Claude places the message in the input box for user approval while ChatGPT sends it and streams the answer immediately. Streaming tool arguments update the widget incrementally as tokens arrive, shown later with an Excalidraw canvas drawing mermaid-syntax diagrams live in Claude. Widgets can trigger further tool calls, and dual outputs split what goes where, a privacy pattern Zullo emphasizes: show a card full of private data in the UI while the model receives only a note that the user is viewing their own information. Display modes cover inline, picture-in-picture, and fullscreen, where the chat input overlays the widget for things like video editing, and servers can detect from client metadata whether the host renders widgets, returning a text alternative when it does not.

On distribution, all three major stores scan submitted servers for annotated tools and working declared auth, then test them partially manually against provided test prompts before acceptance. Manufact's cloud runs those publishing checks in advance and generates submission artifacts like screenshots and test cases. The bigger claim is about dynamic discovery: Claude today, when handed a task with no matching tool, searches the MCP registry for the right connector on its own, and Zullo expects ChatGPT to follow. His pitch is that being in the registry when a billion-plus users express intent in chat is a wave of high-intent organic distribution. He closes with his own workflow, pulling Granola meeting notes into Linear tickets that an agent then implements from Claude Code, and endorses Paul Graham's line that AI apps are the new browsers, extending it: if AI apps are the browsers, the connectors are the new websites, and an MCP app is how your product returns a UI there. He no longer wants to look at dashboards outside of Claude.

## Notable moments

- [0:04:05](https://www.youtube.com/watch?v=sAOBXCDiDOs&t=245s) The timeline: MCP-UI in May 2025, OpenAI's Apps SDK, the stores quietly opening, and MCP apps going official in January 2026.
- [0:08:17](https://www.youtube.com/watch?v=sAOBXCDiDOs&t=497s) The set-state primitive: the widget updates what the model knows about UI state, so follow-up messages see user selections.
- [0:13:20](https://www.youtube.com/watch?v=sAOBXCDiDOs&t=800s) The privacy pattern: the user sees full private data in the widget while the model is told only that the data is displayed.
- [0:24:28](https://www.youtube.com/watch?v=sAOBXCDiDOs&t=1468s) Dynamic discovery: Claude searches the MCP registry for the right connector when it lacks a tool for an assigned task.

## Connections

- [Composio](../../companies/agent-orchestration/composio.md) attacks the same MCP distribution problem from the integration side, with a consumer MCP server plugging 500-plus apps into Claude, ChatGPT, and Cursor.
- [Session recaps](../../notes/session-recaps.md) note the Vercel conversation flagging tool discovery as an unsolved, useful problem, the exact gap the MCP registry and store search address.
