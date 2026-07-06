# Voice Agents That Handle Interrupts
> Two AWS solutions architects break turn taking in voice agents into three implementation levels, from a silence timer to a local turn detection model, with latency budgets and a live Pipecat demo.

- **Speaker:** Chintan Agrawal, Amazon Web Services (with Daniel Weijia, AWS)
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=hMlLw1LeIK8) (AI Engineer channel; ~33m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary
Agrawal, a solutions architect on the AWS APJ startup team, frames turn taking as an audio engineering problem rather than an LLM problem: the same model and prompt can feel broken or natural depending on how fast the pipeline notices a user speaking. His anchor number is 200 milliseconds, the speed at which humans switch turns in conversation. At 800 ms an agent starts to feel off, and at 1.5 seconds users hang up. He cites Salesforce results published in March 2026 where the best measured response time was 755 ms, roughly 4x slower than human turn taking, so the pipeline has to compensate with better turn detection.

The pipeline he describes is the standard STT, LLM, TTS cascade plus three pieces people miss: voice activity detection (VAD) at the front, a smart turn detector that decides whether to respond or wait, and an interruption handler that flushes TTS and cancels LLM generation within about 50 ms on a barge-in.

He then walks three levels of turn detection. Level one is Silero VAD, a 300,000 parameter, 2 MB model (spectral features into four convolutional layers, an LSTM, and a sigmoid speech probability) where the minimum-silence parameter is the entire user experience: around 200 ms for a snappy sales agent, 1,000 to 1,200 ms for domains where users need time. Its limit is that a 300 ms pause looks identical whether the user finished a thought, is catching a breath, or is just saying "yeah" as a backchannel. Level two delegates endpointing to the STT provider; Agrawal quotes roughly 300 ms P50 for Cartesia's in-socket turn detection and about 250 ms for Deepgram Nova 3, with the trade-off that misfires happen inside someone else's server with no explanatory logs. Level three keeps local VAD as a safety net and adds Smart Turn v3.2, an 8 MB BSD-2 licensed model with 58.9 percent recall and 68.4 percent precision, so about six in ten completed sentences get a fast response and the VAD timer catches the rest. A Meta paper from around March reported 87.7 percent recall but shipped no code. Owning the classification also lets you triage interruptions: stop for a correction, keep going through a filler, ignore a cough.

On latency, he relays production measurements from Kwindla Hultman Kramer of Daily, creator of Pipecat: mic input about 40 ms, network and jitter buffer 52 ms, transcription plus endpointing about 300 ms, LLM time to first byte 500 to 650 ms as the dominant bottleneck, then TTS and playback, totaling roughly 1,100 to 1,300 ms for a cloud-API setup. Daily demonstrated about 500 ms voice-to-voice by co-locating all models on one GPU cluster. His June 2026 LLM benchmarks put Nemotron-3 Ultra at 529 ms P50 time to first token and GPT-4.1 at 536 ms, but he warns that P95 tails matter more in voice: GPT-4.1 spiked to 1.7 seconds and a Claude model exceeded 4 seconds at P95, and one slow turn breaks the whole flow. He also flags multi-turn drift after 15 to 20 turns and notes that false interruptions measurably raise escalations to human support. Weijia closes with a Pipecat demo showing all three levels as near-identical Python files where only the turn detection configuration changes, and the level-one agent visibly cuts him off mid-sentence at a 300 ms stop timer while levels two and three wait him out.

## Notable moments
- [0:01:03](https://www.youtube.com/watch?v=hMlLw1LeIK8&t=63s) Side-by-side problem statement: same LLM and prompt, but the left agent talks over a correction for 2 seconds while the right one backs off in under 200 ms.
- [0:10:12](https://www.youtube.com/watch?v=hMlLw1LeIK8&t=612s) Smart Turn v3.2 numbers: 58.9 percent recall, 68.4 percent precision, 8 MB, pip-installable, with VAD as the fallback timer.
- [0:15:19](https://www.youtube.com/watch?v=hMlLw1LeIK8&t=919s) Full latency budget breakdown from Daily production data; STT and LLM eat about two thirds of the 1,100 to 1,300 ms total.
- [0:25:23](https://www.youtube.com/watch?v=hMlLw1LeIK8&t=1523s) Demo failure on purpose: the Silero-only agent interrupts Weijia's unfinished "I'm thinking of going to um..." because the 300 ms silence timer fires.

## Connections
- [AWS](../../companies/cloud-compute/aws.md), the speakers' employer; the talk closes by pointing at an AWS guidance reference architecture for enterprise voice deployments.
- [Daily](../../companies/voice-realtime/daily.md), source of both the Pipecat framework used in every demo and the production latency numbers from co-founder Kwindla Hultman Kramer.
- [Deepgram](../../companies/voice-realtime/deepgram.md), cited as the level-two option with roughly 250 ms P50 endpointing in Nova 3.
- [Adaptive turn-taking for real-time multi-party voice agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md), research on the same endpointing problem the talk treats at the systems level.
