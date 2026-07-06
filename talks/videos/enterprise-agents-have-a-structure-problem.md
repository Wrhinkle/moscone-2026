# Enterprise Agents Have a Structure Problem

> Why enterprise data agents fail on ambiguity, staleness, and preference, and a source-of-truth hierarchy plus context lifecycle to fix the first two.

- **Speaker:** Ishita Daga, Tesla
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=B8l81jhvHbI) (AI Engineer channel; ~12m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Daga, a machine learning engineer building enterprise agents at Tesla, opens by dismissing the reflex fixes for a bad agent answer: a bigger model, a longer context window, or piling on more .md files, documents, and MCP servers. Fair solutions, she says, but they do not improve the data agent itself. She names three structural problems instead. Ambiguity: the agent cannot tell which table, column, data source, or knowledge base is the source of truth for a given question when everything is weighted equally. Staleness: KPI definitions, decisions, and processes change constantly, and nobody keeps the .md files and skills current. Preference: teams and individuals legitimately compute the same metric differently, and the agent has no way to know whose definition applies.

For ambiguity, Daga proposes treating sources of truth as a hierarchy running from cleanest and least flexible to messiest and most dynamic, with the agent always starting at the clean end. Her framework has three buckets. The semantic layer is the best source: a curated set of queries, KPI definitions, metric calculations, and business definitions, so the agent finds the closest KPI and references its data points. Canonical tables come next, a list of parametric queries the agent chooses among and adapts with its own filters, trading some cleanliness for a wider range of answerable questions. The database graph is last: every table linked to its columns and to the metrics it can answer, which is the most flexible and also the hardest to build and maintain. Her rollout advice is concrete: the first two layers are easy to set up and solve about 80% of the problem, and the graph covers the remaining 20%.

For staleness, she proposes a context lifecycle with two components. First, embed live knowledge sources that are always updated and reviewed, such as GitHub, CRM tools, Tableau, or dbt semantic layers, as mandatory data sources. Second, a feedback loop she says most enterprise data agents miss: log every correction event, a wrong database, an outdated definition, a new way to calculate a metric, a new required filter, and use those events to update the agent's context. Evaluation closes the loop, either a curated suite of human-annotated questions or an automated comparison of recent answers against known-correct ones. Daga argues agents fail so often precisely because teams skip evaluation and never track whether the agent is improving.

Preference she presents as unsolved. Her example: team A measures average milestone time from completion of the previous milestone to completion of the current one, team B from the start of the current milestone to the start of the next. Both are correct and give very different answers. Storing every calculation variant in the semantic layer works only if the user prompts for the right one, which recreates the ambiguity problem. Agent memory, whether Mem0 or a memory.md file, stores a preference but cannot distinguish which of two metrics applies when. What she wants is routing to the right metric based on which team or individual is asking, which she describes as building a hive mind for the data agent, and she closes by calling it a research problem the industry has not answered.

## Notable moments

- [0:01:04](https://www.youtube.com/watch?v=B8l81jhvHbI&t=64s) The three problems named: ambiguity, staleness, and preference.
- [0:03:06](https://www.youtube.com/watch?v=B8l81jhvHbI&t=186s) The source-of-truth hierarchy, from semantic layer to canonical tables to database graph.
- [0:06:11](https://www.youtube.com/watch?v=B8l81jhvHbI&t=371s) The context lifecycle: live knowledge sources plus a logged feedback loop and evaluation.
- [0:09:11](https://www.youtube.com/watch?v=B8l81jhvHbI&t=551s) The team A versus team B milestone-time example that makes the preference problem concrete.

## Connections

- [dbt Labs](../../companies/data-infrastructure/dbt-labs.md) ships the semantic layer Daga names as a live knowledge source and as her cleanest source-of-truth bucket.
- [Cognee](../../companies/memory-rag-search/cognee.md) builds the graph-plus-memory substrate that maps to her database-graph layer and its maintenance burden.
- [Are We Ready for an Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md) examines the same gap she hits with Mem0-style memory, storage without the judgment of which stored fact applies when.
