# Reducto

> API platform that turns messy real-world documents (scanned PDFs, spreadsheets, forms, handwriting) into accurate, LLM-ready structured data — the ingestion layer in front of RAG pipelines and document agents.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** platinum
- **Founded:** 2023, San Francisco; Y Combinator W24 batch (Verified — YC directory, press)
- **Website / GitHub:** https://reducto.ai · https://github.com/reductoai (RD-TableBench)

## What they do

Reducto sells document-understanding APIs. The core is **Parse**: send a document (30+ formats — PDF, images, Excel, PowerPoint), get back layout-aware, chunked, LLM-ready output with bounding boxes for citations. Architecturally it's a multi-pass hybrid: traditional CV/layout models segment the page, then Vision-Language Models review and correct the output — what they brand "Agentic OCR," a VLM checking the OCR's work on edge cases like handwriting, checkboxes, redlines, and rotated scans. On their own open benchmark of 1,000 hand-labeled complex tables (RD-TableBench), they report ~0.90 similarity, roughly 10–20 points above AWS Textract, Google, and Azure document APIs (Reported — their benchmark, but the dataset and scoring code are open source).

Around Parse sit **Extract** (schema-driven structured extraction — invoice fields, form data, financial disclosures — into JSON), **Split** (separating multi-document files, e.g. a 200-page loan or claims packet, into individual units), **Edit** (programmatic form-filling of detected blanks, tables, and checkboxes without templates or bounding boxes), and a **Studio** UI for iterating on pipelines. Pricing is public and self-serve: pay-as-you-go at $0.015/credit with 15k free credits, then Growth/Enterprise tiers adding zero-data-retention, BAA/HIPAA, data residency, and VPC/on-prem deployment. SOC 2 and HIPAA compliance, 99.9% uptime SLA (Verified — pricing/site).

## Founders & origins

**Adit Abraham** (CEO) and **Raunak Chowdhuri** (CTO), who met as students at MIT (Verified — Fortune, funding press). Abraham did CS at MIT, PM work on Ads/Search at Google, and ML research at MIT Media Lab; Chowdhuri spent time at Nvidia (Reported — Fortune, YC profile). Origin story: while consulting on LLM projects they kept hitting the same wall — models were fine, but PDF ingestion was garbage — so they built the parser as the product. YC Winter 2024.

## Funding

- **Seed:** $8.4M, October 2024, led by First Round Capital with YC, BoxGroup, SV Angel, Liquid 2; angels include Arash Ferdowsi (Dropbox) and Andrew Ofstad (Airtable) (Verified — Finsmes, company blog)
- **Series A:** $24.5M, April 2025, led by Benchmark (Verified — Fortune exclusive, GlobeNewswire)
- **Series B:** $75M, October 2025, led by Andreessen Horowitz with Benchmark, First Round, BoxGroup, YC (Verified — PRNewswire, multiple outlets)
- **Total raised:** $108M (Verified — company announcement)

## Evidence of real-world use

Unusually strong for a two-year-old company. Named customers with documented usage, not just logos: **Harvey** (legal AI, 1,300+ orgs) has a published case study — Reducto replaced their OCR layer after complaints about handwriting/redlines, in production within 6 weeks, with built-in citations for auditability. **Airtable, Scale AI, Rogo, Vanta, Medallion, Newfront, JLL, Toast** and an unnamed Fortune 10 enterprise are cited across funding press and the site. Scale claims: 3B+ pages processed (site, 2026); monthly volume grew 6x in the five months between Series A and B (Reported — Series B release). A Modal case study documents their infra (3x latency improvement), independent corroboration that real volume flows through the system. Public pay-as-you-go pricing = real self-serve product. RD-TableBench is community-cited (e.g., by third-party parser comparisons and the PulseBench-Tab paper lineage).

## Relevance to agentic AI engineering

Reducto is the ingestion boundary of the agent stack: any back-office agent — document packet auditing, subcontractor bill intake, invoice extraction, insurance/claims workflows — is only as good as what it can read, and Extract's schema-level JSON output is exactly the "structured JSON extraction / missing-information detection" pattern in this repo's back-office landscape. It feeds directly into the RAG-evaluation and retrieval concerns of *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* and *Memory for Autonomous LLM Agents* (garbage ingestion poisons memory and retrieval alike). Its "Agentic OCR" self-correction loop is a concrete instance of the verify-your-own-output pattern discussed in *Reproducible, Explainable, and Effective Evaluations of Agentic AI*; bounding-box citations serve the same auditability goal as *Governance by Construction for Generalist Agents*. For a construction back office (job packet readiness, sub bills, permit/HOA checklists), it's the obvious candidate parse layer.

## Use cases & considerations

**Use cases:** (1) parse layer for RAG over contracts, claims, or job packets where tables/handwriting break naive PDF-to-text; (2) invoice/sub-bill intake — Extract with a fixed schema plus citation bounding boxes for human review; (3) splitting mixed multi-document uploads (closing packets, permit bundles) before routing to agents; (4) form-filling automation via Edit.

**Considerations:** per-page costs compound at volume — model spend before committing; it's a proprietary API (self-host only at Enterprise), so lock-in is real versus OSS like Docling, Unstructured, or LlamaParse. Competitors: LlamaParse (LlamaIndex), Unstructured, Extend, Tensorlake, and the hyperscaler document APIs — plus the standing risk that frontier multimodal models get "good enough" at raw PDF reading. Benchmark leadership claims come from their own (open) benchmark; validate on your documents. Open question: how durable the moat is as VLM costs fall.

## Sources

- https://reducto.ai/
- https://reducto.ai/pricing
- https://reducto.ai/blog/reducto-series-b-funding
- https://reducto.ai/blog/rd-tablebench
- https://reducto.ai/blog/reducto-harvey-legal-ai-customer-story
- https://fortune.com/2025/04/25/exclusive-reducto-ai-document-parsing-startup-raises-24-5-million-series-a-led-by-benchmark/
- https://www.prnewswire.com/news-releases/reducto-raises-75m-series-b-to-define-the-future-of-ai-document-intelligence-302581462.html
- https://www.finsmes.com/2024/10/reducto-raises-8-4m-in-seed-funding.html
- https://www.globenewswire.com/news-release/2025/04/25/3068298/0/en/Reducto-Raises-24-5M-Series-A-Round-to-Help-Enterprises-Unlock-Unstructured-Data.html
- https://www.ycombinator.com/companies/reducto
- https://github.com/reductoai/rd-tablebench
- https://modal.com/blog/reducto-case-study
