# The Production AI Playbook: Deploying Agents at Enterprise Scale

> A five-pillar framework for taking agents to production, illustrated by a retail banking chatbot project that picked its model in week seven of an eight-week engagement.

- **Speaker:** Sandipan Bhaumik, Databricks
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ObTPqBGsEbA) (AI Engineer channel; ~37m, released 2026-06-18)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Bhaumik is a technical lead for data and AI at Databricks, previously five years as a principal architect at AWS. He describes a pattern he saw in every customer conversation two years ago: pick a model first, build features, demo in a controlled environment, ship, then watch it fail against real usage. From those failures he distills three gaps, observability (no trace of what the AI decided), evaluation (no defined, continuously measured success metric that matters to the business), and governance (no one accountable when it fails at 3 a.m.), and builds them into five pillars: evaluation, observability, data foundation, orchestration, and governance.

On evaluation, define success in numbers before touching code, build golden datasets with domain experts including gray areas and edge cases, and automate the pipeline so production responses get scored against the test set. He splits evaluation into three layers: deterministic checks (regex, formats, classic ML for intent and PII), semantic checks (LLM-as-judge on groundedness, safety, relevance), and behavioral checks (did the agent call the right tools, loop, or make duplicate calls). Behavioral is the layer teams miss: an agent that answers a balance question correctly but hits the database three times is fine in a demo and expensive at thousands of queries a day. Observability means tracing every decision; his banking example walks a trace from intent classification through account lookup, policy retrieval from a vector database, reasoning, and guardrail checks, and he notes regulators in Europe effectively mandate this before production. The data foundation takes 60 percent of his project time and splits into question data (what the agent needs to answer) and tracking data (traces that need their own schema and strategy). His line: data was built for humans, and humans are forgiving; agents find the wrong data and give the wrong answer confidently. Orchestration covers orchestrator-worker, choreography over a message bus for parallel independent agents, and human-in-the-loop below confidence thresholds. Governance covers audit trails, PII pre-validation (47 PII breaches caught during testing on his project), prompt versioning treated as change management with documented reasons per change, and model change management driven by your own eval set rather than public benchmarks.

The case study is a retail bank with about 20,000 chatbot calls a month, 60 percent simple queries it wanted deflected from human agents. A prior POC burned 85,000 dollars over six months and failed, with no one able to say why. Bhaumik's eight-week engagement spent weeks one and two collecting 200 real human-agent answers into an eval dataset and setting targets (60 percent deflection, roughly 85 percent accuracy), built the data and tracing foundation next, and only selected the model in week seven by running candidates against the eval set. Post-launch, the system proved itself when the bank changed interest rate policies: customer thumbs-down feedback spiked, traces showed the agent citing an outdated policy document whose embeddings had never been updated in the vector database, and the fix was quick. He closes with a production incident playbook (detect via eval dashboards, diagnose via traces, contain via prompt rollback or human deflection, fix and grow the test library) and cost advice: behavioral evals get expensive, so run a subset on each prompt change in CI and the full suite only on merge to main.

## Notable moments

- [0:09:12](https://www.youtube.com/watch?v=ObTPqBGsEbA&t=552s) The three evaluation layers: deterministic, semantic with LLM-as-judge, and the behavioral layer most teams miss.
- [0:12:15](https://www.youtube.com/watch?v=ObTPqBGsEbA&t=735s) Walking a full banking chatbot trace, from intent classification to guardrail checks on an overdraft fee dispute.
- [0:25:22](https://www.youtube.com/watch?v=ObTPqBGsEbA&t=1522s) The case study: an 85K dollar failed POC versus an eight-week rebuild that chose the model in week seven.
- [0:29:28](https://www.youtube.com/watch?v=ObTPqBGsEbA&t=1768s) The payoff: a CSAT drop traced to stale policy embeddings in the vector database within days of a policy change.

## Connections

- [Arize](../../companies/evals-observability/arize.md) sells the tracing and evaluation layers of this playbook as a standalone product, against Databricks bundling them into MLflow and Agent Bricks.
- [Braintrust](../../companies/evals-observability/braintrust.md) covers the same evals-plus-observability loop, including the living eval dataset practice Bhaumik describes.
- [Temporal](../../companies/agent-orchestration/temporal.md) provides the durable workflow machinery behind orchestrator-worker patterns and the fault-tolerance concerns in pillar four.
