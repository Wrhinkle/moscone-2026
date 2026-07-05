# DatologyAI

> Automated training-data curation as a service: you point it at your petabyte-scale pretraining corpus, it hands back a smaller, cleaner, better-ordered dataset so your model trains faster, cheaper, and ends up stronger.

- **Category:** models-inference
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, Redwood City, CA (Verified — TechCrunch, Tracxn)
- **Website / GitHub:** [datologyai.com](https://www.datologyai.com/) — no significant public GitHub presence found; research is published via arXiv and their blog

## What they do

DatologyAI sells data curation for foundation-model pretraining. The pitch translated to engineer terms: most web-scale corpora are full of redundant, low-quality, or task-irrelevant samples that burn GPU hours without improving the model. Datology's pipeline scores, filters, deduplicates, rebalances, and reorders data — and increasingly rewrites it as synthetic data — so a customer can train to the same quality with a fraction of the compute, or to higher quality with the same compute. Their headline claim is "train to the same performance ~10x faster at 1/10 the cost"; their published CLIP work claims up to 43x training speedups over raw baselines and inference-cost reductions of ~2.6–2.7x by letting smaller architectures match bigger ones (Reported — their own benchmarks, methodology published in technical deep-dives).

Deployment is notable for an enterprise buyer: BYOC (runs inside your own cloud) or on-prem, so proprietary pretraining data never leaves your control. Supported modalities are text/LLM and image-text; engagements come bundled with direct researcher support rather than being pure self-serve. There is no public pricing page — this is a high-touch enterprise product, not a PLG tool (Verified — product page).

Their most cited research artifact is **BeyondWeb** (arXiv 2508.10975, Aug 2025): a framework for rephrasing web documents into denser, more instructional synthetic pretraining data, reporting 7.7x faster training than open web data and 2.7x faster than Nemotron-Synth (Reported — their paper; independently covered by The Decoder).

## Founders & origins

- **Ari Morcos (CEO)** — Harvard neuroscience PhD; ~2 years at DeepMind, ~5 years at Meta AI (FAIR) working on understanding model mechanisms. Co-authored influential data-pruning research before founding the company (Verified — TechCrunch, company site).
- **Matthew Leavitt (Chief Science Officer)** — previously MosaicML and Meta AI (Verified — TechCrunch).
- **Bogdan Gaza (CTO)** — former engineering lead at Amazon and Twitter, ~decade of infra engineering (Verified — TechCrunch, SiliconANGLE).

The origin story is essentially "the data-pruning researchers went commercial": Morcos's academic line of work (e.g., *Beyond neural scaling laws*) argued curation beats brute-force scaling, and the company productizes that.

## Funding

- **Seed:** $11.65M, announced Feb 2024, led by Amplify Partners, with Radical Ventures (Verified — TechCrunch, SiliconANGLE).
- **Series A:** $46M, May 2024, led by Felicis (Viv Faga, Astasia Myers); participation from Radical Ventures, Amplify Partners, Elad Gil, M12 (Microsoft), and the Amazon Alexa Fund (Verified — company blog, SiliconANGLE, Crunchbase).
- **Total raised:** ~$57.65M across two rounds. No Series B found in public sources as of 2026-07-02.

## Evidence of real-world use

- **Arcee AI** (documented case study, not just a logo): Arcee's AFM-4.5B foundation model was pretrained on a Datology-curated ~8T-token dataset; Arcee claims it matched models trained on ~4x more data and benchmarks comparably to Qwen 3 14B and Llama 3.1 70B Instruct in blind Yupp rankings. Arcee's Lucas Atkins: working with Datology was "like expanding my research team with an extra 30 world-class researchers" (Reported — joint case study on Datology's blog).
- **Thomson Reuters** (April 2026 case study): Head of Research Jonathan Schwarz cites "clear, measurable improvements across both public and proprietary legal evaluations" on a small data budget (Reported — Datology site).
- Public technical deep-dives with reproducible-ish detail (billion-sample multimodal curation, state-of-the-art text dataset work) signal real production pipelines rather than vaporware, but the customer list that's public is short — consistent with a small number of large enterprise engagements.

## Relevance to agentic AI engineering

Datology sits upstream of the agent stack: it doesn't touch tool-calling, memory, or orchestration at runtime — it shapes the models agents run on. The relevant thread for this repo: agentic capability (the kind measured by the agentic SWE benchmark papers in our landscape) is increasingly attributed to pretraining/midtraining data mix, and BeyondWeb-style synthetic rephrasing is exactly the lever labs use to inject reasoning- and instruction-dense data. For a team fine-tuning or mid-training its own agent model (à la Arcee), Datology is the "data diet" vendor. It is *not* relevant to the tool-use/governance or agent-memory layers of the stack, and it's honest to say so.

## Use cases & considerations

**Use cases:** (1) an enterprise pretraining or mid-training a domain model (legal, finance) on proprietary corpora wanting more capability per GPU-dollar; (2) a small-model builder (Arcee-style) trying to punch above its parameter count; (3) multimodal teams cutting CLIP-style training and inference costs; (4) synthetic-data generation to stretch a limited proprietary corpus.

**Considerations:** results are mostly self-reported benchmarks plus two named customers — ask for evals on *your* distribution. No public pricing; sales-led. Only matters if you actually train models — irrelevant if you're purely an API consumer. Competitors/adjacent: Cleanlab, Lilac (acquired by Databricks), Scale AI's data engine, NVIDIA NeMo Curator (open source), and in-house lab curation teams. Open questions: post-2024 funding, revenue scale, and how defensible curation is as labs build this internally.

## Sources

- https://www.datologyai.com/ (product, customers, announcements)
- https://www.datologyai.com/product
- https://techcrunch.com/2024/02/22/datologyai-is-building-tech-to-automatically-curate-ai-training-data-sets/
- https://siliconangle.com/2024/02/22/datologyai-raises-11-65m-automate-data-curation-efficient-ai-training/
- https://www.datologyai.com/blog/datologyai-raises-46m-series-a
- https://siliconangle.com/2024/05/08/datologyai-raises-46m-streamline-ai-model-training-data-diets/
- https://www.crunchbase.com/organization/datologyai
- https://tracxn.com/d/companies/datologyai/__AZmsJFy_PSdCFTnTFMNtr7BnP35MNspgCv9RwXYachM
- https://www.datologyai.com/blog/arcee-case-study
- https://www.datologyai.com/blog/clip-gets-a-data-upgrade-outperforming-sota-with-improved-data-curation-only
- https://www.datologyai.com/blog/productionized-multimodal-data-curation-at-the-billion-sample-scale
- https://www.datologyai.com/blog/beyondweb / https://arxiv.org/abs/2508.10975
- https://the-decoder.com/reformulating-web-documents-into-synthetic-data-addresses-the-growing-limits-of-ai-training-data/
