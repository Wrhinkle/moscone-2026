# Druid (DRUID AI)

> Enterprise agentic-AI platform from Romania: build, orchestrate, and govern fleets of business-process AI agents (HR, customer service, banking ops) on a central orchestration engine called Conductor.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** gold
- **Founded:** 2018, Bucharest, Romania (Verified — company site, EU-Startups, TechCrunch); now positions as global with US as largest market
- **Website / GitHub:** https://www.druidai.com · docs: https://docs.druidai.com (no significant public OSS presence found)

*Disambiguation:* not Apache Druid (the OLAP database, commercialized by Imply). This is DRUID AI, the agent platform — confirmed as the AIEWF exhibitor via their own event page (booth L-G11, demos of Solution Builder and Conversation Toolkit).

## What they do

Druid started (2018–2022) as an enterprise conversational-AI/chatbot platform tightly coupled with RPA — UiPath resold it globally as the conversational front-end to their robots. Since ~2024 it has repositioned as an end-to-end agentic platform. The core is **Druid Conductor**, a multi-agent orchestration engine: it decomposes a business goal into a task graph and dispatches steps to specialist agents (Knowledge, Process, Voice, Workspace), running them in parallel or sequence while serializing a unified execution context (user identity, conversation state, entity slots, retrieved data, workflow progress) across every hop. Governance is built in: audit trails, policy enforcement, RBAC (Reported — vendor docs/site).

The intelligence layer is LLM-agnostic — Azure OpenAI, Claude, Mistral, custom models — abstracted from agent logic so you can swap or A/B models without touching flows or integrations. Notably, they ship **Becus**, a proprietary model for air-gapped/on-prem deployments in regulated environments, running on the same Conductor/RAG stack (Reported — vendor site). Deployment is containerized Kubernetes: cloud (Azure/AWS/GCP), on-prem, hybrid, or fully air-gapped. In 2025 they also announced "self-building" agents / an agent "factory" — agents generated from process descriptions (Reported — AI Business, AI News; treat as directional marketing until independently validated).

What you'd actually buy: a low-code builder plus the orchestration/governance runtime and a Knowledge Base layer that unifies databases, documents, email, CRM, and HR systems for RAG. This is a sales-led enterprise product (no public self-serve pricing found) — the opposite posture from developer-first orchestration tools.

## Founders & origins

Founded by **Liviu Drăgan** (founding CEO), previously founder of TotalSoft, one of Romania's largest software companies — a well-known figure in Romanian tech (Verified — multiple press). Co-founders include **Andreea Pleșea** (CRO, later interim CEO), **Daniel Bălăceanu** (Head of Products), and, per press, **Bogdan Grigorescu** and **Bogdan Pietroiu** (Reported). In September 2025, **Joseph Kim** — ex-CEO of Sumo Logic, prior CPTO roles at Citrix and SolarWinds — became CEO (Verified — SiliconANGLE, EU-Startups).

## Funding

- **2020: $2.5M** round led by GapMinder, with Early Game Ventures (Verified — Druid, GapMinder; labeled "Series A" at the time)
- **2022: $15M Series A** led by Karma Ventures and Hoxton Ventures, with GapMinder (Verified — Finsmes, Druid)
- **Sept 2023: $30M Series B** led by TQ Ventures; Smedvig Capital, Endeavor, Verve Ventures, plus existing investors (Verified — TechCrunch, PR Newswire)
- **Sept 2025: $31M Series C** led by Cipio Partners; TQ Ventures, Karma, Smedvig participating (Verified — SiliconANGLE, EU-Startups)
- **Total raised: ~$80M+** (computed; round labels overlap across sources, so treat as approximate)

## Evidence of real-world use

