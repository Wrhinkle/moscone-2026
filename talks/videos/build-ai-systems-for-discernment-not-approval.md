# Build AI Systems for Discernment, Not Approval

> Duolingo English Test security work showing that expert human reviewers rubber-stamp AI signals, and how interaction design rather than model fixes restores independent judgment.

- **Speaker:** Angel Ortmann Lee, Duolingo
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=CDqzWpwkSls) (AI Engineer channel; ~26m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Ortmann Lee, a software engineer on security for the Duolingo English Test, argues that the human in your loop often is not thinking, and that the fix lives in the interaction design. She grounds the problem in a Wharton study of what it calls cognitive surrender, where a person forgoes deliberation and adopts AI output as their own with minimal scrutiny. In that study, when the AI was right, human performance rose by 25 percentage points; when it was wrong, performance fell by 15; and 80 percent of participants accepted AI answers even when those answers were wrong.

Duolingo tested the same effect on its own proctors and published the result as a case study titled When Machines Mislead. The DET is a high-stakes, fully online, remotely proctored English exam trusted by 6,000 programs, with results feeding college admissions and visa decisions. One of its AI cheating detectors flags copy typing by spotting anomalies in keystroke patterns, since transcribing and composing produce different typing. The experiment took historical sessions with no cheating at all, attached fake copy-typing alerts, and slipped them into proctors' normal workflow (no test takers were affected). Proctors who consistently score above 90 percent on accuracy calibration accepted 50 percent of the fake signals, falsely upholding cheating flags at a coin-flip rate. Ortmann Lee reads that as automation bias: the model was fine (1 percent false positive rate) and the people were skilled, so the team targeted the interface. A guideline copy change stating that the AI signal is only a preliminary alert, and that proctors must find independent evidence in the video before upholding a flag, raised rejection rates by 21 percentage points, to 71 percent of the fake sessions correctly cleared, with no model or UI changes.

The middle of the talk generalizes this into a loop argument. Human-in-the-loop is cyclical rather than linear: model output shapes an interaction, the interaction shapes human behavior, and that behavior becomes the labels for your evals and the next model. A confident model plus an interface that never elicits deliberation produces rubber stamps logged as truth, so the model grows more confident and the human defers more, a vicious cycle. An interface that forces independent judgment surfaces real disagreements and yields honest positive and negative labels. Her examples: Duolingo's headphone detection flag hid two questions in one yes/no (did the model correctly detect headphones, and is this a violation), which mislabeled hearing-aid cases until the questions were split; a writing tutor that returns 400 lines of praise, feedback, and an unrequested rewrite versus a markup UI with color-coded inline annotations tied to specific text; and coding agents that either dump a thousand-line diff or ping for approval every few minutes, both of which turn the developer into a rubber stamp, versus an agent that behaves like a good junior developer who plans, surfaces assumptions, and ships reviewable chunks.

She closes with design principles. Engineer the reasoning you want, framing the human as investigator rather than validator. Match friction to the stakes: add deliberate review gates where decisions carry weight, and keep casual interactions frictionless. Treat every interaction as a label, including the diff when a human accepts output and then silently edits it, which otherwise pollutes the dataset with false positives. And define success metrics before building, so the interaction is designed to collect the evidence the next iteration needs. Her summary line: sometimes the fix is neither a better model nor more oversight, it is engineering the interaction itself.

## Notable moments

- [0:02:00](https://www.youtube.com/watch?v=CDqzWpwkSls&t=120s) The Wharton cognitive surrender numbers: plus 25 points when AI is right, minus 15 when wrong, 80 percent acceptance of wrong answers.
- [0:06:05](https://www.youtube.com/watch?v=CDqzWpwkSls&t=365s) The headline result: proctors above 90 percent accuracy accepted 50 percent of fake cheating signals.
- [0:08:06](https://www.youtube.com/watch?v=CDqzWpwkSls&t=486s) A guideline copy change alone raises correct rejections by 21 percentage points.
- [0:12:08](https://www.youtube.com/watch?v=CDqzWpwkSls&t=728s) The headphone flag hid two questions in one, mislabeling hearing-aid wearers until the CTA was split.

## Connections

- [Session recaps](../../notes/session-recaps.md) covers the in-person Anthropic session on not handing off the thinking, the same failure mode this talk measures in proctors.
- [Snorkel](../../companies/evals-observability/snorkel.md) builds its business on the talk's closing premise that interactions and expert judgments should become structured training labels.
