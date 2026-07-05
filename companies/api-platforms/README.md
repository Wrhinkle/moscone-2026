# API Platforms

**Category definition:** API management, gateways, API development and testing tools.

APIs are how software talks to software, and this category exists because that plumbing needs a control layer: something to expose, secure, rate-limit, document, and observe every interface an organization publishes. What makes the category interesting in 2026 is that all four vendors here — spanning a 21-year-old middleware incumbent to an Envoy/Istio-native challenger — have converged on the *same* repositioning: APIs' next big consumer is agents, so the API gateway is becoming the agent gateway. Every company in this folder now ships some combination of "turn your existing REST APIs into MCP servers," "govern agent-to-tool and agent-to-agent (A2A) traffic at the gateway," and "catalog agents/tools so they can be discovered and authorized." This is the commercial answer to a question the governance papers keep raising: how do you safely expose hundreds of internal APIs to agents without every team reinventing auth, quotas, and audit logging?

## How to read this category

Start with **[Postman](postman.md)** — the biggest name (40M+ developers, $5.6B peak valuation) and the developer-workflow end of the spectrum: its API→MCP-server generator and March 2026 Git-native platform rebuild show what "AI-native API tooling" looks like for the individual engineer. Then read **[Gravitee](gravitee.md)**, the sharpest articulation of the gateway-side bet: its Agent Mesh (LLM/A2A/MCP traffic under one policy engine) is the fullest agent-governance control plane in the folder, and it's the AIEWF gold sponsor. The remaining two differentiate on infrastructure heritage: **[Solo.io](solo-io.md)** comes from the Kubernetes/service-mesh world (kagent, agentgateway — agents as in-cluster infrastructure resources), while **[WSO2](wso2.md)** is the legacy-enterprise-middleware path to the same destination (MCP Gateway + MCP Hub for governing what big regulated orgs already run).

The axis that splits the category: **developer workspace vs. runtime gateway**. Postman sells seats to the humans (and now agents) who design and test APIs; Gravitee, Solo.io, and WSO2 sell the enforcement layer the traffic actually flows through — differing mainly in whether their center of gravity is events/streams (Gravitee), Kubernetes/service mesh (Solo.io), or legacy enterprise integration and IAM (WSO2).

## Companies

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Gravitee](gravitee.md) | Event-native API management platform repositioned as an "agent mesh" — one gateway governing REST, Kafka, LLM, MCP, and A2A traffic | Gold | $125M+ total; $60M Series C (May 2025, Sixth Street); ~$22M ARR FY2024 | 2024 & 2025 Gartner MQ Leader for API Management; its MCP Tool Server converts an existing API estate into governed agent tools |
| [Postman](postman.md) | The default API client for 40M+ developers, rebuilt (March 2026) as an AI-native platform that generates MCP servers from its 100k-API network | Silver | ~$433M raised; $5.6B valuation (2021), secondaries reportedly ~$3.2B — a ~40% markdown | 98% of the Fortune 500 uses it; its 2025 State of the API report found 1 in 4 developers now design APIs specifically for AI agents |
| [Solo.io](solo-io.md) | Envoy/Istio-based gateway and service-mesh vendor extending into an agent data plane: kagent, agentgateway, agentregistry | Silver | ~$175M raised; $135M Series C (Oct 2021) at ~$1B valuation | Treats agents and skills as first-class Kubernetes infrastructure resources — the most cloud-native take on agent governance here |
| [WSO2](wso2.md) | Two-decade-old open-source API management / identity / integration incumbent, now shipping an MCP Gateway and searchable MCP Hub | Supporting | Acquired by EQT Private Capital Asia (Aug 2024) for $600M+ | 800+ customers in 90+ countries (Wells Fargo, AT&T, eBay) — the deepest pre-AI enterprise install base in the category |

All four expected profiles for this category are present; nothing is missing or re-filed elsewhere.

## Related papers

The research thread this category commercializes lives mostly in [`papers/tool-use-governance/`](../../papers/tool-use-governance/):

- [The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) — the tool-provisioning question these platforms industrialize: Postman's MCP Builder and Gravitee's/WSO2's API→MCP conversion are production pipelines for giving agents tools.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) — the academic counterpart to enforcing policy at a gateway rather than trusting agent code; directly cited in the Postman and Gravitee profiles.
- [CaMeLs Can Use Computers Too: System-Level Security for Computer-Use Agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) — system-level (not model-level) security enforcement, the same architectural bet as an MCP/AI gateway.
- [CLAWLESS: A Security Model of AI Agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md) — a security model for agent capabilities; maps to the agent-identity and IAM work Gravitee and WSO2 are shipping.
- [Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md) — whether agents need curated, machine-readable descriptions to find the right tool bears directly on Postman's AI-readable Collection v3 + API Catalog and the MCP Hub/Agent Catalog plays.

## Open questions

1. **Incumbents vs. agent-natives.** Every profile here is an API-era company retrofitting agent governance (all agent features are roughly a year old atop decade-old cores). Do they win the agent-gateway layer, or do agent-native entrants (LiteLLM, Portkey, Cloudflare AI Gateway, Composio/Arcade on the tool side) take it?
2. **Curated catalogs vs. ad hoc integration.** Postman's bet is that agents consume APIs through governed MCP catalogs; the alternative is agents generating integrations on the fly from raw OpenAPI specs. Which pattern wins determines whether the catalog/hub products matter.
3. **Does A2A traffic materialize?** Gravitee and Solo.io both ship agent-to-agent protocol governance, but the profiles show little evidence yet of production A2A traffic at enterprise scale — the mesh may be ahead of the market.
4. **Where does enforcement consolidate?** Four vendors now sell overlapping MCP gateways; enterprises won't run all of them. Does agent-traffic governance fold into the existing API-management purchase, the service mesh, or the identity/IAM stack?
