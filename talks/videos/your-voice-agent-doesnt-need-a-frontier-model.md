# Your Voice Agent Doesn't Need a Frontier Model

> A five-minute case for running voice agents on small models: move all reasoning into a state machine outside the model so a Haiku-class model can start talking inside a 950 millisecond budget.

- **Speaker:** Joel Allou & Ornella Bahidika, Microsoft
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=fnLBmfsI_Fg) (AI Engineer channel; ~6m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Bahidika and Allou built Ace, a live AI voice tutor that runs on a small model on purpose, and this short talk explains why that is a design choice rather than a compromise. Bahidika's framing is that a voice budget is measured in milliseconds, not IQ. When a voice agent pauses for even a second, the caller's brain decides it is dead. Ace's model needs to start talking in about 950 milliseconds, so a frontier model that thinks for a full second has already lost the room no matter how good its answer is.

The architecture removes the hardest jobs from the model entirely. The model does not decide what happens in the lesson, does not track what the student knows, and does not plan what comes next. Allou describes extracting all of that thinking into a state machine that covers every lesson scenario and coordinates each step to the next, with an intelligence layer on top that derives the mastery a student needs for the lesson to complete. Every turn, the system hands the model a summary, and the model does the one thing it is good at: talking. Sequencing, what to display, and how to answer are all computed outside the model in code, and the model speaks the output.

The demo makes the tradeoff concrete with two side-by-side videos of the same simple question. Without the scaffolding, a frontier Claude Opus model reasons for a couple of seconds before answering. With the state machine in place on Claude Haiku 4.5, a much smaller model, the answer arrives in about 900 milliseconds and feels almost instant, because the smart parts already happened before the model spoke. Allou is direct about the cost: a small model like Haiku 4.5 without scaffolding drifts on long structure and needs strict rules to stay organized. The scaffolding is the price, but you pay it once, in code, rather than on every turn in tokens and latency.

The closing rule generalizes: pick the fastest model your latency budget allows, then spend the rest of your time building the scaffolding, the state machine, the reasoning process, and the scenario handling outside the model. Allou argues this holds for voice, for any real-time application where latency is the priority, and for anything high volume, cases where the model is the smallest part of the system.

## Notable moments

- [0:00:30](https://www.youtube.com/watch?v=fnLBmfsI_Fg&t=30s) The budget: the model must start talking in about 950 milliseconds, and a full second of thinking loses the room.
- [0:03:01](https://www.youtube.com/watch?v=fnLBmfsI_Fg&t=181s) Side-by-side demo: the frontier model reasons for seconds while scaffolded Haiku 4.5 answers in about 900 milliseconds.
- [0:04:01](https://www.youtube.com/watch?v=fnLBmfsI_Fg&t=241s) The honest cost accounting: small models drift without strict scaffolding, but you pay that price once in code.

## Connections

- [Microsoft](../../companies/cloud-compute/microsoft.md) is the speakers' company, whose agent stack this small-model pattern sits inside.
- [LTS-VoiceAgent](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md) formalizes the same separation of thinking from speaking for real-time voice.
- [Vapi](../../companies/voice-realtime/vapi.md) orchestrates the STT to LLM to TTS pipeline where this pick-the-fastest-model rule gets applied in practice.
