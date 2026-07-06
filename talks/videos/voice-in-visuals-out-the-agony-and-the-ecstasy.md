# Voice In, Visuals Out: The Agony and the Ecstasy

> Allen Pike on why voice input plus visual output is the interaction model to build for now, and the three latency techniques that make it feel instant.

- **Speaker:** Allen Pike, Forestwalk Labs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=65X0pQ6Lmbg) (AI Engineer channel; ~13m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Pike builds on Andrej Karpathy's argument from the month before: voice is the human-preferred input for AI, visuals the preferred output, yet most of us still type to models that type back markdown. He takes the visuals-out half as intuitive, a third of the brain processes visual information, and models can now return rich HTML, interactive controls, and illustrations. The controversial half is voice in. Most people's reference experience is Siri failing to turn the lights on or ChatGPT voice mode being awkward, which Pike summarizes as slow and dumb. He defends speech anyway: it carries more words per minute than typing and more meaning per word, which is why people jump on a call when something matters.

Forestwalk built an agent that sits in the team's calls and acts on spoken intent. Pike recounts mentioning a suspected Slack-integration bug to his co-founder on a call, saying "let's file that as a Linear issue," and having the voice agent confirm the filing within a second, without interrupting the conversation. The barrier to making that feel natural is what he calls the tyranny of latency. He cites three human thresholds known since the 1960s: about 100 milliseconds to feel instant, about 1,000 milliseconds before people lose their train of thought, and 200 milliseconds or less for full voice-in-voice-out conversation with interruptions and interjections. Running network, speech-to-text, inference, and the return trip inside 200 milliseconds is, in his words, ridiculous. He notes a recent demo he attributes to Thinking Machines that time-slices continuous inference into 200-millisecond chunks, but his practical answer is to switch the output channel: voice in, visuals out, which relaxes the budget to the one-second visual envelope.

He closes with three techniques for staying inside that envelope. First, use a genuinely fast model on an inference platform that prioritizes latency. When GPT-5 mini launched, Forestwalk measured 5,000-millisecond latencies, 7,000 at P95, sometimes 10,000, despite the model being small and cheap; Haiku's P95 was much better, so he recommends a Haiku-class or small open-source model for the real-time path, handing heavier work to a larger model asynchronously and interleaving its results back in. Second, use short inference intervals: waiting for a second of silence blows the budget before inference starts, so send speculative inference every one to two seconds while the person is still talking. Third, keep a stable caching regimen. Prefix caching can make inference up to 90 percent cheaper and faster, so structure requests so the first 90 percent of the context is identical from turn to turn, vary only the tail, and minimize output tokens. Pike argues the same principle now applies to most long-running or frequently running agents, and invites anyone experimenting at these boundaries to compare notes.

## Notable moments

- [0:04:02](https://www.youtube.com/watch?v=65X0pQ6Lmbg&t=242s) The in-call agent files a Linear issue from an offhand spoken request and confirms within a second.
- [0:05:02](https://www.youtube.com/watch?v=65X0pQ6Lmbg&t=302s) The tyranny of latency: the 100ms, 1,000ms, and 200ms human thresholds that box in voice UX.
- [0:09:04](https://www.youtube.com/watch?v=65X0pQ6Lmbg&t=544s) GPT-5 mini measured at 5,000 to 10,000ms latency in practice versus Haiku's far better P95.
- [0:11:05](https://www.youtube.com/watch?v=65X0pQ6Lmbg&t=665s) The caching regimen: keep the first 90 percent of context stable for up to 90 percent cheaper, faster turns.

## Connections

- [Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md): formalizes the eager-inference-versus-waiting-for-silence tradeoff Pike solves by inferring every one to two seconds.
- [Building Interactive Real-Time Agents with Asynchronous I/O](../../papers/voice-realtime/building-interactive-real-time-agents-with-asynchronous-i-o.md): the same fast-model-plus-async-heavy-model split Pike recommends for the real-time path.
- [LiveKit](../../companies/voice-realtime/livekit.md): supplies the real-time transport layer that in-call agents like Forestwalk's ride on.
