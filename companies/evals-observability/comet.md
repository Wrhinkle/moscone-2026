# Comet

> MLOps veteran (experiment tracking since 2017) that pivoted its center of gravity to Opik, an Apache-2.0 open-source LLM/agent observability, evaluation, and prompt-optimization platform.

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** 2017, New York City, with a Tel Aviv office; emerged from the Techstars-powered Amazon Alexa Accelerator (Verified — company about page, TechCrunch; company sometimes says "launched 2018," which matches the April 2018 seed/launch press)
- **Website / GitHub:** https://www.comet.com · https://github.com/comet-ml/opik

**Disambiguation:** not Perplexity's "Comet" browser and not the French freelance marketplace Comet. This is Comet (formerly Comet.ml), the ML/LLM developer platform — the AIEWF sponsor, listed under evals/observability.

## What they do

Comet has two product generations. The original **Comet platform** (experiment management, model registry, artifacts, production model monitoring) is classic MLOps: log training runs, hyperparameters, and metrics from Python code, compare experiments, and manage the train→deploy lifecycle. This is the business that got them to 150+ enterprise customers by 2021 and remains relevant to teams that fine-tune or train models.

The strategic bet since September 2024 is **Opik**, an open-source (Apache-2.0) platform for LLM applications and agents. Concretely: distributed tracing of every LLM call, tool call, and agent step (the team reports 40M+ traces/day across the user base); automated evaluation with datasets, experiments, and LLM-as-judge metrics (hallucination, moderation, RAG groundedness); production dashboards; prompt management; and guardrails. Integrations cover 60+ frameworks — OpenAI, Anthropic, LangChain, LlamaIndex, CrewAI, Google ADK, AutoGen, LiteLLM — via Python/TypeScript SDKs and REST. You can run it self-hosted (Docker Compose or Kubernetes/Helm) or use Comet's cloud; paid cloud tiers start at $19/month with a real free tier (public pricing page = real self-serve motion).

Two differentiators worth noting. The **Opik Agent Optimizer** is an SDK of six algorithms that automatically refine not just prompts but tool schemas and MCP tool definitions against your eval datasets — optimization of the agent's tool surface, not only its instructions. And in June 2026 Comet shipped **Cost Intelligence**, which it pitches as the first tool giving engineering leaders visibility into Claude Code and Codex spend — observability for the coding-agent bill, a genuinely new category (Reported — company press release via GlobeNewswire/Businesswire).

## Founders & origins

- **Gideon Mendels**, co-founder & CEO (Verified). NLP/speech researcher: Columbia University (M.Sc. CS; IARPA Babel low-resource speech recognition, language ID across 500+ languages) and Google (hate-speech/deception detection). Origin story: repeatedly inheriting ML projects with no record of prior experiments led to building experiment tracking (Verified — company bios, conference bios).
- **Nimrod Lahav**, co-founder & CTO (Verified). Software engineer previously at Wix and VMware (Reported — company about page).

## Funding

- **Seed, Apr 2018:** $2.3M led by Trilogy Equity Partners; Two Sigma Ventures, Founders Co-op, Fathom Capital, Techstars Ventures (Verified — FinSMEs, TechCrunch, SiliconANGLE).
- **Seed extension, Apr 2020:** $4.5M from Trilogy, Two Sigma, Founders Co-op (Reported).
- **Series A, Apr 2021:** $13M led by Scale Venture Partners (Verified — TechCrunch).
- **Series B, Nov 2021:** $50M led by OpenView, with Scale, Trilogy, Two Sigma; announced alongside 5x ARR growth and 150 business customers (Verified — Businesswire, TechCrunch).
- **Total raised:** ~$70M (Verified — matches company's own about page). No publicly announced round since 2021 — notable in a category where competitors (Braintrust, Arize) raised large 2025–26 rounds.

## Evidence of real-world use

Solid and multi-era. Named customers: **Uber, Netflix, Etsy, Zappos, Shopify, Ancestry, AssemblyAI, NatWest** (Verified for Uber/Zappos/Etsy via 2021 TechCrunch; the fuller list Reported via company about page, which also claims 150,000+ developers). OSS traction is the strongest current signal: **Opik has ~20.3k GitHub stars, 1.6k forks, 6,200+ commits, 510+ releases** and active issue/PR flow (Verified — GitHub, 2026-07-02). Third-party docs integrate it (LiteLLM ships an Opik logging integration), and 2026 vendor-comparison content (Future AGI, Goodeye Labs) treats Opik as a default baseline — competitor attention is a usage signal.

## Relevance to agentic AI engineering

Opik is the observability/eval layer under an agent stack: trace capture and scoring for the long-horizon, multi-step behavior that this repo's agentic-SWE benchmark papers (*SWE-EVO*, *ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*) argue must be evaluated at the trajectory level, not per-response. The Agent Optimizer's tuning of tool schemas and MCP definitions connects directly to *The Evolution of Tool Use in LLM Agents*; its guardrails and full audit trace map to the enforcement needs in *Governance by Construction for Generalist Agents*. Cost Intelligence for Claude Code/Codex is operational telemetry for exactly the coding-agent workflows those SWE benchmarks measure. Voice teams (see *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*) would use the same dataset-plus-judge loop; AssemblyAI as a named customer is adjacent evidence.

## Use cases & considerations

Use cases: (1) self-hosted tracing/evals for a back-office document agent where data can't leave your VPC — Opik's Apache-2.0 self-host is the cheapest credible option; (2) LLM-as-judge regression suites over golden datasets before shipping prompt changes; (3) automatic prompt/tool-schema optimization for an MCP-tool-heavy agent; (4) tracking Claude Code spend across an engineering org.

Considerations: open-source-first is the moat and the risk — low lock-in for you, unclear monetization pressure for them, and no fresh funding disclosed since 2021. The legacy MLOps business splits focus. Competitors: **Braintrust, LangSmith, Arize Phoenix/AX, Langfuse (closest OSS analog), W&B Weave, Datadog LLM Observability**. Open questions: enterprise conversion rate from OSS, and whether Agent Optimizer results hold up outside vendor benchmarks.

## Sources

- https://www.comet.com/site/about-us/ · https://www.comet.com/site/products/opik/ · https://www.comet.com/docs/opik/
- https://github.com/comet-ml/opik
- https://www.comet.com/site/about-us/news-and-events/press-releases/comet-launches-opik/
- https://www.businesswire.com/news/home/20211118005975/en/Comet-Raises-$50-Million-Series-B-to-Accelerate-ML-Development-for-the-Enterprise
- https://techcrunch.com/2021/11/18/mlops-startup-comet-nabs-50m-series-b-just-six-months-after-raising-its-a/
- https://techcrunch.com/2018/04/05/cometml-wants-to-do-for-machine-learning-what-github-did-for-code/
- https://www.finsmes.com/2018/04/comet-ml-raises-2-3m-in-seed-funding.html
- https://www.globenewswire.com/news-release/2026/06/09/3309065/0/en/comet-launches-cost-intelligence-in-opik-the-first-tool-to-give-engineering-leaders-complete-visibility-into-claude-code-and-codex-spend.html
- https://docs.litellm.ai/docs/observability/opik_integration
- https://trilogyequity.com/blog/comet-opik-open-source-lllm-evals/
- https://futureagi.com/blog/future-agi-vs-comet/
