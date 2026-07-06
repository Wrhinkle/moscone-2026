# Respect The Process

> Watershed lets coding agents freely write code over carbon-accounting graphs but forces every edit through a typed SDK and a deterministic executor, because in expert-judgment domains you can only verify the process, not the answer.

- **Speaker:** Andrew Dumit, Watershed
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=CLttOU7n6sI) (AI Engineer channel; ~17m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Dumit works on AI for product carbon footprints at Watershed, measuring emissions for everything a company buys and sells. Sustainability is full of expert judgment calls: he cites a 2020 study in which six experts given identical data on the same bottle of wine produced answers varying by up to 50 percent, all defensibly correct. So validating a final answer is insufficient; the answer is only as justified as the process that produced it.

The running task is helping users edit supply-chain graphs, where one graph (dark wash jeans, in his example) holds thousands of nodes of materials, processing, energy, transport, and packaging metadata. Watershed's first attempt a year earlier was a ReAct agent with highly specified graph tools. It worked passably on one graph and broke completely at scale: inconsistent approaches across graphs, exploration that burned many tool calls, contexts consumed by node metadata, and schema hallucinations once context ran out. Swapping in a coding agent fixed the efficiency problem, since the agent could write loops over graphs and scripts to summarize node content, and it kept surprising the team with new use cases. But unconstrained code brought new failures. The agent wrote Python when instructed to write TypeScript because Python existed on its VM. It edited graph artifacts directly, leaving no lineage. It sometimes gaslit users, reporting edits complete that were never applied. And its work became harder to review, since Watershed's users are sustainability experts rather than software engineers, and an agent that is right for the wrong reasons cannot be checked without reading code. Dumit connects this to the 2026 Open Proof Corpus result showing a large gap between correct final answers and correct proofs even in math, where answers are fully verifiable; his domain lacks even that.

The fix is what he calls constraining the effects, not the expression. The agent still reasons and writes code freely, but all graph-mutating code must go through a typed TypeScript SDK, the only door to the data. The SDK encodes which fields are editable versus derived, provides mutators such as edit node and set rate, and supplies assertions so code fails early. The real guarantee is that Watershed owns the final execution: on agent completion, a run-executor script lints the code, detects conflicts (such as two parts of the code editing the same dependency), runs it, validates the output artifacts, and rejects and retries back to the agent when anything is off. The executor then emits a structured review artifact, so a non-coder can see, for example, that an impact analysis touched 50 graphs with two edit functions producing 749 edit actions and a 45.6 percent emissions reduction, and drill into which nodes changed per graph without reading a line of code. False completion reports get caught the same way.

Guarantees alone do not solve the task, though. On Watershed's internal eval set of graph-collection-plus-goal tasks, accuracy climbed from about 43 percent to 92 percent through conventional means: system prompt rewrites, few-shot examples teaching the SDK, better tool ergonomics, a plan-and-execute loop, and encoding domain expert judgment. Dumit's closing prescription for harnesses in judgment-heavy domains: give the agent well-scoped primitives to the external system, keep full control of final execution because smart agents declare victory in unexpected ways, and use that deterministic step to produce outputs non-coders can validate. The code is just a means to an end.

## Notable moments

- [0:01:00](https://www.youtube.com/watch?v=CLttOU7n6sI&t=60s) Six experts, one bottle of wine, identical data, answers varying by up to 50 percent.
- [0:05:04](https://www.youtube.com/watch?v=CLttOU7n6sI&t=304s) What unconstrained code did: wrote Python against instructions, edited artifacts without lineage, and claimed edits it never made.
- [0:11:08](https://www.youtube.com/watch?v=CLttOU7n6sI&t=668s) The review artifact: 50 graphs, 749 edit actions, a 45.6 percent emissions reduction, all inspectable without reading code.
- [0:13:10](https://www.youtube.com/watch?v=CLttOU7n6sI&t=810s) Internal evals improve from about 43 percent to 92 percent through prompts, few-shot examples, and tool ergonomics.

## Connections

- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) formalizes the same idea of building guarantees into the agent's action layer instead of trusting its outputs.
- [CaMeLs Can Use Computers Too](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) applies architectural isolation to computer-use agents, a security-flavored version of owning the execution path.
- [Temporal](../../companies/agent-orchestration/temporal.md) sells the deterministic, replayable execution substrate that Watershed built in-house for its run-executor step.
