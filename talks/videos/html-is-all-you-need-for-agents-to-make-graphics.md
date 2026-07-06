# HTML is All You Need (for Agents to Make Graphics)
> The case that agents fail at slides and graphics because we hand them canvas tools built for humans, and that HTML is the medium models can actually reason in.

- **Speaker:** Amol Kapoor, Nori
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=JRTAtZ5iBkU) (AI Engineer channel; ~7m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Amol Kapoor, CEO of Nori, which deploys an AI employee that understands a company's code, docs, and Slack, argues that "coding agent" is bad marketing: the same agents can produce almost anything, including visual artifacts like slides, docs, and video, if you think like the agent instead of like a user. His motivating numbers: the world pours roughly 34,000 human years per day into slide decks, and a deck that takes 10 hours should take about 25 minutes once the fiddling (formatting, branding, moving boxes) is stripped away from the thinking.

The diagnosis starts with tooling. PowerPoint, Slides, Figma, and Canva are canvas tools built for human hands and eyes: click, drag, resize, snap to grid. Their underlying data structures are readable only by the application, so when an agent drives them, the output overlaps, misaligns, and reads as garbage. Skeptics conclude that agents cannot reason about space, and Kapoor cites Simon Willison's running test, asking every new model to draw a pelican riding a bicycle in raw SVG, where results are genuinely bad. His counter is that the medium is at fault. A human could not handwrite a pelican in SVG either, because SVG is a wall of numbers, and Figma MCPs, PowerPoint CLIs, and screenshot-and-replace loops all repeat the mistake of forcing the agent through a human-shaped interface.

The fix is to give the model a language-native medium for layout. HTML is a layout language the models have seen billions of examples of, it carries semantic structure (a heading, a chart, a grid), and the browser turns it into pixels, so the model never places a coordinate. Effects, charts, fonts, and motion come along free. The same pelican prompt in HTML produces a recognizable bird in a structure you can read, theme, and edit line by line. Kapoor's broader observation is that the editing format is arbitrary: PowerPoint is just one editor for the presentation mode the audience actually sees, so you can pick the editing format agents are already good at and render to PDF or other formats afterward.

Nori runs this internally for its board decks, sales decks, and docs, and the talk's video is itself HTML and CSS, "divs all the way down." Kapoor adds that a beautiful deck is worthless without content, which is where the company's product comes in: give the model access to call transcripts and email and it can build the deck end to end, which is what Nori Sessions does. He says he has built entire board decks from his phone on the subway because the Nori bot lives in the company's data. The takeaway he closes on: stop thinking like a user, think like the model, and for graphics the right language is HTML.

## Notable moments
- [0:02:08](https://www.youtube.com/watch?v=JRTAtZ5iBkU&t=128s) Simon Willison's pelican-on-a-bicycle SVG test and the genuinely bad results.
- [0:03:10](https://www.youtube.com/watch?v=JRTAtZ5iBkU&t=190s) The argument that a canvas is the wrong interface and language is the model's native medium.
- [0:04:11](https://www.youtube.com/watch?v=JRTAtZ5iBkU&t=251s) The same pelican prompt in HTML: readable, themeable, editable structure.
- [0:05:11](https://www.youtube.com/watch?v=JRTAtZ5iBkU&t=311s) The reveal that the talk video itself is HTML and CSS.

## Connections
- [Builder.io](../../companies/coding-agents/builder-io.md) works the same seam between agents and visual output, translating design intent into web code.
- [Session recaps](../../notes/session-recaps.md) records the DeepMind session's open question about a programming language designed for LLMs; Kapoor's answer for graphics is that HTML already is one.
