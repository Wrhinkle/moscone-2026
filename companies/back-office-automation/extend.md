# Extend

> Developer-first API platform that turns messy documents (PDFs, scans, forms) into structured, validated data using vision-language models — the "document processing cloud" for production pipelines.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** silver
- **Founded:** 2023, New York, NY — Y Combinator Winter 2023 batch (Verified: YC directory + press)
- **Website / GitHub:** [extend.ai](https://www.extend.ai) · docs at [docs.extend.ai](https://docs.extend.ai) · no significant public OSS presence found

## What they do

Extend sells document processing as a set of APIs rather than a horizontal "intelligent document processing" suite. The core primitives are Parse (layout-first parsing of PDFs/scans into machine-readable structure, currently branded "Parse 2.0"), Extract (schema-driven field extraction with semantic chunking and bounding boxes), Split (breaking multi-document files apart with reading-order analysis), Classify, and Edit. On top of those sit document workflows — durable, versioned multi-step pipelines — plus a Studio/evals interface for schema iteration and regression testing, and confidence scoring so low-certainty extractions can be routed to human review before they hit production. (Verified: company site + docs.)

The pitch translated to engineer terms: instead of stitching together OCR + an LLM + your own eval harness + retry logic, you call their API with a schema and get structured JSON back, with per-field confidence and an eval loop for tuning. They expose multiple processing modes (low-latency, cost-optimized, max-accuracy) and offer fine-tuned dedicated models on private GPU infrastructure for large customers. A "Composer" agent automates schema refinement — an agentic layer that iterates on your extraction schema against eval sets. SDKs in Python and TypeScript plus a CLI; SOC 2 / HIPAA / GDPR posture and a self-hosted option for regulated industries. Pricing is credit-based per page per operation, with public pay-as-you-go, Scale, and Enterprise tiers — a real, self-serve commercial product, not demo-ware. (Verified: pricing page + docs.)

## Founders & origins

- **Kushal Byatnal (CEO)** — early engineer at Brex, then co-founder of Stir, a creator-economy fintech that reportedly processed hundreds of millions in payment volume. (Verified: YC profile + press.)
- **Eli Badgio (CTO)** — built data infrastructure at Flatiron Health, specializing in data quality/validation pipelines for regulated industries. (Reported: company about page and press coverage.)

Both founders' prior employers (Brex, Flatiron Health) are now flagship customers — a credible origin story: they built the document infrastructure they'd previously needed. Team size ~25 as of the YC listing (Reported).

## Funding

- **$17M total across seed + Series A**, announced June 17, 2025; Series A led by **Innovation Endeavors**, with Y Combinator, Homebrew, and Character participating, plus angels Scott Belsky (ex-Adobe CSO) and Guillermo Rauch (Vercel CEO). (Verified: BusinessWire release, SiliconANGLE, company blog.)
- No Series B found in public sources as of 2026-07-02.
- CEO claims multi-millions in ARR and cash-flow positivity at the time of the raise. (Reported: company/press statements, not independently verifiable.)

## Evidence of real-world use

Stronger than the usual logo wall. Named customers: Brex, Square, Checkr, Chime, Mercury, Flatiron Health, Opendoor, Upstart, Valon, Amgen, CH Robinson, HomeLight. A published Brex case study describes standardizing document processing company-wide on Extend, shipping Bill Pay and receipt parsing on it, with fine-tuned models deployed on private GPUs to meet latency SLAs — documented usage, not just a logo. (Verified: Extend case study; customer list Reported via company materials and press.) The company claims millions of pages processed daily (Reported). Public pricing, public docs, and SDKs indicate genuine self-serve adoption beyond enterprise deals.

## Relevance to agentic AI engineering

Extend sits at the **tool layer** of an agent stack: agents operating on real-world business processes (finance ops, underwriting, background checks, healthcare) constantly hit unstructured documents, and a high-accuracy extraction API with confidence scores is exactly the kind of verifiable tool the tool-use/governance research in this repo argues agents need — bounded, auditable calls with machine-checkable outputs rather than free-form LLM reads of PDFs. Their Composer agent (automated schema refinement against evals) is a working example of the eval-in-the-loop agentic optimization pattern discussed in the agentic SWE benchmark literature. Structured extraction also feeds agent memory: turning document streams into typed records is a practical substrate for the long-horizon memory systems covered in the repo's agent-memory papers. Less relevant to the voice-agent line of work. Note: despite the consumer-ai category assignment for this repo, Extend is squarely a B2B developer-infrastructure company.

## Use cases & considerations

Use cases for a builder/operator:
1. Back-office agent pipelines — invoices, receipts, insurance docs, submittals — where an agent needs structured fields plus confidence scores to decide auto-process vs. human review.
2. Replacing brittle homegrown OCR+regex+GPT stacks with a single API and eval harness.
3. Splitting/classifying large mixed scan bundles (loan files, medical records) before downstream automation.
4. RAG/agent-memory ingestion where layout-aware parsing quality dominates retrieval quality.

Considerations: proprietary hosted service (self-host exists but enterprise-gated) — schema and eval investment creates soft lock-in. Credit-based pricing can get opaque at volume; model per-page costs before committing. Crowded space: competitors include Reducto, LlamaIndex (LlamaParse/LlamaCloud), Tensorlake, Unstructured, AWS Textract, Google Document AI, and incumbent IDP vendors (ABBYY, Hyperscience). Open questions: durability of accuracy edge as frontier VLMs commoditize parsing, and whether the workflow/eval layer is enough moat.

## Sources

- https://www.extend.ai/
- https://www.extend.ai/about
- https://www.extend.ai/pricing
- https://www.extend.ai/resources/series-a
- https://www.extend.ai/resources/how-brex-reached-99-accuracy-across-millions-of-financial-documents
- https://www.ycombinator.com/companies/extend
- https://www.businesswire.com/news/home/20250617790342/en/Extend-Raises-$17-Million-to-Build-the-Document-Processing-Cloud
- https://siliconangle.com/2025/06/17/extend-gets-17m-funding-boost-speed-accuracy-document-processing-llms/
- https://docs.extend.ai/product/general/how-credits-work
- https://www.builtinnyc.com/articles/extend-raises-17m-seed-series-a-20250618
