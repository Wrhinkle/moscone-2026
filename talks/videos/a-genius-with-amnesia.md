# A Genius With Amnesia
> Why coding agents are constrained in space (one repo) and time (no memory), and how Nx's Polygraph meta-harness gives any agent a unified multi-repo graph and shared session memory.

- **Speaker:** Victor Savkin, Nx
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=jVjt-2g8NMY) (AI Engineer channel; ~20m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary
Victor Savkin opens with a genie analogy: you wish for the best engineer and get John Carmack, but he can only see one thousandth of your codebase and remembers nothing between conversations. That, he argues, is what agents are: a genius on one side, something deeply deficient on the other. He walks through a worked example with four repos (a UI library, two modules, a platform) where one conceptual change requires seven separate explanations, including re-explaining the original change when the published library breaks a consumer and again a week later when a production bug appears, often across different people, with developer time and tokens burned each time.

Savkin sorts the causes into two categories. Space: agents are repo-bound, so they never see the system, cannot align a change with downstream consumers, cannot reach best practices that live in other repos, and cannot validate or update consumers even when, at the moment of the change, they hold perfect information to do so. Changing something across 20 repos means re-explaining it 20 times. Time: agents have no episodic memory, every session starts blank, and the human becomes the memory. He sharpens the point with a thought experiment: an agent that could see one file at a time and five messages back would be considered impossible to work with, and what we have now is similar.

The fix is Polygraph, an agent-agnostic meta-harness Nx built. It analyzes every repo a GitHub user can reach, owned and open source (Savkin's own graph covers about 300 owned repos and thousands of dependencies), extracting what each project produces and consumes, package-wise and API-wise, without changing a line of code. That metadata creates the illusion of one large codebase any agent can read and write. A session pulls in the relevant repos, sets up source, dependencies, and one agent per repo wired together, and treats a multi-repo change like a single-repo change: multiple pull requests, CI treated as one vector, and when one repo's CI fails Polygraph works out whether that module needs a patch or the upstream component broke everyone.

The same machinery fixes memory. Polygraph captures intent, repos, PRs, and full agent traces for every session, then relates them. Savkin demos resuming his session on a coworker's machine: same repos, same SHAs, agents primed with his traces, even though he used Claude and the coworker picked Codex, which he compares to a Star Trek transporter. He reviews PRs by resuming the author's session and interrogating the agent about decisions instead of asking the person. Referencing an old session plus "there is a bug" is enough for the agent to reconstruct state and fix it. Sessions and repos can also be selected by query: update every repo depending on a library version, or find past sessions relevant to adding a vector index and replicate the approach of an engineer you respect. Because sessions cross developer boundaries, every agent draws on the whole organization's work, which Savkin likens to a hive mind. The project lives at try.polygraph.com.

## Notable moments
- [0:00:04](https://www.youtube.com/watch?v=jVjt-2g8NMY&t=4s) The genie analogy: Carmack with 1/1000 visibility and no memory.
- [0:02:05](https://www.youtube.com/watch?v=jVjt-2g8NMY&t=125s) Seven explanations for what is essentially one change across four repos.
- [0:06:08](https://www.youtube.com/watch?v=jVjt-2g8NMY&t=368s) Polygraph introduced: a unified dependency graph over every repo you can reach.
- [0:12:10](https://www.youtube.com/watch?v=jVjt-2g8NMY&t=730s) Resuming a session on another machine with a different agent, traces and state intact.

## Connections
- [Sourcegraph](../../companies/coding-agents/sourcegraph.md) built its business on the same cross-repo code visibility Polygraph now packages for agents.
- [Are we ready for an agent-native memory system?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md) treats the episodic-memory gap Savkin calls amnesia as a research problem.
- [Session recaps](../../notes/session-recaps.md) shows memory beyond a single session recurring across the in-person program, from GraphRAG traversal to world models for long-running agents.
