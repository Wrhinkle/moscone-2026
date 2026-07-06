# The Missing Layer After Launch
> Why shipping an agent is when the real work begins, and the three-agent meta harness Wandero built to monitor, diagnose, and auto-fix its production travel agent.

- **Speaker:** Raphael Kalandadze, Wandero AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=kZsf_Sfm7RU) (AI Engineer channel; ~20m, released 2026-07-05)
- **Program:** Online Track 2026

## Summary
Kalandadze argues that most agent talks end at the moment of shipping, when shipping is actually where the real work begins. With current models you can write 100,000 lines of code and stand up a product in weeks; the hard part is knowing whether it works across hundreds or thousands of real conversations a day. He calls the feedback loop after launch the missing layer and says it matters at least as much as the product itself.

Agents break the assumptions behind classical monitoring. There is no predefined flow to pretest, coverage is endless, and the same input can take different trajectories. The failure mode that keeps him up at night is silent recovery: an agent struggles mid-task, gets lucky, finds a workaround, and every dashboard stays green while a real defect stays hidden in the codebase. Technically successful runs can still fail the user; in Wandero's travel domain, an agent built an itinerary but picked a different service and miscalculated the price, so the run passed and the customer was unhappy. Unit tests, regexes, and simulated customer conversations helped, but he calls them one slice of the problem because customers always do something the team did not script.

His answer is a set of agents that operate the production agent, since digging through log volumes and separating symptom from root cause is itself an agent-shaped problem. The first is a log monitoring agent that runs every hour, or every 15 minutes, over a one-hour log window with codebase access. It diagnoses problems, sends Slack alerts for critical ones, and opens PRs with descriptions, mermaid diagrams, and HTML artifacts. A separate review agent with fresh context criticizes each PR from a different angle, runs focused tests, requests changes, or closes it outright, which filters the volume before a human sees it. Kalandadze says the PR and review agents produce ten times more PRs per day than his three-person team, so the loop delivers a fix-ready PR in about half an hour and the human review step is designed to be removable later: close the loop first, become the bottleneck, then remove yourself.

The second system is a session analyzer that scores every conversation and produces a health dashboard: session counts, cost, average score, success rate, sentiment, tool-call analytics, and AI insights that connect patterns across sessions with root causes and recommended fixes. He built it in-house despite existing vendors because he knows what he is looking for; it runs once or twice a week for a zoomed-out pulse rather than bug-level fixes. The third piece is a computer-use agent that logs into the product like a customer, since some UI problems never show up in logs or code; a custom skill that knows the site's DOM made it much faster than generic browsing, at real token cost. He calls the whole assembly a meta harness: everyone can use the same models, so the internal system that watches, diagnoses, and improves your agent is where the edge lives.

## Notable moments
- [0:03:02](https://www.youtube.com/watch?v=kZsf_Sfm7RU&t=182s) Why unit tests, regex checks, and simulated conversations only cover one slice of production behavior.
- [0:04:03](https://www.youtube.com/watch?v=kZsf_Sfm7RU&t=243s) The lucky-recovery failure mode: hidden defects behind green dashboards.
- [0:10:08](https://www.youtube.com/watch?v=kZsf_Sfm7RU&t=608s) The hourly log monitoring agent and its auto-generated PRs with diagrams and artifacts.
- [0:14:10](https://www.youtube.com/watch?v=kZsf_Sfm7RU&t=850s) The session analyzer dashboard: health score, cost, sentiment, and AI insights across every conversation.

## Connections
- [Resolve.ai](../../companies/evals-observability/resolve-ai.md): sells the productized version of this pattern, multi-agent investigation and guarded remediation of production incidents.
- [Sentry](../../companies/evals-observability/sentry.md): the vendor path for the agent monitoring layer Kalandadze chose to build in-house.
- [Session recaps](../../notes/session-recaps.md): the Sonar session's compounding-loops and zero-trust verification framing is the in-person cousin of this talk's close-the-loop argument.
