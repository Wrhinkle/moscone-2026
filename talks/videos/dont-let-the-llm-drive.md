# Don't Let the LLM Drive

> Two Microsoft engineers explain how they made a live AI voice tutor reliable by moving all control flow out of the model and into a state-machine harness.

- **Speaker:** Ornella Bahidika & Joel Allou, Microsoft
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=m24UKZomm7k) (AI Engineer channel; ~6m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Bahidika and Allou built Ace, a live AI voice tutor that runs a full lesson start to finish. Their opening claim frames the whole talk: multi-step agents fail in production because reliability is a control problem, and prompting harder does not fix it. Bahidika describes the familiar failure pattern. The demo works, then a real user gets in, and halfway through the agent decides it is done, skips a step, or loops. Her framing is that the model is the talent and the harness is the director. The model delivers a line well but is bad at remembering whether it is on step three of six, so they stopped asking it to.

The design is a small state machine. A lesson has six states: intro, teach, check, grade, advance, and wrap. Each step sends the model a narrow contract that says do this one thing and return it. The harness validates what comes back, advances the state, and decides what happens next. The model never decides where the lesson is. Allou summarizes the division of labor in one sentence: the model proposes, the harness decides.

Allou then makes the cost argument. A live tutor speaking back and forth with students needs to be reliable, cheap, and fast at the same time. Instead of routing everything through a heavy frontier model, which he names as Claude Opus 4.7, the harness confines each step so tightly that a much smaller model, Haiku 4.5, performs at the level they need. He says the smaller model lacks the reasoning depth of the larger one, but the harness makes that irrelevant while cutting cost and latency. A recorded lesson plays with logs on screen showing the harness layers in action: a section harness that tells the model exactly what to speak about, a whiteboard drawing harness, queue clearing, and lesson-ending logic. Three questions got engineered outside the model entirely: when is the lesson done, did the student actually learn the material, and what comes next.

The pair close with a transfer argument and a decision rule. Allou says the pattern applies beyond voice tutors, listing coding agents, ops runbooks, and onboarding flows. The rule for when to apply it: if your agent's reliability feels like a coin flip, take the control flow out of the model, build the decisions around it, and feed it inputs simple enough that it can reliably produce outputs. The closing line restates the title. Let the model talk, but don't let it drive.

## Notable moments

- [0:00:14](https://www.youtube.com/watch?v=m24UKZomm7k&t=14s) Bahidika names the production failure mode: near the demo everything works, then a real user arrives and the agent decides it is done halfway through.
- [0:01:03](https://www.youtube.com/watch?v=m24UKZomm7k&t=63s) The six-state lesson machine, and the contract where the harness validates, advances state, and decides next steps.
- [0:02:04](https://www.youtube.com/watch?v=m24UKZomm7k&t=124s) Allou explains swapping Opus 4.7 for Haiku 4.5 once the harness confines each step, saving money and latency.
- [0:05:10](https://www.youtube.com/watch?v=m24UKZomm7k&t=310s) The coin-flip rule for when to pull control flow out of the model.

## Connections

- [Microsoft](../../companies/cloud-compute/microsoft.md), the speakers' employer and a major agent-platform vendor in its own right.
- [Session recaps](../../notes/session-recaps.md) cover an in-person session on sandbox, tools, and subagents as harness primitives, the same design layer this talk argues over.
