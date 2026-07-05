# Wisedocs

> AI platform that turns huge, messy medical-record files into indexed, deduplicated, summarized, and searchable claim documents for insurers, IME firms, and legal teams — with clinician review in the loop.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2018, Toronto, Canada (Verified — company about page, BetaKit, Goodmans)
- **Website / GitHub:** https://www.wisedocs.ai/ — no public GitHub presence found

## What they do

Wisedocs is a vertical document-processing SaaS for the insurance-claims ecosystem: workers' compensation, disability, liability, medical malpractice, and independent medical evaluations (IMEs). The core problem is concrete — a single claim file can be thousands of pages of co-mingled PDFs, faxes, and handwritten clinical notes. The platform ingests these, detects and separates co-mingled records, deduplicates redundant pages, converts handwriting to structured data, and indexes everything into a medical chronology (a searchable timeline of events) plus categorized list views.

On top of that indexing layer sit generative products: **Medical Summaries** (launched June 2023 as one of the earlier production GenAI products in insurtech), **Medical Insights** (search/filter/explore claim data), **WiseChat** (a conversational interface over a claim file), **Custom Reports**, and a newer **Claims Decision Intelligence** layer positioned to move from "summarize the file" toward "support the decision." The company says its models are trained on 100M+ documents (Reported — company claim, not independently verifiable). Delivery is via web app plus an API for integrating claims/records/summary data flows into existing claims systems. A differentiator they lean on hard: expert clinician QA on outputs, since summaries feed legal-defensible reports — this is human-in-the-loop as a product feature, not an afterthought.

Practically, what you'd buy is a processing pipeline plus review workflow; what you'd integrate is their API to push claim documents in and pull structured chronologies/summaries out.

## Founders & origins

- **Connor Atchison** — co-founder & CEO. Canadian Armed Forces veteran; the origin story (Verified across company site and BLG interview) is his experience with broken medical-records handling during veterans' claims and transition to civilian life.
- **Jenna Earnshaw** — co-founder & COO (Verified — BLG, company site).

## Funding

- **Seed, March 2022:** CA$4.1M, oversubscribed, led by Ripple Ventures with Greensky Capital and angels including George Papayiannis (Vena) and Tim Lett (Verified — Goodmans, The SaaS News).
- **Series A, January 2024:** US$9.5M (CA$12.7M), oversubscribed, led by Information Venture Partners with Thomson Reuters Ventures and ManchesterStory (Verified — BusinessWire, BetaKit, Insurtech Insights).
- **Growth debt, August 2024:** CA$4.5M from CIBC Innovation Banking (Verified — company/CIBC announcement).
- **Follow-on, February 2025:** ~$3.5M (Reported — Tracxn only).
- **Total:** roughly US$16M equity + CA$4.5M debt (approximate; mixed currencies). No Series B found in public sources as of 2026-07-02.

## Evidence of real-world use

Stronger than the median supporting-tier sponsor. Named customers on their site include **WCF Insurance, HRSA, MEDconfirm, Rising, Island Insurance, and UHG** (logos — treat as directional). More convincing are the specific case studies: **AGS** automated ~90% of repetitive work and processed claims documents 83% faster; **Turner Vocational Services** cut record-review time ~50%; a named IME physician scaled from 1–2 to 5–6 assessments/week; an insurance legal team reported a 70% drop in 20+ hour-per-case reviews (all Reported — company success stories, but named and specific). Third-party signals: ~50 customers and "more than doubled customer base" at Series A (Verified via press), Thomson Reuters Ventures on the cap table (a strategic in legal-document workflows), and revenue of ~$14.4M with ~116 employees in 2025 (Reported — GetLatka, unverified methodology).

## Relevance to agentic AI engineering

Wisedocs is a reference case for regulated-domain back-office automation: long-document ingestion → structured extraction → grounded generation → human expert QA. The clinician-review layer is a working example of the oversight patterns in **Governance by Construction for Generalist Agents**, and their chronology/indexing substrate is exactly the structured-metadata question raised in **Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval** — WiseChat only works because the indexing layer exists first. The medical-chronology timeline is also a domain-specific instance of the long-term memory structures surveyed in **Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation**. Coding-agent and voice-agent papers in this repo are not relevant here.

## Use cases & considerations

- Claims teams: automate intake, dedup, and chronology of multi-thousand-page medical files.
- IME/legal firms: defensible summaries and custom reports with clinician sign-off.
- Builders: study their HITL + API design as the pattern for document-heavy agent products (relevant to Ridgeline-style insurance-restoration paperwork, where claim files look structurally similar).

**Considerations:** closed platform, no public pricing (enterprise sales motion), no OSS/GitHub footprint, and outputs are only as defensible as the QA layer. Competitors: **EvenUp** and **Eve** (legal-side medical chronologies), **Tonic/Digital Owl**, **Reducto** (this repo — general document parsing you'd build with, vs. Wisedocs' full vertical workflow), and incumbent IME service bureaus. Open question: whether Claims Decision Intelligence crosses from summarization into recommendation, which raises a different regulatory bar.

## Sources

- https://www.wisedocs.ai/
- https://www.wisedocs.ai/company/about-us
- https://www.wisedocs.ai/success-stories
- https://www.blg.com/en/insights/2024/ri/how-to-turn-your-ai-startup-into-tomorrows-success-story
- https://www.businesswire.com/news/home/20240130175319/en/
- https://betakit.com/ai-powered-medical-record-reviewer-wisedocs-closes-12-7-million-cad-series-a-round/
- https://www.insurtechinsights.com/wisedocs-raises-9-5-million-in-series-a-funding-to-expand-ai-driven-insurtech-solutions/
- https://www.goodmans.ca/insights/post/goodmans-tech-blog/wisedocs-closes-4.1-million-eyes-u.s.-expansion
- https://www.thesaasnews.com/news/wisedocs-secures-cad-4-1-million-in-seed-round
- https://www.wisedocs.ai/blogs/cibc-innovation-banking-provides-growth-capital-financing-to-wisedocs-inc
- https://www.businesswire.com/news/home/20230628432354/en/
- https://tracxn.com/d/companies/wise-docs-tech/__CNlalipxSmf0YFeaD90ExIjucURo0BNXDPVRpQswDdM/funding-and-investors
- https://getlatka.com/companies/wisedocs.ai
