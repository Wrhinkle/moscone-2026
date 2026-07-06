# Does GenAI "belong" to data scientists?

> A Braintrust solutions engineer argues both sides of who should own agent development, and lands on diverse teams where data scientists guard rigor rather than own the product.

- **Speaker:** Phil Hetzel, Braintrust
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=NKwIX3CiRgU) (AI Engineer channel; ~19m, released 2026-05-25)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Hetzel leads solutions engineering at Braintrust, an agent quality platform built on two pillars, evals during experimentation and observability in production. Before Braintrust he spent 12 years in consulting, most recently running the global Databricks business unit at Slalom, where he watched customers produce generative AI proofs of concept prolifically and get them to production rarely. That vantage point shapes the talk's observation: traditional enterprises and AI natives organize agent work differently. In the traditional enterprise, an executive reads that the company needs agents, delegates it, and the work lands on the existing ML or data science platform team because generative AI has AI in the name. AI natives instead run small cross-functional teams spanning product and AI engineering, and because the companies are smaller, each person sits closer to the problem the agent is meant to solve.

Hetzel then stages a debate with himself. The case for data scientists owning agents: they understand how neural networks and LLMs work, so they appreciate the risks; they have rigorous processes for pushing model assets to production; and they bring a testing mindset. The case against starts with the fact that the model is already built. Anthropic, OpenAI, and Mistral did the data pipeline, training, and deployment, so the cross-validation dance does not apply, and behavior changes through prompts and context rather than feature engineering. His biggest argument is that ML engineers often do not know what they are testing for: they lock onto precision, recall, and F1 because those metrics got them here, while evaluating agents requires judging functional performance across a much broader surface. On the other side, LLMs are just APIs, which product engineers consume daily; distributed agents running across different compute calling different systems are a systems problem, not a statistics problem; and subject matter experts and product managers, the people with the most proximity to the problem, should control prompts and drive the human annotation workflow, reading agent traces and explaining why an output is good or bad.

His landing spot is a mixed team. Data scientists add value in three specific ways beyond building product: acting as the adult in the room when teams get aggressive with a technology they do not understand; keeping LLM-as-judge honest, since judges are just prompts and models, by building labeled datasets and scoring the judges themselves with recall, precision, and F1; and fine-tuning open source models when a use case genuinely needs it. Product, application, and systems engineers implement requirements and build the eval and observability pipelines that close the loop between production and experimentation, while non-technical experts annotate and do prompt and context engineering. In the Q&A he agrees the framing should be problem-first rather than ownership-first, and describes Braintrust's loop for keeping evaluators honest: gather production data into the offline eval set continuously and track whether LLM judges are converging toward or diverging from human agreement.

## Notable moments

- [0:03:14](https://www.youtube.com/watch?v=NKwIX3CiRgU&t=194s) The traditional enterprise delegation chain: CEO magazine to delegate to the existing ML platform team, with a show of hands from the room.
- [0:09:14](https://www.youtube.com/watch?v=NKwIX3CiRgU&t=554s) The core argument: teams obsess over precision, recall, and F1 while agent evaluation covers a far broader functional surface.
- [0:13:16](https://www.youtube.com/watch?v=NKwIX3CiRgU&t=796s) How data scientists should judge the judges: labeled datasets and classical metrics applied to LLM-as-judge outputs.

## Connections

- [Braintrust](../../companies/evals-observability/braintrust.md) is the speaker's company; the talk is a culture-level argument for its evals-plus-observability product shape.
- [Arize](../../companies/evals-observability/arize.md) competes in the same agent evaluation and observability market with a stronger ML-engineer heritage.
