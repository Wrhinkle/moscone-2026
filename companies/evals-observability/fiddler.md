# Fiddler

> Enterprise AI observability and guardrails platform — born in ML explainability/monitoring, now positioning as an "AI control plane" for agentic systems, sold hard into regulated industries (banks, insurers, healthcare, defense).

- **Category:** evals-observability
- **AIEWF 2026 tier:** silver
- **Founded:** October 2018, Palo Alto, CA (Verified — press releases and multiple profiles agree)
- **Website / GitHub:** https://www.fiddler.ai — https://github.com/fiddler-labs — https://docs.fiddler.ai

## What they do

Fiddler is a monitoring/evaluation/guardrails platform that spans three model generations: classic predictive ML (drift, performance, explainability — their original 2018 product), LLM applications, and now multi-agent systems. The agentic product ingests traces via OpenTelemetry (framework-agnostic) or native integrations for LangGraph, Amazon Bedrock, AWS Strands Agents, and Google ADK, then organizes them into a hierarchy — application → session → agent → trace → span — so you can debug agent reasoning chains, tool calls, and cross-agent dependencies, with evaluators run over both dev experiments and sampled production traffic. (Verified — product pages + docs.)

The technically distinctive piece is the **Fiddler Trust Service** with in-house fine-tuned small models (branded "Trust Models," recently "Centor Models") for Faithfulness (hallucination vs. supplied context), Safety (11 dimensions including jailbreak detection), and PII detection/redaction. These power **Fiddler Guardrails**, invoked as a low-latency HTTP API (they claim <100ms enforcement), and critically they execute inside your environment — no per-call external LLM-judge API fees, and deployable in VPC/air-gapped setups. That deployment posture is a real differentiator for their regulated-industry customer base. (Verified for architecture/claims via docs and case studies; latency figures are vendor-reported.)

What you'd actually integrate: an OTel exporter or the Fiddler LangGraph SDK for tracing, the Guardrails REST API in your request path, and the platform UI/alerting for monitoring. Explainability tooling for tabular ML models (Shapley-style attributions) remains part of the platform — unusual among LLM-era observability vendors.

## Founders & origins

- **Krishna Gade (CEO)** — engineering leadership at Facebook (led the team behind the "Why am I seeing this?" news-feed explainability feature), plus Pinterest, Twitter, and Microsoft (Bing). (Verified)
- **Amit Paka (co-founder, COO/CPO)** — previously founded shopping app Parable; product background including Samsung/PayPal ecosystem. (Verified as co-founder; prior-company details Reported)
- Nilesh Dalvi is listed as CTO in exec profiles (Reported; not consistently described as a founder).

Origin story: Gade's Facebook explainability work convinced him enterprises would need "explainable AI as a service" — Fiddler launched in 2018 squarely as an XAI company and rode the category shift from explainability → ML monitoring → LLM observability → agent control plane. (Verified across interviews and Amazon Science Q&A.)

## Funding

- **Seed:** $3M, Oct 2018 — Lightspeed, Bloomberg Beta, Haystack. (Verified)
- **Series A:** $10.2M, Sept 2019 — led by Lightspeed and Lux Capital. (Verified — PRNewswire)
- **Strategic:** Lockheed Martin Ventures investment, Aug 2020; Amazon Alexa Fund also an early backer. (Verified/Reported)
- **Series B:** $32M, June 2021 — led by Insight Partners. (Verified)
- **Series B prime (extension):** $18.6M, late 2024/Jan 2025 — Cisco Investments, Capgemini (ISAI Cap), Samsung Next, Dallas VC, others; total Series B $50M+. (Verified)
- **Series C:** $30M, announced Jan 27, 2026 — led by RPS Ventures; LG Technology Ventures, Mozilla Ventures, Benhamou Global Ventures joining existing investors. **Total raised: ~$100M** (company figure). Company reported >4x revenue growth over the prior 18 months (vendor-reported, Unverified independently). (Verified round via BusinessWire + company PR)

## Evidence of real-world use

