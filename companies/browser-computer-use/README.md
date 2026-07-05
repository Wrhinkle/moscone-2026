# Browser & Computer Use

Browser infrastructure for agents, computer-use agents, agent-native browsers and personal AI devices. This is the layer where agents stop being chatbots and start acting on the world: clicking through websites that will never ship an API, driving desktop apps by screen and keyboard, or living in the browser/device the human already uses. The category exists because the overwhelming majority of real-world software — vendor portals, legacy GUIs, checkout flows, government sites — is only reachable the way a person reaches it, and every serious agent product eventually needs a substrate (headless browser fleet, sandboxed VM, or agentic browser) to do that reliably, safely, and at scale.

## How to read this category

The load-bearing entries are **Browserbase** (the headless infrastructure end — managed browser fleets plus the widely adopted Stagehand SDK; the category's only platinum sponsor and its clearest commercial success), **Cua** (the sandbox/eval end — "Docker for computer-use agents," full-OS VMs for training and benchmarking screen-acting models), and **Yutori** (the model end — the rare vertically integrated player training its own pixels-to-actions foundation model rather than wrapping frontier APIs). Read those three and you have the stack: infrastructure → environment → action model.

The axis that differentiates the rest is **who the agent works for and where it lives**. The Browser Company's Dia is the human-facing surface (an AI browser you adopt, not a platform you integrate); Zo Computer is a persistent personal cloud computer with an agent attached; Bee Computer is ambient hardware capture feeding an agent loop; era labs is a pre-product research lab on agent-human trust standards (the profile flags serious verification caveats — read the disambiguation note before citing it).

**Start here:** [browserbase.md](browserbase.md), then [cua.md](cua.md), then [yutori.md](yutori.md).

## Companies

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Browserbase](browserbase.md) | Managed headless-browser cloud + Stagehand OSS SDK for web agents | Platinum | $67.5M raised; $300M valuation (Series B, Jun 2025) | Stagehand at ~23.3k GitHub stars; ~50M browser sessions run in 2025 |
| [Cua](cua.md) | Open-source sandboxed full-OS VMs + benchmarking for computer-use agents | Supporting | ~$500K (YC X25) — earliest-stage of the group | Founders built Microsoft's Windows Agent Arena; ~19.4k GitHub stars on ~$500K of funding |
| [Yutori](yutori.md) | Trains its own browser-use model (n1/n1.5) plus Scouts/Delegate agent products | Supporting | $15M seed (Radical Ventures); no Series A found | Claims n1 beat Claude Opus 4.6 on Navi-Bench at 5.6x lower cost — and open-sourced the benchmark |
| [The Browser Company](the-browser-company.md) | Arc and Dia — the consumer/work-facing agentic browser bet | Supporting | Acquired by Atlassian for $610M cash (closed Oct 2025) | Killed Arc at 1M+ users to go all-in on Dia; Atlassian plans distribution into ~300K customer orgs |
| [Zo Computer](zo-computer.md) | Persistent personal cloud computer (Linux server + AI agent) reachable by chat, text, or email | Supporting | ~$7.8M reported (Craft, Lightspeed, Factorial — not independently verified) | State persists: the agent keeps running files, jobs, and hosted services after you close the tab |
| [Bee Computer](bee-computer.md) | $49 always-listening wearable turning conversations into notes, reminders, and actions | Supporting | $8.5M raised; acquired by Amazon (announced Jul 2025) | A $49 consumer device Amazon bought — a reference architecture for ambient capture → proactive agent |
| [era labs](era-labs.md) | Pre-product research lab on agent-human trust/interaction standards — identity partially unverified | Supporting | Unknown — no funding, founders, or customers found | Easily confused with the separate $11M "Era" AI-gadgets startup; confirm identity at the booth before citing |

## Related papers

The tool-use & governance area is effectively this category's research counterpart:

- [Verifiable Software Worlds for Computer-Use Agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md) — reproducible, checkable environments; exactly what Cua's snapshot-native sandboxes provide and the live-vs-simulated tension in Yutori's RL-on-live-websites training.
- [CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) — the prompt-injection/authority threat model for agents acting in logged-in sessions (Dia, Scouts, Browserbase all live inside it).
- [AI Planning Framework for LLM-Based Web Agents](../../papers/tool-use-governance/ai-planning-framework-for-llm-based-web-agents.md) — the planning layer that assumes a managed browser runtime underneath.
- [WebXSkill: Skill Learning for Autonomous Web Agents](../../papers/tool-use-governance/webxskill-skill-learning-for-autonomous-web-agents.md) — Dia's user-authored Skills are the productized version of this research question.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — constraining what a generalist agent may do with a user's sessions and credentials.
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — where MCP-exposed browsers/desktops (Browserbase, Cua, Yutori all ship MCP servers) fit in the tool-orchestration arc.
- [Agentic Search in the Wild: Intents and Trajectory Characteristics](../../papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md) — characterizes the autonomous browsing trajectories these platforms host.
- [Memory for Autonomous LLM Agents](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) and [Are We Ready For An Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md) — Dia's Memory feature and Zo's persistent agent desktop are production tests of both.

## Open questions

1. **Does the infrastructure layer survive the frontier labs?** OpenAI Atlas, Anthropic computer use, and Gemini-in-Chrome could commoditize browser automation from above; Browserbase, Cua, and Yutori are each betting a different layer stays independent.
2. **Where does the agent live — headless cloud, your browser, or your device?** Browserbase (invisible infra), Dia (the browser itself), Zo (a personal server), and Bee (a wearable) are four incompatible answers, and the category hasn't picked a winner.
3. **Who bears the security consequences of agents in logged-in sessions?** Yutori's on-device credentials, Dia's browser-level memory of everything you do, and Bee's always-on audio all outrun the governance patterns in the papers above.
4. **Can vendor-run benchmarks be trusted as the buying criterion?** Yutori grades itself on its own (open-sourced) Navi-Bench; Cua's founders built the benchmarks their product now runs. Independent evaluation of computer-use agents barely exists.
5. **Is there a business under the OSS?** Stagehand and Cua's stack are MIT-licensed; the managed clouds are the moat — but Cua's ~$500K funding and Yutori's unquantified consumer traction leave the revenue question open outside Browserbase.
