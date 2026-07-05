# Paper Compute

> Open-source infrastructure for running AI agents in production: zero-instrumentation telemetry (Tapes) plus a hardened, sandboxed Linux OS built for agents (stereOS).

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** silver
- **Founded:** Reported 2026 (per third-party company-profile sites; not confirmed on primary sources); location not confirmed
- **Website / GitHub:** https://papercompute.com · https://github.com/papercomputeco

## What they do
Paper Compute builds the "missing layer" beneath production AI agents. **Tapes** is a zero-instrumentation observability library that intercepts and records agent activity (requests, responses, tool calls, retries) without requiring code changes — turning agent sessions into replayable, searchable telemetry that can be converted into reusable "skills" and runbooks. **stereOS** is a hardened, Linux-based operating system purpose-built to run agents in isolated sandboxes, aimed at teams needing tighter control over agent behavior in regulated or on-prem environments (auditability, compliance, security boundaries). Together they form an agent-ops stack: capture what an agent did, then constrain what it's allowed to do.

## Founders & origins
Founded by Brian Douglas, former GitHub director of developer advocacy and founder of OpenSauced, alongside CTO John McBride (Verified — The New Stack, daily.dev).

## Funding
Investor names (e.g. Batch Ventures, Mozilla Ventures, Zeal Capital Partners) appeared in aggregator data, but amounts could not be verified and some aggregator results conflated this company with an unrelated company also named "Paper" — treat as **Unverified**. No funding figures found on primary sources.

## Evidence of real-world use
Tapes is open source on GitHub (~248 stars at time of research) under the papercomputeco org; stereOS is also open source. No named enterprise customers or case studies found — evidence is limited to OSS repo activity and founder credibility (GitHub, OpenSauced).

## Relevance to agentic AI engineering
Directly maps to the agent-orchestration and observability layer of the stack: session recording/telemetry for agents, sandboxed execution environments, and guardrails — relevant to any builder running coding or ops agents in production and needing audit trails.

## Use cases & considerations
Use cases: capturing agent telemetry without instrumenting app code; running untrusted or high-autonomy agents in a locked-down sandbox; converting successful agent runs into reusable playbooks. Considerations: very young company/product (2026), thin public evidence of paying customers, competes conceptually with agent observability tools (e.g. LangSmith, Braintrust) and sandboxing tools (e.g. E2B, Modal).

## Sources
- https://papercompute.com/
- https://papercompute.com/blog/introducing-stereos/
- https://github.com/papercomputeco
- https://github.com/papercomputeco/stereOS
- https://thenewstack.io/paper-compute-agent-infrastructure/
- AI Engineer World's Fair 2026 sponsor list (silver tier), https://www.ai.engineer/worldsfair/2026
