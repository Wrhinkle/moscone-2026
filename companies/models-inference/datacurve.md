# Datacurve

> Sells frontier-quality coding training data to AI labs, sourced by paying expert engineers bounties on a gamified platform called Shipd.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified — YC profile, Sacra, TechCrunch agree)
- **Website / GitHub:** https://datacurve.ai/ · Shipd platform: https://shipd.datacurve.ai/ · No significant public GitHub presence found

## What they do

Datacurve is a training-data company for code, positioned explicitly against Scale AI and Surge. The core insight: high-quality coding data for post-training can't be scraped or fully synthesized, and the engineers capable of producing it won't take traditional annotation jobs. So instead of a labeling workforce, Datacurve runs **Shipd**, a gamified bounty platform where vetted software engineers pick "quests" — algorithm problems, testing, UI/UX tasks, ML/data-science challenges — submit solutions, and get paid per accepted contribution. Co-founder Serena Ge frames it as "a consumer product, not a data labeling operation" (TechCrunch).

The commercial workflow (per Sacra's analysis): evaluate a customer's model to find weaknesses, convert the gaps into bounty quests on Shipd, then deliver datasets in standard LLM training formats — supervised fine-tuning pairs, RLHF preference traces, reinforcement-learning environments, and agentic workflow traces — that plug into Ray, MosaicML, or internal lab pipelines. Revenue is project-based custom-dataset contracts, not a self-serve product; there is no public pricing page, consistent with a lab-facing services/data business rather than an API you integrate.

In May 2026 they released **DeepSWE**, a long-horizon agentic coding benchmark (Reported — single detailed source: 113 original tasks across 91 open-source repositories in five languages), signaling a move from pure data supply into evaluation, and their homepage now emphasizes RL environments and "evaluation, iteration, and reinforcement" as the frontier need.

## Founders & origins

**Serena Ge (CEO)** and **Charley Lee**, both University of Waterloo computer science students (Verified — YC, TechCrunch, Waterloo CS news). Ge interned at Cohere on model training/reasoning; Lee interned at Google on AI research. YC Winter 2024 batch; the YC profile listed them as 19 years old at the time. Origin story: they hit the coding-data bottleneck directly and concluded the scarce resource was expert engineers' time, which quality-of-experience — not just pay — would unlock.

## Funding

- **Seed: $2.7M** (Reported — TechCrunch), investors including former Coinbase CTO Balaji Srinivasan and Y Combinator.
- **Series A: $15M, October 2025**, led by Mark Goldberg at Chemistry, with angels who are employees at DeepMind, Vercel, Anthropic, and OpenAI (Verified — TechCrunch, Maginative, Waterloo CS news).
- **Total: ~$17.5–17.7M.** Ge's own announcement says "$17.5 million"; the Waterloo article says $17.7M. Minor discrepancy, both public.

## Evidence of real-world use

- **$1M+ paid out in Shipd bounties** (Verified — TechCrunch and others), which is real money flowing through the supply side, not vanity metrics.
- Contributor count is inconsistent across sources: "more than 1,400 participating engineers" (Tech Funding News) vs. "14,000+ vetted engineers" (Sacra). Treat both as Reported; the order-of-magnitude gap is unresolved.
- **No named customers.** Sacra describes "dependence on a small number of frontier AI labs"; the Series A angel list (DeepMind/Anthropic/OpenAI employees) hints at lab proximity, but no lab has publicly confirmed being a customer. YC's blurb also cites gen-AI dev-tool startups (code editing, design-to-code, PR generation) as buyers of custom data — Reported, unnamed.
- Not found in public sources: revenue figures, case studies with named companies.

## Relevance to agentic AI engineering

Datacurve sits at the *training and eval input* layer of the coding-agent stack — upstream of everything in the coding-agents and swe-infrastructure categories. Their shift toward RL environments and agentic workflow traces is exactly the substrate the agentic-SWE benchmark literature in this repo argues is missing: DeepSWE's "original tasks across real repos" pitch responds directly to the contamination and realism critiques in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* and complements production-derived efforts like *ProdCodeBench* and long-horizon evals like *SWE-EVO* and *SlopCodeBench*. If you're building or fine-tuning coding agents, Datacurve is where task distributions and reward signals come from, not a runtime dependency.

## Use cases & considerations

Use cases: (1) commissioning custom SFT/RLHF datasets targeting a coding model's measured weaknesses; (2) buying RL environments and agentic traces for post-training a coding agent; (3) using DeepSWE as a harder second-opinion eval when public leaderboards saturate; (4) as an engineer, earning on Shipd.

Considerations: customer-concentration risk on a handful of labs; synthetic-data progress could commoditize the offering; no self-serve product or pricing — expect enterprise sales; competitors include Scale AI, Surge AI, Mercor, and labs' internal data teams. Open questions: real contributor count, any named customers, and whether DeepSWE gains third-party adoption.

Note on categorization: they train no models and serve no inference; "models-inference" fits only in the sense of being a model-training input supplier.

## Sources

- https://techcrunch.com/2025/10/09/datacurve-raises-15-million-to-take-on-scaleai/
- https://sacra.com/c/datacurve/
- https://www.ycombinator.com/companies/datacurve
- https://datacurve.ai/
- https://shipd.datacurve.ai/
- https://uwaterloo.ca/computer-science/news/cs-led-startup-secures-177m-transform-ai-training-data
- https://techfundingnews.com/datacurve-raises-15m-series-a-chemistry-high-quality-ai-coding-datasets/
- https://www.maginative.com/article/datacurve-raises-15m-series-a-led-by-chemistry/
- https://x.com/serenaa_ge/status/1976328983458480539
- https://mer.vin/2026/05/deepswe-benchmark-how-datacurve-separates-real-agentic-coding-ability/
