# Auditoria AI

> Agentic AI SaaS for the CFO's back office — AI agents that sit on top of your ERP and email to run accounts payable, accounts receivable, and finance helpdesk workflows end to end.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2019, Santa Clara, California (Verified — company site, funding press releases)
- **Website / GitHub:** https://www.auditoria.ai · no significant public GitHub presence (closed-source enterprise SaaS)

## What they do

Auditoria sells finance-domain AI agents that act as a "system of engagement" layered over the ERP system of record. The agents connect to ERPs and email inboxes, read incoming documents and messages, and execute transactional finance work with an audit trail. The two flagship suites: **SmartVendor** (accounts payable) bundles an *AP Helpdesk* agent that answers vendor emails about invoice status and payment timing, an *AP Invoices* agent that captures invoices from email via computer vision/OCR, extracts header and line-level data, runs 2-way PO matching, codes non-PO invoices from historical patterns, and posts to the ERP, and an *AP Accruals* agent that generates month-end accruals from open POs and receipts. **SmartCustomer** (accounts receivable) does collections: AI-driven dunning, payment reminders, inbox monitoring, dynamic worklist prioritization based on payer behavior, and escalation to humans with recommended actions. A **SmartResearch** agent and a newer FP&A agent (announced 2025) round out the lineup (Verified — company site, Gartner Peer Insights, PYMNTS).

Integration surface is broad and marketplace-verified: Oracle NetSuite, Sage Intacct (listed on the Intacct Marketplace), Workday (SmartCustomer AR Collections on the Workday Marketplace), Oracle Fusion Cloud ERP and E-Business Suite (Oracle Cloud Marketplace), SAP, Coupa, and — as of 2026 — ServiceNow for autonomous finance workflows (Verified — marketplace listings, Yahoo Finance/press). In May 2026 they introduced **"Governed Autonomy"** at the Gartner CFO Symposium: instead of human-in-the-loop approval per action, the enterprise defines policies upfront — what agents can do, when they can act, how authority is enforced, how every action is audited — and agents execute inside those guardrails (Verified — GlobeNewswire, company). Notably they also ship an explicit human-in-the-loop mode for automation-wary teams (Reported — CFO Dive).

## Founders & origins

Three co-founders, all with a shared Oracle/Palerra history (Verified — company site, funding press): **Rohit Gupta** (CEO) was founder/CEO of Palerra, an early cloud access security broker acquired by Oracle in 2016, then Group VP for Cloud Security at Oracle. **Adina Simu** (co-founder, CCO/CPO) held product roles at Oracle, Palerra, CipherCloud, VMware, Proofpoint, ZL Technologies, and Cisco. **Gaurav Bhatia** is the third co-founder on the engineering side (Reported — Crunchbase/Tracxn; less press detail on his background). The origin thesis: apply the ML-plus-automation playbook from cloud security to ERP financial operations.

## Funding

- **Seed:** $6M, April 2020, co-led by Neotribe Ventures, Engineering Capital, Firebolt Ventures (Verified — Global Venturing, company)
- **Series A:** $15.5M, March 2021, led by Venrock, with Workday Ventures, B Capital, and existing investors (Verified — company PR, Crunchbase)
- **Series B:** $38M, announced February 24, 2025, led by Innovius Capital, with Dell Technologies Capital, Sentinel Global, and existing investors Venrock, Neotribe, Engineering Capital, KPMG Ventures (Verified — company PR, PYMNTS, Wilson Sonsini)
- **Total raised:** ~$60.5M over 5 rounds (Reported — Tracxn)

Strategic investors worth noting: Workday Ventures, KPMG Ventures, Dell Technologies Capital — channel-relevant, not just financial.

## Evidence of real-world use

