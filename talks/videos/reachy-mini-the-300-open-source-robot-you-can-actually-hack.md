# Reachy Mini: the $300 open source robot you can actually hack

> Hugging Face's case for a cheap, hackable, deliberately non-humanoid desk robot, plus the voice pipeline and TTS inference optimizations that let 7,500 shipped units hold conversations.

- **Speaker:** Andres Marafioti, Hugging Face
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=0jeZfjJMfmo) (AI Engineer channel; ~21m, released 2026-05-29)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Marafioti, who leads multimodal research at Hugging Face, argues robotics is advancing fast and in the wrong shape for experimentation. Humanoids start around $50K and self-driving cars run into six figures, so no high school orders ten of them for students to play with. He also questions the humanoid form itself: it exists so people can reason about what the robot does, when a spider-shaped machine might be faster, more agile, and more stable. Reachy Mini is Hugging Face's answer, an expressive desk robot aimed at hackers, researchers, students, and dreamers. Two versions sell for $450 and $300; the more expensive one adds a Raspberry Pi and a battery, and the cheaper one sells in bulk to schools. The robots ship unassembled on purpose, so owners learn to repair anything that breaks. Community hacks include 3D-printed Halloween parts and someone discovering the robot reacts to being petted. It also stacks with Hugging Face's other open hardware, the SO100 and SO101 arms and the three-wheeled Kiwi base.

The middle of the talk covers how conversation actually gets served. Marafioti maintains Hugging Face's speech-to-speech pipeline: voice activity detection feeds a speech-to-text model (Parakeet, chosen for speed, transcribing every 150 milliseconds and streaming partial transcriptions so the robot can react mid-sentence), then an LLM that can also tool-call for movements and camera use, then a text-to-speech model. On the robot itself, a conversation app handles echo cancellation, tool dispatching for emotions and movement, and camera face tracking. Because owners are, in his words, GPU poor, the pipeline runs on Hugging Face inference endpoints with a load balancer scaling compute nodes to the number of connected robots. The LLM (a 27B open model) is scaled separately from the conversation nodes, since eight chatty users and eight quiet ones on the same node load the system very differently. With 7,500 robots shipped, the conversation app is the most used app on the fleet.

The most technical section covers making a recently released open TTS model (rendered as "Coqui 3 TTS" in the auto-captions) fast enough for voice agents; Marafioti says the released weights matched the paper's quality claims but not its latency claims, and he spent about two weeks fixing that. The model generated a full utterance before returning anything, so he added streaming. As an autoregressive model it ran 500 steps per audio packet with CPU-GPU round trips on each, so he swapped the dynamic KV cache for a static one and used CUDA graph capture to keep generation on the GPU. Real-time factor went from 0.8 (slower than real time) to 5.8, and time to first audio dropped from seconds to under 200 milliseconds. He notes infrastructure overhead now costs as much as the model itself, a reminder that voice agent latency budgets include everything around inference. Everything, models, agents, and the optimized TTS, is open source, and he says a working robot app can be one-shotted by a coding agent pointed at the repo.

## Notable moments

- [0:05:16](https://www.youtube.com/watch?v=0jeZfjJMfmo&t=316s) The design goals: non-humanoid on purpose, affordable, shipped unassembled so it stays repairable.
- [0:08:19](https://www.youtube.com/watch?v=0jeZfjJMfmo&t=499s) Demo video: the robot banters, takes a photo, describes Marafioti's outfit, and performs a happiness emote.
- [0:10:20](https://www.youtube.com/watch?v=0jeZfjJMfmo&t=620s) Serving architecture for the 7,500-robot fleet: speech pipeline nodes load-balanced separately from LLM endpoints.
- [0:13:21](https://www.youtube.com/watch?v=0jeZfjJMfmo&t=801s) TTS optimization details: streaming, static KV cache, CUDA graphs, real-time factor 0.8 to 5.8.

## Connections

- [Hugging Face](../../companies/models-inference/hugging-face.md): the speaker's company; the profile covers the LeRobot robotics stack and Pollen Robotics acquisition behind this hardware line.
- [Gradium](../../companies/voice-realtime/gradium.md): the Paris voice AI lab Marafioti points to as evidence that commercial voice agents are mature.
