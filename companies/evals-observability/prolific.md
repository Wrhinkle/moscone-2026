# Prolific

> A vetted-participant marketplace for collecting human feedback, labels, and evaluation data — the human layer behind preference tuning, RLHF, and AI safety evals.

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** 2014, UK (Verified); pivoted heavily toward AI data/evals in recent years
- **Website / GitHub:** https://www.prolific.com

## What they do
Prolific runs a two-sided marketplace connecting researchers and AI teams with a pool of 200,000+ vetted, demographically-profiled human participants for paid studies. For AI engineers, the relevant product is human-in-the-loop data generation: preference-tuning data (RLHF/RLAIF), safety and red-teaming evals, benchmark construction, and "human feedback from representative populations ... you can defend" — i.e., an API/dashboard to source and manage panels of real people for tasks a model can't self-supervise, with quality controls and demographic targeting that distinguish it from lower-quality crowd platforms.

## Founders & origins
Founded by Ekaterina Damer, Jim Moodie, and Phelim Bradley (CEO); went through Y Combinator (Verified — Crunchbase, TechCrunch).

## Funding
$1.4M seed (via YC), then a £25M ($32M) Series A in July 2023 co-led by Partech and Oxford Science Enterprises — roughly $33-34M total raised (Verified — TechCrunch, Prolific).

## Evidence of real-world use
Reported customers include Google, Stanford, Hugging Face, and Asana; AI2 reportedly cut human-data-collection timelines from weeks to hours using the platform. Sacra (a single, third-party source) estimated ~$350M annualized revenue in April 2026, with 380,000+ studies delivered and 11,000+ AI annotation specialists in 2025 — treat this revenue figure as directional/Reported, not confirmed.

## Relevance to agentic AI engineering
Core to the evals/observability layer: any agent or model that needs human preference data, human-graded benchmarks, or red-team coverage before shipping relies on exactly this kind of vetted-panel infrastructure — an alternative or complement to fully synthetic/LLM-judge eval pipelines.

## Use cases & considerations
Use cases: sourcing RLHF preference pairs, running safety/red-team studies, building human-graded eval sets, UX research for AI products. Considerations: cost and latency of human data vs. synthetic/LLM-judge evals, panel quality/fraud control at scale, competitors include Surge AI, Scale AI's data-labeling arm, and Appen.

## Sources
- https://www.prolific.com/
- https://techcrunch.com/2023/07/11/prolific-raises-32m-to-train-and-stress-test-ai-models-using-its-network-of-120k-people/
- https://www.prolific.com/resources/series-a-fundraise
- https://sacra.com/c/prolific/
- AI Engineer World's Fair 2026 sponsor list (silver tier), https://www.ai.engineer/worldsfair/2026
