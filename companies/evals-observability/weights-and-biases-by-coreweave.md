# Weights & Biases by CoreWeave

> The de facto standard for ML experiment tracking, now a CoreWeave-owned "AI developer platform" whose Weave product competes in LLM/agent observability and evals.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2017, San Francisco (Verified — company site, Crunchbase, press). Acquired by CoreWeave, deal closed May 5, 2025 (Verified).
- **Website / GitHub:** https://wandb.ai · https://github.com/wandb/wandb

## What they do

Two product families under one platform. **W&B Models** is the classic MLOps suite: experiment tracking (log metrics/hyperparameters from any training run via a `wandb.init()` call in Python), Sweeps (hyperparameter search), Artifacts (dataset/model versioning with lineage), Registry, and Launch (job packaging to compute). This is the tool most training teams already have wired into PyTorch/HF Trainer callbacks; it's why "check the wandb dashboard" is generic vocabulary in ML labs.

**W&B Weave** is the newer LLM/agent layer and the reason they belong in this category: SDK-based tracing of LLM calls and tool calls, an evaluation framework (datasets + scorers, including LLM-as-judge), online monitors over production traffic, Guardrails (pre-built scorers for toxicity, PII, hallucination, coherence), and playgrounds for prompt/model comparison. In 2025–26 Weave was explicitly repositioned around production agents: end-to-end trace observability, failure-mode surfacing, and a loop from production traces back into evals and training. They ship an official MCP server (wandb/wandb-mcp-server) so coding agents like Claude Code can query runs and traces, run evals, and iterate autonomously.

Post-acquisition, the platform is fusing with CoreWeave's GPU cloud: **W&B Inference** (hosted open-weight models behind an OpenAI-compatible API), Serverless RL for post-training agents, CoreWeave Sandboxes, and — announced June 30, 2026, GA alongside Weave's agent capabilities — **CoreWeave ARIA**, a research agent built into W&B that analyzes thousands of runs and metrics to propose next experiments. Public pricing (Verified, third-party pricing summaries 2026): Free tier (5 seats, 1 GB/mo Weave ingestion), Pro from ~$60/mo, custom Enterprise (single-tenant, HIPAA, SSO). Self-managed/dedicated deployments exist for enterprises.

## Founders & origins

**Lukas Biewald** (CEO), **Chris Van Pelt** (CISO), **Shawn Lewis** (CTO) — Verified. Biewald and Van Pelt previously co-founded CrowdFlower/Figure Eight (data labeling; acquired by Appen). The origin story (Verified via press/Insight Partners interview): Biewald embedded with OpenAI circa 2017, saw researchers tracking experiments in spreadsheets, and built tooling for that gap.

## Funding

- **Series A, May 2018:** $5M co-led by Trinity Ventures and Bloomberg Beta (Verified).
- **Series B, 2019–2021:** $15M led by Coatue (Reported); Insight Partners led a $45M round in Jan/Feb 2021 (Verified).
- **Series C, Oct 2021:** $135M led by Felicis, ~$1B valuation (Verified — PR Newswire, TechCrunch).
- **Strategic round, Aug 2023:** $50M from Nat Friedman and Daniel Gross at $1.25B valuation (Verified — TechCrunch).
- **Total raised:** ~$250M pre-acquisition (Verified — Tracxn, TechCrunch).
- **Exit:** acquired by CoreWeave; announced March 2025, closed May 5, 2025. Price widely reported at ~$1.4B in stock (~21.9M CoreWeave Class A shares); one outlet says $1.7B — treat the exact figure as Reported, the acquisition itself as Verified.

## Evidence of real-world use

