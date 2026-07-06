# Develop at Idea Velocity

> A hands-on workshop walking through a Slack-driven OpenClaw setup that turns brief messages into orchestrated fleets of Claude Code workers.

- **Speaker:** Jeffrey Lee-Chan, Snapchat
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=9arM9b7JgOo) (AI Engineer channel; ~15m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

This is a workshop recording rather than a stage talk. Lee-Chan opens by splitting the room between people who have never installed OpenClaw and advanced users who want to try an experimental staging setup running two OpenClaw instances at once. His daily loop, which he says works maybe 70% of the time, is describing a task in a brief Slack message and letting OpenClaw's context and memory fill in the rest. Telling it "fix the skeptic agent," his custom code-review project, works because the system remembers prior conversations, so nothing needs re-explaining. He runs multiple agents in git worktrees for parallelization and notes his own replies to the system are ordinary enough that he thinks an agent could replace him, which is what he is building toward next.

His stack diagram has three layers. The top is frictionless communication, the ability to talk to your AI from Slack instead of remote-desktopping into a machine. The middle is the orchestration axis, ranging from OpenClaw's agent-orchestrator managers that run workers automatically to terminal sessions he drives himself when he wants personal control, using a forked open-source agent-orchestrator framework for the workers. The bottom is what he calls managed agents: workers run Claude Code, which spawns its own agents and sub-agents, a layer he treats as someone else's stack.

Asked why OpenClaw instead of Claude Code directly, Lee-Chan answers specialization of context. Opening Claude Code loads CLAUDE.md files, skills, and MCP servers, so around 25% of the context window is spent on how to implement before the task even starts. OpenClaw's context is the spec, the goals, and the history of related Slack messages from the past two weeks. He adds that agents have improved fast at browser-based verification: a year ago his agent struggled to find a pop-up and enter a password, and now visual browser tests mostly work unattended.

He demos two projects built this way: an AI RPG that generates a reactive custom world with a D&D-style dice system so players cannot simply win by narrating, and a multi-AI analysis site that fans a question out to several models and synthesizes the answers, which he prefers to any single model's reply. A manager-versus-worker observation follows: an agent working on PR 294 alone would have declared it amazing and pushed to merge, while the manager with different context concluded another PR superseded it and it should be closed. Lee-Chan credits the vertical tabs and notification queue of cmux, and Austin, one of its creators, speaks briefly about shipping a Claude Code Teams integration and cmux SSH for reaching remote machines, including OpenClaw instances on Mac minis. On models, Lee-Chan defaults to Codex 5.3, finds GPT-5.4 burns more tokens, and falls back to MiniMax when his quota runs low, a choice he frames as about money rather than preference. He closes the excerpt distinguishing Docker-style sandboxing from his staging pattern: local development, integration tests on a staging instance, then merge and deploy to the production instance, which raises token usage but buys reliability.

## Notable moments

- [0:01:02](https://www.youtube.com/watch?v=9arM9b7JgOo&t=62s) The 70%-of-the-time happy path: brief Slack messages plus memory, agents parallelized in git worktrees.
- [0:05:12](https://www.youtube.com/watch?v=9arM9b7JgOo&t=312s) Why OpenClaw over raw Claude Code: about 25% of context is spent on implementation setup before the task starts.
- [0:10:24](https://www.youtube.com/watch?v=9arM9b7JgOo&t=624s) The manager agent, holding different context, recommends closing PR 294 instead of merging it.
- [0:11:24](https://www.youtube.com/watch?v=9arM9b7JgOo&t=684s) A cmux creator on the Claude Code Teams integration and cmux SSH for remote machines.

## Connections

- [MiniMax](../../companies/models-inference/minimax.md) is Lee-Chan's budget fallback model when his Codex quota runs out, a working example of cost-driven model routing.
- [Session recaps](../../notes/session-recaps.md) records the Vercel conversation about what OS and system agents need and how to run large agent teams affordably, the questions this workshop answers at personal scale.
