# Orkes

> Managed durable-execution platform for workflows and AI agents, built by the original creators of Netflix Conductor.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, Cupertino, California (Verified — TechCrunch, company site; city Reported)
- **Website / GitHub:** [orkes.io](https://orkes.io) · [github.com/conductor-oss/conductor](https://github.com/conductor-oss/conductor)

## What they do

Orkes commercializes Conductor, the event-driven workflow orchestration engine its founders built at Netflix. The core idea: separate orchestration from business logic. Workflows are declarative JSON DAGs (with loops, branches, sub-workflows) executed by a durable engine; workers are plain code in any language with no determinism constraints — the main architectural contrast with Temporal, whose workflows are code that must replay deterministically. SDKs exist for Java, Python, JavaScript, Go, C#, plus incubating Ruby and Rust.

Since ~2024 the pitch has shifted from "microservices orchestration" to "the operating system for AI agents and workflows." Conductor now ships LLM task types (14+ native providers), MCP and function/tool calling, human-in-the-loop approval tasks, vector-DB tasks for RAG, and prompt management ("prompts as first-class citizens"). Because workflows are JSON data rather than code, LLMs can generate and modify them at runtime — Orkes leans on this for dynamic agent loops that stay durable across iterations. They also position as an execution/governance layer under agent frameworks, with documented integrations for LangGraph, OpenAI Agents SDK, Google ADK, and CrewAI (Reported — company site).

You'd buy it as Orkes Cloud (managed SaaS, 99.99% SLA claim), self-hosted on-prem, or use the free Developer Edition; the OSS engine is Apache 2.0. Enterprise layer adds RBAC with fine-grained policies, audit logs, and observability/explainability over agent actions.

## Founders & origins

Verified: Jeu George (CEO; ex-Netflix, senior engineering at Uber), Viren Baraiya (ex-Netflix, led engineering for Google Firebase), Boney Sekh (ex-Netflix, headed Robinhood's payments platform), and Dilip Lukose (CPO; ex-Microsoft Azure product, early AWS). George, Baraiya, and Sekh built Conductor at Netflix (open-sourced 2016); they reunited in 2021 to offer it as a managed platform. Netflix formally handed OSS stewardship to the community in December 2023; Orkes is now the primary maintainer of conductor-oss.

## Funding

- **Seed, Feb 2022:** $9.3M at launch from stealth (Verified — TechCrunch, PRWeb). Battery Ventures and Vertex Ventures US were early investors (Verified via later-round reporting listing them as existing investors; seed lead attribution: Reported).
- **Series A, Feb 2024:** $20M led by Nexus Venture Partners, with Battery Ventures and Vertex Ventures US (Verified — TechCrunch, Orkes blog).
- **Series B, Apr 2026:** $60M led by AVP, with Prosperity7 Ventures, Nexus, Battery, Vertex US (Verified — Businesswire, multiple outlets).
- **Total raised:** ~$90M (Verified).

## Evidence of real-world use

Unusually strong for this category. Documented case studies (not just logos): United Wholesale Mortgage (153 microservices orchestrated after failing to self-host Conductor via Helm), Collective (PoC to production in ~2.5 months with one dedicated engineer), Normalyze (90% debug-time reduction), Tafi (payments risk workflows editable without engineering), Freshworks (~1B workflows/day claim). Series B press names Twilio, LinkedIn, Quest Diagnostics, Woodside Energy, Naveo Commerce, and "one of the world's largest global retailers"; customer base reportedly tripled since Series A (Reported). The OSS project claims production use at Netflix, Tesla, LinkedIn, J.P. Morgan; conductor-oss shows ~32k stars as of 2026-07-02 (Reported — GitHub page). Caveat: OSS Conductor adoption (Atlassian, GE Healthcare, etc.) is not the same as paying Orkes customers.

## Relevance to agentic AI engineering

Orkes sits at the durable-execution/runtime layer of the agent stack — below frameworks like LangGraph/CrewAI, competing with Temporal, Inngest (see companies/agent-orchestration/inngest.md), and AWS Step Functions. It addresses the failure mode the tool-use/governance literature keeps surfacing — τ-bench-style results showing agents are unreliable at policy-following over long multi-step tasks — by moving retries, state, approvals, and audit out of the model loop into an engine. Human-in-the-loop tasks and RBAC map directly to the governance concerns in this repo's tool-use/governance area. Less relevant to agent-memory or voice-agent papers: Conductor persists workflow state, not semantic memory.

## Use cases & considerations

Use cases: (1) long-running agent pipelines needing retries/resume (document processing, underwriting); (2) human-approval gates inside agent workflows; (3) wrapping existing microservices as agent-callable tools; (4) LLM-generated workflows executed under governance.

Considerations: JSON-DSL workflows can get unwieldy vs. code-first (Temporal's counter-pitch); enterprise features (RBAC, audit) are proprietary, so OSS-to-cloud lock-in is real; no public per-unit pricing — sales-led (Developer Edition aside). Open question: whether the agent-framework integrations are deep or adapters. Competitors: Temporal, Inngest, Restate, AWS Step Functions, LangGraph Platform.

## Sources

- https://techcrunch.com/2022/02/28/orkes-from-the-creators-of-netflixs-open-source-conductor-workflow-orchestration-tool-comes-out-of-stealth-with-9-3m/
- https://techcrunch.com/2024/02/21/orkes-raises-20m-series-a/
- https://orkes.io/blog/orkes-has-raised-a-20m-series-a-to-power-our-next-phase-of-growth/
- https://www.businesswire.com/news/home/20260423550324/en/Orkes-Raises-$60M-as-Developers-Increasingly-Use-Its-Platform-to-Deploy-AI-Confidently-in-Production
- https://www.finsmes.com/2026/04/orkes-raises-60m-in-series-b-funding.html
- https://orkes.io/ (product, customers)
- https://orkes.io/customers · https://orkes.io/case-study/collective · https://orkes.io/case-study/uwm · https://orkes.io/case-study/normalyze · https://orkes.io/case-study/tafi · https://www.orkes.io/case-study/freshworks
- https://github.com/conductor-oss/conductor
- https://www.prweb.com/releases/orkes-raises-9-3m-and-launches-first-cloud-hosted-platform-for-enterprises-using-netflix-s-popular-open-source-conductor-project-859443460.html
