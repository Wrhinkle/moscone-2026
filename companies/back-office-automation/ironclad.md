# Ironclad

> Contract lifecycle management (CLM) platform — legal teams design contract workflows, store agreements as structured data, and increasingly delegate intake, review, and redlining to a family of purpose-built AI agents ("Jurist").

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2014, San Francisco; Y Combinator S15 (Verified — Wikipedia, YC blog, Contrary Research)
- **Website / GitHub:** https://ironcladapp.com · no significant public OSS presence

## What they do

Ironclad is SaaS for the full contract lifecycle. The classic platform has three pillars: **Workflow Designer** (no-code builder for intake/approval/signature flows — sales, procurement, HR, NDAs), a **Repository** that stores executed agreements as searchable digital records with AI-extracted metadata (the system can detect ~190+ contract elements and flag clauses that diverge from the negotiated agreement — Reported, Forbes/press), and an **Editor** with AI-assisted redlining. The AI layer was built early on OpenAI models — Ironclad was a published GPT-3/GPT-4 launch partner for its **AI Assist** redlining feature (Verified — Wikipedia, OpenAI case study, IntuitionLabs deep dive). Clickwrap/embedded-consent came via the PactSafe acquisition (Reported — press, 2021).

Since 2024 the strategic bet is **Jurist**, an agentic AI legal assistant comprising Manager, Drafting, Editing, Review, and Research agents that operate against org-specific **Playbooks** (codified negotiation positions). On November 13, 2025 Ironclad announced its "next wave" of agents in beta: an **Intake Agent** (extracts metadata from third-party paper and auto-populates launch forms), a **Redlining Agent** (flags missing clauses, risky terms, and compliance gaps against playbooks), and **Conversational Search** over the repository (Verified — company announcement, PRNewswire). In engineer terms: a domain-constrained document agent stack — schema extraction on intake, policy-conditioned generation for redlines, retrieval over a structured contract store — sold as an integrated suite rather than APIs.

## Founders & origins

**Jason Boehmig** (CEO 2014–2025), a former corporate attorney at Fenwick & West, and **Cai GoGwilt** (CTO, later Chief Architect), a former Palantir software engineer (Verified — YC blog, Contrary Research, Epicenter profile). Origin: Boehmig's deal work at Fenwick exposed how manual contract processes were; they launched through YC S15 with ~200 beta companies (Reported — YC/Contrary). Leadership shifted notably: in April/May 2025 **Dan Springer**, former DocuSign CEO, took over as CEO with Boehmig moving to executive chairman (Verified — Bloomberg Law, Law360, company blog); in June 2026 Boehmig joined OpenAI to lead legal-sector product development (Verified — LawSites, Global Legal Post). Current CTO is Sunita Verma (Reported — Nov 2025 launch press).

## Funding

- **Series A:** $8M, 2017, Accel (Reported — Contrary/Clay)
- **Series B:** $23M, 2018, Sequoia (Reported)
- **Series C:** $50M, 2019 (Reported)
- **Series D:** $100M, 2020–21, ~$1B valuation (Reported)
- **Series E:** $150M, Jan 2022, led by Franklin Templeton with Accel, Sequoia, Emergence, Bond — 100% insider round, **$3.2B valuation** (Verified — Forbes, multiple databases)
- **Total raised:** ~$333M over 7 rounds (Reported — Tracxn/Clay). No raise found after Jan 2022 in public sources.

## Evidence of real-world use

Strong. **2,000+ customers** (Reported — company/press), with named, documented usage rather than just logos: **L'Oréal** (published webinar/case study on AI contract review with a named associate GC), **Mastercard, Reddit, Dropbox, Snap, OpenAI** itself (Verified across press and company materials). OpenAI's own case study documents AI Assist in production. Claimed metrics: first-pass review cut from ~40 minutes to ~2 (Reported — company); nearly one-third of new customers adopting Jurist with ~6x YoY Jurist revenue growth (Reported — company via press). Third-party revenue estimate ~$140M ARR in 2024 (Unverified — GetLatka only). A decade of operation, a hired-in public-company CEO, and an 11-year customer base make this one of the more de-risked "AI back office" vendors at the conference.

## Relevance to agentic AI engineering

Ironclad is a live case study in shipping constrained document agents into a risk-averse back office. Its Playbook-governed Redlining Agent is essentially policy-as-guardrail — the pattern argued for in *Governance by Construction for Generalist Agents*, applied to legal text instead of tool calls. The Repository-as-structured-record design (agents read/write typed metadata, not raw PDFs) maps to the retrieval questions in *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* and the durable-state concerns of *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*. The multi-agent Jurist decomposition (intake → review → redline → search) echoes *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. For a construction back office, contracts are the substrate: subcontractor agreements, change orders, and insurance scope docs are exactly the intake/readiness-audit problem the Job Packet Readiness Auditor pattern addresses.

## Use cases & considerations

**Use cases:** (1) intake + metadata extraction for third-party paper (sub agreements, vendor MSAs) feeding downstream agents; (2) playbook-driven first-pass redlining before human counsel; (3) conversational search over an executed-contract repository ("which subs have indemnity clause X?"); (4) clickwrap for embedded consent flows.

**Considerations:** enterprise, quote-based pricing (no public pricing page) — mid-market/SMB fit is questionable; it's a suite, not an API platform, so builders integrate *around* it rather than on it; repository lock-in is real. Competitors: Icertis, Agiloft, LinkSquares, Sirion, Evisort (now Workday), DocuSign CLM/IAM, and Harvey pressing in from the legal-AI side. Open questions: how it navigates its awkward OpenAI relationship (customer, model dependency, and now employer of its founder as OpenAI enters legaltech), and whether frontier-model contract review commoditizes the AI layer, leaving workflow + repository as the moat.

## Sources

- https://ironcladapp.com/
- https://en.wikipedia.org/wiki/Ironclad_(software)
- https://research.contrary.com/company/ironclad
- https://www.ycombinator.com/blog/qa-with-cai-gogwilt-and-jason-boehmig-cofounders-of-ironclad/
- https://www.forbes.com/sites/kenrickcai/2022/01/18/ironclad-series-e-3-billion-valuation/
- https://ironcladapp.com/resources/articles/ai-agentic-launch
- https://www.prnewswire.com/news-releases/introducing-ironclads-next-wave-of-ai-agents-every-agreement-is-now-an-asset-302614708.html
- https://ironcladapp.com/product/ai-assistant/legal
- https://ironcladapp.com/journal/webinars/how-loreal-performs-ai-contract-management/
- https://openai.com/index/ironclad/
- https://www.lawnext.com/2026/06/ironclad-founder-jason-boehmig-joins-openai-to-develop-products-for-the-legal-sector.html
- https://news.bloomberglaw.com/legal-ops-and-tech/ironclad-names-former-docusign-ceo-dan-springer-as-new-leader
- https://ironcladapp.com/resources/articles/ironclad-ceo-dan-springer
- https://intuitionlabs.ai/articles/ironclad-ai-contract-management-capabilities
- https://www.clay.com/dossier/ironclad-funding
