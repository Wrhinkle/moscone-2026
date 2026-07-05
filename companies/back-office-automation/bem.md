# Bem

> API platform that turns any unstructured input — PDFs, email threads, images, audio, even SMS/WhatsApp — into schema-valid, confidence-scored JSON, positioned as the "production layer for unstructured data" for regulated industries.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** silver
- **Founded:** 2022, San Francisco (Reported — company site says 2022; public launch and seed announcement came June 2024)
- **Website / GitHub:** https://bem.ai · https://github.com/bem-ai (SDK repos, e.g. go-sdk)

## What they do

Bem sells a pipeline API for unstructured data. The current V3 API exposes seven composable functions — **Extract** (multi-modal: PDF, image, audio, video, email, SMS, WhatsApp → structured JSON, with automatic selection across 15+ underlying models), **Classify** (route inputs to workflows), **Parse**, **Split** (segment 100+ page document packets), **Join** (three-way entity matching across systems), **Enrich** (resolve/augment against CRM/ERP data via semantic search), and **Payload Shaping** (JMESPath-based output formatting for downstream systems). Functions chain into **Workflows**: versioned graphs with branching logic, fallback states, and idempotent semantics (Verified — platform page, docs).

The differentiating pitch is auditability rather than raw extraction quality: per-field confidence scores, audit trails, golden datasets with regression testing, precision/recall/F1 metrics, drift detection, a built-in human-review inbox, and fine-tuning that auto-retrains on corrections. Their own framing is contrarian — "we don't sell software, we sell trust," self-described "AI skeptics" building deterministic guardrails around model outputs for regulated industries (Verified — company page). Integration surface: stateless REST API with webhook delivery, auto-generated SDKs in TypeScript, Python, Go, and C#, a Terraform provider, and a CLI; plus no-code **Forge** (visual workflow composition) and **AI Forms** (auto-generated operator UIs). Deployment ranges from multi-tenant cloud (US/EU) to AWS PrivateLink to air-gap-capable on-prem/VPC. SOC 2, HIPAA, GDPR. Free tier of 100 monthly function calls, then graduated pay-as-you-go — a public self-serve pricing page (Verified — site).

## Founders & origins

**Antonio Bustamante** (CEO) and **Upal Saha** (co-founder). Bustamante previously founded **Silo**, an operating system for the food supply chain, where Saha was an engineering manager (Verified — seed announcement authored by both, press, Crunchbase). The origin story follows directly: years of watching supply-chain businesses run on faxes, PDFs, and manual re-keying led to building "the universal data pipeline that transforms anything and everything into your desired schema" (Verified — their seed blog post, June 2024). Bustamante writes a Substack (bem-log) and hosts a podcast, "Hard Software."

## Funding

- **Seed:** $3.7M, announced June 6, 2024, led by Uncork Capital, with Kevin Mahaffey, Roar Ventures, Garry Tan, and logistics/supply-chain founders and executives (Verified — company blog, Businesswire, VentureBeat)
- Some profiles cite ~$4M total including SNR and Antigravity (Reported — single aggregate source)
- **Series A:** Not found in public sources as of 2026-07-02. **Total raised:** ~$3.7–4M.

## Evidence of real-world use

Moderate and mostly self-reported. Named customers with claimed outcomes on the site: **Fleetio** (fleet software; 65% processing-time reduction), **Ascend** (finance; 4× usage growth in year one), **PromptWell** (insurance; 80% reduction in engineering overhead), **Ply** (manufacturing; 15 hrs/week saved per team member), **Rapide**, plus logos for **Alvys**, **Clasp**, and **Auto Integrate** (Reported — company site; no independent case-study write-ups found). At seed they claimed ~10 early customers (Verified — funding press). Their about page claims millions of documents processed daily for Fortune 500 companies in regulated industries (Unverified — own blog only). Stronger signals: a public self-serve pricing page with a free tier, four maintained SDKs plus Terraform/CLI, and active hiring (DevRel, AE) — this is a real commercial developer product, but adoption scale is not independently corroborated.

## Relevance to agentic AI engineering

Bem sits at the ingestion boundary of an agent stack — the same layer as Reducto (also profiled in this repo), but with more emphasis on workflow orchestration, entity resolution, and governance than raw parsing accuracy. Its composable typed functions are effectively pre-built tools for tool-calling agents, echoing the multi-tool orchestration patterns in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. The confidence-scored, audited, human-review-gated output design is a shipping instance of the auditability agenda in *Governance by Construction for Generalist Agents*, and its golden-dataset regression testing mirrors the reproducible-evaluation argument of *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*. Clean schema-valid extraction also feeds retrieval/memory quality — the concern of *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*. For a construction back office: bill-of-lading/invoice/sub-bill intake, splitting mixed job-packet uploads, and email-thread-to-JSON pipelines (they publish a freight-inbox automation tutorial) map directly onto job-packet readiness auditing.

## Use cases & considerations

**Use cases:** (1) email/attachment intake agents — classify and extract quotes, invoices, rate confirmations from a shared inbox into typed JSON; (2) document-packet splitting and three-way matching (PO/invoice/receipt) for AP automation; (3) customer onboarding via bulk data-dump import into your schema; (4) human-in-the-loop extraction where per-field confidence routes low-confidence fields to a review inbox.

**Considerations:** proprietary hosted API — lock-in comparable to Reducto/Extend, mitigated somewhat by on-prem options; adoption metrics are self-reported, so pilot on your own documents; small team and seed-stage funding against much better-capitalized competitors (Reducto at $108M raised, Unstructured, LlamaParse, Tensorlake, hyperscaler document AIs) is a durability question; the "consumer-ai" categorization here is a repo convention — the product is squarely B2B infrastructure. Open questions: Series A status, and whether the governance/workflow layer is enough moat as frontier multimodal models commoditize extraction itself.

## Sources

- https://www.bem.ai/
- https://www.bem.ai/platform
- https://www.bem.ai/company
- https://www.bem.ai/use-cases
- https://blog.bem.ai/p/bem-raises-seed
- https://blog.bem.ai/about
- https://blog.bem.ai/p/how-to-build-a-freight-email-automator
- https://www.businesswire.com/news/home/20240606931609/en/Bem-an-AI-Powered-Data-Interface-Raises-$3.7M-Seed-to-End-Manual-Data-Integration
- https://venturebeat.com/ai/bem-secures-3-7m-to-automate-unstructured-data-conversion-for-engineers
- https://www.crunchbase.com/organization/bem-5eb1
- https://tracxn.com/d/companies/bem/__641K7KK5M8MuNQOhoSi25j5dnUUTELod4gkfeZvtijU
