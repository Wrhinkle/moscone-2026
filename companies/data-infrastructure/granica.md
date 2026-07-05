# Granica

> An "AI data efficiency" platform that compresses, deduplicates, screens for PII, and selects the most valuable samples out of the massive data lakes companies use to train and run AI/ML.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** silver
- **Founded:** launched from stealth June 2023 (Reported — press coverage; founding year not independently dated)
- **Website / GitHub:** https://www.granica.ai

## What they do
Granica is a cloud-native layer that sits on top of data lakes (S3, GCS, Snowflake, Databricks) and attacks the cost/risk of AI training data from three angles via separate products: **Granica Crunch** (lossy/lossless compression and dedup, claiming up to 80% storage/compute cost reduction and up to 60% smaller Parquet files with faster query/load times per TPC-DS benchmarks), **Granica Screen** (scans data lakes for PII/sensitive data before it reaches an LLM), and **Granica Signal** (selects the most informative training samples, reportedly matching full-dataset accuracy with ~30% of the data). It's infrastructure you'd plug in ahead of a training or fine-tuning pipeline rather than a model itself.

## Founders & origins / Funding
Co-founded by CEO Rahul Ponnala and CTO Tarang Vaish, both former engineers at Pure Storage and Cohesity (Verified — multiple press sources). Raised a $45M Series A (June 2023) led by NEA and Bain Capital Ventures, with angel participation from ex-Tesla CFO Deepak Ahuja, Eventbrite's Kevin Hartz, and Okta's Frederic Kerrest (Verified).

## Evidence of real-world use
No named enterprise customers or case studies found in public sources beyond the company's own benchmark claims — treat compression/accuracy figures as vendor-reported, not independently verified.

## Relevance to agentic AI engineering
Fits the data-pipeline layer feeding fine-tuning/RAG systems: reducing storage cost and screening for PII before data enters an agent's context or training set is a real operational concern for teams scaling agentic systems.

## Sources
- https://www.granica.ai/
- https://siliconangle.com/2023/06/08/granica-launches-stealth-ai-efficiency-platform-45m-funding/
- https://pulse2.com/granica-ai-45-million-in-funding/
- https://www.nea.com/blog/granica-catalyzing-ai-efficiency-in-the-concurrent-eras-of-ai-and-efficient-growth
- https://www.granica.ai/blog/improving-ai-via-optimal-selection-of-training-samples
