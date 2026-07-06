# Dark Factory: OpenClaw Ships Faster Than You Can Read the Diff

> An OpenClaw core maintainer explains the working process behind a project that peaked at 800 commits a day, and argues that engineers are becoming factory managers for agent swarms.

- **Speaker:** Vincent Koc, OpenClaw
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=pmoDeA3RBZY) (AI Engineer channel; ~17m, released 2026-06-05)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Koc is one of 10 to 15 core maintainers on OpenClaw, all with day jobs, and the numbers frame the whole talk. The project peaked at 800 commits a day. On March 15 he personally hit close to 3,000 commits in a day, enough that GitHub rate limits him hourly, and his commit history maps his sleep schedule. He argues this is not luck or Ralph looping to the max. There is engineering underneath, and he compares the moment to the Industrial Revolution: handlooms in cottages gave way to centralized mills, and the bottleneck moved from the weaver's hands to the factory manager. In his version, engineers stop writing code in editors, swarms run across repos, and the bottleneck becomes taste.

The centerpiece story is what the team calls the great refactor. During a session at Nvidia's offices, where he and fellow maintainer Peter were helping build Nemo Claw, another maintainer moved entire messaging channels to a new location in the codebase. At 2 a.m. the team decided to refactor the whole project into a plugin architecture, so that a provider like OpenAI or Anthropic could own its own piece of the code. The result: 2,700 commits, close to a million lines changed, 82 percent of the core codebase touched. Koc says the saving grace was the overfitting unit tests that AI code generation loves to produce; when everything was ripped apart, green runs on those overfit tests signaled the pieces were still roughly in place. The motivation was bloat control. When tokens are cheap you can merge everything, so the hard job is deciding who to say no to.

His day-to-day setup, which he calls his factory, is 5 to 20 swim lanes of Codex sessions divided by work type: low-supervision lanes for test refactors, conversational lanes for features and bugs, and lanes watching new P0s and P1s, including agents that live in a Discord channel and summarize the last two hours before a release. During the Nvidia session he and Peter ran maybe 15 foreground sessions and up to 60 or 70 agents counting subagents. He regrets adopting Git worktrees, since he ends up with 70 or 80 active ones a day and says cloning the repo ten times would have been simpler. He uses no plan mode or spec mode, just conversation. Quality control is intuition built from a year of token maxing: he judges a session by how it explains itself, and when an agent starts waffling like an employee bullshitting a manager, he nukes the session.

There is process beyond vibes. He maintains a versioned library of skills, dot skills alongside dot files, both on GitHub, and runs a skill that reads Codex session logs and improves the other skills. The team built semantic graph embeddings over roughly 60,000 GitHub PRs and issues to deduplicate demand and treat clustered pressure as a roadmap signal. After the refactor they built a fake Slack with synthetic and real models to run evaluation loops against every provider and channel. When people ask how he manages 10 plus agents, he asks back how they manage 10 plus staff, and argues the soft skills of management transfer directly. His closing line: 2025 was about token maxing, 2026 is about not wasting them.

## Notable moments

- [0:04:18](https://www.youtube.com/watch?v=pmoDeA3RBZY&t=258s) The scale numbers: 800 commits a day at peak, Koc's personal 3,000-commit day, Anthropic's C compiler work and Steve Yegge's 50 solo PRs a day as evidence the norm is shifting.
- [0:08:20](https://www.youtube.com/watch?v=pmoDeA3RBZY&t=500s) The great refactor: 2,700 commits and near a million lines changed at 2 a.m., rescued by overfit AI-generated unit tests.
- [0:11:24](https://www.youtube.com/watch?v=pmoDeA3RBZY&t=684s) The Matrix analogy: after enough volume you can feel the reasoning tokens, and a session that waffles gets nuked.
- [0:15:24](https://www.youtube.com/watch?v=pmoDeA3RBZY&t=924s) "How do you manage 10 plus agents?" answered with "How do you manage 10 plus staff?", and the closing pivot from token maxing to token efficiency.

## Connections

- [NVIDIA](../../companies/models-inference/nvidia.md) hosted the session where Nemo Claw was built and the great refactor started.
- [Effective strategies for asynchronous multi-agent collaboration](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md) studies the parallel-agent coordination problem Koc manages by hand with swim lanes.
- [Session recaps](../../notes/session-recaps.md) record the Vercel conversation asking how to run a thousand-agent team without going broke, the question this talk answers at smaller scale.
