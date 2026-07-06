# LLM Observability, Evaluation, Experimentation Platform
> An Arize field view of how enterprises instrument agents: OpenTelemetry-first tracing, five flavors of eval signal at four scopes, and a push to automate the whole improvement flywheel.

- **Speaker:** Dat Ngo, Arize
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=JsCCrBF7F1g) (AI Engineer channel; ~17m, released 2026-06-07)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Dat Ngo, an AI architect at Arize who works with large enterprises on making AI systems work, frames the talk around the vantage point the company gets from seeing what every team builds and where it breaks. He estimates he personally burned between 100 billion and 1 trillion tokens in the past year. His through-line is that the AI space is software reimagined, the same engineering patterns in a new flavor, and it reduces to three questions: what is happening in the thing I built (observability), how do I derive signal from it (evals), and how do I improve it without regressions (experimentation), since a fix in a non-deterministic system often ships two or three regressions you did not notice.

On observability, Ngo stresses that everything Arize does is OpenTelemetry-first, so any harness, agent, or SDK can be instrumented, often with a one-line auto-instrumenter that emits traces and spans. Traces are the audit record of what an agent did, because code no longer audits agents; telemetry does. Beyond traces he covers sessions, the back-and-forth state across a conversation, and a distributional view unique to Arize AX: aggregate all instantiations of an agent to see every path, branch, and loop, what percentage of traffic takes each branch, and which component adds latency. Trajectory analysis catches ordering bugs, like an agent calling B before A when B depends on A, which context can then fix.

On evals, Ngo lays out five flavors of signal: LLM-as-judge, human feedback, golden datasets labeled by trusted domain experts (used to tune the judge until it approximates the person you trust), deterministic code-based checks like JSON schema validation, and the business metrics everything serves, which he reduces to making money, saving money, or saving time. He pairs the technical builder persona with the subject matter expert who knows what the AI experience should be, so Arize exposes eval authoring in a non-technical UI as well as programmatically. Evals also have scope: a single span's input and output, multi-span evals that need data from several components (did agents pass data to each other correctly), trajectory evals over the whole path, and session-level evals over the state machine (was the user ever frustrated, did we answer everything). His caution: just because you can eval something does not mean you should; find the minimal set that yields signal, because evals cost money.

The closing section covers experimentation, collecting bad traces into datasets and testing changes to prompts, models, orchestration, and configuration, and where Arize thinks the category goes: nobody wants to live in dashboards. All primitives are exposed through a CLI plus tools and skills so Claude Code or Codex can drive them, and an built-in AI called Alex plans and runs diagnosis tasks itself. Ngo says the company's goal is to automate users out of the observability-evals-experimentation flywheel entirely, including choosing the evals. Products: open source Phoenix, a single container with no Kubernetes required, and Arize AX for enterprises like Uber, Booking, and Reddit.

## Notable moments
- [0:02:07](https://www.youtube.com/watch?v=JsCCrBF7F1g&t=127s) The three-part frame: observability, evals, experimentation, and fixes that create hidden regressions.
- [0:05:08](https://www.youtube.com/watch?v=JsCCrBF7F1g&t=308s) Distributional view of an agent: every path, branch, and loop across all instantiations.
- [0:07:10](https://www.youtube.com/watch?v=JsCCrBF7F1g&t=430s) The five flavors of eval signal, from LLM-as-judge to business metrics.
- [0:13:11](https://www.youtube.com/watch?v=JsCCrBF7F1g&t=791s) Alex, the built-in AI, diagnosing latency and errors on request from a coding agent.

## Connections
- [Arize](../../companies/evals-observability/arize.md) is the speaker's company; the talk demos Phoenix and Arize AX directly.
- [Braintrust](../../companies/evals-observability/braintrust.md) competes for the same eval-and-experimentation workflow Ngo describes.
- [Session recaps](../../notes/session-recaps.md) notes evals-everywhere verification discipline as a recurring theme in the in-person program.
