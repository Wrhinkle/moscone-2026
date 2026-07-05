# Snyk

> Developer-first security platform — scans your dependencies, code, containers, and IaC from inside the dev workflow, and is now repositioning as the enforcement/governance layer for AI coding agents and MCP servers.

- **Category:** security-identity
- **AIEWF 2026 tier:** gold
- **Founded:** 2015, London / Tel Aviv (Verified — Wikipedia, Contrary Research); dual HQ Boston/London today (Reported)
- **Website / GitHub:** https://snyk.io · https://github.com/snyk (open-source CLI, `mcp-scan` via Invariant Labs)

## What they do

Snyk's core is a suite of scanners that plug into the places developers already work — CLI, IDE, git PR checks, CI — rather than a standalone security console. The pillars: **Snyk Open Source** (SCA: flags known-vulnerable dependencies and suggests minimal upgrade/patch paths), **Snyk Code** (SAST built on the 2020 DeepCode acquisition, ML-assisted static analysis fast enough to run in the IDE), **Snyk Container** (image/base-image scanning), **Snyk IaC** (Terraform/K8s misconfig), **Probely** DAST (acquired Nov 2024), and **AppRisk** ASPM (partly from the 2023 Enso Security acquisition). Distribution is classic PLG: a free tier and a public pricing page (Team plans priced per product per month), with enterprise contracts on top.

The 2025–2026 pivot is AI security. The **AI Trust Platform** (2025) added Snyk Assist (contextual guidance), Snyk Agent (automated fixes), and Snyk Guard (real-time policy enforcement). In June 2025 Snyk acquired **Invariant Labs**, the ETH Zürich-linked research group behind early MCP attack research (tool poisoning, MCP "rug pulls") and the open-source `mcp-scan` tool; that team now runs **Snyk Labs**. On June 23, 2026 Snyk launched **Evo Agentic Development Security (ADS)** — GA June 29 — which governs what coding agents *use* (MCP servers, plugins, skills), *do* (runtime actions), and *generate* (code), enforced inside the agent workflow rather than post-hoc scanning (Verified — Snyk newsroom, GlobeNewswire, SiliconANGLE). Their supporting telemetry claim: 43% of developers run 2+ AI coding environments, over half have MCP servers installed, and 1 in 12 developers with MCP servers has a high/critical finding (Reported — company data).

## Founders & origins

**Guy Podjarny** (founder, CEO until 2019, then President/board until early 2025 — he left to found Tessl), **Assaf Hefetz** (co-founder, former CTO), **Danny Grander** (co-founder, security research) — Verified across Wikipedia, Contrary Research, Snyk's own pages. Podjarny and Grander came out of Israeli IDF cyber/intelligence units (Unit 8200 lineage); Podjarny previously founded Blaze (web performance), acquired by Akamai in 2012, where he was CTO of the Web Performance unit. Origin thesis: security tooling should adopt the usability and distribution of developer tools (New Relic/GitHub/Heroku model), not enterprise-security sales motions. **Peter McKay** (ex-Veeam co-CEO, Snyk board member since 2016) has been CEO since July 2019 (Verified).

## Funding

- Total raised: ~$1.3–1.6B depending on counting method (Tracxn says $1.32B over 17 rounds; other sources ~$1.6B) — Reported, sources disagree on the total.
- $75M strategic investment from Salesforce Ventures and Atlassian, 2021 (Verified — VentureBeat).
- Series F, Sept 2021: ~$530M (primary+secondary) at **$8.5B valuation** (Verified — SDxCentral, multiple press).
- Series G, Dec 2022: **$196.5M at $7.4B** — a down round — led by QIA (Verified — multiple sources).
- Smaller extension ~$25M, April 2024 (Reported — Tracxn).
- Revenue: ~$343.8M ARR 2024, ~$407.8M 2025 (Reported — GetLatka; not independently verified). IPO long rumored, not filed as of 2026-07-02 (Unverified).

## Evidence of real-world use

Strong and documented beyond logos: **Atlassian** has a named case study (container scanning across products; 99% of Atlassian services run in containers) and **Salesforce** documents automating its OSS review pipeline with Snyk, saving ~150 engineering hours/year — both are also investors, which cuts both ways (Verified — snyk.io case studies, VentureBeat). Free CLI with years of community adoption, public pricing, large case-study library (Google, Twilio, Revolut appear in Snyk's customer pages — Reported, company-published). The DeepCode/Invariant acquisitions brought real research output: Invariant's MCP tool-poisoning disclosures were widely covered in 2025 and `mcp-scan` is used independently of Snyk's paid platform.

## Relevance to agentic AI engineering

Snyk is betting the company on the **agentic SDLC**: if coding agents (the SWE-bench / agentic-SWE-benchmark class of tools) write an increasing share of production code, someone has to scan what they generate and govern what they touch. Evo ADS is directly a **tool-use/governance** play — runtime policy enforcement over agent tool calls and MCP configurations, the enforcement layer that policy-compliance benchmarks like τ-bench implicitly assume exists. Invariant Labs' tool-poisoning and MCP-security research is among the most-cited practitioner work on agent attack surfaces. Little connection to the agent-memory or voice-agent threads in this repo, except that any voice/back-office agent with MCP access inherits the same supply-chain and injection risks.

## Use cases & considerations

1. Baseline SCA + SAST in CI for any product with AI-generated code volume (free tier makes trial cheap).
2. Audit a team's MCP server sprawl with `mcp-scan` / Evo ADS before agents get production credentials.
3. Policy gate for autonomous coding agents: block risky dependency introductions or tool calls in-workflow.

**Considerations:** down round + long-delayed IPO signal pricing pressure; enterprise pricing beyond Team tier is opaque; scanner noise/false-positive tuning is a known complaint; Evo ADS is brand-new (GA June 2026) and unproven. Competitors: GitHub Advanced Security/Dependabot, Semgrep, Sonar (also in this repo), Checkmarx, Veracode, Socket (supply chain), and emerging MCP-security startups. Open question: whether agent-security lands as a Snyk product or gets absorbed into agent platforms themselves.

*Confidence statements as of 2026-07-02.*

## Sources

- https://en.wikipedia.org/wiki/Snyk
- https://research.contrary.com/company/snyk
- https://snyk.io/news/snyk-launches-evo-agentic-development-security/
- https://snyk.io/news/snyk-acquires-invariant-labs-to-accelerate-agentic-ai-security-innovation/
- https://labs.snyk.io/resources/snyk-labs-invariant-labs/
- https://snyk.io/news/snyk-acquires-developer-first-dast-provider-probely/
- https://www.globenewswire.com/news-release/2026/06/23/3315918/0/en/snyk-adds-agentic-development-security-to-its-ai-security-platform-the-enforcement-layer-for-the-ai-agents-now-building-enterprise-software.html
- https://siliconangle.com/2026/06/23/snyk-launches-evo-agentic-development-security-police-ai-coding-agents/
- https://snyk.io/case-studies/atlassian/
- https://snyk.io/case-studies/salesforce/
- https://venturebeat.com/business/salesforce-and-atlassian-double-down-on-developer-security-with-75m-snyk-investment/
- https://www.sdxcentral.com/news/snyk-says-85b-valuation-validates-developer-security-vision/
- https://tracxn.com/d/companies/snyk/__R962gE3cLhPYE6YfvOOI_C7Ek9zrtlGPOgVeCjDvLBI
- https://getlatka.com/companies/snyk
- https://crew.vc/perspectives-insights/guy-podjarnys-journey-to-building-snyk/
