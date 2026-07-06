# Deterministic Infra for Non-Deterministic AI Agents
> A Meta infrastructure lead argues that agent reliability is a distributed-systems problem: models propose, deterministic platforms decide, and an agentic control plane is the emerging layer.

- **Speaker:** Nishant Gupta, Meta Superintelligence Labs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=APh1Vx0oLmQ) (AI Engineer channel; ~7m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary
Gupta, a software engineering tech lead at Meta working on training and inference infrastructure, compresses an infrastructure thesis into seven minutes. His starting observation: the conversation has moved from model capability to reliability. As agents go beyond answering questions into planning, tool calls, and decisions that touch production systems, the systems stay probabilistic while infrastructure is not allowed to be.

He names the core problem "the great mismatch." Modern cloud infrastructure assumes short-lived requests, mostly deterministic services, known execution paths, and bounded failures. Autonomous agents violate nearly all of it: they are stateful, long-running, dynamic in their decisions, and may execute different workflows for identical inputs. Demos ask whether an agent can complete a workflow once; production asks whether it can do it 10,000 or a million times, recover from failures, and hit acceptable cost and latency. Most engineering effort therefore moves below the model layer into orchestration, monitoring, safety evaluation, and recovery.

Gupta's most concrete section covers failure modes. Hallucinations, he says, are often the least interesting failure. What he sees instead are infrastructure failures: recursive reasoning loops, workflow deadlocks, retry amplification, context corruption, memory poisoning, and cost explosions. His worked example is retry amplification: an agent calls a tool incorrectly, gets an error, and generates a slightly different but still invalid request; each retry deepens reasoning and consumes more GPU until a minor API error becomes a compute incident. The model makes a mistake and the infrastructure turns it into an outage.

The architectural principle he recommends most strongly: never let the model directly control production systems. The model generates proposals, infrastructure validates them, a policy engine approves them, and an execution gateway enforces them. The model suggests, the platform decides. Around this he sketches an emerging layer he calls the agentic control plane, analogous to what Kubernetes was for containers and service meshes for microservices: scheduling, memory coordination, policy enforcement, evaluation, monitoring, and workload routing, an operating system for autonomous AI.

Supporting points come fast. Observability must capture why, not just what: planning decisions, tool calls, memory lookups, and state transitions, because debugging an autonomous workflow depends on the chain of decisions. Shared memory across agents reintroduces classic consistency problems (stale reads, conflicting updates, context drift), and many multi-agent failures are consistency failures masquerading as reasoning failures. Safety must be layered: prompt controls, tool permissions, policy validation, human approvals, and audit. Humans stay in the system permanently as exception handlers and calibration signals rather than as a temporary crutch. And AI workloads increasingly look like cluster scheduling problems, with bursty demand and workflows running minutes instead of milliseconds, so inference becomes a resource orchestration problem. His reassurance is that distributed systems already solved analogues: circuit breakers become tool isolation, rate limits become agent limits, resource quotas become cost governance. His closing line: the future of AI will be won by better systems, not better prompts.

## Notable moments
- [0:02:06](https://www.youtube.com/watch?v=APh1Vx0oLmQ&t=126s) Retry amplification walkthrough: a minor API error compounds into exponential GPU consumption.
- [0:03:08](https://www.youtube.com/watch?v=APh1Vx0oLmQ&t=188s) The core principle: models propose, infrastructure validates, policy approves, a gateway enforces.
- [0:06:10](https://www.youtube.com/watch?v=APh1Vx0oLmQ&t=370s) Mapping distributed-systems patterns onto agents: circuit breakers, rate limits, quotas, and tracing.

## Connections
- [Temporal](../../companies/agent-orchestration/temporal.md), whose durable-execution engine is a shipping example of the deterministic reliability substrate Gupta argues agents need.
- [Session recaps](../../notes/session-recaps.md), where agent-native infrastructure as an open design space recurred as an in-person theme.
