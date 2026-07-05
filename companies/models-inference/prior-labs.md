# Prior Labs

> Makers of TabPFN, a pre-trained foundation model for tabular/structured data that replaces hand-tuned ML pipelines with in-context prediction.

- **Category:** models-inference
- **AIEWF 2026 tier:** silver
- **Founded:** late 2024, Germany (Verified — multiple funding-press sources)
- **Website / GitHub:** https://priorlabs.ai · https://github.com/PriorLabs/TabPFN

## What they do
TabPFN is a transformer trained via in-context learning to do classification/regression on tabular data (spreadsheets, database tables) without per-dataset tuning — you feed it a table and it predicts, the same way an LLM completes a prompt, instead of you fitting gradient-boosted trees or running AutoML. Prior Labs publishes it open source (PriorLabs/TabPFN on GitHub, ~7K stars, ~3M+ PyPI downloads) alongside a commercial/hosted version, and it now integrates with Databricks, AWS SageMaker, and Azure. The underlying research was published in *Nature* (Jan 2025) and has ~400 citations within its first year — unusually fast, credible validation for an applied ML product.

## Founders & origins
Founded by Frank Hutter (AutoML researcher), Noah Hollmann (ex-Google/BCG), and Sauraj Gambhir (Verified — Balderton, TechFundingNews).

## Funding
€9M pre-seed (Feb 2025) led by Balderton with XTX Ventures, the Hector Foundation, Atlantic Labs, and Galion.exe, plus angels including Hugging Face's Thomas Wolf and DeepMind's Ed Grefenstette (Verified). In May 2026, SAP announced a definitive agreement to acquire Prior Labs, committing over €1B over four years to build it into a frontier lab for structured data (Verified — TechCrunch, SAP newsroom).

## Evidence of real-world use
Named production deployments across finance (TD Bank, Creditplus Bank, Taktile), healthcare (BostonGene, Oxford Cancer Analytics, an NHS trust), and industrials (Hitachi Rail, reporting a 40% anomaly-detection improvement) — a stronger-than-average evidence bar for a company this young.

## Relevance to agentic AI engineering
Relevant where agents need to reason over structured/tabular data rather than text — e.g. an agent doing fraud triage, forecasting, or anomaly detection as a tool call into a TabPFN endpoint instead of a classical ML pipeline.

## Use cases & considerations
Use cases: fast baseline models on small/sparse tabular datasets, agent tool-calls for structured prediction tasks, replacing brittle AutoML pipelines. Considerations: now mid-acquisition by SAP, which will likely reshape independence and pricing/access; competitors include classical AutoML (H2O, DataRobot) and general foundation-model vendors extending into tabular.

## Sources
- https://priorlabs.ai/
- https://github.com/PriorLabs/tabpfn
- https://www.balderton.com/news/prior-labs-raises-e9m-to-revolutionise-how-businesses-interact-with-their-tabular-data/
- https://techfundingnews.com/tabpfn-to-bridge-ai-gap-in-structured-data-germanys-prior-labs-lands-e9m-from-hugging-face-silo-ai-and-sap-founders/
- https://techcrunch.com/2026/05/05/sap-bets-1-16b-on-18-month-old-german-ai-lab-and-says-yes-to-nemoclaw/
- https://news.sap.com/2026/05/sap-to-acquire-prior-labs-establish-frontier-ai-lab-europe/
- AI Engineer World's Fair 2026 sponsor list (silver tier), https://www.ai.engineer/worldsfair/2026
