# Your Agents Need a Save Button

> Agent runtimes should checkpoint full execution state, not just emit traces, so teams can replay production runs with a different model or a mocked tool and diff what would have happened.

- **Speaker:** Hamza Tahir, ZenML
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=bZISsg7H7DA) (AI Engineer channel; ~17m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Tahir, a ZenML co-founder, opens with the observation that documents have had a save button since the 1980s but agents do not. The closest thing today is a trace, and he argues traces are disconnected from the runtime: variables in state, the file system in flight, the decisions in code, and the code itself are all lost, stamped as read-only telemetry in a tool far from where the code lives. What is missing is a connection between OTel-style observability spans and the execution itself. Save matters because save enables replay, and replay lets you ask what-if questions: swap in a cheaper open source model, mock a tool's return value, or degrade something intentionally to see what breaks.

He describes an emerging layer of the stack that sits below the agent framework or harness as a durable runtime, augmenting traces with code execution and environment snapshots so state is complete. Production then already contains what you need: checkpoint, replay, diff, decide. As evidence the approach scales, he cites a DoorDash blog post from June 1 describing a simulated environment for replaying customer bots; what took hours now takes 5 minutes across hundreds of simulations, with 90 percent fewer hallucinations, and results land within two points of production because the simulations are grounded in real runs.

The demo uses Kitaru (the name is garbled by auto-captions in places), a newly launched open source runtime from ZenML. A support agent handles chargeback dispute refunds, and each tool call is a checkpoint recording configuration, code, artifacts in and out, and the environment (Docker image or sandbox). Tahir replays the execution from a specific checkpoint with the model swapped to GPT-5 Nano; the first three checkpoints are skipped because their state already exists, and only the changed step onward executes. A second replay holds the model constant and mocks the lookup-policy tool with another function from the codebase. A diff command then renders the original and both forks side by side: the baseline segments match exactly, the third run diverges after the policy change, and the final artifacts differ, with the original two runs concluding "needs review" while the policy-changed run says "safe to answer," at lower token cost.

Single replays are not enough, though. Tahir cites tau-bench to note that a model passing 60 percent of the time is self-consistent only about a quarter of the time, so one replay is an anecdote. The tool supports cohort replays, such as taking the most expensive runs and applying one change across all of them, emitting a JSON report. He then feeds that report to the Kitaru MCP server and has an LLM analyze the cohort, which matters once cohorts reach thousands of runs. He also warns against naive model swaps, citing a Braintrust study on the false economy of looking at cost alone while resolution quality drops. The live cohort analysis returns its verdict near the end of the talk: don't ship the cheaper model, even though the single replay had looked equivalent and cheaper. His playbook: start from real production runs rather than synthetic data, build cohorts that matter (expensive, long, risky), never ship from one or two replays, automate the loop, and keep a human at the end.

## Notable moments

- [0:04:03](https://www.youtube.com/watch?v=bZISsg7H7DA&t=243s) The DoorDash result: replay simulations drop from hours to 5 minutes, with 90 percent fewer hallucinations and results within two points of production.
- [0:07:07](https://www.youtube.com/watch?v=bZISsg7H7DA&t=427s) Replay from a checkpoint with GPT-5 Nano swapped in; earlier checkpoints are skipped because their state is already saved.
- [0:14:12](https://www.youtube.com/watch?v=bZISsg7H7DA&t=852s) The tau-bench point: a 60 percent pass rate means roughly one-quarter self-consistency, so a single replay is an anecdote.
- [0:15:14](https://www.youtube.com/watch?v=bZISsg7H7DA&t=914s) The cohort analysis verdict comes back: don't ship the cheaper model, despite the promising single replay.

## Connections

- [Braintrust](../../companies/evals-observability/braintrust.md) is cited directly for the false-economy study on naive model swaps, and sells the trace-to-eval loop Tahir describes.
- [Temporal](../../companies/agent-orchestration/temporal.md) occupies the same durable-runtime layer under agents, with checkpointed state that survives failure.
- [Arize](../../companies/evals-observability/arize.md) represents the trace-centric observability approach the talk argues is incomplete without runtime state.
