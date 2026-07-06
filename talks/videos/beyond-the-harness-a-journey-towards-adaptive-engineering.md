# Beyond the Harness: A Journey Towards Adaptative Engineering

> A practicing doctor turned AI engineer argues that fixed agent harnesses suit today's problems but will break in the real world, and proposes letting the harness emerge and adapt at runtime.

- **Speaker:** Rajiv Chandegra, Annicha Labs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=qdZzND79mcg) (AI Engineer channel; ~37m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Chandegra, a practicing medical doctor in London who has done AI engineering for a few years through Annicha Labs, proposes a design philosophy he calls adaptive engineering. His account of the current paradigm: engineers pick or build a fixed harness ahead of runtime, whether Pi, Claude Code, Cursor, or Codex, with predetermined roles, tools, and sequencing. He calls this the factory model, Taylorism for AI, where every station is engineered in advance and each agent has one job, a fixed place, and a defined handoff. It delivers three payoffs: reliability, auditability, and linear causality when something breaks. He is careful to say harnesses can be customized, but the customization happens before the engineering run, not during it.

His critique rests on two predictions. Models will improve fast enough that carefully built harnesses go stale within a month, and AI engineering will leave the sandbox and touch the physical world, with multiple agents, humans, and institutions interacting. Reliability in a fixed harness is bought by suppressing the variance that novelty requires, and every unanticipated situation needs a human to patch the harness until the harness is more complicated than the problem. His one-line summary: the factory method is the right answer to a fixed problem and the wrong answer to a moving one.

The middle of the talk goes philosophical. He contrasts a reductionist worldview, where wholes decompose into stable parts, with a relational one where processes and relationships come first and a stable thing is a slow pattern in a flow, an organism being more flame than crystal. Emergence is his key concept: water is wet though oxygen and hydrogen are not, and a flock arises from three local rules with no bird containing a flock. He cites Russell Ackoff's idea of a mess, a system of problems in motion that cannot be decomposed into tidy boxes, and distinguishes complicated problems like a jumbo jet, which experts can analyze and plan, from complex ones like markets and organizations, which you probe, sense, and respond to. Treating complex problems as complicated is, he argues, one of the most expensive mistakes in modern engineering.

Adaptive engineering, as he defines it, is the discipline of designing constraints so that the harness emerges on its own, stabilizes, and adapts to the changing environment in ways you could not specify in advance. The harness becomes the ongoing output of the process rather than its input. He simulates how undifferentiated agents coupling at increasing rates would specialize relative to each other, form clusters, and crystallize conventions, producing governance without a governor. The engineer's levers become the rate of coupling, rewards for cohering toward a goal, and costs for leaving a container. He distinguishes his proposal from existing adaptive systems: Hermes' self-improving skills are vertical intelligence, making one agent smarter, while his thesis is that horizontal intelligence, how groups of agents coordinate, is the higher leverage point. He also lists failure modes honestly: settling into suboptimal attractors, drift without genuine selection pressure, monoculture from shared training data, collapsing legibility, and no predictability ahead of runtime. His closing claim is that the limiting factor of future systems will be the adaptability of the harness rather than the strength of the model.

## Notable moments

- [0:07:09](https://www.youtube.com/watch?v=qdZzND79mcg&t=429s) The factory framing: Taylorism for AI, with each agent given one job, a fixed place, and a defined handoff.
- [0:10:10](https://www.youtube.com/watch?v=qdZzND79mcg&t=610s) The takeaway line about fixed answers to moving problems.
- [0:21:21](https://www.youtube.com/watch?v=qdZzND79mcg&t=1281s) The formal definition of adaptive engineering, with the harness as output rather than input.
- [0:28:29](https://www.youtube.com/watch?v=qdZzND79mcg&t=1709s) Vertical versus horizontal intelligence, and why coordination across agents beats making individual agents smarter.
- [0:32:34](https://www.youtube.com/watch?v=qdZzND79mcg&t=1954s) The failure modes: suboptimal attractors, drift, monoculture, and legibility collapse.

## Connections

- [LangChain](../../companies/agent-orchestration/langchain.md), named in the talk as an example of the multi-agent orchestration harnesses whose structure is fixed ahead of runtime.
- [Effective Strategies for Asynchronous Multi-Agent Collaboration](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md) studies the agent-coordination question his horizontal-intelligence thesis turns on.
- [Session recaps](../../notes/session-recaps.md) cover an in-person session that treats sandbox, tools, and subagents as harness primitives, the paradigm this talk wants to move past.
