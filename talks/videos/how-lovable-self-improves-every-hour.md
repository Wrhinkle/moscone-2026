# How Lovable self-improves every hour
> Two production systems Lovable uses to learn from user failures: an internal Stack Overflow mined from stuck sessions, and a vent tool that lets the agent complain to its creators.

- **Speaker:** Benjamin Verbeek, Lovable
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=KA5kPbdkK2E) (AI Engineer channel; ~19m, released 2026-06-02)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Verbeek, a member of technical staff at Lovable with a physics background in satellites and fusion reactors, frames the talk around continuous learning at scale: a mistake should happen once and never again. Lovable builds for the 99% who cannot code, and that changes the failure economics. A technical user hits a friction point, edits a config, and moves on. A non-technical user hits the same block and walks away, never experiencing AI working at all. When Verbeek joined about a year before the talk Lovable had a few thousand users; it now creates over 200,000 projects per day, enough that GitHub banned the company on his first day for creating too many repos.

The first system is what he calls a Stack Overflow for Lovable. An LLM judge scans sessions for stuck signals: a user asking for the same thing twice, complaining about an implementation, or abandoning a session they would otherwise have continued. When a session flips from stuck to unstuck without the user giving up, that transition is a high-signal sample containing both the friction and the solution. The team asks what context should have been injected at the start of the original query to jump straight to the fix, clusters similar issues to avoid overfitting to one prompt, has an agent reviewer run a quick eval against the collected examples, and adds the entry to a continuously updated knowledge bank. A lightweight model injects relevant entries into the main agent at runtime, and for a sample of cases it deliberately injects a blank, giving a production A/B comparison of whether each entry actually helps. Entries that improve project success get shown more; ones that hurt get shown less. Verbeek stresses that this rebalancing loop is the most important part, because the knowledge goes stale every time a model or feature changes, and stale entries cause context rot. Messages with fixing intent are down significantly and deployment completion, a key metric, is up. All top models in Lovable's internal ranking use this Stack Overflow context.

The second system covers failures that no prompt can solve, such as product bugs. Lovable gave its agent a vent tool: a send-feedback function it is prompted to use only when genuinely frustrated by missing tools, mismatched schemas, conflicting docs, or broken platform behavior. Vents go straight to Slack. The agent has more context on the root cause than the user does, and the format is instantly legible to engineers. One vent complained about Framer Motion's TypeScript types demanding casting gymnastics for a cubic bezier. Another exposed a copy tool that failed on file names with spaces; 20 complaints arrived in the first hour, and follow-up vents revealed that WhatsApp and Mac screenshots insert non-breaking spaces the fix's regex missed. Spikes in vent volume turned out to track platform incidents, making the tool an incident detector. An agent now deduplicates vents, investigates, and opens PRs that engineers review and often merge, and Verbeek says the remaining goal is to fully close the loop from detected shortcoming to merged, evaluated fix.

## Notable moments
- [0:04:18](https://www.youtube.com/watch?v=KA5kPbdkK2E&t=258s) The non-technical user failure curve: one technical block and they walk away for good.
- [0:09:24](https://www.youtube.com/watch?v=KA5kPbdkK2E&t=564s) The blank-injection trick that turns every knowledge entry into a production A/B test.
- [0:14:28](https://www.youtube.com/watch?v=KA5kPbdkK2E&t=868s) The agent vents to Slack about Framer Motion's TypeScript types.
- [0:17:29](https://www.youtube.com/watch?v=KA5kPbdkK2E&t=1049s) Vent volume spikes match platform incidents, turning agent frustration into monitoring.

## Connections
- [Builder.io](../../companies/coding-agents/builder-io.md): competing bet on non-developers shipping real software through an AI agent, from the visual development side.
- [Braintrust](../../companies/evals-observability/braintrust.md): the trace-to-dataset-to-eval loop Lovable built in-house is the workflow Braintrust sells as a platform.