Among the strongest in this category. **OpenAI trained GPT-4 using W&B** (Verified — W&B customer page, TechCrunch). Other named customers with case studies: Meta, NVIDIA, Toyota/Woven (AV research on DGX), Snowflake, AstraZeneca, Canva, Square, Wayve. ~700K users reported at the 2023 round (Reported — Synthedia). OSS client wandb/wandb: 11.2k stars, 883 forks, MIT license, 187 releases (Verified, GitHub 2026-07-02) — and it's a default integration in Hugging Face, Lightning, and most training frameworks, which understates raw star counts. Official NVIDIA partnerships (TAO Toolkit, NIM data-flywheel blueprint) are documented on NVIDIA's own properties. Caveat: the usage moat is strongest in Models/training; Weave's agent-observability adoption is newer and less independently documented.

## Relevance to agentic AI engineering

Weave covers the eval-and-trace layer this repo's agentic-SWE benchmark papers (*SWE-EVO*, *ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*) argue must be trace-level and reproducible; its tool-call tracing and Guardrails map to *The Evolution of Tool Use in LLM Agents* and the audit posture of *Governance by Construction for Generalist Agents*. The differentiator vs. Braintrust/LangSmith is the closed loop into training: production traces → evals → Serverless RL post-training on CoreWeave GPUs. ARIA and the MCP server make W&B itself an agent surface — relevant to any Claude Code-driven improvement loop. Voice-agent evals (*From Text to Voice…*) would live in the same scorer framework.

## Use cases & considerations

Use cases: (1) tracing + eval gating for a production tool-calling agent (e.g., a job-packet auditor's structured outputs scored against golden sets); (2) fine-tuning/post-training runs with full experiment lineage; (3) Guardrails scorers (PII, hallucination) on customer-facing agent output; (4) letting a coding agent query eval history via the MCP server.

Considerations: post-acquisition gravity pulls toward CoreWeave compute — the company says the platform stays infra-neutral, but watch where new features (Inference, Serverless RL, ARIA) land first. Weave is younger than the Models suite; competitors in LLM observability are LangSmith, Braintrust, Arize, Langfuse, Datadog LLM Observability. Weave ingestion pricing (per-GB) can climb on chatty agent traces. Open question: whether a training-era incumbent wins agent-era evals, or splits attention across too many surfaces.

## Sources

- https://wandb.ai/site/ · https://docs.wandb.ai/weave · https://wandb.ai/site/weave/ · https://wandb.ai/site/customers/
- https://github.com/wandb/wandb · https://github.com/wandb/wandb-mcp-server
- https://www.coreweave.com/blog/coreweave-completes-acquisition-of-weights-biases
- https://www.prnewswire.com/news-releases/coreweave-completes-acquisition-of-weights--biases-302445966.html
- https://techcrunch.com/2025/03/04/coreweave-acquires-ai-developer-platform-weights-biases/
- https://techcrunch.com/2023/08/09/weights-biases-who-counts-openai-as-a-customer-lands-50m/
- https://techcrunch.com/2021/10/13/weights-biases-raises-new-capital-as-developer-tools-remain-a-venture-focus-ml-matures/
- https://www.prnewswire.com/news-releases/weights--biases-raises-its-series-c-at-a-billion-dollar-valuation-301399022.html
- https://tracxn.com/d/companies/weights-biases/__uVC3y5h56PSBeov63SBmKNjSxWpMaR4hyT-qaotxi5Q
- https://www.insightpartners.com/ideas/weights-and-biases-ceo-lukas-biewald-on-building-an-ai-developer-powerhouse/
- https://www.coreweave.com/news/coreweave-aria-launches-as-an-ai-research-and-iteration-agent-with-autonomous-research-and-collaborative-intelligence
- https://siliconangle.com/2026/06/29/coreweave-debuts-aria-agent-automate-ai-research-weights-biases/
- https://wandb.ai/wandb_fc/product-announcements-fc/reports/New-in-W-B-Weave-Observability-and-continuous-improvement-for-production-agents--VmlldzoxNzAzMTcxNg
- https://developer.nvidia.com/blog/accelerating-ai-development-with-nvidia-tao-toolkit-and-weights-biases/
- https://synthedia.substack.com/p/weights-and-biases-lands-50m-investment
