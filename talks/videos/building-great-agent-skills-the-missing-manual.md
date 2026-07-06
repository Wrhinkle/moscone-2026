# Building Great Agent Skills: The Missing Manual

> A four-part checklist for writing and auditing agent skills: trigger, structure, steering, and pruning.

- **Speaker:** Matt Pocock, AI Hero (no byline in the video metadata; the talk references his mattpocock skills repo and aihero.dev newsletter)
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=UNzCG3lw6O0) (AI Engineer channel; ~21m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Recorded remotely after family matters kept him from San Francisco, this talk diagnoses what the speaker calls skill hell: thousands of freely downloadable agent skills, no shared rubric for telling good ones from bad, and organizations unable to turn their operating procedures into things an agent can run. He maintains one of the most popular engineering skill repos and says he feels partly responsible, so the talk delivers a checklist with four sections. The whole framework also ships as a skill called writing-great-skills in his repo.

Section one is the trigger. Skills can be user invoked or model invoked, and he frames the choice as a trade between two loads. Every model invoked skill puts its description into the agent's context, so 100 model invoked skills means 100 descriptions taxing every request; that is context load. User invoked skills keep the context clean but require the pilot to remember what exists and when to use it; that is cognitive load. He contrasts his repo with the popular superpowers set, which is mostly model invoked, and explains why he prefers user invocation: every context pointer the model can choose to follow is a source of unpredictability, and skipping model invocation removes the whole class of evals that check whether a skill fired at the right time.

Section two is structure. He decomposes skills into two units, steps and reference, using his to-PRD skill as the worked example: three steps (gather context, confirm test seams with a human in the loop, write the document) plus two reference pieces (a definition of test seams and a PRD template). The constraint is keeping skill.md as small as possible, since every shaved word is a token saved on every use. His main technique is branch analysis: if reference material is only needed on one branch of the skill, move it to a separate file behind a context pointer, as his domain-modeling skill does with its ADR and glossary templates.

Section three, steering, carries what he calls the main idea of the talk: leading words. These are short phrases that pack dense meaning, get repeated by the agent in its own reasoning traces, and thereby change behavior. His example is fixing layer-by-layer coding by seeding the phrase vertical slice, then watching the reasoning trace say "we're going to do this as a thin vertical slice." A second steering lever is leg work: when an agent skimps on a step because it can see the end goal, split the step into its own skill. He argues every plan-mode implementation he has tried under-asks clarifying questions for exactly this reason, so he separated grill-with-docs from to-PRD so the agent sees one phase at a time.

Section four is pruning: enforce a single source of truth to kill duplication, clear out sediment that accumulates when many people append to a shared file, and run deletion tests to find no-ops, paragraphs that appear to do something but change nothing if removed. His example: deleting an instruction to write long commit messages usually changes nothing, because the agent does that anyway.

## Notable moments

- [0:05:01](https://www.youtube.com/watch?v=UNzCG3lw6O0&t=301s) Context load versus cognitive load, and why his repo differs from superpowers on model invocation.
- [0:11:03](https://www.youtube.com/watch?v=UNzCG3lw6O0&t=663s) Hiding branch-specific reference material behind context pointers to shrink skill.md.
- [0:13:04](https://www.youtube.com/watch?v=UNzCG3lw6O0&t=784s) The leading words technique, with vertical slice as the fix for layer-by-layer coding.
- [0:15:04](https://www.youtube.com/watch?v=UNzCG3lw6O0&t=904s) Why plan mode never asks enough clarifying questions, and splitting skills to force leg work.

## Connections

- [Session recaps](../../notes/session-recaps.md): the Anthropic in-person session covered a related discipline of process design for not handing all the work to the agent.
- [WebXSkill: skill learning for autonomous web agents](../../papers/tool-use-governance/webxskill-skill-learning-for-autonomous-web-agents.md): the research-side counterpart, where agents learn skills instead of humans authoring them.
