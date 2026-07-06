# The maturity phases of running evals

> Braintrust's Phil Hetzel walks through four stages teams pass through as agent evals mature, from documented vibe checks to whole-trace evaluation of agents that touch external systems.

- **Speaker:** Phil Hetzel, Braintrust
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=FB-MLPhL9Ms) (AI Engineer channel; ~19m, released 2026-05-27)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Hetzel leads solutions engineering at Braintrust, which he describes as an agent quality company treating evals and observability as the same systems problem: evals build confidence before production, observability keeps it afterward. He came to the product as a user during 12 years in consulting (4 at KPMG, 8 at Slalom, where he led the global Databricks business unit) after noticing clients were prolific at generative AI proofs of concept and far less prolific at shipping them.

His first move is to separate evals from unit tests. Unit tests aim at exhaustiveness; evals should target the specific failure modes of your agent, identified by you or a subject matter expert, because the space of possible agent failures is infinite and enumerating it means never shipping. Eval results can be directional rather than perfect, especially with LLM-as-judge scoring. The primitives are a task (the agent or prompt under test), a dataset of examples that invoke it, and scoring functions that judge output quality.

The maturity phases run as a continuum. Phase one is getting started, and Hetzel defends vibe checking as a legitimate origin so long as it is documented: run ten example inputs, have a human (ideally a domain expert) mark each output thumbs up or down, and require a written justification. The justifications extract domain knowledge you will later scale. Phase two is measuring to manage: run those justifications through Cursor, Claude Code, or Codex to derive the actual failure modes, then automate scoring with LLM-as-judge for subjective criteria and plain code for objective ones like too many tool calls or tokens. He warns that putting a robe on an LLM does not make it trustworthy; judges themselves need evals against human-labeled ground truth. The dataset should shift toward captured production traces, because evals are closer to rerunning production than to running tests. That closes what Braintrust calls the flywheel: capture traces, find what went wrong, pull examples into offline experiments, and let results steer the next agent change.

Phase three accounts for complexity once agents call external systems. Hetzel splits tools into context-gathering ones and CRUD ones, and notes evaluation now covers whole traces rather than single outputs, down to individual tool or MCP calls. CRUD creates two unsolved-in-general problems: reproducing the state external systems were in when an input was captured, and running evals without writing to production data. His mitigations are to cram system state into the arbitrarily large trace itself and encapsulate it there, to use mock APIs, and to run timestamp or version queries against stores that support them, such as vector databases queried as of the original task time. Phase four, sketched in the last two minutes, is topic modeling at scale to surface failure modes from production automatically, plus driving evals from Claude Code and eval-provider CLIs. In Q&A he lands on a hybrid position: embrace LLM-as-judge for subjective quality, then eval the judge, which is tractable because judge outputs are discrete.

## Notable moments

- [0:04:16](https://www.youtube.com/watch?v=FB-MLPhL9Ms&t=256s) Evals are not unit tests; build them around known failure modes, not exhaustive coverage.
- [0:07:17](https://www.youtube.com/watch?v=FB-MLPhL9Ms&t=437s) Documented vibe checking: thumbs up or down plus a required justification from a human annotator.
- [0:11:20](https://www.youtube.com/watch?v=FB-MLPhL9Ms&t=680s) The flywheel: capture production traces, diagnose, rerun production as evals, improve the agent.
- [0:14:23](https://www.youtube.com/watch?v=FB-MLPhL9Ms&t=863s) Why CRUD tools break offline evals: external system state and the risk of touching production data.

## Connections

- [Braintrust](../../companies/evals-observability/braintrust.md): the speaker's company; the talk is a vendor-neutral version of its evals-plus-observability thesis.
- [Arize](../../companies/evals-observability/arize.md): competing agent evaluation and observability platform working the same trace-capture flywheel.
- [Session recaps](../../notes/session-recaps.md): the in-person program's "evals everywhere" theme overlaps this talk directly.