Stronger than logos: **Nielsen** has a detailed case study (multi-agent copilot; 99% jailbreak-block precision claimed vs. Bedrock Guardrails, sub-100ms guardrails); **U.S. Navy (PMS 408)** case study claims 97% reduction in model-update time; **Integral Ad Science** has an attributed SVP quote about production observability. Customer wall includes Mastercard, AIG, American Family Insurance, DTCC, Ally, Elevance, Thumbtack, UWM, LendingPoint — heavily financial services/insurance/healthcare. (Case-study details are vendor-published — Reported.) Ecosystem: native Amazon SageMaker AI integration, Google Cloud partner blog, NVIDIA NIM/NeMo ties, AWS Marketplace listing. Gartner Market Guide (AI evaluation/observability) inclusion and CB Insights AI 100. OSS footprint is small: **fiddler-auditor** (LLM red-teaming/robustness library) has only ~190 GitHub stars — this is a top-down enterprise sale, not a bottoms-up dev tool. No public self-serve pricing found (sales-led; a "Lite" AWS Marketplace SKU exists).

## Relevance to agentic AI engineering

Fiddler is betting the observability category converges on agent governance — guardrails + hierarchical trace monitoring as a "control plane," which is essentially the productionization of the repo's tool-use/governance thread (*Governance by Construction for Generalist Agents*; *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*). Their session→agent→span hierarchy is the operational counterpart to long-horizon eval work like *SlopCodeBench* and *SWE-EVO*, and their in-environment judge models address the same reproducibility concerns as *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*. Faithfulness guardrails over retrieved context intersect the memory/RAG evaluation questions in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*.

## Use cases & considerations

1. Put Guardrails (safety/faithfulness/PII) in the request path of a customer-facing agent without paying per-call judge-LLM fees or exfiltrating data.
2. Trace a LangGraph/Bedrock multi-agent app end-to-end and drill from session-level KPIs to individual tool-call spans.
3. Satisfy model-risk-management/compliance requirements (SR 11-7-style) with one platform covering both legacy ML models and new LLM apps.

Considerations: enterprise-first — no meaningful free/self-hosted tier, so poor fit for small teams versus Phoenix/Langfuse; guardrail quality claims are vendor benchmarks; the "control plane" framing is crowded (Arize, Galileo, LangSmith, Braintrust, Datadog LLM Observability, Dynatrace, plus hyperscaler-native guardrails). Lock-in is moderate: OTel ingestion is portable, but Trust Models and dashboards are proprietary. Open question: whether a ~$100M-raised independent can hold the governance layer as AWS/Google bundle guardrails into their agent runtimes.

## Sources

- https://www.fiddler.ai/agentic-observability
- https://www.fiddler.ai/customers
- https://www.fiddler.ai/guardrails
- https://docs.fiddler.ai/observability/llm/guardrails
- https://www.fiddler.ai/press-releases/fiddler-raises-30m-series-c
- https://www.businesswire.com/news/home/20260127042634/en/Fiddler-Raises-$30M-Series-C-to-Power-the-Control-Plane-for-AI-Agents
- https://www.fiddler.ai/blog/series-b-prime
- https://www.prnewswire.com/news-releases/fiddler-raises-32-million-in-series-b-funding-as-it-leads-the-market-of-machine-learning-explainability-and-performance-management-301314395.html
- https://www.prnewswire.com/news-releases/fiddler-labs-raises-10-2m-in-series-a-funding-to-make-ai-explainable-in-every-enterprise-300924967.html
- https://www.prnewswire.com/news-releases/fiddler-and-lockheed-martin-ventures-collaborate-to-accelerate-ai-explainability-and-monitoring-301111322.html
- https://www.amazon.science/latest-news/machine-learning-fairness-alexa-fund-fiddler-ai-ceo-krishna-gade-interview
- https://www.fiddler.ai/blog/fiddler-delivers-native-enterprise-grade-ai-observability-to-amazon-sagemaker-ai-customers
- https://cloud.google.com/blog/topics/partners/built-with-google-ai-achieve-better-observability-for-ml-models-with-fiddler-ai
- https://github.com/fiddler-labs/fiddler-auditor
- https://aws.amazon.com/marketplace/pp/prodview-imsoert6oehmm
