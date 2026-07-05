# Anterior

> Clinical-reasoning AI for health insurers: automates prior authorization and other payer back-office review work, with nurses/clinicians kept in the loop.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** Summer 2022 (Verified — TechCrunch; note: MedCity News says 2023, likely dating the rebrand), New York. Originally named **Co:Helm**, rebranded to Anterior in mid-2024 (Verified).
- **Website / GitHub:** https://www.anterior.com/ — no significant public GitHub presence found.

## What they do

Anterior builds an LLM-powered clinical reasoning platform for **health plans (payers)**, not providers. The wedge is prior authorization: the process where an insurer's nurses review a treatment request against medical-necessity guidelines before approving it. Anterior's system reads the incoming request (including faxes), extracts the clinical facts from medical records, evaluates them against the plan's policy documents, and produces an approval recommendation with cited evidence; a human clinician reviews rather than assembles the case. Their original product framing was "Florence," an AI co-pilot for nurse reviewers (Reported — Sequoia/press, 2023–24); the current platform framing is modular "Actions" — discrete AI tasks like fax reading, medical-record interpretation against guidelines, and converting policy PDFs into machine-usable criteria — composed into "Solutions" per workflow (Verified — company site, MedCity).

What you'd actually buy: a hosted platform integrated into a payer's utilization-management stack. There is a strategic integration with HealthEdge's GuidingCare care-management platform (Reported — company release). Pricing is value-based per use case, with optional per-task fees such as per auto-approved prior auth (Reported — MedCity interview). Deployment is service-heavy by design: a "Forward Deployed Clinician" model embedding engineers and clinicians with the customer, claiming ~5-day average deployments (Reported — company).

## Founders & origins

- **Abdel Mahmoud, MD — co-founder/CEO** (Verified). Libyan-born UK refugee; Sandhurst-trained (reportedly the UK's youngest infantry officer), then a physician who left clinical practice out of frustration with paperwork, took a CS master's at UCL, and did product work at Facebook and Google (Verified across VentureBeat/TechCrunch/Sequoia).
- **Zahid Mahmood — co-founder** (Verified). Prior founder (Buskana, Crowdfund NFT); ~6 years as a software engineer at Global Aerospace (Reported — Exa/directory profiles).

Origin story: Mahmoud's stated goal is making prior auth "invisible, like swiping a credit card." Angel backing includes Mustafa Suleyman (Reported — TechCrunch).

## Funding

- **Seed:** $3.2M, Sept 2023, led by Sequoia (Verified — TechCrunch, Sequoia).
- **Series A:** $20M, June 2024, led by NEA at $95M post-money; Sequoia, Blue Lion Global, Neo participating; NEA's Mohamad Makhzoumi joined the board (Verified — TechCrunch, company).
- **Series B:** $40M, Feb 2026; returning NEA and Sequoia plus new investors FPV Ventures and Kinnevik; valuation not disclosed (Verified — MedCity News, Fierce Healthcare headline, company release).
- **Total raised:** ~$63–64M (Verified — company states $64M; sum of rounds is $63.2M).

## Evidence of real-world use

Stronger than typical for a supporting-tier sponsor, though customer counts are small and mostly company-reported:

- **Geisinger Health Plan** — named deployment; cancer-care prior auths completed in ~155 seconds vs. weeks (Reported — MedCity interview with CEO).
- **MedWatch** and **WNS-HealthHelp** named as customers; customers collectively cover ~50M lives (Reported — company Series B release).
- **99.24% clinical accuracy validated by KLAS Research** — a genuinely independent healthcare-IT evaluator, so this is more than a marketing number (Reported — company citing KLAS; underlying KLAS report not independently fetched).
- One customer processing ~6M prior auths/year; claims of ~75% shorter review cycles and 90+ staff satisfaction (Reported — company site).
- No public pricing page, no OSS footprint — enterprise sales motion only.

## Relevance to agentic AI engineering

Anterior is a reference case for **regulated back-office agents**: document-heavy intake (faxes, PDFs, EHR records), policy-as-rules extraction, evidence-cited reasoning, and mandatory human review — the same shape as construction job-packet auditing or claims workflows. Their "modular Actions" decomposition maps directly onto the multi-tool orchestration patterns in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*, and their oversight/controls posture is a live instance of the concerns in *Governance by Construction for Generalist Agents*. The KLAS-verified accuracy claim is a useful data point for the human-review-loop and benchmark-validity debates raised in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* — domain-specific, independently audited accuracy beats generic benchmarks for buyer trust.

## Use cases & considerations

Use cases: (1) payer utilization-management automation (their core); (2) a pattern to copy — policy-PDF → structured criteria → evidence-cited verdict — for any compliance-review workflow; (3) forward-deployed-clinician model as a template for selling agents into skeptical regulated buyers.

Considerations: payer-only focus (providers are not the customer); prior auth itself is under regulatory pressure (CMS rules) which could shrink or reshape the market; heavy services component may limit self-serve evaluation; competitors include **Cohere Health**, **Availity/Olive remnants**, **Latent Health**, and EHR-native players like **Epic**'s payer tools. Open questions: real customer count beyond the three named; whether the 99.24% KLAS figure covers full case adjudication or sub-tasks.

## Sources

- https://techcrunch.com/2024/06/08/anterior-grabs-20m-from-nea-at-95m-valuation-to-expedite-health-insurance-approvals-with-ai/
- https://medcitynews.com/2026/02/anterior-ai-health-plan/
- https://www.anterior.com/
- https://www.anterior.com/insights/anterior-raises-40m-series
- https://venturebeat.com/ai/meet-the-startup-using-ai-to-slash-healthcares-trillion-dollar-administrative-burden
- https://sequoiacap.com/article/partnering-with-anterior-the-co-pilot-for-health-care/
- https://www.fiercehealthcare.com/ai-and-machine-learning/payer-ai-company-anterior-banks-40m-funding-round (headline only; page blocked fetch)
- https://www.crunchbase.com/organization/co-helm (via search snippet)

*Profile compiled 2026-07-02.*
