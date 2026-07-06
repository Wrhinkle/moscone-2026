# The Log Is The Agent

> Argues an agent's identity lives in its append-only event log, not the model or runtime, and builds an architecture on that claim.

- **Speaker:** Ishaan Sehgal, Omnara
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=UPwGaM2MKHY) (AI Engineer channel; ~15m, released 2026-06-25)
- **Program:** Online Track 2026

## Summary

Ishaan Sehgal, CEO of Omnara, opens with a Skyrim analogy: your hundred-hour character is not the game engine, the console, or the controller, it is the save file. If the PlayStation burns down, you restore the data and resume. He applies the same inversion to agents. The model and the runtime matter, but the agent is its data, specifically an append-only log of every user input, model output, tool call, tool result, permission, and failure. Every state transition gets written; everything else in the system just reads from and appends to that log.

Sehgal argues this makes the agent loop disposable. A worker can claim a session, reconstruct state from the log, advance the agent one step, write the result, and vanish; any other worker can pick it up later. He draws the precedent from databases: underneath every serious database is a log of changes, and tables, indexes, and materialized views are projections of it. For agents, the context fed to the model, the rendered UI, debugging, auditing, and compaction are all projections; only the log is the durable history.

He answers two objections. On compaction, context windows are finite, so the log must eventually be summarized, but a compaction is lossy, so it is a projection, a best-effort fork you can resume as a new log. Keep the raw log and you can always generate new projections; keep only the compaction and you have lost part of the agent. On external state, an agent edits files and sends emails, and forking the log will not unsend an email. The log is not the world, it is the agent's view of the world, just as a Skyrim save stores player state, not the game engine.

The payoff is a list of properties that fall out structurally. Reliability: he cites Claude Code losing a pending permission prompt when the process dies mid-session, which he calls unacceptable in production; with a log-first design a new worker reconstructs state and the prompt is still there. Scalability: instead of one process per agent, one process can advance thousands of agents, making failover trivial with no sticky sessions or state migration. Forking: branch the log and run one branch on Claude, another on GPT, another on an open model. Multiplayer: sharing an agent means granting access to its history rather than pasting transcripts into Slack. Migration: if identity lives in provider-specific threads, moving is painful; if the log is the agent, migration is an adapter problem, and an agent can start on Claude, continue on GPT, and finish on Qwen.

Sehgal then criticizes current harnesses for treating the log as exhaust: Claude Code and Codex write fire-and-forget JSONL to local disk, and OpenCode's SQLite state has GitHub issues about corruption and data loss. His sharpest claim is about ownership: the deepest lock-in is not model or API lock-in but log lock-in. As Anthropic and Google push managed agents, whoever hosts your log, which records your personal data, workflows, and decisions, effectively owns your agent. Omnara's answer is an open source managed agents platform where workers, model calls, and sandboxed tools all coordinate around a session log the user fully owns and can inspect, launching at omnara.com/managed.

## Notable moments

- [0:00:14](https://www.youtube.com/watch?v=UPwGaM2MKHY&t=14s) The Skyrim save file analogy that frames the whole talk.
- [0:03:01](https://www.youtube.com/watch?v=UPwGaM2MKHY&t=181s) The loop is disposable: workers claim, advance, and abandon sessions, echoing how databases are logs underneath.
- [0:06:50](https://www.youtube.com/watch?v=UPwGaM2MKHY&t=410s) Claude Code's vanishing permission prompt as the failure mode of runtime-centric agent design.
- [0:11:05](https://www.youtube.com/watch?v=UPwGaM2MKHY&t=665s) Log lock-in: whoever owns your log owns your agent, aimed at managed-agent offerings from Anthropic and Google.

## Connections

- [Temporal](../../companies/agent-orchestration/temporal.md): durable execution built on replayable event histories, the same log-first pattern Sehgal advocates for agents.
- [Inngest](../../companies/agent-orchestration/inngest.md): event-driven durable workflows occupying adjacent territory for surviving worker crashes and restarts.
- [Are we ready for an agent-native memory system?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): research framing of the same question of what durable state an agent should carry.
