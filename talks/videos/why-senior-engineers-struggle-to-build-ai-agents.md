# Why (Senior) Engineers Struggle to Build AI Agents

> A ten-minute list of five habits from traditional software that break when building agents, from treating text as state to replacing unit tests with evals.

- **Speaker:** Philipp Schmid, Google DeepMind
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=3_gYbhABcAE) (AI Engineer channel; ~11m, released 2026-05-30)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Schmid works on agents for Gemini and the Gemini API at DeepMind, and says he watches engineers hit the same walls daily, both inside Google and outside. His framing device: traditional software followed spec, code, tests, deploy, while agent building is an iterative loop of instructions, run, observe, adjust prompts and tools, run again. The engineer's role shifts from traffic controller, who decides the lights and the roads, to dispatcher, who names the destination and lets the agent pick the route, including routes that look weird but arrive.

He gives five concrete examples. First, text is the new state. Data structures and boolean flags cannot capture semantic meaning, so a deep research agent can now accept "approve the plan, but focus on the US market and ignore California" in one step instead of a decline-and-refine loop, and personalization such as "Celsius generally, but Fahrenheit for cooking" cannot be modeled as profile flags at all. Second, hand over control. The old customer-support pattern of an intent classifier feeding a predefined churn workflow cannot react when the user changes their mind mid-flow; Schmid argues you have to trust the LLM rather than force stateful workflows onto every path. Third, errors are just inputs. When HTTP requests were cheap you reran the whole thing, but an agent 15 minutes into a run cannot restart from scratch without burning compute and losing context, so failures should be fed back to the model like any other input, the way Go treats errors as values. Fourth, move from unit tests to evals. Agents are non-deterministic, so the same input does not guarantee the same steps or output; what matters is how often something works, judged on outcomes (with LLM-as-judge or human experts) rather than asserted step by step, because a prompt that works one time in ten is not shippable. Fifth, agents evolve and APIs don't. A delete-item endpoint is self-explaining to the team that built it, but an agent sees only schemas and docstrings, so tools need to be self-documenting with semantic interfaces rather than assuming years of tribal knowledge.

The closing summary compresses the five into slogans: give trust but verify, stop fighting the model, preserve meaning because everything is context now, design for recovery, evaluate rather than only assert, and build to delete, since software is disposable and will be rebuilt many times as models improve. The material, with code examples, is also on his blog.

## Notable moments

- [0:01:08](https://www.youtube.com/watch?v=3_gYbhABcAE&t=68s) The traffic controller versus dispatcher analogy for what agent builders actually control.
- [0:04:10](https://www.youtube.com/watch?v=3_gYbhABcAE&t=250s) Why the classic intent-classifier-plus-workflow support bot fails when the user changes their mind.
- [0:06:11](https://www.youtube.com/watch?v=3_gYbhABcAE&t=371s) Unit tests to evals: reliability as pass rate over runs, not input-output assertions.
- [0:09:16](https://www.youtube.com/watch?v=3_gYbhABcAE&t=556s) The closing rules, ending with build to delete.

## Connections

- [Google DeepMind](../../companies/models-inference/google-deepmind.md): the speaker's employer; the profile covers the Gemini agent tooling his examples draw on.
- [Session recaps](../../notes/session-recaps.md): overlaps the in-person Google DeepMind session on code complexity and what programming for LLMs should look like.
