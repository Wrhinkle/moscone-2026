# I Run a Fleet of AI Agents Across Three Machines. Here's What Broke.

> A field report on running a daily fleet of coding agents across a MacBook and two Linux boxes, the five failures that followed, and why Kubernetes is the next layer down.

- **Speaker:** Kyle Jaejun Lee, KRAFTON
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=4kYl2_mqmnQ) (AI Engineer channel; ~9m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Lee runs a fleet of AI coding agents every day across three machines: a MacBook for heavy coding, an always-on Linux box for long-running coding tasks, and a second Linux box for short-lived side projects, all under one control plane. He stresses this is his actual daily setup, not a demo built for the talk. The first thing that broke was him. With four to six live tmux contexts open, he had become the scheduler, the memory, and the reviewer for the whole fleet, and one human in three roles across six contexts does not scale.

His fix borrows from how executives run companies of thousands: separate context so each person sees only their slice. He built a real hierarchy of entity types, CEO, VP, manager, worker, each an agent with its own scoped context and approval boundary. Context flows down, results flow up, and Lee reviews only what reaches the top, holding one context instead of six. State moved out of the model too. Every entity gets a workspace on disk with its mission, current status, and a handoff folder; shared context lives in a shared directory and machine-bound state under machines. Lee calls the consequence the most practical thing he learned all year: he stopped compacting context. Compaction is slow, he cannot choose what survives, and what it discards is gone. Instead he clears the context completely and lets the agent read back its own handoff and history files, so a wiped context or even a machine crash never loses the work. Plan drift got a review gateway: any layer that wants to act submits a plan and blocks until Lee approves from a single web inbox, at which point a hook fires the work off. An infra team of agents inside the fleet built the gateway itself.

Then one machine stopped being enough, and five things broke. Orchestrators did work themselves instead of dispatching, until a CLI harness with skills made delegation the only available path. Managers spawned so many worker panes in one window that tmux capture-pane could not read them. Claude Code and MCP processes buried the activity monitor and nearly filled swap. Git credentials crossed over between workspaces until each got a fully separated environment. And the MacBook, being a laptop, once restarted itself under load and killed every in-flight job, which led to a one-command boot that restores the whole fleet from the state files.

Moving to three machines raised new problems. Context moves between machines by committing the files to git and poking the remote machine over SSH with tmux send-keys to pull. Divergence between machines forced per-machine directories, with shared state changed only through pull requests. Per-machine review gateways collapsed into one main gateway on an always-on Linux box, since a control point cannot live on a machine that sleeps. After losing track of which machine he had built a feature on, Lee made Discord the single router, one bot per machine, so his phone is the remote control for the fleet.

He closes with four unsolved problems: consistency across machines, abstracting Mac-only tools like MCP servers and the browser, secure credential handoff, and resource management. He argues these are the questions Kubernetes already answers, so he is stacking Kubernetes underneath for compute, secrets, and tools and building the orchestration manager, review flow, and context management on top.

## Notable moments

- [0:01:00](https://www.youtube.com/watch?v=4kYl2_mqmnQ&t=60s) One human as scheduler, memory, and reviewer across six live contexts, the bottleneck that started the project.
- [0:02:02](https://www.youtube.com/watch?v=4kYl2_mqmnQ&t=122s) State moves to files on disk, and Lee explains why he resets context instead of compacting it.
- [0:04:04](https://www.youtube.com/watch?v=4kYl2_mqmnQ&t=244s) The five failures begin, from orchestrators refusing to delegate to an out-of-memory MacBook.
- [0:07:07](https://www.youtube.com/watch?v=4kYl2_mqmnQ&t=427s) Discord becomes the single router, one bot per machine, phone as fleet remote control.

## Connections

- [HumanLayer](../../companies/agent-orchestration/humanlayer.md) productizes the same pattern as Lee's review gateway, human approval as a blocking control point for agent fleets.
- [Superconductor](../../companies/swe-infrastructure/superconductor.md) sells a cloud workspace for running and reviewing parallel coding agents, the hosted version of what Lee hand-built.
- [Session recaps](../../notes/session-recaps.md) records Vercel's open question about running a thousand-plus agent team without going broke, the scaled form of Lee's problem.
