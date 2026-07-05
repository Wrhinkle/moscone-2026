# Encord

> A data annotation, curation, and model-evaluation platform for multimodal AI — now repositioning as "the data layer for physical AI" (robotics, AVs, drones).

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** bronze
- **Founded:** 2020, London (Verified; legal entity Cord Technologies Inc., launched via Y Combinator in 2021; also operates from San Francisco)
- **Website / GitHub:** https://encord.com — https://github.com/encord-team (OSS: `encord-team/encord-active`)

## What they do

Encord sells a platform for turning raw unstructured data into training- and evaluation-ready datasets. Three named products cover the lifecycle:

- **Annotate** — labeling for images, video, audio, text, documents, and DICOM (medical imaging), with configurable human-in-the-loop review workflows, AI-assisted pre-labeling, and consensus/QA stages. You integrate via a Python SDK and API to push data in, script workflow stages, and build custom pre-labeling agents.
- **Index** — data management and curation at petabyte scale: embedding-based search, dedup, metadata filtering, and dataset slicing across multimodal data. The company states the platform manages 5+ PB of customer data (Reported, company Series C announcement).
- **Active** — model evaluation and error discovery: surface failure modes, prioritize the highest-value data for labeling, and close the active-learning loop. An earlier open-source version exists (`encord-active`, ~457 GitHub stars — modest adoption; the commercial hosted product is clearly the main artifact).

They also ship **Data Agents** — SDK-driven automations for repetitive pipeline steps (routing, pre-labeling, validation). In practice you'd buy Encord instead of stitching together CVAT/Label Studio + a vector store + custom eval scripts, particularly if you have regulated or physical-world data (medical imaging, driving footage, warehouse video). Since 2025–26 the marketing centers on "physical AI" data infrastructure — sensor, video, and robotics data — positioning against Scale AI's data-engine business.

## Founders & origins

- **Eric Landau** (CEO) and **Ulrik Stig Hansen** (President) — Verified across Crunchbase, YC, Tracxn, and company site. Hansen holds an M.S. in Computer Science from Imperial College London (Reported). Landau's background is in quantitative research/physics (Reported; single-source interviews). Some databases also list **Leeho Lim** as a co-founder (Reported, Tracxn).
- Origin story: founded 2020 as Cord Technologies, went through Y Combinator (2021), initially focused on computer-vision annotation with "micro-models" for automated labeling, then broadened to full multimodal data infrastructure.

## Funding

- Seed: $4.5M, 2021 (Verified — Hansen's own Medium post plus databases; CRV and YC among first investors).
- Series A: Oct 2021, with Harpoon Ventures and CRV (Verified that the round happened; amount not found in the sources I used — commonly reported as ~$12.5M, Unverified here).
- Series B: $30M, Aug 2024, led by Next47, with CRV, Crane Venture Partners, Y Combinator (Verified — company blog + press).
- Series C: $60M (~€50M), Feb 2026, led by Wellington Management, with YC, CRV, Next47, Crane, Harpoon, plus new investors Bright Pixel Capital and Isomer Capital (Verified — company blog, SiliconANGLE, TNW).
- Total raised: ~$110M (Verified, multiple sources).

## Evidence of real-world use

Strong. Beyond logos, there are named, detailed case studies on encord.com: **UiPath** (10x dataset growth for table-extraction models), **Voxel**, **Standard AI** (retail vision), **CONXAI** (construction AI — claimed 60% faster labeling), **Plainsight** (claimed 90% less data-management overhead), **Neurons**. The Series C press cites 300+ AI teams including **Woven by Toyota, Zipline, Skydio, and AXA** (Reported, company-sourced but echoed by press), plus revenue from physical-AI customers up ~10x year-over-year (Reported). Public pricing/product docs and an active docs site confirm a real self-serve-able commercial product. Caveat: usage metrics originate mostly from Encord itself; the case studies are vendor-published.

## Relevance to agentic AI engineering

Encord sits in the **data/eval layer** of the stack rather than the agent runtime: it's where training data, human review loops, and model-failure analysis live. Its HITL review workflows and evaluation tooling connect to the repo's eval-rigor thread — *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering* — since the same review-queue discipline applies when grading agent trajectories, not just labels. Index's metadata/curation layer is relevant to *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*: curated, metadata-rich datasets are what make agentic retrieval over enterprise data work. Their "Data Agents" are themselves an example of SDK-scripted pipeline agents (tool-use orchestration in the *Evolution of Tool Use in LLM Agents* sense, applied to data ops). For vision-heavy agents (computer-use, robotics, jobsite video), Encord is a plausible source of evaluation and fine-tuning data.

## Use cases & considerations

Use cases: (1) labeling and QA for a vision model over jobsite/warehouse video or drone imagery; (2) curating a multimodal corpus (docs + photos) before fine-tuning; (3) RLHF/eval review queues with human sign-off; (4) medical-imaging (DICOM) annotation under compliance constraints.

Considerations: enterprise-priced SaaS with sales-led motion (pricing not fully public); data-gravity lock-in once petabytes and workflows live there; the OSS footprint is small, so no real self-host escape hatch. Competitors: **Scale AI, Labelbox, V7, SuperAnnotate, Roboflow**, and OSS **CVAT/Label Studio**. Open question: how much of the "physical AI" repositioning is substance vs. rebrand of the annotation core.

## Sources

- https://encord.com/ and https://encord.com/customers/
- https://encord.com/blog/encord-announces-60-million-series-c/
- https://encord.com/blog/encord-announces-30-million-series-b/
- https://www.ycombinator.com/companies/encord
- https://www.crunchbase.com/organization/cord-0d3f
- https://tracxn.com/d/companies/encord/__z_gFxzFOXuLt1zVy5O1W9GwV1-0_1zgECDZnIxu_ETE
- https://medium.com/cord-tech/how-we-raised-a-4-5m-seed-round-and-why-we-went-with-mostly-american-investors-99bc75495726
- https://siliconangle.com/2026/02/26/physical-ai-data-infrastructure-startup-encord-lands-60m-accelerate-intelligent-robot-drone-development/
- https://thenextweb.com/news/encord-raises-e50m-to-build-the-data-layer-for-physical-ai
- https://github.com/encord-team/encord-active
- https://encord.com/customers/conxai-case-study/ (and UiPath, Voxel, Standard AI, Plainsight, Neurons case-study pages)
- https://www.uktech.news/news/founder-interviews/encord-founder-ulrik-stig-hansen-20220408

*Profile written 2026-07-02.*
