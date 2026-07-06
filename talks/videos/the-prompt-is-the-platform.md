# The Prompt is the Platform

> Resonate's bet that specifications, not implementations, are the product, and how deterministic simulation lets agents design distributed systems rather than just build them.

- **Speaker:** Dominik Tornow, Resonate HQ
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=DqtmZE6Hl0g) (AI Engineer channel; ~18m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Tornow opens with a prediction: in 2026, coding agents will quietly retire their first software platform, not because it is bad but because it is unnecessary. His working theory is that general purpose implementations will increasingly be replaced by bespoke ones generated on demand as minimal extensions of infrastructure already in place. Reuse then moves upstream: instead of reusing an implementation, you reuse a specification and derive many tailor-made implementations from it. At that point the prompt is a platform.

For Resonate, a durable execution company with a server and SDKs in TypeScript, Python, Rust, Go, and Java, this is an existential question about where the value lives. Tornow's answer is that the product becomes the specification, the protocol, from which multiple server implementations are derived: a general purpose reference server, plus implementations built with infrastructure partners so customers get durable execution natively on their existing stack. The talk's case study is Resonate on NATS.io, with Synadia as the partner.

The first attempt failed instructively. Asked to build a Resonate server in Rust on Postgres straight from the abstract specification, the agent produced a happy-path prototype that passed basic tests but broke on concurrency, process failure, and network failure. The gap was too large, so the team inserted an intermediary artifact, a concrete specification pinning down the schema, indices, SQL queries, and transaction boundaries. With those decisions written down the agent did build a production system, but a human drove the design. Tornow's point is that if the specification is the product, an agent that only implements is not enough; agents have to move upstream into design.

The NATS work reframed the question as what the agent needs to design first and build second. The answer was a deterministic simulation environment, built in Python, simulating the NATS primitives Resonate depends on: queues, a versioned key-value store, and delayed messages. The agent's task changed too: build a simulated implementation, which Tornow calls executable design, whose purpose is discovering the correct algorithm under partial order and partial failure. The simulated KV store sometimes returns stale reads under control of a deterministic random generator, and enforces optimistic concurrency on writes, because a correct implementation must handle everything the target platform legally allows, not just what it conveniently does.

The mechanism he dwells on is what the team calls the forbidden fruit. In production a reader cannot know whether a read was fresh or stale. The simulator records it anyway, emitting trace events that mark each read as fresh or stale and include the latest value the algorithm never saw. The algorithm is forbidden from depending on that information, but the agent may use it to debug, turning "the invariant failed" into "the invariant failed because the algorithm decided from a stale view of the world." With that feedback loop the agent built a proof of concept in the simulator, derived the concrete specification from a design already known correct, and only then wrote the production implementation. Tornow credits two prerequisites, minimalism and simplicity, earned over three years of shrinking the protocol to two objects, a durable promise and a durable task, and he is clear they are the finish line rather than the starting point.

## Notable moments

- [0:00:02](https://www.youtube.com/watch?v=DqtmZE6Hl0g&t=2s) The opening claim that coding agents will retire their first software platform in 2026.
- [0:05:09](https://www.youtube.com/watch?v=DqtmZE6Hl0g&t=309s) The failed first attempt: a Rust-on-Postgres server that passed basic tests but broke on concurrency and failure.
- [0:07:09](https://www.youtube.com/watch?v=DqtmZE6Hl0g&t=429s) The pipeline emerges: abstract spec, simulated implementation as executable design, concrete spec, production implementation.
- [0:13:13](https://www.youtube.com/watch?v=DqtmZE6Hl0g&t=793s) The forbidden fruit: simulator trace events reveal stale reads the algorithm may never depend on but the agent may debug with.

## Connections

- [Temporal](../../companies/agent-orchestration/temporal.md), the durable execution incumbent whose implementation-centered model this talk's specification-as-product thesis challenges.
- [Inngest](../../companies/agent-orchestration/inngest.md), an adjacent durable workflow engine competing in the same execution-reliability space.
