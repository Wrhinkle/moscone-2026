# Building Agent Interfaces: Lessons from Chrome DevTools (MCP) for Agents

> Four engineering lessons from shipping Chrome DevTools as an MCP server for coding agents: measure token efficiency, design for error recovery, audit tool descriptions, and keep trust boundaries intact.

- **Speaker:** Michael Hablich, Google
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=_B4Pv9ttFgY) (AI Engineer channel; ~23m, released 2026-06-05)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Hablich, product manager for Chrome DevTools at Google, explains why his team built a separate DevTools surface for agents. Chrome DevTools for humans serves millions of web developers; the agent version is an MCP server (with a CLI variant) that works in any MCP-capable harness, including Gemini CLI, Claude Code, and Codex. The origin story is blunt: about a year and a half ago, coding agents could generate code but could not validate it against a running page. The team's first instinct was to hand agents raw data. A performance trace file runs to multiple megabytes and roughly 50,000 lines of JSON, and feeding it to a model blew through the context window. The fix was to return markdown and semantic summaries instead, pointing the agent at the right sentence rather than making it read the whole book.

From there Hablich frames agents as a distinct user segment. Agents and humans share intent (find and fix page errors) but have different cognitive bottlenecks, so the interface has to be designed separately. His core metric is tokens per successful outcome, which he calls the fuel efficiency of an interface. The caveat is that efficiency means nothing without effectiveness, and the metric only compares meaningfully within a user journey: web scraping is cheap, debugging a broken responsive layout is legitimately expensive. The team attacks token burn from three angles. Niche tools, such as Chrome extension debugging, hide behind command line flags. A slim mode exposes only three tools (select page, navigate page, evaluate script), trading context savings for extra agent turns. The CLI lets agents chain commands so post-processing happens on the local machine, for example grepping the accessibility tree and piping a control ID into a click command instead of pushing everything through the model.

On error recovery, Hablich argues every agent error costs retry tokens, so error messages should enable self-healing. Adding one sentence to a navigation error ("history entry to navigate was not found") let agents fix themselves without a human. The team also uses proactive detours to counteract model training data, steering agents toward the performance trace tool rather than a Lighthouse audit, plus a troubleshooting skill for setup problems. On discoverability, the original design was one monolithic debug-webpage tool. It was neat engineering and it did not work, so they decomposed it into 25 tools, which shifted the problem to tool selection. Hablich cites a paper finding that 97 percent of MCP tool descriptions have quality smells, and argues the schema is the UI for the agent. Better descriptions cost context and can bias smaller models toward the wrong tools, so tuning is an endless quest for the minimum viable description.

The final lesson is trust. Users asked the autoconnect feature to remember their consent choice, and the team refused: in agent delegation, that friction is by design. Citing Simon Willison's lethal trifecta, Hablich sketches three tiers, a local dev environment with a human in the loop, CI environments with separated Chrome profiles and containers, and internet-facing agent fleets that need domain allowlists and prompt injection mitigations. Tiers one and three may share a tool, and they should share nothing about a security model.

## Notable moments

- [0:03:08](https://www.youtube.com/watch?v=_B4Pv9ttFgY&t=188s) Why they built it: coding agents were flying blind, and a 50,000-line JSON trace blew the context window.
- [0:08:08](https://www.youtube.com/watch?v=_B4Pv9ttFgY&t=488s) Tokens per successful outcome as the fuel efficiency of an agent interface.
- [0:15:14](https://www.youtube.com/watch?v=_B4Pv9ttFgY&t=914s) The monolithic debug-webpage tool becomes 25 tools, and the 97 percent tool-description quality-smell finding.
- [0:18:16](https://www.youtube.com/watch?v=_B4Pv9ttFgY&t=1096s) Autoconnect keeps per-use consent on purpose: friction as a trust-boundary design choice.

## Connections

- [Google](../../companies/models-inference/google.md): the speaker's employer, and the Gemini CLI shown driving the MCP server in the demo.
- [Browserbase](../../companies/browser-computer-use/browserbase.md): adjacent vendor selling browser automation infrastructure for agents, where the same CDP-level debugging surface matters.
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): paper note covering the tool-selection and description problems Hablich hits with 25 tools.
