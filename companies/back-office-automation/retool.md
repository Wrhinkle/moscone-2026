# Retool

> Low-code platform for building internal business software — admin panels, ops dashboards, approval workflows — now extended with hourly-priced AI agents that act through the same database/API connectors the apps use.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2017, San Francisco; Y Combinator W17, pivoted from a UK payments startup ("Cashew") (Verified — Retool blog, First Round, Contrary Research)
- **Website / GitHub:** https://retool.com · https://github.com/tryretool (retool-onpremise, retool-helm, terraform-provider-retool)

## What they do

Retool's core product is a drag-and-drop builder for internal tools: you compose UIs from ~100 prebuilt components (tables, forms, charts), wire them to your own Postgres/MySQL/Mongo/REST/GraphQL/gRPC resources, and drop JavaScript anywhere the visual layer runs out. The pitch in engineer terms: the fastest path from "ops team needs a refund/KYC/inventory panel" to a deployed CRUD app with auth, audit logs, and permissions, without writing a frontend. Around that sit **Workflows** (cron/webhook-triggered automation, Zapier-shaped but code-first), **Retool Database** (managed Postgres), Mobile, and a self-hosted distribution deployed via Docker/Kubernetes/Helm for enterprises that can't send data to Retool's cloud (Verified — docs, GitHub).

The 2025 pivot into AI is what makes them interesting to this landscape. **AppGen** (April 2025) generates full Retool apps from natural language. **Retool Agents** (announced May 28, 2025, public beta) is a full-stack toolkit for building, deploying, and observing LLM agents that use Retool's existing resource connectors as their tool layer — the reasoning is the model's, the actions are the same integrations powering the internal apps. Two distinctive choices: an observability surface for watching/managing agents mid-run, and pricing **by the hour of agent work** (LLM costs bundled into the hourly rate) rather than per token, seat, or call — deliberately framed as paying for labor (Verified — Businesswire, Retool blog, docs). Retool claims 100M+ cumulative hours of work automated on the platform (Reported — company announcement).

## Founders & origins

**David Hsu**, founder and CEO; CS + Philosophy at Oxford (Verified — Sequoia, Forbes, multiple profiles). Origin: his YC W17 fintech (a UK Venmo competitor) was burning ~$1k/day; weeks before Demo Day he pivoted, realizing the internal fraud/KYC/AML tooling they'd built for themselves was the real product. Retool famously reached ~$2M ARR before a public launch by selling directly to developers (Reported — First Round podcast, KITRUM profile). Hsu is consistently described as the sole founder; no cofounder found in public sources.

## Funding

- **Series A:** led by Sequoia, ~2019 (Reported — Contrary Research/Tracxn; amount varies by source)
- **Series B:** $50M, October 2020, Sequoia (Verified — multiple databases)
- **Series C (first tranche):** $20M, December 2021, Sequoia, at $1.85B (Reported — Tracxn/press)
- **Series C extension:** $45M, July 2022, at **$3.2B**, Sequoia plus Patrick and John Collison, Nat Friedman, Elad Gil, BOND (Verified — company newsroom, Sacra, press)
- **Total raised:** ~$141M–$165M — sources disagree (Sacra says ~$141M, Tracxn ~$165M); exact total Unverified
- **Revenue:** ~$120M ARR as of October 2025, up from ~$90M at end of 2024 (Reported — Sacra)

## Evidence of real-world use

Strong and documented, not just logos. **DoorDash** has a published case study: internal tool build time cut from 1–2 months to hours, 40+ operational tools running in Retool (Verified — retool.com/customers/doordash). **Amazon/AWS, Databricks, Brex, Coinbase, NBC, the NFL, Mercedes-Benz, Lyft, Plaid, Ramp** appear as customers across the customers page, press, and Contrary Research; the "100M hours automated" figure is attributed to workloads including AWS and Databricks (Reported). Public self-serve pricing, a large community forum, an active GitHub org (self-hosted repos updated as recently as July 2026), and third-party ecosystems (consultancies, comparison sites) all indicate genuine commercial breadth. Note the AI-agent claims are newer and thinner than the internal-tools evidence — Agents-specific named case studies were still mostly Retool's own blog content as of July 2026.

## Relevance to agentic AI engineering

Retool is a bet that the agent control plane belongs where the company's data connections and permissions already live. Its connector catalog becomes the agent's tool inventory — directly the multi-tool orchestration problem in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*. The observe-and-manage-agents-mid-run surface and permissioned, audited action layer are a commercial instance of the guardrails argument in *Governance by Construction for Generalist Agents*, and measuring "hours of productive agent work" raises exactly the evaluation questions in *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*. For back-office builders (intake triage, invoice/sub-bill review queues, packet-readiness dashboards), Retool covers the human-in-the-loop UI half that pure agent frameworks lack: the review screen an agent escalates to is a Retool app.

## Use cases & considerations

**Use cases:** (1) human-review consoles for agent pipelines — approval queues, exception handling, audit views; (2) agents that act on internal systems (refunds, record updates, notifications) using connectors ops teams already trust; (3) replacing brittle spreadsheet-plus-email back-office processes with Workflows plus an agent for the judgment step; (4) fast admin panels over an existing database.

**Considerations:** apps are stored as proprietary JSON, not exportable code — lock-in is real; per-seat pricing compounds at scale and self-hosting is enterprise-tier. Hourly agent pricing is legible but hard to compare against token-priced alternatives. Competitors: Appsmith, ToolJet, Budibase, Windmill, Superblocks (internal tools); Zapier Agents, n8n, Gumloop, and custom LangChain/Temporal stacks (agents). Open question: whether a UI-builder company can win agent infrastructure against agent-native platforms.

## Sources

- https://retool.com/blog/retool-founding-story-david-hsu
- https://retool.com/agents
- https://retool.com/blog/retool-automates-100-million-hours-of-work-launching-agents
- https://retool.com/blog/cost-of-ai-agents-hourly-pricing-model
- https://retool.com/customers/doordash
- https://retool.com/newsroom/series-c
- https://retool.com/pricing
- https://docs.retool.com/support/billing-usage/agents
- https://www.businesswire.com/news/home/20250528644298/en/
- https://sacra.com/c/retool/
- https://research.contrary.com/company/retool
- https://tracxn.com/d/companies/retool/__3Qw2mDrisfHcLzB8sG6xEXwD7lueXw7kuVlus34H2KY
- https://github.com/tryretool
- https://review.firstround.com/podcast/how-retool-reached-2m-in-arr-before-launch-by-focusing-on-developers-david-hsu/
- https://sequoiacap.com/article/david-hsu-retool-spotlight/
