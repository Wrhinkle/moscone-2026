# What Does Done Even Mean? Agents and Paperclip's Liveness Model

> Why "done" is a bundle of operational claims rather than a checkbox, and how Paperclip's control plane balances liveness against verification for agent task fleets.

- **Speaker:** Dotta, Paperclip
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=7P0elyLIxXo) (AI Engineer channel; ~7m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Dotta, creator of Paperclip, opens with an agent that opens a pull request, passes the tests, updates the docs, closes the issue, and comments "Looks done to me." Done enough to merge, to deploy, and to announce to customers are fundamentally different operational claims, and most agent systems flatten them into a single green check mark. The talk's premise is that agents now produce more code and documentation than any human can verify, which creates a new failure mode: agents create more work than humans have time to check.

Dotta's core move is to unbundle "done." Claiming completion actually asserts that an artifact was produced, that evidence exists, that there is a rubric to verify against, that the owner of the next step is known, and that the next step itself is known. There are also levels of doneness: the producer claims completion, a reviewer finds no obvious issues, the evidence meets a specified standard, someone authorized approves it, someone stands behind the decision, and ideally the outcome survives real-world conditions. Exhaustive human verification fails at volume; if humans must sign off on every task, the result is what Dotta calls verification theater.

The design problem is a tension between two properties. Human review gives assurance of correctness but stops the task dead. Liveness means work continues with no blockers. All liveness and no approval produces AI slop, a large output with no quality control that Dotta argues is worse than producing nothing. All review produces a queue humans cannot clear. A for loop over a task manager falls apart as soon as dependency trees, blockers, multiple agents, and idempotent checkouts with locks enter the picture. Dotta names three invariants for an agentic control plane: productive work continues, only real blockers stop work, and infinite loops are bounded.

Paperclip's mechanisms follow from the invariants. Every task has explicit transitions to valid next states. Blockers between tasks are first class and enforced by the control plane. Interactive human approvals leave an audit trail. Reviewers and approvers can be set on tasks explicitly, so completion can trigger review by another agent. Watchdogs are a maximizer mode: a separate agent given a goal that keeps all other agents working until the goal is achieved. The watchdog is harness agnostic, one interface whether the underlying agents run in Claude Code, Codex, or other harnesses.

The closing advice is portable beyond Paperclip: treat done as an object, not a Boolean, with fields for artifact, scope, rubric, evidence, verifier, sign-off authority, remaining risk, and next action. Dotta's checklist for getting 100 times more work done: define done precisely per task, separate the verifier from the author, ideally using a different model, so Claude-written code gets verified by Codex; require evidence rather than a yes, giving agents browsers, screenshot tooling, and hooks to click through and test their own work; and keep a clear chain of custody so every agent knows who receives the work next.

## Notable moments

- [0:00:00](https://www.youtube.com/watch?v=7P0elyLIxXo&t=1s) The opening: merge, deploy, and announce are different claims that agent systems flatten to one green check.
- [0:02:00](https://www.youtube.com/watch?v=7P0elyLIxXo&t=120s) The liveness-versus-verification tension: human review means assurance, but the task is dead in its tracks.
- [0:04:01](https://www.youtube.com/watch?v=7P0elyLIxXo&t=241s) Three control-plane invariants and Paperclip's mechanisms, including harness-agnostic watchdog agents.
- [0:06:05](https://www.youtube.com/watch?v=7P0elyLIxXo&t=365s) The checklist: separate verifier from author, demand evidence, keep a chain of custody.

## Connections

- [HumanLayer](../../companies/agent-orchestration/humanlayer.md) builds the human-approval and review layer for agent fleets that Paperclip's approval and audit-trail mechanisms overlap with.
- [Temporal](../../companies/agent-orchestration/temporal.md) is the durable-execution incumbent for keeping tasks in valid states, the substrate Paperclip's control plane competes with for agent workloads.
- [Effective Strategies for Asynchronous Multi-Agent Collaboration](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md) studies the same coordination problem, gating merges with tests and dependency graphs instead of a liveness model.