Strong for this category. **UiPath formally partnered to resell Druid** — a real distribution/co-engineering signal, with a Druid listing on UiPath Marketplace (Verified). Named customers per press and case studies: **AXA Insurance, Carrefour Group, the FDA, NHS, Georgia Southern University, Banca Transilvania, PROFI** (HR automation across ~1,400 stores), and Australia's largest retailer (a 13-language customer-support agent) (Reported — mostly vendor case studies; the AXA/FDA/NHS list comes via SiliconANGLE's funding coverage). Company-claimed metrics: 1B+ conversations, 4,000+ agents, 300+ customers, 2.7x ARR growth YoY (Reported — company via press). Gartner placed them as a **Challenger** in the Magic Quadrant for Conversational AI Platforms (Reported).

## Relevance to agentic AI engineering

Druid is a production data point for the questions in this repo's **tool-use/governance** papers: Conductor is essentially a governed task-graph executor with policy enforcement and audit trails — the enterprise answer to "who is allowed to let an agent do what." Their unified execution context carried across agents connects to the **agent-memory** literature (state/context handoff rather than long-term skill memory). Voice AI Agents on the same orchestration layer make them relevant to the **voice-agent** papers. Not relevant to agentic SWE benchmarks — this is business-process automation, not coding agents. Contrast with Composio (same category folder): Composio sells the tool/auth layer to developers; Druid sells the whole governed agent runtime to enterprises.

## Use cases & considerations

Use cases: (1) HR/employee-service agents over SAP/Workday-class systems (the PROFI/Carrefour pattern); (2) regulated-industry deployments needing on-prem or air-gapped LLMs (banking, government — the Becus pitch); (3) customer-service agent fleets with RPA hand-offs via UiPath; (4) multi-agent process orchestration where audit/RBAC is a hard requirement.

Considerations: proprietary low-code platform — real lock-in, and flows aren't portable. Legacy chatbot DNA means some "agentic" claims are rebranding; validate Conductor's autonomy versus scripted flows in a POC. No public pricing; enterprise sales cycle. Most usage evidence is vendor-published. Competitors: **Kore.ai, Cognigy (NiCE), Amelia, Sierra, Salesforce Agentforce, Microsoft Copilot Studio**, and UiPath's own agentic push (a partner that could become a competitor). Open question: whether a Romanian-rooted, RPA-era platform can win US enterprise agentic deals under the new CEO before hyperscaler suites absorb the category.

## Sources

- https://www.druidai.com/ and https://www.druidai.com/platform/ai-agent-orchestration
- https://docs.druidai.com/1385954/Content/1_Druid%20AI%20Platform/Druid%20Platform.htm
- https://events.druidai.com/meet-druid-at-the-ai-engineer-worlds-fair
- https://siliconangle.com/2025/09/16/agentic-ai-startup-druid-ai-targets-growth-raising-31m-hiring-new-ceo/
- https://www.eu-startups.com/2025/09/romanian-startup-druid-ai-raises-e26-million-to-accelerate-agentic-ai-platform-growth-under-new-ceo/
- https://techcrunch.com/2023/09/12/druid-a-conversational-ai-platform-for-enterprises-that-integrates-with-chatgpt-raises-24m/
- https://www.prnewswire.com/news-releases/druid-secures-30-million-as-part-of-series-b-round-to-enhance-enterprise-productivity-through-conversational-business-applications-and-generative-ai-301923791.html
- https://www.finsmes.com/2022/05/druid-raises-usd15m-in-funding.html
- https://www.druidai.com/news/druid-ai-series-a-investment-venture-capital-gapminder-early-game
- https://www.druidai.com/news/uipath-rpa-chatbot-partner-process-automation-druid
- https://marketplace.uipath.com/organizations/druid-ai
- https://www.druidai.com/case-studies/australian-retail-customer-support-ai-agent
- https://www.druidai.com/news/druid-ai-chatbots-uipath-rpa-hr-employee-onboarding
- https://en.bancatransilvania.ro/news/comunicate-de-presa/trei-companii-din-romania-parteneriat-pentru-inovatie-banca-transilvania-uipath-si-druid
- https://www.artificialintelligence-news.com/news/druid-ai-agentic-factory-automation-in-the-real-world/
- https://aibusiness.com/agentic-ai/druid-launches-self-building-ai-agents
