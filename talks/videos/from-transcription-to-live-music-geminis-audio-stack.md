# From Transcription to Live Music: Gemini's Audio Stack
> A live tour of Google DeepMind's audio lineup: multilingual audio understanding in one API call, promptable voice direction for speech generation, the real-time Live model, and Lyria 3 music generation.

- **Speaker:** Thor Schaeff, Google DeepMind
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Bc6Ojl2XS1w) (AI Engineer channel; ~20m, released 2026-06-09)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Schaeff works on developer experience for the Gemini API and Google AI Studio, having joined the team the day before Gemini 3 shipped. The talk is a demo-heavy walkthrough of DeepMind's audio stack, opening with him greeting the audience in German, French, Japanese, and Mandarin to seed his own demo. He situates the releases first: Gemma 4 open models with audio understanding baked in for on-device use, Veo video models with audio generation on the gen-media side, and Gemini 3.1 Flash Live, the full duplex real-time speech-to-speech model, launched a few weeks earlier.

The foundation of the stack is audio understanding in the frontier Gemini models: not just transcription but emotion, pacing, language, and speaker identity, including transcribing people talking over each other. His EchoScript demo app (built with AI Studio and available in its gallery) processes the multilingual opening recording in a single API call with a structured-output response schema. The prompt asks for a summary, speaker labels by name where context allows, timestamps, language identification, English translations, and an emotion label per segment. The results come back mostly right, with honest misses shown on screen: his Japanese line garbles, and he jokes the model usually classifies his German as angry.

Speech generation inverts the usual TTS model. Instead of filtering a huge voice library by gender and accent, Gemini offers around 30 base voices that you direct like an actor. The prompt structure builds an audio profile, sets a scene, and gives a director's note; because the model understands what scenarios sound like, it can transform a standard American base voice into a convincing Irish pub storyteller ("cozy crowded pub on the coast of County Clare") or a Singaporean hawker-center recommendation complete with "lah" particles. He uses Gemini 3 Flash itself to construct the speech-generation system prompt from a short description like "high pitch Irish male."

Gemini 3.1 Flash Live handles real-time multimodal conversation over a WebSocket: text, audio, and video in (video capped at one frame per second), audio plus text transcript out. The distinction he stresses is that reasoning is baked into the audio model rather than a cascading pipeline that detours through text and a separate LLM. In the live demo the model, instructed to speak with an Irish accent, comments on his Gemini shirt and backwards hat from the camera feed, then recites a German poem on request while amusingly keeping the Irish accent. All of it is testable free at ai.studio/live, and he points developers to published Gemini agent skills that help coding agents work with the trickier real-time API.

The finale is music. Lyria 3 generates music with lyrics in two variants, a 30-second clip model and a Pro model for full-length songs. His Live Jukebox application gives the real-time Live model a tool that calls Lyria, recreating calling a radio DJ: he requests a German techno Schlager about the UK startup scene, the DJ persona asks follow-up questions about vibe and buzzwords, and the song plays out the talk.

## Notable moments
- [0:04:19](https://www.youtube.com/watch?v=Bc6Ojl2XS1w&t=259s) EchoScript demo: speaker names, timestamps, languages, translations, and emotions extracted in one structured API call.
- [0:09:22](https://www.youtube.com/watch?v=Bc6Ojl2XS1w&t=562s) Voice direction: a director's note turns a standard American base voice into an Irish pub storyteller.
- [0:13:25](https://www.youtube.com/watch?v=Bc6Ojl2XS1w&t=805s) Live multimodal demo: the model sees his outfit through the camera and answers in an Irish-accented German poem.
- [0:16:30](https://www.youtube.com/watch?v=Bc6Ojl2XS1w&t=990s) Live Jukebox: a real-time DJ agent takes a song request and calls Lyria 3 to generate a German techno track.

## Connections
- [Google DeepMind](../../companies/models-inference/google-deepmind.md), the speaker's employer; this talk is the audio-specific slice of the Gemini model lineup profiled there.
- [Deepgram](../../companies/voice-realtime/deepgram.md), a speech-to-text specialist competing with the transcription-plus-understanding capability shown in EchoScript.
- [Session recaps](../../notes/session-recaps.md), which includes a separate in-person Google DeepMind conversation from the same conference cycle.
