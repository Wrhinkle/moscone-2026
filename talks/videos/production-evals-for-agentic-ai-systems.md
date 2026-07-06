# Production Evals For Agentic AI Systems
> Why agentic systems shift evaluation from scoring model outputs to measuring production behavior, and the SRE-style metrics that matter.

- **Speaker:** Nishant Gupta, Meta Superintelligence Labs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=vljxQZfJ9wY) (AI Engineer channel; ~8m, released 2026-06-25)
- **Program:** Online Track 2026

## Summary
Nishant Gupta, a software engineering tech lead building training and inference infrastructure at Meta Superintelligence Labs, argues that evaluation for agentic systems has to move out of the benchmark suite and into production. His opening contrast: a model scores 90% on a benchmark, a new version scores 92%, the team celebrates, but that number answers the wrong question. Benchmarks ask whether the model generated the right answer. Agentic systems plan, call tools, retrieve information, and execute workflows, so the real question is whether the system behaved correctly.

Gupta names the gap directly. Offline benchmarks keep improving while production reliability stays unpredictable, because benchmarks measure model capability and production measures system behavior. Benchmarks do not capture tool failures, API outages, context changes, user variability, or long-running workflows, and as systems get more autonomous that gap widens. He lays out a hierarchy of failure modes that output-only evaluation misses: at the foundation, memory, retrieval, and safety failures; above that, reasoning mistakes and poor planning and incorrect tool execution; at the top, multi-agent coordination failures.

His central mindset shift is to stop thinking like a researcher and start thinking like an SRE. SREs do not measure success with accuracy, they measure reliability, availability, latency, cost, and recovery. Gupta makes reliability the North Star metric and demotes accuracy to an input. He organizes evaluation as a pyramid: benchmarks at the base (scalable, repeatable, limited operational value), scenario-based evaluations in the middle (customer support, code generation, research workflows run inside a simulated environment), and production telemetry at the top as the highest-value signal. His argument is that offline evaluation should be scenario driven rather than prompt driven, measuring task completion rate, tool correctness, planning quality, and resource usage.

Once a system is in production, Gupta says every interaction becomes a signal. Execution traces, user outcomes, escalations, failures, and feedback turn production traffic into the largest and most representative evaluation dataset an organization will ever have. He reframes humans as evaluators rather than fallback systems, because they assess correctness, trust, usefulness, and safety in ways automated metrics cannot, and the best systems pair automated evaluation with targeted human review. He warns that agents drift constantly as models, prompts, tools, and user behavior change, and that reliability degrades slowly enough that teams often do not notice until users complain, which makes continuous monitoring essential. Observability and evaluation are inseparable in his framing: agent traces are the equivalent of distributed tracing for autonomous workloads, and without them evaluation is guesswork. He closes on an architecture where evaluation lives in the control plane, continuously observing the execution plane, running simulations, and coordinating human review, and on the point that his business-outcome metric slide deliberately omits accuracy because business success depends on much more than it.

## Notable moments
- [0:01:04](https://www.youtube.com/watch?v=vljxQZfJ9wY&t=64s) The hierarchy of agentic failure modes, from memory and retrieval up to multi-agent coordination.
- [0:02:04](https://www.youtube.com/watch?v=vljxQZfJ9wY&t=124s) The SRE reframing that makes reliability the North Star and accuracy just an input.
- [0:06:10](https://www.youtube.com/watch?v=vljxQZfJ9wY&t=370s) The business-outcome metric slide that deliberately leaves accuracy off the list.

## Connections
- [Braintrust](../../companies/evals-observability/braintrust.md) builds the eval-first trace logging and scoring pipeline Gupta describes as production evaluation infrastructure.
- [Arize](../../companies/evals-observability/arize.md) is an adjacent observability vendor focused on the agent tracing and drift monitoring Gupta says is inseparable from evaluation.
- [Session recaps](../../notes/session-recaps.md) capture the in-person "evals everywhere" theme that this talk restates for production agents.
