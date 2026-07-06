# Your Attention Is the Bottleneck, Not Your Agents

> A WorkOS applied AI engineer on staying sane while running parallel agents: signal layers, voice-first input, remote control from the trail, and mining your own transcripts for missing skills.

- **Speaker:** Zack Proser, WorkOS
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=so9l_MwS2yg) (AI Engineer channel; ~25m, released 2026-06-11)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Proser, on WorkOS's Applied AI team, opens with a show of hands: who codes with agents and feels fried by 11 a.m. despite shipping more than ever? His diagnosis is that agents scale infinitely, verification criteria and tools can be handed to them, but human attention still degrades under load and is now the hard constraint. He cites Simon Willison saying he runs four parallel agents and is wiped out by 11 a.m. The anchor story is a Slack bot he built that lets anyone at WorkOS request a uniform blog post; a colleague reported that its sentence-case pass was mangling acronyms like SCIM and SSO. Instead of fixing it across a wall of windows, he gave Claude Code read and write access to Slack alongside his existing Linear access and told it to fix the bug and verify its own work end to end. The agent fixed the code, fired a test request into the Slack channel, watched the bot process it, and confirmed the fix before he returned. He found the completed loop both thrilling and scary, since there is no ceiling: the tools are nuclear and our nervous systems are ancient, so nothing stops you burning yourself out fixing 150 bugs a day.

His stack for staying balanced has four layers. Signal layers put an agent between you and the noise: Claude Code reads his Slack on a loop for mentions and real asks and deduplicates them against Linear, because if he combed Slack himself there is an 80 percent chance a thread derails him. Voice-first flows: after a year and a half of voice coding he hits 184 words per minute against his old 90 typing, which lets him prompt across multiple Cursor, Codex, and Claude windows before a typing developer finishes one prompt. Remote control: Claude Code's remote control flag lets a session running on his dev machine stay reachable from his phone miles away, which turns the shower principle, diffuse-mode insight arriving once you leave the desk, into working time; he filmed a 32-minute proof that you can review PRs from the woods. Verification gates make that safe, in levels: lint, build, and unit tests via hooks; browser click-through checks; then constitution-style review where a second agent verifies the first followed the rules. Fourth, the system improves itself: since Claude Code saves every conversation as local JSONL, a scheduled weekly pass reviews his own transcripts for places where he and the agent burned thinking tokens fighting ambiguity, then proposes the skills or MCP servers that would tighten the loop next week.

The rest is texture and Q&A. He connected his Oura ring by MCP, so Claude sometimes refuses the full task list on no sleep. He tells an early-career questioner not to use AI for anything you cannot already do yourself, since his years of hand-built TypeScript and AWS scar tissue are what let him catch hallucinations instantly. On overnight work he runs OpenClaw on cron jobs producing content he reviews and mostly rejects each morning, and describes a target end state of Linear tickets tagged agent-ready with a loop churning every 15 minutes around the clock. His prescription: build one signal layer, add verification gates, and spend the reclaimed margin on a walk rather than more output, because the default path is burnout turbo.

## Notable moments

- [0:01:14](https://www.youtube.com/watch?v=so9l_MwS2yg&t=74s) The sentence-case bug fixed end to end: Claude Code patches the code, posts to Slack, watches the bot run, and verifies its own fix.
- [0:03:15](https://www.youtube.com/watch?v=so9l_MwS2yg&t=195s) The thesis: agents are no longer the bottleneck, attention is, with Simon Willison wiped out by 11 a.m. as evidence.
- [0:09:18](https://www.youtube.com/watch?v=so9l_MwS2yg&t=558s) Remote control turns the shower principle into work time: leaving the desk no longer means stopping work.
- [0:13:22](https://www.youtube.com/watch?v=so9l_MwS2yg&t=802s) The weekly self-improvement pass: an agent mines his own JSONL transcripts for friction and proposes the missing skills.

## Connections

- [WorkOS](../../companies/security-identity/workos.md) is the speaker's company, whose Applied AI team workflows the talk draws on.
- [Session recaps](../../notes/session-recaps.md) record verification discipline for agent-written code as a recurring in-person theme, the same gates Proser layers under his remote workflow.
