# Using Spec-Driven Development for Production Workflows

> A walkthrough of spec-driven development, writing requirements, design, and task documents before code, with AWS's Kiro IDE as the worked example.

- **Speaker:** Erik Hanchett, AWS
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=IddXPepIAS4) (AI Engineer channel; ~18m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Hanchett, a senior developer advocate at AWS with over 15 years of development experience, defines spec-driven development as writing structured specifications, in practice markdown requirements and design documents, before any code exists. His pitch is quality as much as speed. He compares coding assistants to AI interns who drop everything for the last instruction they heard, retelling a story about a VP whose hallway ideas derailed his own internship until he learned to write requests down and route them through his manager. Specs play that same disciplining role for LLMs.

To the objection that frontier models can already do everything, Hanchett answers that models improve incrementally and by leaps but remain imperfect, and that more context guides them in the right direction, especially as requirements change. He adds three cautions. Context has a Goldilocks zone: agents.md or claude.md steering files can carry too much information as easily as too little. Skills, on-demand instruction files triggered by keywords or slash commands, pair well with the spec workflow. And trust stays with the human: you review every generated document and every line of code, because you get blamed when it breaks, not the agent, though he endorses AI review tools and multiple human reviewers on top.

The history section explains where Kiro came from. AWS saw teams and customers vibe coding without getting the outputs they wanted, and some inventing a bespoke pattern of having agents write full requirements and design documents first. AWS shipped Kiro, an AI IDE plus a CLI, with explicit vibe and spec modes; the preview went viral enough that AWS gated downloads and people found a way around the gate. Hanchett is explicit that the process does not require Kiro: you can run it manually with any assistant by prompting for user requirements, then a design document, then an implementation task list, reviewing each in turn, and he gives a shout-out to GitHub's open source Spec Kit. He also pushes back on the greenfield assumption, saying he has seen years-old apps carrying dozens of spec files, and notes Kiro added a spec mode for bug fixes.

The mechanics: requirements documents use the EARS format with user stories, generated after clarifying questions; design documents include mermaid and sequence diagrams and are the point where he tells you to stop and inject your own expertise; the task list includes property-based tests generated against the requirements and design. His quick tip is to ask the assistant to reorder the top four tasks into an MVP so you see something working early. He also connects specs to MCP, arguing the protocol is still maturing rather than dead at six months old, because it lets the spec flow pull tickets and product-manager requirements straight from Jira or Asana when generating documents.

The demo builds a movie website in Kiro's spec mode, starting from the design document this time. It produces architecture and sequence diagrams, an EARS requirements file, and property-based tests using fast-check in TypeScript that run dozens to hundreds of times with varied values, including one verifying genre extraction returns a sorted set of unique genres. The regenerated task list labels tasks one through four as a working MVP with search, genre filtering, sorting, and an 80s synthwave theme.

## Notable moments

- [0:01:00](https://www.youtube.com/watch?v=IddXPepIAS4&t=60s) The AI intern analogy: assistants go off the rails with a little leeway, like a young Hanchett dropping everything for a VP's hallway ideas.
- [0:08:01](https://www.youtube.com/watch?v=IddXPepIAS4&t=481s) How to run spec-driven development without Kiro: requirements, then design, then tasks, with GitHub's Spec Kit as an open source option.
- [0:12:07](https://www.youtube.com/watch?v=IddXPepIAS4&t=727s) The MVP tip: ask the agent to move four tasks to the top so a working version ships before the rest of the list.
- [0:15:07](https://www.youtube.com/watch?v=IddXPepIAS4&t=907s) The Kiro demo, including property-based tests generated against the requirements document.

## Connections

- [AWS](../../companies/cloud-compute/aws.md) is the speaker's employer and ships Kiro, the IDE built around this workflow.
- [GitHub](../../companies/coding-agents/github.md) maintains Spec Kit, the open source alternative Hanchett recommends for other assistants.
- [Session recaps](../../notes/session-recaps.md) covers the in-person AWS Builder Loft session and Sonar's related push toward verification discipline in agent coding.
