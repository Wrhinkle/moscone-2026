# Snorkel (Snorkel AI)

> Stanford-spinout that turned programmatic data labeling into an "expert data" platform for evaluating and tuning enterprise AI agents — benchmarks, specialized evaluators, and human-expert data pipelines instead of generic LLM-as-judge.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2019, Redwood City, CA — spun out of a Stanford AI Lab project started in 2015 (Verified — company site, Contrary Research, press)
- **Website / GitHub:** https://snorkel.ai · https://github.com/snorkel-team

**Disambiguation:** the AIEWF sponsor "Snorkel" is Snorkel AI, the data-development/evals company — not the open-source library alone (which they also maintain).

## What they do

Snorkel's core idea, carried over from the original Stanford research on weak supervision, is that labels/judgments should be written as *code* (labeling functions, programmatic evaluators) and then denoised statistically, rather than collected one annotation at a time. The company productized this as **Snorkel Flow**, an "AI data development platform": subject-matter experts encode judgment as functions, the platform aggregates and error-corrects them, and you get large high-quality labeled/eval datasets in hours instead of months.

Since ~2024 the platform has pivoted from classic ML training data toward the agent era, with three commercial surfaces: (1) **Snorkel Evaluate** (GA May 2025) — build benchmark datasets and *specialized evaluators* that grade model/agent outputs against custom, expert-calibrated criteria with programmatic pass/fail, plus error-mode analysis and correction; (2) **Snorkel Expert Data-as-a-Service** — a managed network of domain experts (finance, legal, medicine, coding) producing eval and tuning data, sold to enterprises and frontier labs; (3) fine-tuning/alignment tooling that closes the loop from eval failures back into training data. Their current research direction is executable **simulation environments** for agent testing (they cite work on Agents' Last Exam and Terminal-Bench-style projects), and they published **UNDERWRITE**, an expert-first benchmark for AI agents in insurance underwriting (accepted paper at AIEWF 2026).

What you'd actually buy: an enterprise platform (SaaS or in your Azure/VPC environment) where your experts define what "correct" means, and evaluators are trained/calibrated on expert-adjudicated data rather than a single generic judge prompt.

## Founders & origins

Founded 2019 by five Stanford AI Lab collaborators (Verified): **Alex Ratner** (CEO, did his PhD on weak supervision under Ré), **Christopher Ré** (Stanford professor; prior spinouts include Lattice Data, acquired by Apple, and co-founding SambaNova), **Braden Hancock**, **Henry Ehrenberg**, and **Paroma Varma**. The Snorkel research project (2015–2019) was developed with Google, Intel, Stanford Medicine, and DARPA before incorporation — an unusually deep research pedigree (60+ weak-supervision papers pre-company; the team now claims 200+ peer-reviewed publications).

## Funding

- **Seed/Series A, out of stealth July 2020:** $15M, Greylock and GV among backers (Verified).
- **Series B, April 2021:** ~$35M led by Lightspeed (Verified).
- **Series C, August 2021:** $85M led by Addition and BlackRock, ~$1B valuation (Verified).
- **Series D, May 2025:** $100M led by Addition, with Prosperity7 Ventures, Greylock, Lightspeed, and strategic investors **BNY** and **QBE Ventures**, at a **$1.3B valuation** (Verified — BusinessWire, Forbes, FinSMEs).
- **Total raised:** ~$237M (Verified). Accenture Ventures also invested (2023) to push Snorkel into financial services (Verified — Accenture newsroom).

## Evidence of real-world use

Strong for an evals vendor, with the usual caveat that many banking customers are unnamed. Documented: **five of the top 10 US banks** as customers (Verified — repeated in company and independent coverage); named enterprise users/partners include **Wayfair, Experian, BNY, QBE** (the latter two put money in — a usage-backed signal), plus government work via **DARPA and In-Q-Tel** heritage. Case studies with numbers: a global systemically-important bank built a customer-intent classifier to >99% accuracy in under 24 hours vs. a month of hand-labeling; a global bank's contract-extraction agent on Azure went from ~25% accuracy to 95% expert acceptance after Snorkel-style eval/data rework (Reported — Microsoft blog, May 2026); design partner **Rox** (agentic sales startup) improved evaluator accuracy from 75% (LLM-as-judge) to 99%+ (Reported — Series D press). Forbes reports frontier labs buy their expert data (Reported). OSS: `snorkel-team/snorkel` (~5.9k stars, Reported) is historically influential but in maintenance mode — the company's value is now the commercial platform. Microsoft Pegasus program member; booth L-G12 and two talks at AIEWF 2026.

## Relevance to agentic AI engineering

Snorkel sits in the eval/data layer of the agent stack, and its "expert-calibrated evaluator + simulation environment" thesis maps directly onto this repo's benchmark papers: their UNDERWRITE benchmark is the enterprise cousin of *FeatureBench*, *ProdCodeBench*, and *SWE-EVO*, and their position — generic benchmarks mislead — echoes *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* and *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*. Their AIEWF talk on a 4B model beating a 235B model on financial tool-use via RL and "tool discipline" connects to *The Evolution of Tool Use in LLM Agents*; the executable-simulation-environments work parallels *Verifiable Software Worlds for Computer-Use Agents*.

## Use cases & considerations

Use cases: (1) building a domain-specific eval harness for a back-office document agent (e.g., grading a job-packet auditor's JSON against expert-defined readiness criteria rather than a generic judge); (2) creating benchmark datasets from real workflow traces for regulated domains; (3) turning eval failures into fine-tuning data for a small specialized model; (4) buying expert eval data outright.

Considerations: enterprise-first pricing (no public pricing page — sales-led; expect six figures), heavier lift than plug-in observability tools; this is eval *construction*, not tracing — it complements rather than replaces LangSmith/Braintrust/Arize-style trace observability. Competitors: **Scale AI, Surge AI, Mercor, Labelbox** (expert data) and **Braintrust, LangSmith, Arize, Galileo, Patronus AI** (evals). Open questions: how much of revenue is platform vs. data-services, and whether frontier-lab data demand is durable.

## Sources

- https://snorkel.ai/ · https://snorkel.ai/company/ · https://snorkel.ai/our-technology/snorkel-evaluate/
- https://snorkel.ai/ai-engineer-world-fair/
- https://www.forbes.com/sites/rashishrivastava/2025/05/29/snorkel-ai-raises-100-million-to-build-better-evaluators-for-ai-models/
- https://www.finsmes.com/2025/05/snorkel-ai-raises-100m-in-series-d-funding-at-a-1-3-billion-valuation.html
- https://www.businesswire.com/news/home/20250529083998/en/ (Series D announcement)
- https://blogs.microsoft.com/bayarea/2026/05/20/how-snorkel-ai-helps-enterprises-build-ai-agents-they-can-trust/
- https://research.contrary.com/company/snorkel-ai
- https://newsroom.accenture.com/news/2025/accenture-invests-in-snorkel-ai-to-help-financial-services-firms-transform-data-into-ai-solutions
- https://snorkel.ai/blog/successful-ai-adoption-in-finance-why-5-of-the-top-10-us-banks-choose-snorkel-ai/
- https://github.com/snorkel-team/snorkel
- https://www.clay.com/dossier/snorkel-ai-funding
