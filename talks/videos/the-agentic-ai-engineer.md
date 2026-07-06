# The Agentic AI Engineer

> Mutagent's founders lay out a full agent lifecycle, spec through production diagnostics, and argue each stage should itself be run by agents once teams operate more than a handful of them.

- **Speaker:** Benedikt Sanftl (CEO) and Burak (CTO), Mutagent
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=pSto5YaNGUo) (AI Engineer channel; ~35m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Sanftl opens with the claim that agent building runs on two loops. The offline loop is build, test, evaluate, improve. The online loop starts at deployment: monitor traces, diagnose failures, feed fixes back into optimization. Done manually, the cycle is slow because every step waits on human review, and Sanftl argues it stops scaling entirely once an organization runs hundreds of agents. The talk's thesis is that the loop itself should be executed by agents, which the founders call the agentic AI engineer, because agents fit many more cycles into the same time window.

Burak walks the stages. A spec captures the agent's responsibilities, context requirements, integrations, and constraints, and stays isolated from implementation details so the same spec can be rebuilt on a different harness when the current framework hits a roadblock, something he says happens regularly after three years of building agents. Build hands the spec to a coding agent targeting any platform. Evaluation is the termination condition, the equivalent of unit tests: Burak argues the real eval suite is a product of discovery rather than something domain experts can write upfront, accumulating metrics and edge cases from user feedback and production failures. He prefers binary pass-fail criteria over score-based LLM-as-judge metrics because a failed binary check tells you exactly what to fix, and he stresses calibrating judges since the same judge scores the same trace differently across runs.

The diagnostics material is the most concrete. Reading millions of agent traces costs more than the executions themselves, so Mutagent's approach is to pay an upfront cost deep-reading traces per failure mode, then extract code-checkable indicators, specific content or tool-call sequences that flag the failure, so future diagnosis runs without an LLM reading everything. Multi-tier filtering picks a representative sample, failures get grouped by root cause, whether a prompt section or a missing or malfunctioning tool, and each category generates both new evals to detect the problem and candidate remedies. Once the eval suite is in place, an autonomous optimization loop mutates the agent, and anything that reaches target scores ships to production automatically, closing the outer loop.

The demo shows Mutagent's product, two agents in research preview connected through an orchestrator that runs inside your coding environment, Claude Code in the demo. An evaluator agent builds eval sets and datasets. A diagnostics agent pulls traces from a configured source such as Langfuse, local transcripts, or exported JSONL, and produces an HTML report: detected failure modes with frequencies, a recursive why-chain tracing each problem to its origin, an assumptions block flagging where the agent guessed without code access, and multi-choice remedies. Accepted decisions compile into a markdown task definition for your coding agent to apply. Everything runs in your environment today, cloud and local, with a managed service planned. The closing pitch: stop debugging by hand and have agents do the tedious work.

## Notable moments

- [0:17:17](https://www.youtube.com/watch?v=pSto5YaNGUo&t=1037s) Why binary evals beat scores: a failed criterion is a call to action, and uncalibrated LLM judges add noise that makes experiments inconclusive.
- [0:21:25](https://www.youtube.com/watch?v=pSto5YaNGUo&t=1285s) The economics of diagnosis: reading millions of traces costs more than running them, so learned code-checkable indicators replace LLM reads.
- [0:27:27](https://www.youtube.com/watch?v=pSto5YaNGUo&t=1647s) The product tour: evaluator and diagnostics agents in research preview, wired through an orchestrator in your coding environment.
- [0:31:30](https://www.youtube.com/watch?v=pSto5YaNGUo&t=1890s) The diagnostics report walkthrough: failure modes with frequencies, why-chains, an assumptions block, and multi-choice remedies.

## Connections

- [Braintrust](../../companies/evals-observability/braintrust.md) sells the eval-first loop, traces to datasets to judge scores gating releases, that Mutagent wants agents to run autonomously.
- [Arize](../../companies/evals-observability/arize.md) covers the trace instrumentation and evaluation layer the diagnostics agent consumes from sources like Langfuse.
