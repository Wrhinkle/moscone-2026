# Resolve.ai

> An "AI SRE" — a multi-agent system that investigates production alerts and incidents across code, infra, and telemetry, and can remediate within guardrails.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2024, San Francisco (Verified for SF and the Oct 2024 stealth exit; founding year Reported as 2024 by US News/Tracxn, one database says 2023)
- **Website / GitHub:** https://resolve.ai · no significant public GitHub org found (Unverified)

## What they do

Resolve AI sells autonomous production operations — the pitch is "AI for prod." Concretely, it's a multi-agent system that connects to the tools a human on-call engineer would use (AWS, Kubernetes, GitHub, Slack, your observability stack — 60+ pre-built integrations across code, infra, observability, incident management, and CI/CD) and does the investigative work when something breaks. Three agent families: **on-call agents** that triage alerts, suppress noise, and route incidents; an **incidents agent** that runs parallel-hypothesis investigations correlating code changes, infrastructure state, and telemetry to find root cause; and **background agents** for scheduled work like deployment monitoring and resource optimization. Engineers steer investigations through a "Workbench" interface rather than fully ceding control.

It acts, not just diagnoses: within configurable guardrails it can silence alerts, revert commits, open PRs, and execute GitHub workflows, with tiered autonomous-vs-approval-required action policies and permission scoping (SOC 2 / GDPR / HIPAA alignment claimed). Under the hood the company says it pairs frontier models with domain-specialized models post-trained on production data, and the system learns from past incidents. It's also extensible outward — MCP, API, and a skills framework let your own agents call Resolve for production context and remediation. No public pricing page found (Unverified) — this is enterprise sales-led.

## Founders & origins

**Spiros Xanthos** (CEO) and **Mayank Agarwal** — met in grad school at UIUC (Verified across multiple sources). Xanthos co-created **OpenTelemetry**, founded Log Insight (acquired by VMware) and co-founded **Omnition** (acquired by Splunk, 2019), then was SVP/GM of Splunk's Observability business. Agarwal co-founded Omnition with him. The founding logic is direct: the people who built the telemetry-collection standard now building the layer that consumes it autonomously.

## Funding

- **Seed, Oct 2024:** $35M led by Greylock (its largest 2024 check, Reported — Reuters/US News), with Unusual Ventures (John Vrionis) and angels including Fei-Fei Li and Jeff Dean (Verified — multiple press sources)
- **Series A, announced Feb 2026 (reported Dec 2025):** $125M led by Lightspeed at a **$1B valuation**, with Greylock, Unusual, Artisanal, and A* participating (Verified — TechCrunch, PR Newswire, company blog)
- **Series A extension, Apr 2026:** $40M led by DST Global and Salesforce Ventures at a **$1.5B valuation**, alongside launching "Resolve AI Labs" (Reported — Forbes, Silicon Valley Investclub)
- **Total:** ~$200M in ~18 months since stealth exit (company says ">$190M")

## Evidence of real-world use

Stronger than usual for an 18-month-old company, though most numbers are vendor-published:

- **DoorDash (Ads team)** — dedicated case study on resolve.ai: deployed mid-2025, up to **87% reduction in time-to-root-cause**; investigations from ~40 minutes to ~1 minute (Reported — company case study, echoed by Forbes)
- **Coinbase** — incidents resolved ~72% faster with Resolve vs. engineers alone (Reported — Forbes/press)
- Named enterprise customers in the Series A release: **Coinbase, DoorDash, MongoDB, MSCI, Salesforce, Zscaler** (Verified as claims in PR Newswire release); Toast and Pinecone also reported. Salesforce Ventures investing after Salesforce became a customer is a meaningful signal.

Treat the percentage metrics as directional (vendor-sourced), but multiple blue-chip customers named in wire releases plus strategic investment from a customer is real usage evidence, not logo-washing.

## Relevance to agentic AI engineering

Resolve is the purest "agent as the product" company in this category: a long-horizon, tool-using investigation agent operating on production systems. Its multi-tool orchestration across 60+ integrations is a deployed instance of *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*; its tiered action guardrails and permission scoping are a commercial expression of *Governance by Construction for Generalist Agents*. The "learns from past incidents" claim connects to the repo's agent-memory thread (*Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*; *GAM: Hierarchical Graph-based Agentic Memory for LLM Agents*). And evaluating an agent that debugs live systems is exactly the gap the agentic-SWE benchmark papers (*ProdCodeBench*, *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*) describe — worth asking vendors like Resolve how they eval.

## Use cases & considerations

Use cases: (1) first-responder triage for on-call — noise suppression and pre-investigated alerts before a human looks; (2) root-cause analysis correlating a bad deploy to the offending PR, with an auto-drafted revert; (3) as an MCP-accessible "production context" tool your own agents can query; (4) background hygiene (deployment watching, resource right-sizing).

Considerations: enterprise-only posture — no public pricing, no self-serve, likely poor fit below serious production scale. Granting an agent revert/PR/workflow rights in prod is a high-trust decision; guardrail design is the whole ballgame. Crowded field: **Datadog Bits AI SRE**, **Cleric**, **Traversal**, **Beeble/Parity**-style AI-SRE startups, and incumbents adding agents to existing observability suites — Resolve's differentiation is founder pedigree (OpenTelemetry) and being observability-neutral. Open questions: how it prices, and how much of the claimed autonomy customers actually enable vs. approval-gated mode.

## Sources

- https://resolve.ai/ · https://resolve.ai/product/overview
- https://resolve.ai/news/resolveai-raises-125-million-series-a
- https://www.prnewswire.com/news-releases/resolve-ai-announces-125m-series-a-at-1b-valuation-to-fix-production-operations-with-ai-302678486.html
- https://techcrunch.com/2025/12/19/ex-splunk-execs-startup-resolve-ai-hits-1-billion-valuation-with-series-a/
- https://techcrunch.com/2026/02/04/ai-sre-resolve-ai-confirms-125m-raise-unicorn-valuation/
- https://www.usnews.com/news/technology/articles/2024-10-01/greylock-backed-resolve-ai-raises-35-million-in-seed-funding-to-help-engineers
- https://www.thesaasnews.com/news/resolve-ai-secures-35-million-in-seed-round
- https://www.forbes.com/sites/sofiachierchio/2026/04/16/this-15-billion-ai-startup-steps-in-when-software-breaks/
- https://resolve.ai/customers/doordash
- https://siliconvalleyinvestclub.com/resolve-ai/
- https://tracxn.com/d/companies/resolveai/__ydzR-6xMI72_g0Llp0zYRjfUujlT23rSQs9PrK_oX5Q
