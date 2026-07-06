# Agents Building Agents
> How Nearform uses coding agents in an eval-gated optimization loop to improve production AI agents, plus a trace-clustering pipeline for fixing failures found in live data.

- **Speaker:** Alfonso Graziano, Nearform
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=aHhB3sjGjkI) (AI Engineer channel; ~30m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Graziano, a tech lead at Nearform and O'Reilly author of Learning AI Native Software Engineering, presents a repeatable process for improving AI agents with other AI agents. His framing: an agent is an LLM in an agentic loop with tools and context, and since agents are just software, coding agents can build and improve them. He tackles two failure classes, bad performance on evals and bad performance on live data.

The foundation is a golden dataset built with subject matter experts: inputs paired with expected outputs, where outputs can be an answer, a required tool call, specific parameters, or a chain of calls. Scorers run the dataset and produce an accuracy number, giving a baseline and regression protection. A deliberately naive demo agent built with Mastra, with no tools and a bare system prompt, passes 18% of its eval suite, the questions answerable from model weights alone.

The centerpiece is AutoAgent, Graziano's adaptation of Andrej Karpathy's auto-research idea to agent code instead of ML hyperparameters. A coding agent (Claude Code in his setup, though it works with others) runs the evals to generate a baseline report, then loops: create a branch, form a hypothesis targeting one failure class, change the target agent's code, rerun the evals, write a report, and update a cross-run memory file. Improvements continue from that branch; regressions roll back. Humans set constraints up front, including the rule that the agent may not edit the golden dataset or scorers to make evals pass. On the naive agent, AutoAgent lifted accuracy from 18% to 83% in about 10 iterations. More telling, on a production agent that had already been optimized by humans it added 10% on internal benchmarks, and on another real production agent it went from 67% to 86% by finding edge cases, improving the system prompt and tool descriptions, and fixing tool logic. Every hypothesis leaves a report, so a human can read a promising failed attempt and steer the next run.

For live data, the pipeline starts with user thumbs up or down feedback plus notes, and subject matter experts annotating traces. Once enough traces accumulate (a run per sprint worked for his teams; one example used 114 traces), a skill instructs the coding agent to cluster failure modes, do root cause analysis using access to both the traces and the agent's source code, and emit a markdown report with failure clusters, linked trace IDs, negative rates, and fix proposals. Humans then triage with subject matter experts: fix now, fix later, or discard false positives. Fixed failure modes become new golden dataset entries so regressions get caught. Graziano reports that a well-instructed coding agent has fixed an entire suite of clustered issues from one prompt, and complex clusters get pointed at AutoAgent to produce draft PRs.

He closes with harness engineering, the practice that makes both loops work: spec-driven environments where each failure mode becomes a spec, quality gates (linting, unit tests, evals, LLM code review), deliberate context engineering, and observability, so the coding agent can validate its own changes.

## Notable moments
- [0:08:05](https://www.youtube.com/watch?v=aHhB3sjGjkI&t=485s) Karpathy's auto-research loop as the inspiration: a coding agent tweaking ML code measurably improves the loss.
- [0:10:07](https://www.youtube.com/watch?v=aHhB3sjGjkI&t=607s) AutoAgent takes the naive Mastra agent from 18% to 83% eval accuracy in about 10 iterations.
- [0:17:11](https://www.youtube.com/watch?v=aHhB3sjGjkI&t=1031s) A production agent already tuned by humans goes from 67% to 86% without cheating on the evals.
- [0:23:14](https://www.youtube.com/watch?v=aHhB3sjGjkI&t=1394s) The trace-clustering skill: 114 traces with feedback become clustered failure modes with root causes and fix proposals.

## Connections
- [Mastra](../../companies/agent-orchestration/mastra.md), the TypeScript agent framework used for the demo agent, whose built-in scorers and evals map onto the golden dataset approach here.
- [Session recaps](../../notes/session-recaps.md), where Sonar's guide-verify-solve cycle and zero-trust verification of AI-written code covered the same compounding-loop territory in person.
