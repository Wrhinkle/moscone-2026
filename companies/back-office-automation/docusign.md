# Docusign

> The e-signature incumbent rebuilding itself as an "Intelligent Agreement Management" platform, with AI agents that review, monitor, and act on contracts — exposed to developers via APIs and an MCP server.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2003, Seattle, WA (Verified; HQ now San Francisco)
- **Website / GitHub:** https://www.docusign.com · https://developers.docusign.com · https://github.com/docusign

## What they do

Docusign's core business is still e-signature: legally binding signing workflows ("envelopes") with audit trails, identity verification, and integrations into CRMs/HR systems. Around that it has built Intelligent Agreement Management (IAM) — a platform that treats the contract corpus as structured data: Navigator (an AI-extracted agreement repository), CLM (contract lifecycle management), and Iris, its agreement-specific AI engine for extraction, risk flagging, and legalese translation.

The 2026 shift is agentic. At Momentum '26 (May 21, 2026), Docusign launched an AI assistant, Iris agents, and Agent Studio (Verified: press release + independent coverage). Agents check drafts against company playbooks, suggest edits, route approvals, monitor executed contracts in the background for obligations/renewals/risks, and trigger next steps. Agent Studio lets teams compose custom agents over their agreement data. As of 2026-07-02 these are in US early access, with broader US rollout "starting in July" — so treat agent capabilities as new, not battle-tested.

For engineers, the concrete integration surfaces are: eSignature/IAM REST APIs, webhooks (Connect), and a beta MCP server (`mcp-d.docusign.com/mcp`) that exposes IAM capabilities to any MCP client — Docusign explicitly documents use with Claude, GitHub Copilot, Gemini CLI, and Microsoft Copilot Studio (Verified: developer docs + The New Stack coverage). Community MCP servers also exist (e.g., luthersystems/mcp-server-docusign with JWT server-to-server auth).

## Founders & origins

Founded 2003 by Court Lorenzini, Tom Gonser, and Eric Ranft (Verified: Wikipedia, SaaS Mag, Crunchbase). Gonser conceived the idea while CEO of NetUpdate (founded 1998); NetUpdate had acquired Seattle e-signature startup DocuTouch, and Lorenzini negotiated purchase of DocuTouch assets to start Docusign. First real traction came in 2005 via zipForm's real-estate forms integration. Current CEO is Allan Thygesen (since 2022; previously President, Americas & Global Partners at Google), who has driven the IAM/AI repositioning (Verified).

## Funding

Public company — NASDAQ: DOCU, IPO April 27, 2018 at $29/share, raising roughly $543M–$629M depending on source (Reported; sources conflict on the exact figure). Pre-IPO it raised an estimated ~$525M total (Reported: Global Corporate Venturing, Tracxn), including: $4.6M in 2004 (Ignition Partners, Frazier Technology Ventures — Reported); ~$47.5–56M in 2012 including Kleiner Perkins (Reported); ~$300M Series F in 2015 with Intel Capital, Dell, and Deutsche Telekom participating (Reported). FY2026 (ended Jan 31, 2026): revenue $3.2B (+8% YoY), ARR $3.27B, record operating margin, plus a $2.0B buyback increase (Verified: SEC 8-K, company press releases).

## Evidence of real-world use

Strongest in this landscape: ~1.8 million paying customers including most large enterprises and 1.5M+ small businesses (Verified: FY2026 filings). E-signature is effectively default infrastructure in real estate, HR, sales, and — relevant to Ridgeline — construction contracts and change orders. For the newer IAM platform specifically: ~40,000 customers and >$350M ARR (Verified: company earnings/press). The agentic products themselves have no independent case studies yet (early access); the "nearly 30% higher ROI" figure is a Docusign-commissioned Deloitte study — treat as vendor marketing. Public pricing exists across tiers, and a large developer ecosystem (SDKs in 6+ languages, active GitHub org) signals real integration usage.

## Relevance to agentic AI engineering

Docusign is a canonical back-office tool surface for agents: the MCP server makes "get this signed," "check contract status," and "extract obligations" callable tools in any agent loop. That maps directly to *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration* (agreement workflows are multi-step, multi-tool by nature) and to the governance papers — *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too* — because signature execution is exactly the class of high-consequence, legally binding action where agent authorization boundaries matter most. Background obligation-monitoring agents also connect to the agent-memory line of work (*Memory for Autonomous LLM Agents*): renewals and obligations are long-horizon state.

## Use cases & considerations

Use cases: (1) agent-triggered signature requests inside a back-office workflow (e.g., a job-packet agent sending subcontractor agreements and change orders for signature); (2) contract-repository Q&A/extraction over Navigator; (3) renewal/obligation monitoring agents; (4) MCP-based agreement tools inside Claude/Copilot workflows.

Considerations: agent features are weeks old and US-only early access; Iris/Agent Studio locks you into the IAM data model; per-envelope and per-seat pricing gets expensive at volume. Competitors: Adobe Acrobat Sign, Dropbox Sign, PandaDoc, and on the CLM/agreement-AI side Ironclad, Icertis, LinkSquares, plus Sirion and Evisort (now part of Workday). Open question: whether an incumbent's agents beat a thin custom agent calling Docusign's plain APIs.

## Sources

- https://www.prnewswire.com/news-releases/docusign-unveils-ai-assistant-and-agents-to-power-the-next-era-of-agreement-work-302777909.html
- https://www.docusign.com/blog/new-ai-assistant-and-agents
- https://www.docusign.com/products/platform/ai
- https://developers.docusign.com/platform/mcp-server/
- https://thenewstack.io/docusign-mcp-agentic-agreements/
- https://github.com/luthersystems/mcp-server-docusign
- https://en.wikipedia.org/wiki/DocuSign
- https://www.saasmag.com/how-tom-gonser-created-a-document-signing-platform-and-built-it-into-a-6-8-billion-saas-giant/
- https://www.sec.gov/Archives/edgar/data/0001261333/000126133326000017/q426ex-991er.htm
- https://www.docusign.com/company/news-center/docusign-announces-fourth-quarter-and-fiscal-year-2026-financial-results-announces-20-billion-increase-to-share-repurchase-program
- https://globalventuring.com/corporate/ipo-of-the-year-docusign/
- https://techcrunch.com/2018/04/26/docusign-raises-629-million-after-pricing-ipo/
- https://tracxn.com/d/companies/docusign/__9RGlMRVIb5qWTHZ_kjE9bTSP8S5z2MnXbceDDr38iDw
- https://thelettertwo.com/2026/05/21/docusign-iris-ai-agents-agreement-automation/
- https://www.docusign.com/company/leadership
