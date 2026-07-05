# Agentic Search in the Wild: Intents and Trajectory Characteristics of Autonomous Web-Search Agents

- **Status:** Located — published as "Agentic Search in the Wild: Intents and Trajectory Dynamics from 14M+ Real Search Requests" ([arXiv:2601.17617](https://arxiv.org/abs/2601.17617))
- **Area:** memory-research-agents
- **Authors / venue / date:** Jingjie Ning, João Coelho, Yibo Kong, Yunfan Long, Bruno Martins, João Magalhães, Jamie Callan, Chenyan Xiong. arXiv v1 2026-01-24, v3 2026-04-28. Accepted to SIGIR 2026.

## Problem
We build search agents on assumptions about how they *should* reformulate queries and consume evidence, but almost no one has looked at what deployed agents actually do at scale. This paper is the first large-scale field study of autonomous web-search behavior: 14.44M search requests across 3.97M sessions from external agentic clients hitting DeepResearchGym, an open search API.

## Approach
Sessions get LLM-annotated with a three-way intent taxonomy (Declarative/fact-seeking, Procedural/how-to, Reasoning) and step-wise reformulation labels (Exploration, Specialization, Generalization, Repetition). The authors introduce **CTAR (Context-driven Term Adoption Rate)** — the fraction of newly introduced query terms lexically traceable to previously retrieved evidence — to measure whether agents actually ground reformulations in what they read. Anonymized logs are released on HuggingFace.

## Key findings
- Intent mix is lopsided: 88.64% Declarative, 7.41% Reasoning, 3.96% Procedural.
- 47.77% of sessions are single-query; >90% of multi-turn sessions have ≤10 steps; 89.21% of inter-step intervals are under one minute (56.12% under 10 seconds).
- Retrieval depth is essentially hardcoded: 91.64% of sessions use K ∈ {1, 5, 10}, and only 1.35% vary K within a session — agents don't adapt how much they retrieve.
- Repetition loops emerge in fact-seeking work: Declarative sessions' near-duplicate rate climbs to 42.68% by step 9, vs. ~18% flat for Reasoning sessions.
- CTAR: ~54% of new query terms appear in accumulated evidence — 78.35% for Specialization moves, 20.92% for Repetition. Earlier steps (beyond the last retrieval) contribute a measurable +5.81pp, i.e., cross-step memory matters.
- Generalization (relaxing constraints) is rare (~8–11%) — agents get stuck narrowing, rarely zoom out.

## Limitations & open questions
No success/correctness labels — a session ending isn't a session succeeding. No client-side visibility (prompts, memory architecture, control policy), so behavior can't be attributed to design choices. CTAR is exact-token match, missing paraphrase-level grounding. One API's traffic may skew toward particular frameworks; a skeptic would ask whether 88% Declarative reflects agent workloads generally or DeepResearchGym's user base.

## Why builders should care
If your agent does fact-seeking search, add repetition detection as a stopping/strategy-shift trigger — near-duplicate loops are the dominant late-session failure mode. Make retrieval depth (K) a per-intent, per-step decision instead of a constant, and keep accumulated evidence terms in context across steps: over half of productive reformulation vocabulary comes from what the agent already retrieved.

## Related companies in this landscape
- **Exa** — search API built for agents; this is exactly the traffic pattern (fixed-K, rapid multi-step sessions) its API design should exploit.
- **Bright Data / Apify / Oxylabs / Firecrawl** — web-data infrastructure for LLM ingestion; the finding that agents fire sub-10-second query bursts shapes rate-limit and caching design.
- **Browserbase** — hosted browser infra for web agents; trajectory-level repetition detection is a natural platform feature.
- **Zep AI / Cognee / LangChain / LlamaIndex** — memory layers and agent frameworks; the +5.81pp cross-step CTAR contribution is direct evidence that persisting earlier-step evidence (not just last retrieval) improves query grounding.
- **Arize / Braintrust** — agent observability/evals; repetition-rate-by-step is a ready-made production metric for detecting stalled research agents.
- **Yutori** — web-monitoring/research agents; the intent taxonomy suggests budgeting retrieval differently for tracking (declarative) vs. synthesis (reasoning) tasks.

## Sources
- https://arxiv.org/abs/2601.17617
- https://arxiv.org/html/2601.17617v3
- https://huggingface.co/papers/2601.17617
