# Browser Agents Don't Need Better Models. They Need Better Eyes.
> A short demo arguing that browser agents fail because of their page representation, and showing a compressed markdown view of the DOM that makes a cheap model fast and reliable.

- **Speaker:** Kushan Raj, ARK
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=JnubYCYunk8) (AI Engineer channel; ~4m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Kushan Raj, previously a founding engineer at Seraphim for two years, opens with the adoption puzzle: browser agents sound compelling but he does not use them himself, and neither do most people. His diagnosis comes from watching an agent run a browser challenge benchmark with a 30-step task list. The agent spends 10 to 20 seconds just clicking the start button, then loops on screenshots while trying to debug what it clicked and why nothing happened. His hypothesis is that the models are smart enough and the infrastructure around them is what fails. Give the agent an environment where it can see the whole page cheaply and get feedback on its actions, and it can plan long sequences correctly.

The core of his approach is a representation that compresses a web page into markdown the model can read in full. His comparison, run on a real page: the full DOM would cost around 20,000 tokens, a screenshot costs about 1,100 tokens but shows only the visible snippet, and his markdown costs about 1,800 tokens while covering the entire page. On top of the representation he layers diff-style feedback between steps: which elements appeared, which disappeared, whether the overlay that blocked a click target is now gone, and whether the click the agent attempted actually registered, all tracked end to end across the session. The combination lets a much cheaper model reason about the page and construct long action sequences without the screenshot-scroll-screenshot loop.

Two head-to-head examples carry the demo. In the first, Claude tries to download an Aadhaar document: it takes the screenshot, finds the obvious button, clicks it, then gets stuck scrolling and re-screenshotting for the rest of a two-minute run. Raj's agent boots and completes the same task almost immediately. In the second, he asks an agent to book a trekking date on a Canadian booking site he found confusing himself; Claude cannot pick the date and stalls, while his agent selects the date and finishes. He is careful to note the cheaper model both times, since the point is that the representation, and only secondarily the model, drives the outcome.

On what comes next, Raj says the code is not especially defensible, so he is considering open sourcing the project and productizing it as an API: send a URL and an intent, get the executed result back, possibly also as a website or a plugin. The stated goal is to make browser agents faster, cheaper, and reliable enough that people actually use them.

## Notable moments
- [0:00:00](https://www.youtube.com/watch?v=JnubYCYunk8&t=0s) A benchmark agent takes 10 to 20 seconds to click a start button on a 30-step task.
- [0:01:01](https://www.youtube.com/watch?v=JnubYCYunk8&t=61s) Aadhaar download: Claude loops for two minutes, his agent finishes almost instantly.
- [0:03:02](https://www.youtube.com/watch?v=JnubYCYunk8&t=182s) Token math: full DOM near 20,000 tokens, screenshot 1,100, his full-page markdown 1,800.
- [0:04:02](https://www.youtube.com/watch?v=JnubYCYunk8&t=242s) Diff feedback: what appeared, what vanished, and whether the attempted click landed.

## Connections
- [Browserbase](../../companies/browser-computer-use/browserbase.md) supplies the browser infrastructure layer this talk argues is the real bottleneck for agents.
- [WebXSkill](../../papers/tool-use-governance/webxskill-skill-learning-for-autonomous-web-agents.md) tackles the same web-agent reliability problem through learned skills rather than page representation.
- [AI planning framework for LLM-based web agents](../../papers/tool-use-governance/ai-planning-framework-for-llm-based-web-agents.md) formalizes the long-sequence planning that Raj's compressed representation is meant to enable.
