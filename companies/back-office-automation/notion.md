# Notion

> The block-based all-in-one workspace (docs + databases + wiki) that has repositioned itself as an "AI workspace" — its 3.0 agents treat your Notion pages and databases as both the tools they operate and the memory they persist.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2013, San Francisco (Verified — Wikipedia, Forbes, Contrary Research)
- **Website / GitHub:** https://www.notion.com · https://github.com/makenotion (incl. `notion-mcp-server`)

## What they do

Notion's core product is a workspace where everything is a composable **block**: documents, wikis, and relational **databases** (tables/boards/calendars with typed properties) live in one permission tree. Adjacent products: **Notion Calendar** (from the Cron acquisition), **Notion Mail**, and **Notion AI** (Q&A/search across the workspace plus connected tools). Revenue is per-seat SaaS with a public pricing page; AI is now bundled into Business/Enterprise plans rather than sold as a separate add-on.

The agent story is **Notion 3.0** (launched September 18, 2025): agents that can do anything a user can in the workspace — create docs, build and bulk-edit databases (hundreds of pages at once), and run multi-step workflows for 20+ minutes, pulling context from Slack, Google Drive, GitHub and the web within the user's permissions. Notably, agent memory is implemented *as Notion pages and databases* — the workspace is the persistence layer. **Custom Agents** (February 2026) run autonomously on schedules and triggers as team-level bots; an April 2026 update cut agent run costs 35–50% and added Salesforce/Box connectors plus **Workers**, a hosted runtime for custom code extending Notion without your own servers (Verified — Notion release notes and blog; Reported for cost-reduction percentages — third-party coverage).

For engineers the integration surfaces are the **public REST API**, webhook triggers, Workers, and the **hosted Notion MCP server** (OAuth, works with Claude Code, Cursor, VS Code, ChatGPT) — one of the most commonly wired-up MCP endpoints, alongside several community MCP implementations on GitHub (Verified — developers.notion.com, makenotion GitHub).

## Founders & origins

**Ivan Zhao** (CEO) and **Simon Last** founded Notion in 2013; Zhao calls Last his product co-founder and **Akshay Kothari** (ex-LinkedIn, Pulse co-founder, joined later as COO) his business co-founder (Verified — Forbes, Sequoia, Wikipedia; Wikipedia also lists early team members Chris Prucha, Jessica Lam, and Toby Schachman as co-founders — Reported). Origin story is well documented: after three years the founders scrapped the codebase, laid off staff, moved to Kyoto to cut burn, and Zhao borrowed $150K from his mother; Notion 1.0 shipped August 2016, and a March 2018 WSJ review of 2.0 ignited growth (Verified — multiple retellings incl. Forbes/Contrary).

## Funding

- Seed ~$2M (2013) (Reported)
- ~$10M round, April/July 2019, at $800M valuation (Reported — sources conflict between $10M and $18.2M; databases vary)
- $50M led by **Index Ventures**, April 2020, at $2B (Verified — TechCrunch, Forbes, Axios)
- $275M led by **Coatue** and **Sequoia**, October 2021, at $10B with ~20M users (Verified)
- ~$270M **tender offer** (secondary, not primary) at $11B, January 2026 (Reported — press citing company disclosure)

Total primary raised: roughly $330–420M depending on database (Reported). Notably low dilution; Forbes estimates Zhao still owns ~30%.

## Evidence of real-world use

Strong. ~$500M ARR as of September 2025 (Verified — CNBC), 100M+ users, ~4M paying customers, and company-reported claims that >50% of ARR comes from AI-enabled customers (Reported). Documented case studies with substance, not just logos: **OpenAI** (GTM-enablement hub; also the original API partner powering Notion AI), **Ramp** (~70% productivity-tool cost reduction, now building agents on Notion), **Figma** (onboarding), plus Nvidia, Cursor, and Vercel named as customers (Verified — notion.com/customers; the Ramp relationship is corroborated by Ramp's own reciprocal case study). Massive template/creator ecosystem and community are independent adoption signals.

## Relevance to agentic AI engineering

Three genuine touchpoints. (1) **Agent memory as a product**: using workspace pages/databases as agent state is a shipping, at-scale answer to the questions in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation* and *Are We Ready For An Agent-Native Memory System?* — a human-readable, permissioned memory substrate rather than an opaque vector store. (2) **Tool-use target**: the hosted MCP server makes Notion a standard read/write tool for external agents, an instance of the trajectory in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*; its permission-scoped, OAuth-bound design is a practical case of *Governance by Construction for Generalist Agents*. (3) **Back-office substrate**: Custom Agents + database triggers + Workers is effectively a low-code agent-orchestration platform where the database doubles as an auditable work queue — relevant to anyone building intake/approval/audit workflows.

## Use cases & considerations

**Use cases:** (1) use a Notion database as the human-review queue and audit trail for an external agent (e.g., a job-packet or invoice auditor writing findings via API/MCP); (2) wire the hosted MCP server into Claude Code/Cursor so agents read specs and write status docs; (3) scheduled Custom Agents for recurring ops reports (meeting-notes rollups, vendor tracking); (4) Workers + webhooks for lightweight automation without separate infra.

**Considerations:** the API is rate-limited and databases are not a real transactional store — heavy automation hits scale walls; agent behavior is only as governable as your (often messy) workspace permission tree; workspace lock-in is real once agents' memory *is* your Notion. Third-party reviews of 3.0 agents are mixed on reliability for long workflows. Competitors: Microsoft (Loop/Copilot), Atlassian (Confluence/Rovo), Airtable, ClickUp, Coda (Grammarly), Glean on the search side. Open question: whether Notion agents stay a feature for Notion-native teams or become a credible orchestration layer for external systems.

## Sources

- https://en.wikipedia.org/wiki/Notion_(productivity_software)
- https://www.forbes.com/profile/ivan-zhao/
- https://research.contrary.com/company/notion
- https://sequoiacap.com/article/notion-spotlight/
- https://techcrunch.com/2020/04/01/notion-hits-2-billion-valuation-in-new-raise/
- https://www.forbes.com/sites/davidjeans/2020/04/01/buzzy-work-app-notion-hits-2-billion-valuation/
- https://www.cnbc.com/2025/09/18/notion-launches-ai-agent-as-it-crosses-500-million-in-annual-revenue.html
- https://www.notion.com/blog/introducing-notion-3-0
- https://www.notion.com/releases/2025-09-18
- https://www.notion.com/product/agents
- https://www.notion.com/customers/openai
- https://www.notion.com/customers/ramp
- https://ramp.com/customers/notion
- https://developers.notion.com/docs/mcp
- https://www.notion.com/blog/notions-hosted-mcp-server-an-inside-look
- https://github.com/makenotion/notion-mcp-server
- https://sacra.com/c/notion/
