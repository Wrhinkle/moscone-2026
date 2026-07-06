# The Prompt Is Still a Punch Card

> A case that prompting is a batch protocol inherited from punch cards, and that AI interfaces should participate in conversation instead of waiting for a packaged turn.

- **Speaker:** Ted Johnson, JoinIn AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=hVJOnuhFmTA) (AI Engineer channel; ~20m, released 2026-07-02)
- **Program:** Online Track 2026

## Summary

Johnson, co-founder of JoinIn AI with 25 years in enterprise software and collaboration systems, wants to make prompting feel strange again. His framework has three parts. The channel is the physical transport for intent: keyboard, microphone, screen, punch card, prompt box. Expression is how much meaning the channel lets through. The protocol is the shape and rules of the exchange. His diagnosis: with LLMs the channel stayed the same, expression exploded, and the protocol never advanced.

He grounds the channel idea in the keyboard, a layout patented around 1860, designed under constraints that vanished a century ago, which nobody alive chose and everyone stopped noticing. Expression, by contrast, made a real leap. Assembly gave a few dozen opcodes, shells gave commands and flags, programming languages gave composable primitives, and each was a fixed menu. Natural language blew the menu open.

The protocol is where the title lands. Punch card computing was batch: encode the entire request in advance, submit the deck, wait hours, read the printout, fix one thing, resubmit. Johnson argues prompting is the same loop with the wait shrunk from overnight to seconds, and the speed fooled us into thinking it became interactive. The machine still engages only after you package a complete turn. Prompt engineering, in his telling, is the punch card operator's skill with a flattering name: think step by step, add examples, ask it to be an expert, paste more context, paste less. He traces batch back past the punch card to the weaving loom, where you set the whole pattern before running the cloth. His summary of the mismatch: model capability curves upward across reasoning, speech, vision, and memory while the interface protocol stays flat, and when the magic words fail, users blame themselves. The fault is the interface, not the user.

The second half is demos. His co-founder asked a frontier speech-to-speech model about the next Timberwolves game, then greeted a person entering the room; the model took the greeting as a turn and answered it, because the protocol has exactly one slot. He notes OpenAI's GPT realtime release from late May now backchannels with "mhm" and "right," and plays Nvidia's PersonaPlex research model yielding to an interruption mid-answer and picking the thread back up. Then he shows JoinIn's own approach: an AI sitting in a multi-person meeting, labeling each utterance as question, proposal, or answer, tracking who holds the floor, and taking a turn only when no one else is speaking. In the demo it answers a requirements question, interjects to resolve whether the scope is expense approvals or general approvals, captures the agreed 5,000 dollar second-approver threshold, and updates it to 10,000 on request. No one wrote a prompt.

His closing design question: what burden do we still put on humans only because the machine used to be too limited to carry it? The answer he wants is the affordances humans already use with each other, a question, a pause, a sketch, a quiet aside, with timing and modality chosen by the AI rather than the person.

## Notable moments

- [0:06:09](https://www.youtube.com/watch?v=hVJOnuhFmTA&t=369s) The core claim: channel unchanged, expression exploded, and prompting is the punch card's batch protocol with interactive sprinkles.
- [0:11:14](https://www.youtube.com/watch?v=hVJOnuhFmTA&t=674s) The "Hey Ted" failure: a voice model answers a greeting meant for a human because its protocol has one slot.
- [0:12:15](https://www.youtube.com/watch?v=hVJOnuhFmTA&t=735s) Nvidia's PersonaPlex yields to an interruption about a marathon signup and resumes the diet thread.
- [0:14:17](https://www.youtube.com/watch?v=hVJOnuhFmTA&t=857s) JoinIn's meeting demo: the AI labels utterances, waits for the floor, and resolves a scope question without a prompt.

## Connections

- [Nvidia](../../companies/models-inference/nvidia.md) built the PersonaPlex research model Johnson plays as evidence real turn-taking is possible.
- [Adaptive turn-taking for real-time multi-party voice agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md) studies the floor-holding problem JoinIn's meeting demo tackles.
- [Tau-Voice: benchmarking full-duplex voice agents](../../papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md) measures the listen-while-speaking capability the talk argues protocols must adopt.
