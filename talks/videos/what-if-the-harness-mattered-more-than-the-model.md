# What if the harness mattered more than the model?

> A case for investing in harness engineering, demonstrated by building a coding agent seven ways in Agency, a new language for writing agents.

- **Speaker:** Aditya Bhargava, Etsy
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=2e9ANoOEn28) (AI Engineer channel; ~32m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Bhargava, a staff engineer at Etsy and author of Grokking Algorithms, pushes back on the advice that models are now good enough to keep the harness thin. He argues that reasoning makes the industry dependent on proprietary frontier models, and that the more useful question is whether a harness can be built well enough that a local open-source model matches cutting-edge performance. He cites a harness benchmark, HarnessBench, with 106 tasks: holding the model and evaluation constant while swapping harnesses moved scores from 52.4% to 76.2%, a gap of more than 20 points, and the effect was larger for weaker models. If a good harness compensates for a weak model, anyone can build one, and nobody has to wait on a handful of labs.

His second claim is that building a good harness requires language-level support, which none of the existing frameworks gave him. He spent six months building Agency, a language for writing agents that looks like TypeScript with some Python syntax. In his terminology an agent is a model plus a harness: Claude Code is the agent, Opus is the model, everything else is the harness.

The body of the talk evolves one coding agent through seven versions of the same task, fixing a buggy median function with a failing test, with the model held constant while the harness improves. Version one is a bare LLM call, which can only reply that it needs to see the code. Version two adds read and write tools; in Agency any function becomes a tool automatically, with its docstring used as the tool description. Agency refuses to run this version because unrestricted file access is unsafe by default. Version three wraps the tools in a handler block: standard-library functions that mutate state or read sensitive data raise an interrupt, and the handler asks the human to approve each call. That is safe but slow. Version four removes the human with partial function application: calling partial on the read tool locks its directory argument to demo, so the LLM never sees the argument and can only touch files inside that directory. Version five adds a ReAct feedback loop, reason, act, observe, so the agent reads the files, runs the tests, edits the code, and reruns the tests to confirm the fix, the first version that actually repairs the file end to end. Version six introduces sub-agents, which in Agency are just functions passed as tools; the top-level agent calls a coding sub-agent and a Wikipedia sub-agent in parallel, keeping unrelated tools out of each other's context. Version seven runs Agency's built-in GEPA-style optimizer over variables marked with an optimize modifier, establishing a 0.2 baseline objective and rewriting the prompts against a stated goal, replacing guess-and-check with measured improvement.

Bhargava closes on Agency's pause-and-resume execution: an interrupt raised inside a for loop, a tool call, or a sub-agent serializes execution, returns control to the user, and can resume at that exact point a week later with no code changes. His summary ladder for harness building: give the agent tools, make it safe, make it autonomous, make it reason, give it sub-agents, and have it self-optimize.

## Notable moments

- [0:02:01](https://www.youtube.com/watch?v=2e9ANoOEn28&t=121s) HarnessBench numbers: same model and evaluation, scores range 52.4% to 76.2% across harnesses.
- [0:16:13](https://www.youtube.com/watch?v=2e9ANoOEn28&t=973s) Partial function application locks the directory argument so the agent runs unattended but stays sandboxed.
- [0:20:16](https://www.youtube.com/watch?v=2e9ANoOEn28&t=1216s) The feedback-loop version reads the files, runs tests, writes the fix, and confirms the tests pass.
- [0:30:25](https://www.youtube.com/watch?v=2e9ANoOEn28&t=1825s) Interrupts pause execution anywhere, serialize it, and resume at the exact point later.

## Connections

- [Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) makes the same core claim with data, that a non-model component can move a score as much as a model-generation jump.
- [Session recaps](../../notes/session-recaps.md) covers Google DeepMind's open question about a programming language designed for LLMs and the DSPy session on GEPA, both directly adjacent to Agency's design.
- [LangChain](../../companies/agent-orchestration/langchain.md) is the incumbent framework approach to harness building that Bhargava argues falls short of language-level support.
