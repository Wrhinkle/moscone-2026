# Ramp

> Corporate cards, expense management, bill pay, and procurement in one platform — now shipping production AI agents that approve expenses, enforce policy, and code transactions to the ERP.

- **Category:** fintech-payments
- **AIEWF 2026 tier:** supporting
- **Founded:** March 2019, New York City; publicly launched February 2020 (Verified — Wikipedia, Forbes, Contrary Research)
- **Website / GitHub:** https://ramp.com · https://github.com/ramp-public/ramp-mcp · https://builders.ramp.com

## What they do

Ramp is a finance operations platform anchored on a corporate charge card. Around the card sits expense management (receipt capture, categorization, policy enforcement), accounts payable/bill pay, procurement (intake, vendor onboarding, purchase orders), travel, and treasury — all syncing into ERPs like NetSuite and QuickBooks. The wedge is that Ramp makes interchange revenue on card spend, so the software layer is aggressively automated and priced to displace Concur/Expensify-era tooling. Scale as of mid-2026: ~$1B annualized revenue (Verified — company + TechCrunch, Aug 2025) and 25,000+ business customers in 2024, with the company claiming 40,000+ since (customer count beyond 2024 is Reported — company figures).

The AIEWF-relevant layer is **Ramp Agents**, launched in tranches: **Agents for Controllers** (July 2025) — autonomous expense approval/rejection with rationale, policy enforcement, and fraud/anomaly scanning, built on OpenAI reasoning models; **Agents for AP** (October 2025) — invoice extraction, ERP coding, and payment prep; **procurement agents** (2026) for intake and vendor onboarding; plus an **Applied AI Solutions** offering (June 2026) helping enterprises deploy agents across finance ops. Company-claimed metrics: 99% policy-enforcement accuracy and 15x more out-of-policy spend caught than non-AI baselines (Reported — Ramp's own PR; treat as marketing until independently benchmarked). Developer surface: a public Developer API and an open-source **MCP server** (`ramp-public/ramp-mcp`) that ETLs Ramp spend data into an in-memory SQLite database so an LLM can run natural-language spend analysis; there is also a hosted remote MCP in their API docs (Verified — GitHub + docs.ramp.com + builders.ramp.com writeup).

## Founders & origins

**Eric Glyman**, **Karim Atiyeh**, and **Gene Lee** (Verified). Glyman and Atiyeh met at Harvard and previously founded **Paribus** (automated price-drop refunds), acquired by Capital One in 2016. They interviewed ~100 finance leaders before building Ramp's card, positioning it against points-driven cards as "the card that helps you spend less." In June 2026, Atiyeh (previously CTO) was elevated to **co-CEO** alongside Glyman, with Rahul Sengottuvelu reported as the new CTO (Reported — American Banker, Banking Dive).

## Funding

Aggressive and unusually fast recent markup curve (Verified via Wikipedia, TechCrunch, PRNewswire unless noted):

- Series A $15M (Feb 2020, Founders Fund) → Series B $115M (Apr 2021, $1.6B) → Series C $300M (Aug 2021, $3.9B) → $8.1B peak (early 2022) → Series D $300M (Aug 2023, **down round** to $5.8B) → Series D-2 $150M (Jun 2024, $7.65B, Khosla + Founders Fund)
- 2025: $13B secondary (Mar) → Series E $200M at $16B (Jun) → E-2 $500M at $22.5B (Jul) → $300M primary at **$32B** (Nov, Lightspeed)
- Jun 2026: **Series F $750M at $44B** — ICONIQ Growth, GIC, Ontario Teachers' (Verified — TechCrunch, PRNewswire)
- Total raised: ~$3.2B (Reported — Tracxn)

TechCrunch explicitly framed the Series F as investors paying up for "fintechs with an AI story" — worth remembering when weighing the valuation against the agent products' maturity.

## Evidence of real-world use

Strong. This is a high-volume production payments business, not a demo: $1B annualized revenue implies tens of billions in processed spend. Documented named customers with quantified outcomes (Verified — Ramp case studies, so favorable selection but specific): **Notion** (consolidated Expensify + separate card + travel onto Ramp), **Snapdocs** (three systems → one; monthly reconciliation 5–6 hours → under 30 minutes), **Zola** (~50% faster month-end close), **Construction One** (reconciliation 40 → 10 hours/month), **ABB Optical Group** (transaction-level compliance visibility). LangChain publishes an independent case study on Ramp's internal "Tour Guide" agent (LangGraph-based in-product copilot). The MCP server is real and third parties (Composio, Merge) ship Ramp connectors for agent frameworks. Independent verification of the agents' 99%-accuracy claims: Not found in public sources.

## Relevance to agentic AI engineering

Ramp is one of the clearest live examples of agents executing consequential, irreversible financial actions under policy constraints — exactly the territory of *Governance by Construction for Generalist Agents* and *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration* (approve → code → sync → pay is a multi-tool workflow with audit requirements). Its agents' need to retain vendor history, policy precedent, and past approval rationale maps to *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*. The ramp-mcp ETL-to-SQLite pattern is a pragmatic answer to the retrieval questions in *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*. For back-office agent builders, Ramp is both a design reference and a data source via MCP.

## Use cases & considerations

Use cases: (1) MCP-based spend-analysis agents over a company's real card/AP data with zero scraping; (2) studying their approval-agent UX (autonomous approval for low-risk, rationale-plus-recommendation for the rest) as a pattern for any human-in-the-loop agent — directly relevant to a construction back office triaging sub bills and job-cost coding; (3) treating Agents for AP as the buy-side benchmark before building invoice automation yourself.

Considerations: deep platform lock-in (card + AP + procurement + ERP sync is sticky by design); agents are proprietary and tied to Ramp's rails; accuracy claims are vendor-reported; interchange-funded economics mean incentives favor card spend. Competitors: **Brex**, **Navan**, **Mercury**, **Bill.com**, **SAP Concur**, **Expensify**, **Airbase/Paylocity**. Open questions: whether the $44B valuation prices in agent adoption that hasn't been independently measured, and how OpenAI-model dependence affects the agents' reliability envelope.

## Sources

- https://en.wikipedia.org/wiki/Ramp_(company)
- https://techcrunch.com/2026/06/04/ramp-raises-750m-at-44b-valuation-as-investors-hunger-for-fintechs-with-an-ai-story/
- https://techcrunch.com/2025/11/17/ramp-hits-32b-valuation-just-three-months-after-hitting-22-5b/
- https://www.prnewswire.com/news-releases/ramp-raises-series-f-at-44-billion-valuation-302791103.html
- https://www.prnewswire.com/news-releases/ramp-introduces-ai-agents-to-automate-finance-operations-302502154.html
- https://www.prnewswire.com/news-releases/ramp-launches-agents-for-ap-to-automate-accounts-payable-302576975.html
- https://www.prnewswire.com/news-releases/ramp-launches-applied-ai-solutions-helping-enterprises-deploy-ai-agents-across-finance-operations-302796179.html
- https://ramp.com/blog/ramp-agents-announcement
- https://ramp.com/intelligence
- https://ramp.com/blog/expense-management-case-studies
- https://www.accountingtoday.com/news/ramp-releases-ai-agents-for-expense-approvals-analytics
- https://www.americanbanker.com/news/ramp-ceo-invites-co-founder-karim-atiyeh-to-share-top-job
- https://www.bankingdive.com/news/ramp-names-karim-atiyeh-co-ceo-glyman-cto-Rahul-Sengottuvelu/824229/
- https://github.com/ramp-public/ramp-mcp
- https://builders.ramp.com/post/ramp-mcp
- https://docs.ramp.com/developer-api/v1/guides/ramp-mcp-remote
- https://www.langchain.com/breakoutagents/ramp
- https://research.contrary.com/company/ramp
- https://tracxn.com/d/companies/ramp/__mMFluFx9yKyt9DXRq5KzSGK2frbsYq5y9jc9XK9-g9E/funding-and-investors
