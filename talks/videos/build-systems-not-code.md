# Build Systems, Not Code

> Angie Jones argues that designing agentic systems exercises the same engineering disciplines as traditional software, walked through a house-hunting agent called Relocation Scout.

- **Speaker:** Angie Jones, Agentic AI Foundation
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ZD9-4fW2HhM) (AI Engineer channel; ~20m, released 2026-06-25)
- **Program:** Online Track 2026

## Summary

Jones opens with the quiet dread many engineers feel that coding agents are taking the fun parts of building. Her advice is to let them have it, because one layer up, architecting agentic systems, the building blocks are different but the discipline is the same. The talk walks a single running example, Relocation Scout, a house-hunting agent that pulls listings and neighborhood signals, weighs them against her criteria, and returns a ranked shortlist, through nine classic engineering skills.

Systems thinking comes first: the agent is part of a system of files, tools, humans, and other agents, and Jones says letting a coding agent build it without thinking through boundaries, dependencies, and failure modes is a mistake. Workflow design follows, since an agent needs more than a goal, it needs a path, and every run ends in stop, retry, or escalate. She then names the agentic version of a code smell: the giant prompt that accretes edge cases, safety rules, and exceptions until the agent drifts because the script is too long. Her Relocation Scout prompt turned out to contain four distinct jobs. Decomposition and separation of concerns assign each to the right home: listing normalization becomes a reusable skill, shortlist formatting becomes a structured output schema, commute calculation goes in a boring script, and neighborhood research becomes a sub-agent. Sub-agents, she says, are architecturally like functions, scoped to one task and free of the session's accumulated context.

The algorithmic thinking section carries her sharpest rule of thumb: use code for determinism, agents for judgment, and humans for authority. Exact-answer tasks like commute math and deduping belong in plain code, which is cheaper and more reliable; the agent decides which listings deserve a closer look; she alone approves booking a tour. Contracts extend this: when another system consumes the agent's output, the decision, score, and reasoning get written as structured data to the agent's memory layer (she uses Compendium Wiki), making it queryable later rather than trapped in a session conversation.

State management gets a concrete failure story. The agent emails her realtor about a viewing, logs the action to memory, then crashes before blocking her calendar. A later lint pass, which she says these systems need to stay healthy, notices the half-finished run and retries, but because the email action is recorded, the retry only completes the missing calendar block instead of pestering the realtor again. Idempotency has to be enforced by the system because model outputs vary enough that a retried request can look like a new task. Threat modeling closes the loop: listing copy, forum threads, and anonymous reviews are untrusted input, evidence rather than instructions, and high-consequence actions like emailing sellers or submitting offers sit behind her approval to limit blast radius.

Her maintainability test is that any human or agent should be able to start cold in the system and know what to do, guided by an agents file at every level describing workflow, policy, resources, and how to keep memory current. If a harness struggles to update the system, she treats that as a signal the design needs work.

## Notable moments

- [0:04:02](https://www.youtube.com/watch?v=ZD9-4fW2HhM&t=242s) The giant prompt as the agentic code smell, growing one edge case at a time
- [0:06:04](https://www.youtube.com/watch?v=ZD9-4fW2HhM&t=364s) Decomposing four hidden jobs into a skill, a schema, a script, and a sub-agent
- [0:09:07](https://www.youtube.com/watch?v=ZD9-4fW2HhM&t=547s) Code for determinism, agents for judgment, humans for authority
- [0:14:14](https://www.youtube.com/watch?v=ZD9-4fW2HhM&t=854s) The crashed-run retry that must not email the realtor twice

## Connections

- [Session recaps](../../notes/session-recaps.md): Sonar's in-person session made a parallel argument for verification discipline and rigor returning to AI-assisted development
- [CLAWLESS: a security model of AI agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md): formalizes the untrusted-input and least-privilege threat modeling Jones applies to Relocation Scout
