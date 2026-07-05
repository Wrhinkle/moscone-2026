# Solo.io

> API-gateway and service-mesh vendor (Envoy/Istio-based) extending its connectivity platform into an "AI-native" data plane for agent-to-agent and agent-to-tool traffic.

- **Category:** api-platforms
- **AIEWF 2026 tier:** silver
- **Founded:** 2017, Cambridge MA (Verified)
- **Website:** https://www.solo.io/ · https://docs.solo.io/

## What they do

Solo.io built **Gloo Edge** (Envoy-based API gateway) and **Gloo Mesh** (Istio-based service mesh, plus a managed "Gloo Cloud" offering) for enterprises running internal microservices. It's now extending that connectivity layer to agents: **kagent** is an open-source, Kubernetes-native framework for building/deploying autonomous agents in-cluster (integrates with Google's Agent Development Kit and LangGraph); **agentgateway** is an MCP/A2A-aware data plane handling agent-to-agent and agent-to-tool traffic with security, observability and governance; **agentregistry** catalogs skills, agents and MCP tool servers across teams. The framing is "agents and skills as first-class infrastructure resources," moving them from prototypes into production platform components (Verified — Virtualization Review interview with Global Field CTO Christian Posta, company docs).

## Founders & funding

Founded by **Idit Levine** (CEO). Raised **~$175M total** including an $11M Series A and a **$135M Series C** (Oct 2021, Redpoint Ventures, True Ventures, Altimeter) at a **~$1B valuation** (Verified — TechCrunch, company press releases).

## Evidence of real-world use

Named Fortune 2000 customers include **Grainger, TomTom, FICO, and Fitch Ratings**; reported ~4K customers and ~$15M revenue as of 2024 (Reported — Latka). kagent and agentgateway are open-source on GitHub under the CNCF-adjacent Envoy/Istio ecosystem Solo.io helped build.

## Relevance to agentic AI engineering

Positions directly in the agent-infrastructure/gateway layer — MCP and A2A protocol support, agent registries, and governance for multi-agent traffic are core building blocks for production multi-agent systems.

## Sources

- https://virtualizationreview.com/articles/2026/02/26/a-conversation-with-solo-io-about-agentic-agents-and-skills-in-enterprise-it.aspx
- https://techcrunch.com/2021/10/07/solo-io-reaches-1b-valuation-with-135m-series-c-investment/
- https://www.solo.io/press-releases/solo-io-advances-application-networking-market-with-135-million-series-c-funding
- https://www.solo.io/
- https://getlatka.com/companies/soloio

*Profile written 2026-07-02.*
