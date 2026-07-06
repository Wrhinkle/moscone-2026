# Beyond Transcription: Building Voice AI That Understands Conversations

> pyannoteAI's co-founder walks through speaker diarization, why speaker-attributed transcription is harder than it looks, and a live demo of reconciling diarization with STT output.

- **Speaker:** Hervé Bredin, pyannoteAI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=mFLlVpnGpds) (AI Engineer channel; ~25m, released 2026-06-05)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Bredin spent his career as an academic researcher on speaker diarization before co-founding pyannoteAI two years ago. His open source pyannote toolkit sits near 10,000 GitHub stars, and he points to the inflection in its star history when OpenAI released Whisper: Whisper made high-quality transcription free but gave no speaker labels, so people combined the two. The talk's frame is a ladder of understanding. Transcription answers what was said. Speaker-attributed transcription answers who said what, enough for meeting note takers to assign action items, and required for applications like video dubbing (keeping voices consistent across translation) and podcast intelligence (tracking a guest across episodes). Precise timing answers when: without word-level timestamps you cannot detect that one speaker interrupted another, that a short "mhm" was a backchannel agreement, or that a pause carried meaning. Beyond that sit how things were said (laughter, coughing, stress on particular words, which can flip a sentence's meaning) and who was addressing whom, all inside an acoustic environment that adds context.

Diarization itself, Bredin explains, runs from voice activity detection through segmentation (speaker change points, overlaps, short backchannels) to assigning anonymous speaker labels. It stays unsolved because the number of speakers is unknown in advance, labels are permutation-invariant, overlap must be handled, and speech time per speaker is imbalanced. In a live notebook he runs pyannote's open community-1 model on a 30-second phone call and scores it with pyannote.metrics: diarization error rate is confusion plus false alarm plus missed detection over total speech, and community-1 lands at 5 percent DER while the company's cloud precision-2 model gets 3 percent on the same file. Asked how good the state of the art is, he says it depends entirely on conditions: around 8 percent DER on conversational telephone speech, but 41 percent for a noisy multi-speaker restaurant setting even with the best systems.

The second half argues that gluing diarization to STT is not a solved join. Most STT models are trained on single-speaker audio and degrade badly on multi-speaker recordings: NVIDIA Parakeet reports 11.4 percent word error rate on the open ASR leaderboard's AMI numbers, which use headset microphones, but Bredin measures 26 percent on the same dataset using the distant table microphone. Even with good transcripts, timestamps from STT and diarization disagree, overlapping speech gets transcribed as one stream, and each system detects speech the other misses. His demo shows a single word falling between two diarized speech turns with no obvious owner. pyannoteAI's cloud orchestration handles the reconciliation, correctly interleaving words from two overlapping speakers in the sample call. In the Q&A he says the trick is partly proprietary, but one published piece is exclusive diarization in community-1: during overlap it selects the speaker an STT model is most likely to transcribe, and the approach is designed to work with any STT model, including privately fine-tuned ones, without retraining it.

## Notable moments

- [0:12:19](https://www.youtube.com/watch?v=mFLlVpnGpds&t=739s) Live notebook demo begins: community-1 diarization runs locally on a Mac and gets scored at 5 percent DER.
- [0:16:21](https://www.youtube.com/watch?v=mFLlVpnGpds&t=981s) State of the art ranges from 8 percent DER on telephone speech to 41 percent in a noisy restaurant.
- [0:17:21](https://www.youtube.com/watch?v=mFLlVpnGpds&t=1041s) Why leaderboard WER misleads: Parakeet at 11.4 percent on headset mics becomes 26 percent on the distant microphone.
- [0:23:33](https://www.youtube.com/watch?v=mFLlVpnGpds&t=1413s) Q&A on the reconciliation trick, including exclusive diarization during overlapping speech.

## Connections

- [AssemblyAI](../../companies/voice-realtime/assemblyai.md) sells speech-to-text with built-in diarization, the integrated alternative to pyannote's model-agnostic approach.
- [Deepgram](../../companies/voice-realtime/deepgram.md) competes in the same transcription stack Bredin's orchestration layer plugs into.
- [Adaptive turn-taking for real-time multi-party voice agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md) tackles the same multi-speaker timing problems (overlap, backchannels, turn boundaries) from the agent side.
