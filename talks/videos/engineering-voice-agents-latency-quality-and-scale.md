# Engineering voice agents: Latency, quality, and scale

> A component-by-component tour of the pipeline architecture for production voice agents, with concrete latency budgets and a look at where speech-to-speech models fall short today.

- **Speaker:** Rishabh Bhargava, Together AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=N7b1PJc7SFc) (AI Engineer channel; ~25m, released 2026-05-31)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Bhargava leads the voice AI team at Together AI, having joined when Together acquired Refuel, the company he co-founded. His premise is that rich voice conversations stopped being a research problem and became an engineering problem in 2026, and the engineering constraint is unforgiving: humans respond to conversational cues in about 300 milliseconds, users notice past 500 milliseconds, and at one to two seconds they hang up. A production voice agent has to hit that latency while staying smart enough for tool calling, sounding natural, and holding up across thousands of concurrent calls. He calls it an and problem, since failing any one dimension sinks the product.

The dominant answer is the pipeline (cascading) architecture: audio streams through an orchestrator such as Pipecat, LiveKit, or something homegrown, into speech-to-text, into an LLM that decides on tool calls, into text-to-speech, and back out. For STT, state-of-the-art models sit around 6 percent word error rate on open benchmarks, and errors there are unrecoverable because the LLM and TTS carry them forward; models Together runs complete transcripts at a P90 around 100 milliseconds after the speaker stops. Turn detection remains, in his words, somewhat unsolved. He flags an architectural shift from batch STT to streaming-native models: Whisper was trained on 30-second clips and needs chunking and silence padding, while a recent NVIDIA model trains its encoder with 80 milliseconds to one second of look-ahead and caches activations so each new audio frame does the heavy computation only once. For the LLM, time to first token should land near 200 to 300 milliseconds, which pins usable model size to roughly 8 to 30 billion parameters; bigger burns the latency budget, smaller loses the tool calling. TTS is judged on time to first audio and real-time factor below one, with emotion-control tags improving but quality still best assessed by listening.

System-level advice follows. The LLM takes the majority of both latency and cost budgets, then TTS, then STT. Autoscaling is asymmetric: scale up early because backed-up requests are fatal, and scale down carefully because stateful long-lived connections mean you cannot arbitrarily kill a pod mid-conversation. His sharpest number is on co-location: in an already optimized pipeline, a 75 millisecond network hop between orchestrator and models (roughly US West to Europe) versus 5 milliseconds intra-datacenter is about a 30 percent reduction in total response time, so putting all the models and the orchestrator in the same building matters.

He closes with speech-to-speech models: OpenAI's realtime API and NVIDIA's recent voice model collapse the pipeline into one model that keeps tone, emotion, and hesitancy, and enables full duplex behavior like backchanneling while the user is still talking. Teams try them, spend weeks prompt engineering around weak instruction following and tool calling, and move back to pipelines, though he expects that to change. In the Q&A he describes guardrail classifiers slotted before the LLM and before TTS, and a thinker-talker pattern where a small conversational LLM says "let me check" while issuing one tool call to a much larger model that produces the substantive answer.

## Notable moments

- [0:07:20](https://www.youtube.com/watch?v=N7b1PJc7SFc&t=440s) The batch-to-streaming shift in STT: NVIDIA's encoder with sub-second look-ahead and cached activations versus Whisper's 30-second clips.
- [0:08:21](https://www.youtube.com/watch?v=N7b1PJc7SFc&t=501s) Why the 200 to 300 millisecond TTFT budget forces LLMs into the 8 to 30 billion parameter range.
- [0:13:25](https://www.youtube.com/watch?v=N7b1PJc7SFc&t=805s) The co-location math: dropping a 75 millisecond network hop to 5 cuts about 30 percent off an optimized voice agent's response time.
- [0:22:32](https://www.youtube.com/watch?v=N7b1PJc7SFc&t=1352s) The thinker-talker pattern: a small LLM holds the conversation while a big model does the real work behind one tool call.

## Connections

- [Together AI](../../companies/models-inference/together-ai.md) is the speaker's company; the talk doubles as the case for running all three pipeline models on one inference cloud.
- [LiveKit](../../companies/voice-realtime/livekit.md) is one of the two agent orchestrators he names in the reference architecture.
- [Daily](../../companies/voice-realtime/daily.md) makes Pipecat, the other named orchestration option.
- [LTS-VoiceAgent: a listen-think-speak framework](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md) formalizes a split similar to the thinker-talker pattern from the Q&A.
