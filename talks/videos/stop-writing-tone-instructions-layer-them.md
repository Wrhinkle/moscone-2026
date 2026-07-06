# Stop Writing Tone Instructions. Layer Them.

> A wedding venue owner's four-layer prompt architecture for brand voice: immutable identity, situational mode, example-anchored voice, and a deterministic post-generation veto.

- **Speaker:** Isadora Martin-Dye, Isadora & Co
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ij-AU9dpJjc) (AI Engineer channel; ~21m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Martin-Dye owns a 225-year-old wedding venue in Virginia and built an AI agent that talks to her couples, then productized it for other venues as Bloom, plus a personal companion app and a public tool for families of missing people. Her framing sets up everything else: she is not programming a robot, she is managing a brilliant intern with a high IQ, a terrible EQ, photographic memory, and no instinct for reading the room. Robots get rules; interns get structure and someone checking their work before it leaves the building.

Her diagnosis of the standard advice, write a detailed system prompt with brand voice examples, is that it only covers the happy path. On turn 21 a user asks something the examples never covered and the model says something technically correct that the brand would never say. That matters most where voice is the product, luxury hotels, high-end real estate, wedding venues, where one wrong sentence can cost more than a refund. The root cause, she argues, is asking one prompt to do four different jobs. Her architecture splits them: layer one is immutable identity, hard rules nothing below can override; layer two is situational mode, adjusting to who the user is and what they are going through; layer three is the example-anchored voice guide where most teams start and stop; layer four is a post-generation veto that reads what actually came out. Before this, her codebase had 24 scattered system prompts with half a dozen different self-conceptions; now every surface composes its prompt through one assembly in a fixed, load-bearing order, which she compares to Google Maps factoring in rules, traffic, and preferences before routing.

Layer one examples carry the talk's weight. Every AI in Bloom discloses it is AI in its first response, before anyone asks, on the bet that a couple who knows from the start trusts more than one who finds out on turn seven. A physical presence boundary forbids "I'd love to show you around" because software has no body and warmth plus that constraint produces a lie. Her cross-product proof is the missing-persons tool, which runs the identical architecture but whose layer one bans the words confirmed, identified, matched, proven, linked, and solved, because the model reaches for "match" as the statistically natural word with full confidence, and saying it to a parent who has spent years not knowing is the most damaging thing the product could do.

Layer two shifts by audience and circumstance: the same AI briefs venue staff like colleagues, hedging forecasts it would never refuse a couple with, and soft context notes ("mom in chemo") shape tone without ever being quoted. The assembler deliberately renders human context before numeric constraints, because reversing the order makes prose feel mechanically slotted. Layer four exists because of a recurring failure: the AI kept warmly offering wedding dates that were already booked, since it was never given the calendar. Every other layer did its job; the veto is the only deterministic one, rejecting any date not on an allow list. Her closing distinction: the first three layers are instructions and probabilistic, layer four is permission and deterministic; everything before it is prompt engineering, the veto is systems engineering. She also names a multi-tenant lesson, a silent default that shipped every venue as sage@hawthornemanner.com, yielding the principle that missing brand identity must crash loudly rather than fall back.

## Notable moments

- [0:02:02](https://www.youtube.com/watch?v=ij-AU9dpJjc&t=122s) The core claim: brand voice fails because one prompt is doing four different jobs, and the four-layer split that fixes it.
- [0:07:06](https://www.youtube.com/watch?v=ij-AU9dpJjc&t=426s) The missing-persons tool's layer one: the AI can never say confirmed, identified, matched, proven, linked, or solved.
- [0:14:11](https://www.youtube.com/watch?v=ij-AU9dpJjc&t=851s) The failure that created layer four: warm, confident offers of wedding dates that did not exist.
- [0:16:13](https://www.youtube.com/watch?v=ij-AU9dpJjc&t=973s) The white-label leak where every venue defaulted to another venue's email identity, and the fail-loud principle it produced.

## Connections

- [EliseAI](../../companies/back-office-automation/eliseai.md) sells conversational AI for property and leasing conversations, an adjacent market with the same voice-is-the-product stakes.
- [Session recaps](../../notes/session-recaps.md) records Sonar's zero-trust, multilayer verification framing, the in-person analog to her deterministic layer-four veto.