Mixed. Strong indirect signals: listings on four enterprise marketplaces (Sage Intacct, Workday, Oracle Cloud, ServiceNow) require real certified integrations; a Gartner Peer Insights page for SmartVendor exists with reviews; the Series B press claims triple-digit revenue growth in 2024; January 2026 UK/European expansion with a London data centre, Ireland secondary, and a country lead hire (Dean Harrigan) implies real enterprise demand with data-residency requirements (Verified — GlobeNewswire). Weak direct signals: FeaturedCustomers shows no public case studies, and named-customer evidence is thin — the clearest is a video testimonial from **Punchh** (CFO Anish Mehta). Outcome claims like "60%+ productivity improvement" and "20–30% DSO reduction" are vendor-stated, not independently documented (Reported). No public pricing page — enterprise sales motion only.

## Relevance to agentic AI engineering

Auditoria is a live case study in production agent governance: "Governed Autonomy" — policy-defined action scopes, enforced authority, per-action audit logs — is exactly the pattern argued for in *Governance by Construction for Generalist Agents*, and its security framing echoes *CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents*. The multi-agent AP/AR suites orchestrating ERP writes, email, and OCR map to *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. Collections agents that reprioritize accounts from payment-behavior history are an applied instance of the long-term memory question in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*. For this repo's back-office thread (Ridgeline: AR Follow-Up Prioritizer, Sub Bill Intake Checker), Auditoria is the enterprise-scale version of the same patterns — worth studying for its escalation and audit-trail design even though it targets mid-market/enterprise ERPs, not contractor back offices.

## Use cases & considerations

**Use cases:** (1) AP inbox automation — invoice capture, matching, coding, posting into NetSuite/Intacct with audit trail; (2) vendor-email helpdesk deflection (invoice status, payment timing); (3) AR collections/dunning with behavior-based prioritization to cut DSO; (4) month-end accrual generation for faster close.

**Considerations:** closed enterprise SaaS with no public pricing and no self-serve — evaluation requires a sales cycle; thin public case-study evidence relative to six years of operation; deep coupling to specific ERPs is both the value and the lock-in. Competitors: HighRadius and Billtrust (AR), Vic.ai and Tipalti (AP), Ramp (spend), Gaviti, Emagia — plus ERP vendors (NetSuite, SAP, Workday) building native agents, which is the structural threat. Open questions: how much is LLM-agentic versus rules/RPA under the hood, and whether Governed Autonomy holds up under adversarial vendor-email inputs.

## Sources

- https://www.auditoria.ai/ and https://www.auditoria.ai/company/
- https://www.auditoria.ai/pr-auditoria-ai-raises-38m-in-series-b-funding-to-usher-agentic-ai-era-for-enterprise-finance-teams/
- https://www.auditoria.ai/pr-auditoria-ai-raises-15-5-million-to-usher-in-the-era-of-zero-touch-autonomous-finance/
- https://www.pymnts.com/news/investment-tracker/2025/auditoria-ai-raises-38-million-to-grow-agentic-ai-for-finance/
- https://www.crunchbase.com/organization/auditoria
- https://tracxn.com/d/companies/auditoria.ai/__N-lab8ldFqKWr2XzhoWl-JGOLu4mznXGJawV2phRa9w
- https://www.globenewswire.com/news-release/2026/05/26/3300995/0/en/Auditoria-AI-introduces-Governed-Autonomy-for-Enterprise-Office-of-the-CFO-at-2026-Gartner-CFO-Symposium.html
- https://www.cfodive.com/news/auditoriaais-human-in-the-loop-option-targets-automation-wary-finance-technology/714914/
- https://marketplace.intacct.com/MPListing?lid=a2D0H00000gluj4UAA
- https://marketplace.workday.com/en-US/apps/413899/auditoriaai-smartcustomer-ar-collections/overview
- https://www.gartner.com/reviews/product/auditoria-smartvendor
- https://www.featuredcustomers.com/vendor/auditoriaai
- https://globalventuring.com/auditoria-organises-series-a-funding/
- https://finance.yahoo.com/news/auditoria-ai-launches-agentic-ai-150000218.html
