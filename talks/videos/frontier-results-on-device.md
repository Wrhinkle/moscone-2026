# Frontier results, on device

> Arize's RL Nabors shows a repeatable eval-driven method for replacing frontier-model API calls with small on-device models, walked through on a real thread-summarization feature.

- **Speaker:** RL Nabors, Arize
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=fWXJM-J0ZB8) (AI Engineer channel; ~31m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Nabors, a web standards veteran (Mozilla, W3C, Microsoft Edge, the React team) now at Arize, opens with the costs of one-size-fits-all inference: cloud LLMs risk data exposure and retention, latency breaks user experience (research on LLM chat in VR puts the believability limit at 4 seconds), third-party inference spend is uncontrollable, and remote models fail offline. Token prices are falling, but total spend is rising because agentic workloads consume tokens faster than prices drop. The counter-move is task-specific models and small language models: MobileNet, YOLO, or MediaPipe for vision, Whisper or Wav2Vec2 for audio, Gemma or Qwen when you genuinely need a language model. SLMs run millions to a few billion parameters, deploy quantized at 4 or 8 bits, and by the research Nabors cites use about 25 percent of an LLM's energy for a task, with task-specific models about half of that again. She leans on Nvidia's 2025 position that SLMs are the future of agentic AI.

The method, built with Google and published at web.dev, is "prototype big, deploy small." First prove the task is possible with the largest capable model. Nabors demonstrates on Mima, her social client side project, which summarizes long conversation threads. She prototyped with Claude, exported a golden dataset of 14 threads with 28 labeled examples, and defined success up front: JSON validity, reference structural validity, factual consistency (LLM-judged), length compliance, and P50/P95 latency. She ran capability evals in Phoenix, Arize's open-source tool, with Claude Sonnet as the ceiling: 2.9 seconds average latency and $0.22 per 14-task run, about a dollar of inference per day of her own usage. The local contestants: Qwen 2.5 1.5B (fastest at about 1 second, weakest accuracy), Qwen 3 1.7B, Llama 3.2 3B, and Gemma 4 E2B, the model peers insisted she use, which averaged about 8 seconds. Llama 3.2 won at roughly 90 percent accuracy. Her label for the target is the SAGE model, the smallest model with acceptable responses, and the on-device cost column is zero because inference moves to the user's hardware.

Closing the last 10 percent came from prompt engineering, one variable per variant. Numbered input over JSON changed nothing, explicit negative rules made results worse, chain of thought added 600 milliseconds for little gain, and few-shot examples won: better length compliance and accuracy for 200 milliseconds. Opening the eval traces showed part of the remaining gap was the judge itself, Claude Opus grading its sibling Sonnet leniently and Llama strictly over wording like "angsty" versus "cross." Harness-level post-processing (truncating length, checking references against thread size) brought JSON and structural validity to 100 percent with P50 around 1 second, meeting or beating the Sonnet baseline. She closes with regression evals run like CI to keep a CTO's prompt tweak from silently degrading the feature, and a pointer to Gemini Nano already shipping in Chrome behind the Prompt API.

## Notable moments

- [0:01:01](https://www.youtube.com/watch?v=fWXJM-J0ZB8&t=61s) The 4-second latency limit of believability, and why frontier API calls often exceed it.
- [0:13:07](https://www.youtube.com/watch?v=fWXJM-J0ZB8&t=787s) Capability evals in Phoenix: Claude Sonnet baseline at 2.9s and $0.22 per run of the golden dataset.
- [0:15:07](https://www.youtube.com/watch?v=fWXJM-J0ZB8&t=907s) Coining the SAGE model: the smallest model that gives acceptable responses.
- [0:27:20](https://www.youtube.com/watch?v=fWXJM-J0ZB8&t=1640s) Cracking open eval traces reveals Claude the judge favoring Claude the contestant.

## Connections

- [Arize](../../companies/evals-observability/arize.md): the speaker's company; Phoenix, its open-source eval tool, runs every experiment in the talk.
- [Nvidia](../../companies/models-inference/nvidia.md): the talk's agentic case rests on Nvidia's 2025 paper arguing SLMs are the future of agentic AI.
- [Google](../../companies/models-inference/google.md): the right-sizing framework was built with Google and published at web.dev, and Chrome ships Gemini Nano via the Prompt API.
