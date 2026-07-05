# Cleric

> An AI site reliability engineer that autonomously investigates production alerts, posts evidence-backed root-cause findings in Slack, and turns every incident into reusable operational memory.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, San Francisco (Verified — founder LinkedIn/Crunchbase place Pienaar leaving Tecton to start Cleric in August 2023)
- **Website / GitHub:** https://cleric.ai — no significant public company GitHub org found (the founders' OSS footprint is Feast, under feast-dev)

## What they do

Cleric sells an agent that does the first-pass diagnostic work of an on-call engineer. When an alert fires (PagerDuty, Datadog, etc.), the agent begins investigating with read-only access to the customer's existing observability and infrastructure stack — logs, metrics, deploy history, Kubernetes state — exploring multiple hypotheses in parallel and correlating "what changed" across systems. It delivers findings in Slack with links to evidence and a confidence score; engineers can steer the reasoning conversationally or drill into diagnostics in a web UI. The company claims findings in ~5 minutes with 92% rated actionable, and that it processes thousands of issues daily across live deployments (vendor-reported).

Two architectural choices matter to an evaluator. First, the safety posture: read-only by default, enforced at the infrastructure level via cloud-provider and Kubernetes RBAC, deployed inside the customer's VPC so telemetry never leaves their boundary; write actions are opt-in. SOC 2 Type II, no training on customer data (Reported, company site). Second, the December 2025 "self-learning" release: each investigation and its human feedback is distilled into **operational memory** — institutional knowledge about that environment's services, dependencies (it auto-maps service ownership), and past fixes — so the agent's signal-to-noise improves per-tenant over time. Cleric has publicly described using LangSmith to compare investigation strategies and aggregate performance metrics across deployments, generalizing successful investigation patterns while anonymizing customer data (Verified — LangChain customer post plus Cleric's own engineering talks).

Integrations named publicly: Slack, Kubernetes, Datadog, Grafana, PagerDuty, AWS, Azure, Cloudflare. No public pricing page — enterprise sales motion (Verified as of 2026-07-02).

## Founders & origins

- **Shahram Anver, CEO** — led engineering for MLOps/DevOps/FinOps platforms at Gojek, the Southeast Asian super-app (Verified).
- **Willem Pienaar, CTO** — creator of Feast, the open-source ML feature store (built at Gojek, later maintained via Tecton, where he worked Nov 2020–Mar 2023); has worked with ML infra teams at Google, Apple, Twitter, Cloudflare (Verified).
- Crunchbase also lists **Dan Siwiec** as a founder (Reported — single source; not featured in company materials).

Origin story: Anver and Pienaar saw platform teams drown in production triage at Gojek scale and set out to automate the investigation layer rather than the dashboard layer.

## Funding

- **Seed, $4.3M** — led by Zetta Venture Partners, announced March 2024, with angels from Google Cloud, Sysdig, Tecton, Neo4j leadership (Verified — PRNewswire, pulse2, TFN).
- **Seed extension, $5.5M** — led by Vertex Ventures US, announced December 2025 alongside the self-learning launch (Verified — Businesswire, Vertex's own post).
- **Total raised: $9.8M** (Verified — stated by both Vertex and press).

## Evidence of real-world use

- **BlaBlaCar** (carpooling marketplace, millions of members, 21 countries) has run Cleric in production since early 2025 — a named, documented deployment, not a landing-page logo (Verified — launch press and Vertex post).
- Named a **Gartner Cool Vendor in AI for SRE and Observability 2025** (Reported).
- Vendor-reported outcomes: 20–30% of engineering capacity reclaimed at early adopters; sub-2-minute average investigations (Reported — treat as marketing until independently benchmarked).
- Multiple detailed engineering talks (MLOps Community "Agents in Production," LangChain case study, several ZenML LLMOps database entries) — unusually high technical transparency for a seed-stage vendor.

## Relevance to agentic AI engineering

Cleric is a working case study in three areas this repo tracks. **Agent memory:** its operational-memory design — distilling episodic investigations into persistent, per-environment knowledge — is a production instance of the agent-memory research thread. **Tool-use and governance:** read-only-by-default RBAC-enforced tool access inside a customer VPC is a concrete governance pattern for granting agents production credentials. **Agentic SWE evaluation:** their LangSmith-based comparison of investigation strategies is the ops-side analogue of agentic SWE benchmarks — note that incident diagnosis still lacks a public SWE-bench-style benchmark, which is why every vendor's accuracy claims are self-reported.

## Use cases & considerations

Use cases: (1) first-responder triage for noisy alert queues; (2) 24/7 coverage for teams too small for a follow-the-sun rotation; (3) onboarding accelerant — the stack map and memory encode tribal knowledge; (4) post-incident pattern mining across services.

Considerations: no public pricing; value depends heavily on observability hygiene (garbage telemetry in, garbage hypotheses out); per-tenant learning creates soft lock-in (the memory is the moat — and the switching cost). Crowded category: **Resolve.ai**, **Traversal**, **Datadog Bits AI**, **incident.io AI**, and Parity are direct competitors. Open questions: independent accuracy numbers, and how well memory transfers across stack migrations.

## Sources

- https://cleric.ai/
- https://cleric.ai/blog/cleric-launches-the-first-self-learning-ai-sre
- https://cleric.ai/blog/introducing-cleric
- https://www.businesswire.com/news/home/20251209625361/en/Cleric-Launches-the-First-Self-Learning-AI-SRE
- https://vvus.com/news/announcing-our-investment-in-cleric/
- https://www.prnewswire.com/news-releases/cleric-unveils-the-first-autonomous-ai-site-reliability-engineer-302095870.html
- https://pulse2.com/cleric-4-3-million-raised-and-autonomous-ai-site-reliability-engineer-unveiled/
- https://techfundingnews.com/cleric-grabs-4-3m-for-first-24-7-autonomous-ai-site-reliability-engineer/
- https://www.langchain.com/blog/customers-cleric
- https://www.zenml.io/llmops-database/ai-sre-agents-for-production-system-diagnostics
- https://www.crunchbase.com/organization/cleric-73c7
- https://www.linkedin.com/in/willempienaar/
- https://siliconangle.com/2025/12/09/cleric-launches-ai-agent-uplevel-site-reliability-intelligent-automation/
