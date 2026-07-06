# The agent-ready web: Simplify user actions with WebMCP

> Google Chrome's Tara Agyemang introduces WebMCP, a proposed web standard that lets sites expose structured tools to in-browser AI agents instead of forcing them to screen-scrape.

- **Speaker:** Tara Agyemang, Google
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ghJmWQCIHRM) (AI Engineer channel; ~22m, released 2026-06-11)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Agyemang, a developer relations engineer on the Chrome team, starts from the mismatch between a web built for human eyes and the agents now using it. Her example is a concert ticket site with Gemini in Chrome: to buy two festival tickets, an agent today parses the entire DOM, walks the accessibility tree, screenshots the page, measures pixel offsets, and clicks, a long, brittle, token-heavy pipeline that an ad pushing content down can still break. She insists on web foundations first: semantic HTML, accessibility, and page performance get a site halfway to agent-ready before any new API. WebMCP is the other half, a proposed standard for declaring a site's capabilities as structured tools, which she summarizes as handing agents a menu instead of making them guess, or the USB-C of agent interactions.

The first demo is a maze game controllable only through tools, inspected with the Model Context Tool Inspector, a Chrome extension from Chrome DevRel that lists every tool a page exposes. Tools are scoped per page: the landing page offers one start-game tool, while the maze page exposes move, look, and item tools that Gemini chains from prompts like "complete the maze." Agyemang positions WebMCP relative to MCP the way JavaScript relates to Java: inspired by it, but distinct. MCP connects agents to server-side services reachable anytime; WebMCP implements the tools portion of MCP for client-side, in-browser agents, and only works while the browser window is open.

There are two APIs. The declarative API adds attributes like a tool name and description to an ordinary HTML form, and the browser generates the JSON schema from the form fields; an agent-invoked boolean attribute even tells you whether a human or an agent filled the form. The imperative API covers multi-step flows: a registerTool call takes a hand-written schema, a description good enough for the agent to know when to call it, and an execute block of plain JavaScript that returns results the agent uses for its next step. Back in her ticket demo, buying two VIP Summer Vibes Festival tickets becomes three tool calls (search concerts, open concert page, purchase ticket), the UI updating in sync at each step so the user can watch, with checkout deliberately left manual since real money is involved.

Status is early preview and the API is still changing week to week. Trying it requires Chrome 146 or later (she recommends Canary), a WebMCP testing flag, and the inspector extension, with an early preview program blog post, plus a GitHub repository holding six or seven demos and an eval CLI for testing your own site's tools. Her closing pitch: agents already use the web, so replace token-heavy screen-scraping by turning every website into a high-performance API for agents.

## Notable moments

- [0:01:16](https://www.youtube.com/watch?v=ghJmWQCIHRM&t=76s) What buying tickets costs an agent today: DOM parsing, accessibility tree, screenshots, and pixel math.
- [0:04:19](https://www.youtube.com/watch?v=ghJmWQCIHRM&t=259s) Maze game demo with the Model Context Tool Inspector showing page-scoped tools.
- [0:12:23](https://www.youtube.com/watch?v=ghJmWQCIHRM&t=743s) The declarative API: a few attributes on an HTML form and the browser emits the JSON schema.
- [0:15:26](https://www.youtube.com/watch?v=ghJmWQCIHRM&t=926s) Concert purchase completed in three chained tool calls with the UI kept in sync.

## Connections

- [Google](../../companies/models-inference/google.md): the speaker's company; WebMCP is driven by the Chrome team with DeepMind colleagues alongside.
- [Browserbase](../../companies/browser-computer-use/browserbase.md): the screen-driving browser-agent approach WebMCP aims to make unnecessary for cooperating sites.
- [The evolution of tool use in LLM agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): paper note on the structured tool-calling trajectory WebMCP extends into the browser.
