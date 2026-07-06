# Why Can't Anyone Answer Questions About the Business?
> How WorkOS built Studio, an internal agent workspace that lets any employee query business data and turn one-off answers into reusable dashboard widgets.

- **Speaker:** Garrett Galow, WorkOS
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=iUWwcG-C8OU) (AI Engineer channel; ~19m, released 2026-06-11)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Garrett Galow, who runs product at WorkOS, presents an internal tool rather than the company's product. The problem: someone in support or go-to-market has a question about the business, lacks SQL access, explains the question to an engineer, waits, gets an answer in Slack, then needs the next layer deeper. Dashboards built in tools like Retool answer one fixed question and go stale the moment someone needs a different cut of the data. WorkOS built Studio, an internal workspace where employees answer these questions themselves.

The live demo asks which website content drives the most new team sign-ups. Studio inspects its available data sources (Snowflake, Linear, Notion), figures out the relevant schemas, and runs the Snowflake queries itself. Under the hood, a Slack bot or the Studio dashboard kicks off an API call into a LangGraph agent running Claude Opus, with an integration proxy to the data sources and a guidance layer that encodes rules for querying them, including how a customer is represented in Snowflake and how to join its sprawling tables. Session state persists in Convex. Galow then asks Studio to turn the answer into a reusable table, which produces what WorkOS calls a widget: sandboxed code containing the UI, the API calls, and the validated query. Once built, a widget re-queries live data with no LLM involved, so refreshes are deterministic and cost nothing in tokens until someone asks the agent to modify the widget. A second widget lets support staff look up why the Radar security product blocked a specific login, replacing a workflow where solutions engineers passed around SQL snippets.

Galow closes with the three things that made Studio reliable. Sequencing: pre-flight checks confirm tools are connected and context is sufficient, clarifying questions come before execution, and tool-specific context (like the Snowflake schema block) is injected only at invocation time to avoid blowing out the context window. Layering: a base prompt, org-level rules per tool, and an explicit instruction to distrust the model's trained knowledge of WorkOS because the product changes faster than training data, so the agent must consult primary sources like the docs. Validation: every generated query runs against the database and must return data before it gets hardcoded into a widget, since a syntactically valid query returning zero rows is a silent failure. In Q&A, Galow says there is no RAG database anywhere in the system, just tools plus context. Encoding quirks once, like a four-join path from customer to users or a filter for non-deleted entities, removes most of the errors LLMs make on schemas. Integrations are currently per-user, and WorkOS is building org connectors on its own Pipes product so one person can connect a source and set default access levels. On cost, he says Opus outperforms other models by enough that trading cost for quality would be unacceptable.

## Notable moments
- [0:02:15](https://www.youtube.com/watch?v=iUWwcG-C8OU&t=135s) Live demo starts: which content drives the most new team creations.
- [0:04:16](https://www.youtube.com/watch?v=iUWwcG-C8OU&t=256s) Architecture walkthrough: Slack bot to API to LangGraph with Opus, guidance layer, Convex for state.
- [0:07:17](https://www.youtube.com/watch?v=iUWwcG-C8OU&t=437s) A widget as sandboxed code that re-queries live data without the LLM.
- [0:09:17](https://www.youtube.com/watch?v=iUWwcG-C8OU&t=557s) The three reliability practices: sequencing, layering, validation.

## Connections
- [WorkOS](../../companies/security-identity/workos.md) is the speaker's company; Studio runs on its own Pipes integration product under the hood.
- [Retool](../../companies/back-office-automation/retool.md) is the incumbent internal-tooling approach Galow contrasts with self-serve agent-built widgets.
- [PromptQL](../../companies/data-infrastructure/promptql.md) attacks the same natural-language-over-business-data problem as a product rather than an internal tool.
