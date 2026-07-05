# WSO2

> A long-established open-source-rooted API management, integration, and identity platform that has recently repositioned around governing AI: turning REST APIs into MCP servers and gatewaying agent traffic.

- **Category:** api-platforms
- **AIEWF 2026 tier:** supporting
- **Founded:** August 2005, Sri Lanka. (Verified — Wikipedia, TechCrunch, company history)
- **Website / GitHub:** https://wso2.com — historically a major Apache-project-adjacent open-source contributor (Axis2, Synapse); github.com/wso2

## What they do
WSO2 is a two-decade-old enterprise middleware vendor for API management, identity/access management, and integration — the kind of platform you'd put in front of internal services to expose, secure, rate-limit, and monitor APIs. In 2026 they launched an "API Platform" positioned as agent-ready: it converts existing REST APIs into MCP-compatible servers, runs an AI Gateway and a dedicated MCP Gateway that sit between MCP clients and MCP servers to apply auth, rate limits, and policy enforcement to tool calls, and organizes all published MCP servers into a searchable "MCP Hub" catalog. Concretely, for an engineer this is infrastructure to avoid hand-rolling access control and observability into every MCP server an org exposes to agents — governance pushed to a gateway layer instead of duplicated in each server.

## Founders & origins
Sanjiva Weerawarana, Paul Fremantle, and Davanum Srinivas, founded August 2005; Weerawarana (ex-IBM researcher, Apache SOAP/Axis contributor) remains CEO. (Verified — Wikipedia, TechCrunch profile of Weerawarana.)

## Funding
WSO2 was acquired by EQT Private Capital Asia in a deal finalized August 2024, reported at $600M+. (Verified — TechCrunch, two independent articles.) Prior venture funding history not re-verified in this pass.

## Evidence of real-world use
Verified/reported: 800+ customers across 90+ countries, with named enterprise logos including Wells Fargo, AT&T, Verizon, Cisco, eBay, Expedia, Hilton, Qantas, Standard Chartered, Nissan, and Honda; recognized by Gartner and Forrester as a leader in API management/identity segments — substantive, well-documented enterprise deployment history predating the AI pivot.

## Relevance to agentic AI engineering
Directly relevant to the tool-calling/infrastructure layer of agent stacks: MCP gateway and governance is exactly the "how do you safely expose 500 internal APIs to agents without every team reinventing auth" problem this repo's api-platforms and security-identity categories track.

## Use cases & considerations
Use cases: auto-generating MCP servers from legacy REST APIs, centralizing rate-limiting/policy/observability for agent-tool traffic, cataloging internal MCP servers for discovery. Considerations: WSO2 markets "no vendor lock-in" but is itself a large incumbent platform with its own adoption cost; competitors in the emerging MCP-gateway space include Kong, Apigee/Google, and various API-gateway incumbents extending into AI governance; open question is how quickly the MCP Gateway/Hub features (GA'd March 2026) mature relative to newer AI-native entrants.

## Sources
- https://en.wikipedia.org/wiki/WSO2
- https://techcrunch.com/2024/08/03/meet-the-founder-who-built-and-sold-a-600m-enterprise-software-startup-from-sri-lanka/
- https://techcrunch.com/2024/05/03/eqt-snaps-up-enterprise-software-company-wso2-for-more-than-600m/
- https://wso2.com/api-platform/ai-gateway/
- https://wso2.com/library/blogs/unified-governance-wso2-mcp-gateway/
- https://www.globenewswire.com/news-release/2026/03/31/3265629/0/en/WSO2-Launches-API-Platform-to-Make-Enterprise-APIs-Agent-Ready-Without-Vendor-Lock-In.html
