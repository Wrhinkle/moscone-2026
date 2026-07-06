# BDD, ADR, PRD, WTF: Capturing Decisions for Humans and AI Alike

> Michal Cichra argues that written decision records plus an enforcement loop of git hooks, linters, and CI are what keep both human teams and coding agents consistent.

- **Speaker:** Michal Cichra, Safe Intelligence
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=504PvfXou5Y) (AI Engineer channel; ~13m, released 2026-06-03)
- **Program:** AI Engineer 2026 release, program placement unconfirmed. Internal evidence points to the AI Engineer Europe Summit in London: Cichra opens by saying Safe Intelligence released Spec27 "yesterday," and Spec27 launched there on April 8, 2026.

## Summary

Cichra opens with the five-monkeys story: monkeys punished for climbing a ladder keep enforcing the rule on newcomers long after every original monkey is gone, and none of them knows why. His point is that humans and LLMs share the same trait of limited context. People forget and leave; LLM context compacts and resets. Eventually every team asks why a flow exists or why code is shaped a certain way, with no founding engineer around to answer. Before Safe Intelligence, where his team had just released Spec27, an agent-testing product, he spent time at Microsoft and Red Hat and ten years on a single product, and says these consistency problems appeared in every product he has seen, arriving faster now with AI.

His answer is three document types plus enforcement. Architecture decision records (ADRs) capture why a rule exists and how it is enforced: his examples include splitting code into layers to prevent N+1 queries, enforced by linting module imports, and requiring database reads to return plain shapes instead of ORM objects. His product carries about 50 ADRs, each scoped to specific files and paired with a tool that rejects violations and links the offender back to the document, so an agent that trips a rule can read the reasoning and fix the code. Product requirements documents (PRDs) stay light: the why, the problem, the goal, and the user journey, useful to the agent and to yourself six weeks later. For validation he revives behavior-driven development via Cucumber, "almost forgotten, suddenly useful again." Spec-driven development leaves a gap, he argues: a markdown spec describes behavior but nothing proves the product follows it, and the only thing harder than reading AI code is reading AI tests. Executable, human-readable BDD scenarios connect directly to PRDs and close that loop. A design system gets the same treatment: document the language (a primary button is blue, this shape, this size), state rules like one primary button per page, build component previews agents can see, and compose upward.

Enforcement runs through what he calls the loop: git hooks, skills, CI, and linters running the same predefined tasks locally and in CI, so a lazy agent that skips hooks gets caught. Checks cover linting, formatting, type checking, code duplication, architecture, and document linting. Code review used to argue about tabs and spaces; now those matters are automated rules with no space for discussion, and review moves to high-level concepts. Architecture enforcement is preventive: the end-to-end BDD suite is forbidden from importing any database module, and rendering templates cannot talk to the database, so N+1 queries cannot exist rather than needing to be found. The loop stays constant while skills change its focus: an ADR skill, a PRD skill, a UI loop that skips checks in favor of fast browser iteration, and a test skill that picks a focused subset of the suite from coverage and file changes. The cost is context: research can burn half the window before work starts. Cichra says he no longer fears compaction, reporting sessions with 20 to 50 context compactions that still work because the important decisions live in documents the agent will look up again. He closes with "may the spec be with you."

## Notable moments

- [0:00:07](https://www.youtube.com/watch?v=504PvfXou5Y&t=7s) The five-monkeys parable as a model for context loss in teams and LLMs alike.
- [0:04:08](https://www.youtube.com/watch?v=504PvfXou5Y&t=248s) The gap in spec-driven development, and Cucumber BDD as the executable layer that closes it.
- [0:07:09](https://www.youtube.com/watch?v=504PvfXou5Y&t=429s) The enforcement loop: git hooks and CI run identical checks so agents that skip them get caught.
- [0:11:13](https://www.youtube.com/watch?v=504PvfXou5Y&t=673s) Sessions surviving 20 to 50 context compactions because decisions persist in lookup-able documents.

## Connections

- [Safe Intelligence](../../companies/evals-observability/safe-intelligence.md): Cichra's company; the Spec27 agent-testing product he mentions at the top is profiled there.
- [Session recaps](../../notes/session-recaps.md): Sonar's in-person session pushed the same verification discipline, hook-triggered context injection and zero-trust review of agent code.
- [How AI Coding Agents Shape Software Architecture](../../papers/planning-architecture/how-ai-coding-agents-shape-software-architecture.md): studies the architecture-drift problem Cichra's ADR-plus-linting regime is built to prevent.
