# Self Driving Products: Product Signals to Pull Requests

> PostHog's pipeline for turning observability signals, errors, replays, and Slack complaints, into researched, grouped, and automatically opened pull requests.

- **Speaker:** Joshua Snyder, PostHog
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=zMiSRliEzv4) (AI Engineer channel; ~16m, released 2026-06-10)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Snyder describes a pipeline PostHog is building, in alpha at the time of the talk, that inverts how teams consume observability data. Today a product signal changes a dashboard metric, someone notices hours or days later, files a Linear issue, and eventually writes a PR, a cycle he says takes hours to days and represents a lot of unglamorous engineering work. The target state: a signal fires, a background agent investigates, and the engineer wakes up to a ready PR in GitHub, possibly already shipped behind a feature flag if the change is low risk.

The pipeline has five stages. Ingestion handles trillions of events a month across error tracking, session replay, logs, experiments, and Slack, and because some sources are public an LLM classifier sits at the top as a safety filter dropping prompt-injection attempts, such as an attacker-crafted error message telling the system to post internal data. Signals are then normalized into a single structure with source, type, content, an importance weight, and an embedding.

Grouping is where Snyder shares the hardest-won lesson. The naive approach, embedding raw signals and clustering, fails because off-the-shelf embedding models match on structural similarity: all errors cluster with errors, all Slack messages with Slack messages, and a checkout error never groups with the Slack message reporting checkout is broken. The fix is to have an LLM generate queries describing what each signal is about and match those queries in embedding space instead. Grouped signals accumulate weight in a report, and past a threshold the report is promoted to a research agent.

The research agent runs the Claude Agent SDK in a Modal sandbox with three context sources: PostHog's MCP server for pulling adjacent data like logs alongside a replay and an error, the codebase, and external MCPs, with Linear and Notion called out as the most useful for grounding. It outputs a problem summary, a priority, and a suggested reviewer derived from git blame. An actionability step then routes reports three ways: back into the pool to gather more evidence, into a morning inbox when a product judgment is needed, or straight to execution. Error-tracking signals are usually specific enough to act on immediately; Slack and replay signals produce generic problems with many possible fixes. Execution clones the repo into another sandbox, writes the fix, opens the PR, and reruns from a snapshot whenever CI fails or a comment lands, iterating until the PR is green.

His four lessons: evals on representative production data beat local vibe checks; embed the right thing, since structural similarity ruins clustering of mixed-format data; agents will always try to fix something, so vague reports must be filtered or you drown in noisy PRs; and treat tokens as free while experimenting. The team initially avoided agents for cost, but running an agent on the same problem a hundred times exposes recurring patterns that can be compressed into a one-shot LLM call or a small trained model later. The roadmap points at a product that ships its own experiments, auto-approves easy changes behind flags, and learns from every rejected PR and rollback.

## Notable moments

- [0:05:18](https://www.youtube.com/watch?v=zMiSRliEzv4&t=318s) Why clustering raw signal embeddings fails and the generated-query workaround
- [0:07:19](https://www.youtube.com/watch?v=zMiSRliEzv4&t=439s) The research agent: Claude Agent SDK in a Modal sandbox with PostHog MCP, code, and external MCPs
- [0:10:20](https://www.youtube.com/watch?v=zMiSRliEzv4&t=620s) Sandbox snapshot and rehydrate loop that iterates PRs until CI is green overnight
- [0:12:22](https://www.youtube.com/watch?v=zMiSRliEzv4&t=742s) Lessons learned, including treating tokens as free during experimentation

## Connections

- [PostHog](../../companies/evals-observability/posthog.md): the speaker's company; this pipeline is its bet on observability that acts instead of reports
- [Sentry](../../companies/evals-observability/sentry.md): the incumbent error-tracking comparison Snyder invokes for signal specificity
- [Modal](../../companies/cloud-compute/modal.md): supplies the sandboxes for both the research and execution agents, credited unprompted in the talk
