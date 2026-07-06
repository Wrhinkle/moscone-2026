# How to talk to statues

> A viral vibe-coded app that gives museum statues voices becomes a group discussion on voice interfaces, interruption, and consumer vibe coding.

- **Speaker:** Joe Reeve, ElevenLabs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=u-rJwPPU3QA) (AI Engineer channel; ~33m, released 2026-06-01)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Joe Reeve works in growth at ElevenLabs, and this session, recorded in an informal discussion format with heavy audience participation, is built around his statue app. Take a photo of a statue at the British Museum, and the app runs an OpenAI deep research pass on the statue's identity, generates historical knowledge and a character prompt, feeds a voice description to ElevenLabs' voice design API, spins up an ElevenLabs agent, and starts a call. The whole pipeline runs in about 30 seconds. Reeve built it in roughly two hours on a Sunday in Cursor, published the one-shot prompt on the ElevenLabs blog, and posted a demo video that did 50,000 impressions on day one and 1.5 million on day two. Three museum groups, TripAdvisor competitors, and auction houses including Bonhams and Christie's reached out; one CEO found his WhatsApp number and called to ask how a two-hour prototype matched what his team of ten had spent a year on.

Reeve's takeaway is that the glue is the product. Nearly everything hard in the app is an existing API designed to scale, so his traffic cannot dent ElevenLabs' API volume, and Cursor plus Supabase can one-shot the login plumbing. The harder, longer-tail work is editorial: getting curators to design the narratives instead of shipping whatever deep research finds on Google, pulling from museum collection APIs like the V&A's. He describes a former British Museum executive now running the Sainsbury Centre who is working through what an inanimate object should sound like at all: stone quarried in China, carved in Vietnam, resident in a British museum for 200 years, surrounded by tourists.

The middle section is a candid group critique of voice interfaces. Reeve wants to talk to a product manager agent that dispatches coding agents, not to the coding agent itself. He observes that people are too polite to interrupt voice agents, and that learning to interrupt aggressively makes the experience better, but nobody knows how to give users permission. Audience members raise the information density problem: voice input is great for dumping raw intent, but a spoken response is low-bandwidth compared to diagrams or generated UI, and a concise text answer feels fine while a concise spoken one sounds rude. The group sketches ideas live: skim listening with forward and back controls that scroll by concept rather than sentence, an indicator that the agent wants to interrupt with a labeled topic, and an asynchronous loop that re-reads the transcript asking "do you have anything to add?" Reeve notes ElevenLabs has playback timestamps, so an interrupted agent's transcript can be edited to forget text the model generated but never spoke.

Two side stories round it out. On consumer vibe coding, Reeve argues nothing has hit its TikTok moment yet, and recalls buying a Fruit Ninja clone for 15 pounds, wiring it to the Facebook Instant Games API, and waking up to 15 million users in Vietnam, which he offers as the template for social vibe coding. On making viral videos, he shares his numbers: median view time of 6 to 12 seconds, so front-load the hook; captions and music matter more than people think; the statue video was edited in about 25 minutes on CapCut on his phone with a borrowed DJI lapel mic.

## Notable moments

- [0:02:09](https://www.youtube.com/watch?v=u-rJwPPU3QA&t=129s) How the statue app works: photo to deep research to voice design to a live agent call in 30 seconds.
- [0:03:11](https://www.youtube.com/watch?v=u-rJwPPU3QA&t=191s) The virality arc, from 50,000 impressions to 1.5 million, and the CEO whose ten-person team spent a year on the same idea.
- [0:11:17](https://www.youtube.com/watch?v=u-rJwPPU3QA&t=677s) People are too polite to interrupt voice agents, and the group designs fixes on the spot.
- [0:17:23](https://www.youtube.com/watch?v=u-rJwPPU3QA&t=1043s) The Facebook Instant Games story: a 15-pound Fruit Ninja clone that hit 15 million users overnight.

## Connections

- [Vapi](../../companies/voice-realtime/vapi.md): competing voice agent platform chasing the same photo-to-conversation and phone-agent use cases.
- [LiveKit](../../companies/voice-realtime/livekit.md): the real-time infrastructure layer that adjacent voice agent stacks build interruption handling on.
- [Adaptive turn-taking for real-time multi-party voice agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md): research on exactly the interruption and turn-taking problems this discussion improvises around.
