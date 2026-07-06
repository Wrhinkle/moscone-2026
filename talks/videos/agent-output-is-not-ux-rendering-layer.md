# Agent Output Is Not UX: Rendering Layer Your LLM Pipeline Is Missing

> An Amazon engineer lays out three patterns for turning model output into native mobile UI: a typed rendering contract, streaming into components, and a backend-for-frontend.

- **Speaker:** Bala Ramdoss, Amazon
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=maTp79FD9gI) (AI Engineer channel; ~14m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Ramdoss opens with a restaurant reservation request. His AI assistant returns a correct text answer, phone number and hours included, but he still has to do the booking work himself. The same answer rendered as a date picker, a time, and a couple of taps completes the task. The layer between the model and something a human can interact with is the subject of the talk. Ramdoss has built customer-facing apps for over a decade and spent the past six years on Amazon Lens, the camera-based shopping feature in the Amazon app, though he flags that the opinions are his own and his employer's are not represented.

His central diagnosis is that the hard problems in agentic UX are delivery problems, living between model output and the screen. Speed, progressive disclosure, and fragmentation across mobile versions and devices all sit in that gap; the model itself does its job fine. He notes the layer now has a name, generative UI, and an open spec, A2UI from Google, where the agent describes UI as data and the client renders it with native widgets. He borrows CopilotKit's three-tier framing of the space: at the bottom the model picks from pre-built components, in the middle it composes from a catalog (where A2UI sits), and at the top it generates novel UI on the fly. Most production mobile apps live in the bottom two tiers because the higher you go, the more the client must trust what the model hands it. Mobile sharpens everything: a web render bug ships a fix in minutes, but a mobile client that meets an unknown content type crashes, and keeps crashing for weeks on devices that have not updated. His governing rule is that you cannot meaningfully patch the client.

The pipeline he proposes has three patterns. First, the rendering contract: a version-aware context tells the model exactly which components each client version supports, and the model streams typed blocks, a conversation block for text and UI blocks for components. The contract even encodes layout rules, such as one to three flights rendering as a swipeable carousel and four or more as a vertical list. The model never invents a component; it chooses from a fixed menu. Second, streaming: render skeletons, then partial fills, then completion, and measure time to first chunk instead of total latency. Spinners no longer work; he cites Lens Live keeping users engaged by letting them tap objects while results load, and Gemini's visible task progress making a 10-second wait acceptable. Third, the backend-for-frontend: a server layer that owns platform-specific rendering rules, hydrates components, and attaches action payloads to every element, covering taps, deep links, and impression metrics, while carrying conversational context across turns. Because the BFF can reuse the flight rows and product cards an app already ships, the agentic feature looks and feels native rather than bolted on.

## Notable moments

- [0:00:01](https://www.youtube.com/watch?v=maTp79FD9gI&t=1s) The reservation example: same model answer, text versus tappable UI, and only one of them books the table.
- [0:03:01](https://www.youtube.com/watch?v=maTp79FD9gI&t=181s) The layer gets a name, generative UI, and an open spec, Google's A2UI, plus CopilotKit's three-tier control spectrum.
- [0:05:02](https://www.youtube.com/watch?v=maTp79FD9gI&t=302s) Why mobile is unforgiving: unknown content types crash clients for weeks, so you cannot meaningfully patch the client.
- [0:09:06](https://www.youtube.com/watch?v=maTp79FD9gI&t=546s) Streaming shifts the metric from total latency to time to first chunk.

## Connections

- [CopilotKit](../../companies/agent-orchestration/copilotkit.md), whose control-to-open-ended generative UI spectrum Ramdoss uses to place production mobile apps, and whose AG-UI protocol targets the same agent-to-UI boundary.
