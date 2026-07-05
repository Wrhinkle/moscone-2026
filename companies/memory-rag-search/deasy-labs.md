# Deasy Labs

> Metadata orchestration for unstructured enterprise data — auto-tags documents at scale so RAG and agent pipelines retrieve the right files; acquired by Collibra in July 2025 and now sold as "Unstructured by Collibra."

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, New York City (Verified — YC profile, press coverage)
- **Website / GitHub:** https://www.deasylabs.com · https://docs.deasylabs.com · https://github.com/Deasie-internal/deasy-labs (SDK repo)

## What they do

Deasy Labs builds a metadata layer for unstructured data destined for GenAI systems. The platform connects to document sources (SharePoint, S3, email stores), OCRs/parses/normalizes files (PDF, DOCX, Excel, PowerPoint, JSON, CSV, UTF-8 text), then uses LLMs to auto-discover or apply a **taxonomy** — a schema of tags with typed outputs (e.g., document type as `word`, effective dates as `list[date]`) — and stamps every file/chunk with that metadata. The claims: tagging "thousands of files per minute" at petabyte scale, sensitive-data (PII) detection and removal, relevance/quality filtering, and auto-refresh so tags stay current as sources change.

As an engineer you integrate via a Python SDK and REST API (post-acquisition the wheel is `unstructured_sdk`, distributed on request from Collibra): define connectors, define or auto-suggest taxonomies, run tagging jobs, then either write metadata back to source systems or push enriched chunks into a vector database for filtered hybrid retrieval. The pitch in engineer terms: RAG failure is usually a retrieval problem, and pre-filtering by structured metadata (department, doc type, date, sensitivity) before/alongside vector search beats brute-force embedding of everything. Deasy claims 10–15% average retrieval-accuracy improvement from metadata and 50–70% cost reduction from not retrieving irrelevant data (Reported — company blog/talks; treat as vendor benchmarks). Deployment is on-prem/your-cloud friendly with custom model endpoints, aimed at financial services and healthcare buyers. Note: no public pricing page — this is enterprise sales-led, especially post-Collibra.

## Founders & origins

**Verified:** Reece Griffiths (CEO), Leonard Platzer, and Mikko Peiponen, all ex-McKinsey/QuantumBlack, where they built McKinsey's ML-based data-quality product (deployed with 11 Fortune 500 companies per the YC profile). Griffiths holds a Cambridge engineering master's; Peiponen a quantitative-finance graduate degree from MIT; Platzer came via Amazon and a chatbot startup. Originally launched as "Deasie" (YC S23), later Deasy Labs.

## Funding

- **Seed, Sept/Oct 2023: ~$2.9M** (Verified amount range; some sources round to $3M) — General Catalyst, Y Combinator, RTP Global, plus enterprise-data angels.
- **Acquisition by Collibra, announced July 24, 2025** (Verified — Collibra press release, TechTarget, BigDATAwire). Terms not disclosed.
- Total raised: ~$2.9M before exit. No later venture rounds found in public sources.

## Evidence of real-world use

- Acquisition by Collibra — a major enterprise data-governance vendor — is itself the strongest validation signal; Collibra's stated rationale was extending governance to unstructured data using Deasy's auto-discovery/enrichment.
- Collibra's press materials describe the platform as "trusted in the financial services and healthcare sector" (Reported — acquirer's PR; no named customers found in public sources).
- Deasy-published case studies (bank customer-service chatbot; financial-institution regulatory-compliance RAG) are anonymized vendor content — directionally useful, not independently verified.
- Community footprint: Qdrant hosted Griffiths on its Vector Space Talks (independent ecosystem signal); active technical blog; docs and SDK are live under Collibra branding. No meaningful OSS adoption metrics — the GitHub SDK repo is a client library, not a community project.

## Relevance to agentic AI engineering

This sits squarely in the retrieval/memory substrate of an agent stack: structured metadata is what lets an agent scope a search ("Q3 change orders, sensitivity: none") instead of hoping cosine similarity finds it. Directly relevant to *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* — Deasy is essentially a commercial bet that the answer is yes. Also connects to *Agentic Search in the Wild* (agents issue filtered, iterative queries that metadata makes tractable) and, on the compliance side, to *Governance by Construction for Generalist Agents* — PII stripping and sensitivity tagging upstream is governance applied at the data layer rather than the agent layer.

## Use cases & considerations

**Use cases:** (1) Pre-processing a document dump (SharePoint/S3) into a filtered, tagged corpus before building RAG; (2) sensitivity/PII gating so agents never retrieve what they shouldn't; (3) taxonomy-driven document routing for back-office automation (for Ridgeline: auto-tagging job packets, sub bills, permits by job/date/type before an agent audits them); (4) metadata write-back to enrich existing DMS/search.

**Considerations:** Post-acquisition, the standalone product's future is uncertain — capabilities are being folded into the Collibra Platform, SDK access is request-only, and the buyer profile skews large-enterprise. PII detection is English-only. Vendor-reported accuracy/cost numbers lack independent benchmarks. Competitors: Unstructured.io (name collision alert — "Unstructured by Collibra" is Deasy, not Unstructured.io), Reducto (see this repo's profile), LlamaIndex parsing/extraction, Aparavi, and DIY LLM-tagging pipelines. Open question: whether Deasy exhibits at AIEWF 2026 as its own brand or as Collibra.

## Sources

- https://www.ycombinator.com/companies/deasy-labs
- https://www.deasylabs.com/
- https://www.deasylabs.com/about-us
- https://docs.deasylabs.com/quickstart
- https://www.collibra.com/company/newsroom/press-releases/collibra-acquires-deasy-labs
- https://www.prnewswire.com/news-releases/collibra-acquires-deasy-labs-to-extend-unified-governance-platform-to-unstructured-data-302512087.html
- https://www.techtarget.com/searchdatamanagement/news/366627998/Collibras-acquisition-of-Deasy-targets-unstructured-data
- https://www.hpcwire.com/bigdatawire/2025/07/25/what-collibra-gains-from-deasy-labs-in-the-race-to-govern-ai-data/
- https://qdrant.tech/blog/metadata-deasy-labs/
- https://www.deasylabs.com/blog/improving-rag-models-with-metadata
- https://github.com/Deasie-internal/deasy-labs
