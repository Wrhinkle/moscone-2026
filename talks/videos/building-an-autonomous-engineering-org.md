# Building an Autonomous Engineering Org
> Angie Jones on moving Block's 3,500-person engineering org to stage-five agentic delivery through a champions program, AI-ready repos, and an internal orchestrator.

- **Speaker:** Angie Jones, Agentic AI Foundation
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=whue9_YquGA) (AI Engineer channel; ~18m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Angie Jones recounts spending two years turning Block's 3,500-person engineering organization into an autonomous one. Block started early, building its internal coding agent Goose before LLMs supported tool calling, partnering with Anthropic on the initial MCP release, and making Goose the reference MCP client implementation. Within months about 90% of engineers were using Goose and Claude Code regularly. On paper Block was all in on AI, but the CEO insisted engineering was not using it because features were not shipping faster. Jones had the metrics and the token bills to prove usage, yet he was right that delivery had not sped up: engineers were using AI inside their IDEs for questions and boilerplate, stuck in what she calls the experimentation phase rather than the impact phase.

She defines an agentic engineering org as one where engineers use agents as their primary means of producing outcomes, decomposing problems, delegating, and reviewing rather than writing code themselves. To map the distance to that goal she built a maturity model, later reorganized with help from Steve Yegge's "Gastown" article, running from stage zero (no AI in the workflow) through autocomplete, chatting, delegating with review, parallel agents, up to stage five where engineers delegate complete tasks and agents produce shippable results without hand-holding. Mid-2025 most engineers sat between stages one and two, and she needed them at five.

Rather than level up all 3,500 engineers, Jones leaned on the 1-9-90 rule and formed the 1%. She handpicked about 50 AI champions from critical repositories who could commit at least 30% of their time and would not quit when the non-deterministic tools failed out of the box. Their first job was making repos AI-ready: context and rules files, repeatable workflows as slash commands and later agent skills, an AI code reviewer, and AI attribution on PRs, all customized per repo. Mono-repos leaned on JVM inheritance patterns with root-level context and service-level overrides, and mobile needed different approaches than web. Then champions wired delegation into where work already arrives, Jira, Linear, GitHub issues, and Slack. Her Slack story: an engineer flags a bug, another @-mentions Goose, Goose pulls the repo, confirms the bug, offers three fixes, the team picks one, and Goose returns a PR, the whole cycle in about 5 minutes.

Three months in, AI-authored code was up 69%, reported time savings up 37%, and automated PRs up 21x. Stage four, multi-agent parallelism, came almost free but exposed a review bottleneck, so Block enabled Codex everywhere with an auto-fix loop where one agent fixes what another flags, and moved agents into dedicated isolated cloud workspaces after laptops ran out of memory. For stage five, champions built an orchestrator called Builder Bot backed by a machine-readable world model of all 25,000 repos, letting agents pull cross-repo context and plan across products. Anyone at the company could then invoke Builder Bot in Slack to fix a bug or ship a feature without touching GitHub. Jones ends on a somber turn: the success was followed by layoffs, and she leaves the audience with open questions about whether enabling this work led to people's dismissal and where the industry is heading.

## Notable moments
- [0:03:01](https://www.youtube.com/watch?v=whue9_YquGA&t=181s) The stage-zero-to-five maturity model for an engineer's relationship with agents.
- [0:05:02](https://www.youtube.com/watch?v=whue9_YquGA&t=302s) Using the 1-9-90 rule to form a 50-person AI champions program instead of leveling everyone.
- [0:10:10](https://www.youtube.com/watch?v=whue9_YquGA&t=610s) The Slack story where Goose diagnoses a bug and returns a PR in about 5 minutes.
- [0:15:13](https://www.youtube.com/watch?v=whue9_YquGA&t=913s) Builder Bot and the machine-readable world model of 25,000 repos that reached stage five.

## Connections
- [Block](../../companies/enterprise-adopters/block.md) is the org whose Goose agent and autonomous transformation this talk documents.
- [How AI Coding Agents Shape Software Architecture](../../papers/planning-architecture/how-ai-coding-agents-shape-software-architecture.md) speaks to the repo-readiness and world-model structure Block built for agents.
- [Session recaps](../../notes/session-recaps.md) hold the in-person threads on agentic SDLC and coding-agent adoption this talk extends to org scale.
