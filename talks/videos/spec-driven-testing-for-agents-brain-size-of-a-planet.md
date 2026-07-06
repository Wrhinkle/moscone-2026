# Spec-Driven Testing for Agents With A Brain the Size of A Planet

> Makes the case that agent evals need full behavioral specs, covering rules, ontologies, roles, and stress envelopes, not just test datasets.

- **Speaker:** Steven Willmott, SafeIntelligence
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=UQKg0td-Bf4) (AI Engineer channel; ~13m, released 2026-05-31)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Steven Willmott, CEO of SafeIntelligence, comes from formal verification: his three-year-old company checks whole regions of a model's input space for points that tip over under perturbation, starting with vision and tabular models. The day before this talk they released an analogous product for language models, where the weights are unavailable, so the work shifts to being clever about generating edge cases. This talk, which follows a Braintrust session he references approvingly, asks the prior question: how do you specify what an agent is supposed to do at all?

Willmott's opening provocation, named for Marvin the depressed robot from The Hitchhiker's Guide to the Galaxy, is that a smarter agent is not automatically a better one. Some jailbreaks work better on large models: wrap a bad instruction in a poem and a low-end model cannot even parse it, while a frontier model happily extracts and executes it. Broad-remit agents create more attack surface and more testing surface, and using a big model for simple math is slow and expensive. Deployment, especially fully automated deployment, is therefore a trade between smart and safe, and the target is a model good enough to perform but not capable of arbitrary harm, bounded on two axes: what instructions it will accept, and what tools it can wield in your infrastructure.

The core of the talk enumerates what belongs in a spec beyond the eval dataset. Ground-truth examples are one component. Rules come next, like never discount more than 10 percent or no refunds past 30 days, and Willmott notes your alarm bells should ring, since proving a rule is never violated is hard. Then ontologies and dictionaries, such as the actual destinations an airline flies; internal terminology no one outside the company knows; domain knowledge about which terms are substitutable, since a general LLM might confuse gross profit with gross sales, which are very different in business; rights and roles, since agents should behave differently for logged-in versus logged-out users; and robustness requirements. He maps the last one back to vision: can the runway detector handle sunset, fog, and camera shake becomes how many typos, rephrasings, and frustrated users a support agent can absorb before results destabilize.

SafeIntelligence uses these specs two ways. For security testing, the spec reveals where an agent is most vulnerable, because it will engage on the domains it is scoped to and holds real power over the tasks it performs. For stress testing, the spec defines the valid envelope within which inputs can be varied. Willmott points to A2A agent cards as a related industry artifact but says even an agent card is not enough to evaluate against, because it does not say what range of variation is valid.

His closing advice is to keep specs independent of implementation, since teams move between LangSmith, Vertex, and other stacks, and the integration, unit, and penetration tests should survive the move. He describes closing the loop as backyard RL: run the agent against the spec, find the gaps, iterate, without touching the model. Willmott co-wrote the OpenAPI spec at his previous API infrastructure company, and he wants the same treatment here: agent behavior specs that live in a GitHub repo, get versioned hard, and pull into any tool.

## Notable moments

- [0:02:09](https://www.youtube.com/watch?v=UQKg0td-Bf4&t=129s) The Marvin problem: why a smarter agent is not automatically better, and the poem jailbreak that only works on big models.
- [0:05:10](https://www.youtube.com/watch?v=UQKg0td-Bf4&t=310s) The spec inventory begins: datasets, hard rules, ontologies, internal terminology, roles, and stress requirements.
- [0:08:12](https://www.youtube.com/watch?v=UQKg0td-Bf4&t=492s) Why A2A agent cards fall short as eval specs, and pulling specs into security testing.
- [0:11:14](https://www.youtube.com/watch?v=UQKg0td-Bf4&t=674s) Keep specs implementation-independent, version them in a repo, and his OpenAPI mea culpa.

## Connections

- [SafeIntelligence](../../companies/evals-observability/safe-intelligence.md): Willmott's company, extending its formal verification products to language model agents.
- [Braintrust](../../companies/evals-observability/braintrust.md): the eval platform whose talk immediately preceded this one; Willmott positions specs as the layer evals are missing.
