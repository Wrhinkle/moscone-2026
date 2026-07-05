# Not Diamond

> A model-routing layer: it predicts, per request, which LLM will answer best (or cheapest at equal quality) and sends the call there — now positioned specifically as intelligent routing for coding agents, plus an "agentic" prompt-optimization product for enterprises.

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified — Crunchbase/Tracxn, VentureBeat launch coverage)
- **Website / GitHub:** https://www.notdiamond.ai · https://github.com/Not-Diamond · https://www.notdiamond.ai/pricing

## What they do
Two products, one thesis: no single frontier model wins on every input, so route per-request.

1) **Model router.** A "meta-model" classifies each incoming prompt and predicts the best target model before execution, returning a routing recommendation in tens of milliseconds (company claims ~60ms decisions; the current site says ~100–200ms added latency per routing decision). It ships as middleware that sits *between your agent harness and your gateway* — Not Diamond recommends the model; your own keys/gateway make the call, which is their anti-lock-in argument. The 2026 positioning is squarely **routing for coding agents** (explicitly including Claude Code), claiming ~5% accuracy gains, 20–40% cost savings, and privacy-preserving routing where Not Diamond never sees payloads or outputs (Verified — notdiamond.ai homepage and pricing page; performance numbers are company-sourced/Reported).

2) **Prompt Adaptation** (launched May 2025 at SAP Sapphire): an agentic system that programmatically rewrites and re-optimizes prompts when you switch models or vendors, replacing manual prompt migration. Company claims 5–60% accuracy improvements on enterprise client datasets (Reported — PRNewswire launch release; SAP's CTO Philipp Herzig previewed an SAP prompt-optimization service in SAP AI Core's generative AI hub built with Not Diamond, Verified — PRNewswire + SAP Sapphire coverage).

Integration surface: Python SDK (`notdiamond` on PyPI), REST API, and a merged LangChain community integration (`NotDiamondRoutedRunnable`). Pricing is public and usage-based: $0.05 per million tokens routed pay-as-you-go, enterprise volume tiers with SSO/SAML and SLAs; no free tier. SOC 2 and ISO 27001 claimed (Verified — pricing page).

## Founders & origins
**Tomás Hernando Kofman** (CEO), **Tze-Yang Tung**, and **Jeffrey Akiki** (Verified — VentureBeat, feedtheai, Taiwan News). Kofman hit the "which model do I use" problem while building a previous no-code AI product and recruited Tung and Akiki (ML engineers) to build routing as infrastructure (Reported — VentureBeat launch story). Taiwan News covered the seed as a Taiwanese-founder story (NT$75.4M ≈ the same $2.3M round), suggesting at least one founder's Taiwan ties (Reported).

## Funding
- **Seed, Jul 30 2024: $2.3M**, led by defy.vc, with a notably heavyweight angel list: Jeff Dean (Google DeepMind), Julien Chaumond (Hugging Face CTO), Ion Stoica (Databricks/Anyscale), Tom Preston-Werner (GitHub), Zack Kass (ex-OpenAI), Scott Belsky, Jeff Weiner (Verified — VentureBeat, Crunchbase, feedtheai).
- **Follow-on round, ~May 2025**: Deepwater Asset Management, IBM (via IBM Ventures), SAP.io Fund, Myriad Venture Partners, defy.vc. **Amount not found in public sources** (Verified that the round happened — Deepwater investment memo, IBM Think post, Myriad LinkedIn announcement; aggregators like Tracxn still show only $2.3M total, so treat total raised as unknown but >$2.3M).

## Evidence of real-world use
- **Strongest signals:** SAP is both strategic investor and documented integration partner — an SAP-built prompt-optimization service in SAP AI Core designed with Not Diamond (Verified). IBM invested and published its own rationale (Verified). **Rootly** (Head of AI Labs, on-site testimonial): "+39% average accuracy, some use cases more than doubling" (Reported — customer quote, no independent write-up found). **OpenRouter's CEO** gives a testimonial — interesting because OpenRouter is also arguably a competitor (Reported).
- **Weaker signals:** homepage logo wall (Hugging Face, Dropbox, DoorDash, American Express, Groq, Forethought, Eden AI, Replicated) with no case studies behind most logos — logos, not documented usage.
- **OSS/community:** notdiamond-python SDK ~52 GitHub stars, ~3.9k weekly PyPI downloads; an `awesome-ai-model-routing` curated list; merged LangChain integration. Modest adoption — this is a commercial API with an SDK, not an OSS-flywheel company.
- Public pricing page = real self-serve commercial product, though pay-as-you-go still requires an application.

## Relevance to agentic AI engineering
Routing is a control-plane decision inside agent loops: every tool-call/plan/patch step is a model invocation someone must pick a model for. For coding agents specifically, the repo's benchmark papers (ProdCodeBench, SWE-EVO, SlopCodeBench on long-horizon degradation) show model quality diverges sharply by task type and horizon — exactly the variance a per-request router monetizes; the "Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering" critique also cuts at router-vendor accuracy claims built on benchmark-style evals. Prompt Adaptation is essentially automated eval-driven prompt migration, adjacent to "Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering." Multi-tool orchestration work (The Evolution of Tool Use in LLM Agents) points the same direction: heterogeneous model portfolios per step, which needs a routing layer.

## Use cases & considerations
Use cases: (1) cost-tiering a high-volume coding agent — route easy diffs to cheap models, hard refactors to frontier ones; (2) multi-vendor resilience/arbitrage without rewriting prompts, via Prompt Adaptation; (3) accuracy lift on classification-ish enterprise LLM workloads (the Rootly pattern). Considerations: routing quality is the whole product and is hard to independently verify — demand evals on *your* traffic before believing 5–60% claims; the router itself adds 100–200ms per call (matters for realtime/voice loops); small team, undisclosed later-round size, so vendor-viability risk is real. Competitors: OpenRouter, Martian, Unify, LMSYS's open-source RouteLLM, and gateway-with-routing plays like Portkey/LiteLLM — plus the null hypothesis that frontier labs' own auto model selection (e.g., in-product model pickers) absorbs this layer.

## Sources
- https://www.notdiamond.ai/
- https://www.notdiamond.ai/pricing
- https://venturebeat.com/ai/not-diamond-automatically-routes-your-query-to-the-best-llm
- https://www.feedtheai.com/not-diamond-secures-2-3m-for-ai-model-routing-technology/
- https://www.taiwannews.com.tw/news/5906945
- https://www.prnewswire.com/news-releases/not-diamond-launches-prompt-adaptation-an-agentic-system-for-multi-model-enterprise-ai-302459831.html
- https://www.deepwatermgmt.com/insights/investing-in-not-diamond
- https://www.ibm.com/think/insights/why-ibm-ventures-invested-in-not-diamond
- https://tracxn.com/d/companies/notdiamond/__-ifpQNdltj98K5h7wki2GzegvCScnOt_vhbDrwaZaA0
- https://github.com/Not-Diamond/notdiamond-python
- https://pypi.org/project/notdiamond/
- https://github.com/langchain-ai/langchain/pull/25897
