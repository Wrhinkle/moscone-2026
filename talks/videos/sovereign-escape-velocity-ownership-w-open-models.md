# Sovereign Escape Velocity: Ownership w Open Models

> Two Google DeepMind Gemma team members pitch the just-released Gemma 4 family as the ownership answer for teams that cannot or should not send data to a hosted frontier model.

- **Speaker:** Gus Martins & Ian Ballantyne, Google DeepMind
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=SS-A8sE7hkw) (AI Engineer channel; ~21m, released 2026-06-10)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Martins opens by conceding that Gemini is Google's strongest model, then explains why Google ships two families: Gemini for maximum intelligence behind an API, Gemma for control. If you need to run on your own hardware, customize the weights, or keep proprietary data inside your infrastructure, a hosted model cannot help, and that is the gap Gemma fills.

Gemma 4, released the week before the talk, comes in four sizes. The E2B and E4B target phones and edge devices; the E stands for effective, meaning the E2B has roughly 5 billion parameters but only 2 billion need to sit in GPU memory, since the rest are token embeddings that can live in other memory. Both take text, vision, and audio input, output text, and handle thinking, coding, and function calling on a phone. The larger pair is a 26B mixture-of-experts that activates about 4 billion parameters per pass, and a 31B dense model that Martins calls the strongest. He cites LMArena ELO placement at fourth and seventh among open models, against competitors that are two to twenty times larger, and notes the 31B runs on a single GPU where rivals need around 200 GB of memory across four or five GPUs. His framing question: do you need the most intelligent model on the planet to summarize your mail?

Martins ties ownership to sovereignty. Gemma 4 drops the custom Gemma license for Apache 2.0, which he says removes the 18-month procurement slog custom licenses trigger in legal departments and unblocks sovereign institutions. He lists examples: Ukraine using Gemma in government services, a Bulgarian national LLM fine-tuned from Gemma 2, and a Brazilian Portuguese variant built on Gemma 3. He adds a candid wrinkle: language fine-tuning is getting harder to justify because the base model is already strong in many languages, so months of work may buy 1 percent.

Ballantyne takes over with the economics of agents. Citing OpenRouter's state of AI report, he notes programming sits among the highest tasks in combined input and output token generation, which is exactly where owning the model on sunk-cost hardware pays off. The Gemma-scale models will not do a full systems architecture redesign, he says, but they reliably follow specific instructions for refactoring, analysis, and modular code generation, so chunks of agent work can be offloaded to a laptop GPU. He frames adoption as three thresholds: is the model capable of the task, does it fit the hardware with acceptable latency, and what does running it cost, noting that on-device the currency shifts from tokens to energy and GPU or NPU utilization. On the enterprise side he points to serving the 31B on a single H100, A100, or even an L4, and to fine-tuned variants like MedGemma running a whole hospital's private workloads on one or two GPUs.

The demos show the range: the Google AI Gallery app running the 2B model on a phone with agent skills that trigger calendar and maps apps, with Gemma 4 now reasoning reliably about which function calls to make, and an LM Studio setup on an M4 Mac with 48 GB of unified memory, where the 26B model at about 26 GB in RAM fans a translation job out to parallel sub-agents and compiles the results into a web page. His closing advice: drop Gemma into existing OpenAI-compatible workflows with a one-line endpoint change, then build evals on your own tasks rather than trusting benchmarks.

## Notable moments

- [0:02:17](https://www.youtube.com/watch?v=SS-A8sE7hkw&t=137s) The E2B/E4B naming explained: 5 billion parameters, but only 2 billion need GPU memory.
- [0:07:20](https://www.youtube.com/watch?v=SS-A8sE7hkw&t=440s) The Apache 2.0 switch and why custom licenses stall sovereign adoption for 18 months.
- [0:13:22](https://www.youtube.com/watch?v=SS-A8sE7hkw&t=802s) Phone demo: Gemma 4 2B reasoning over device skills and making reliable function calls.
- [0:17:25](https://www.youtube.com/watch?v=SS-A8sE7hkw&t=1045s) Local multi-agent translation demo on an M4 Mac, sub-agents fanning out through LM Studio.

## Connections

- [Google DeepMind](../../companies/models-inference/google-deepmind.md), the speakers' organization and home of the Gemma line.
- [OpenRouter](../../companies/models-inference/openrouter.md), whose state of AI traffic report Ballantyne uses to argue programming tokens dominate agent costs.
- [Session recaps](../../notes/session-recaps.md), which cover the in-person Google DeepMind session for adjacent model-direction commentary.
