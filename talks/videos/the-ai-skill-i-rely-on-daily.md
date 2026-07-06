# The AI Skill I Rely On Daily
> A Sentry engineer measures her own AI usage, finds 67% of it is codebase comprehension rather than generation, and builds a "catch me up" skill around that fact.

- **Speaker:** Priscila Andre de Oliveira, Sentry
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=li0SaBt9RDM) (AI Engineer channel; ~17m, released 2026-05-27)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Oliveira, a senior software engineer at Sentry, Verdaccio maintainer, and ViennaJS co-organizer, describes her shift since December 2025 to prompting instead of writing code by hand, a role she jokes is now agent manager. Her recent Sentry contributions with Claude span bug fixes, features, refactors, and cross-repository changes, and even the talk's slides were built with an AI skill. The context matters: Sentry's codebase dates to 2010, carries 15-plus years of history, serves around 100,000 organizations, has roughly 400 employees, and merges about 100 PRs a day, so components, lint rules, and conventions shift constantly. Come back from vacation and your PR is full of conflicts.

She surveys Sentry's internal AI tooling from a recent hackathon: Abacus tracks internal AI usage, Warden reviews PRs, Junior is a Slack bot that turns a bug-report thread into a PR, and an AI SDK testing repository she was told to contribute to by prompting only, never editing code directly. She also notes a three-month quality quarter spent removing TypeScript any types, stale TODOs, and unused feature flags, her evidence that Sentry is going all in on AI while still treating quality as the constraint. She does not want to ship slop into the codebase that pays her salary.

The core of the talk is a measurement. Because her prompts kept repeating, she had Claude analyze 116 of her own sessions and classify them into six categories. The result surprised her: 67% of her AI usage was comprehension and only 2% was code generation. Her claim follows: in a large codebase the biggest unlock from AI is comprehension, and generation is a rounding error. Speed gains come from things like replacing a manual git blame hunt after an incident, or a cross-timezone Slack question about a product decision, with a prompt answered in seconds.

Out of the repeated prompts she built a local skill called catch me up, a detailed markdown prompt that structures comprehension questions into six exploration modes: architecture, convention, feature trace, syntax, testing, and history. It renders answers visually, with structure diagrams and tables, which suits how she works on Sentry's front end. The demo shows her onboarding to the unfamiliar AI SDK testing repository, asking whether it simulates Sentry envelopes; the skill answers that it intercepts real ones by spawning a collector. She also uses it to build enough context to review colleagues' PRs. She endorses the research-plan-implement workflow from Jack Nation's "vibe coding our way to disaster" post but argues it is missing a step: you have to understand the agent's research yourself so you can steer it before planning. She closes citing Armin Ronacher's worry about people no longer knowing what code is in their own codebases, and advises tracking your own AI usage, aligning your mental model before prompting, and treating AI as the teammate who never tires of questions.

## Notable moments
- [0:04:12](https://www.youtube.com/watch?v=li0SaBt9RDM&t=252s) Sentry's internal agent tooling: Abacus, Warden, and the Junior Slack bot that turns complaint threads into PRs.
- [0:09:18](https://www.youtube.com/watch?v=li0SaBt9RDM&t=558s) Claude classifies her 116 sessions: 67% comprehension, 2% generation.
- [0:11:21](https://www.youtube.com/watch?v=li0SaBt9RDM&t=681s) The catch-me-up skill and its six exploration modes.
- [0:14:22](https://www.youtube.com/watch?v=li0SaBt9RDM&t=862s) Her amendment to research-plan-implement: understand the agent's research before you let it plan.

## Connections
- [Sentry](../../companies/evals-observability/sentry.md): the speaker's employer, whose shift into agent observability and AI debugging frames the internal tools she describes.
- [Session recaps](../../notes/session-recaps.md): the Sonar session's verification-discipline theme pairs with this talk's argument that comprehension, not generation, is where engineers should spend attention.
