# You Can't Prompt the Room: The Last Skill AI Won't Replace

> Balázs Horváth argues that once code is cheap, requirements elicitation and stakeholder work become the bottleneck, and shows the analyst toolkit he uses to feed AI the right thing to build.

- **Speaker:** Balázs Horváth, VisualLabs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=6bmM45jkMDY) (AI Engineer channel; ~16m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Horváth's claim is that writing code is no longer the bottleneck in software; figuring out what to build is. His evidence starts at home: at a VisualLabs internal hackathon early in the year, 17 of 21 agent ideas were abandoned for creating no business value, through missing data access or simply not making sense, while the four survivors changed how the company works. He has spent 13 years as the bridge between business and IT, writing functional designs and specifications for large ERP and CRM programs in the US and UK before founding VisualLabs, and says the constant across that period is eliciting requirements from people; what changed is that the output now feeds AI instead of only developers and consultants. You can prompt your code and your specification, but you can't prompt the room. He pairs this with Henry Ford's faster-horse line: AI is trained to return the most common answer, so using it naively replicates what exists, and the job is pushing it away from the average.

The practical core is the analyst toolkit: story mapping, business model canvas, value canvas. Story mapping gets the deep treatment. A support-system example maps the backbone (contacting, triaging, resolving, closing a case), hangs user stories under each stage, and slices a first release, capturing intent, classifying urgency, drafting a grounded answer, logging to a system of record, as the MVP, with sentiment reading and satisfaction checks in the backlog. Horváth insists on the classic story format (as a support lead, I need cases ranked by urgency so escalations don't slip) for an AI-specific reason: models were trained on that structure, so familiar packaging plus acceptance criteria yields better generations, and daisy-chained stories become a coherent specification. He keeps four questions in front of every build: whose problem is this, named to a persona; what does winning look like for them; what would make them refuse to use it; and would it change a decision. Track the answers in a markdown file in the repository so the AI can read them. His broader thinking sequence is VAD, value architecture design: understand how value is created, then the process and architecture underneath it, then design.

He names the anti-patterns of building the wrong thing: high shipping velocity with poor adoption, users trying features once without returning (watch frequency of a specific activity, ignore time on site), the demo as the deliverable, and PRDs with no real user testers. His prescriptions start Monday morning: replace "features shipped last quarter" with "features used more than twice," move the smartest subject-matter experts toward customers and decision-making since building has become cheap and deciding has become the expensive part, and run a mapping session before any build. His own test was writing the same app with and without user stories first; the gap convinced him. The goal, he says, is building the right thing rather than the next thing.

## Notable moments

- [0:00:01](https://www.youtube.com/watch?v=6bmM45jkMDY&t=1s) The hackathon numbers: 17 of 21 agent ideas abandoned for creating no business value.
- [0:04:04](https://www.youtube.com/watch?v=6bmM45jkMDY&t=244s) Story mapping introduced as the single most valuable skill in the post-code-bottleneck toolkit.
- [0:08:08](https://www.youtube.com/watch?v=6bmM45jkMDY&t=488s) The four questions: whose problem, what does winning look like, what causes refusal, does it change a decision.
- [0:12:13](https://www.youtube.com/watch?v=6bmM45jkMDY&t=733s) Anti-patterns of the wrong thing: the demo as deliverable and PRDs without real user testers.

## Connections

- [ReAgent: Requirement-Driven LLM Agents for Software Issue Resolution](../../papers/planning-architecture/reagent-requirement-driven-llm-agents-for-software-issue-re.md): tests the premise that better-specified requirements improve agent output, which Horváth asserts from practice.
- [Bridging Requirements and Architecture](../../papers/planning-architecture/bridging-requirements-and-architecture-multi-agent-orchestr.md): automates the requirements-to-architecture step Horváth's VAD sequence performs manually.
- [Session recaps](../../notes/session-recaps.md): Garry Tan's AI-native company definition, hire humans only for what AI cannot do, is the org-level version of Horváth's move-experts-upstream advice.
