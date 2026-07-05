# Atlassian

> The Jira/Confluence company, now selling an AI layer (Rovo) that turns two decades of accumulated work data — tickets, docs, code, goals — into context and execution surface for agents.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** gold
- **Founded:** 2002, Sydney, Australia (Verified — Wikipedia, company history, press)
- **Website / GitHub:** https://www.atlassian.com · https://github.com/atlassian (incl. `atlassian-mcp-server`)

## What they do

Atlassian sells collaboration and SDLC software: **Jira** (issue tracking/project management), **Confluence** (wiki/docs), **Jira Service Management** (ITSM), **Bitbucket** (git hosting/CI), **Trello**, **Loom** (async video), and **Compass** (service catalog). Public company (NASDAQ: TEAM), 300,000+ customers, $5.2B revenue in FY2025 (Verified — Q4 FY25 shareholder letter / Businesswire).

The AI story is **Rovo**, layered on the **Teamwork Graph** — Atlassian's unified index of work items, pages, code, and goals across its products plus third-party connectors. Rovo ships as Search (cross-tool enterprise search), Chat, and **Agents**: configurable AI teammates that can be triggered in Chat, automation rules, or inline in Jira/Confluence. Core Rovo is bundled free with paid Jira/Confluence plans (usage metered by credits), which drove reported 2.3M AI monthly active users by mid-2025 (Verified — FY25 results). At Team '26 (May 2026), **Rovo Studio** hit GA (no-code agent building), agents became assignable to Jira work items with full audit logging, and a "Max" multistep-reasoning mode entered early access (Reported — SiliconANGLE coverage of Team '26).

For engineers, the concrete integration surfaces are: (1) the **Rovo/Atlassian Remote MCP Server** — official, Cloudflare-hosted, OAuth 2.1, connecting Jira/Confluence/JSM/Bitbucket/Compass to Claude, Cursor, VS Code, etc.; beta May 2025 with Claude as first partner, GA ~February 2026 (Verified — Atlassian blog, GitHub repo, third-party coverage); (2) **Rovo Dev**, a coding agent (CLI + IDE + in-Jira) priced at $20/developer/month that works against Jira acceptance criteria and, via the new Code Intelligence early access, runs intent queries across repos+Jira+Confluence together (Verified — product page; pricing Reported — third-party pricing trackers); (3) **Forge**, the app platform, which now has a `rovo-agent` module for shipping custom agents into the Marketplace.

## Founders & origins

**Mike Cannon-Brookes** and **Scott Farquhar**, University of New South Wales classmates, founded Atlassian in 2002 on ~$10,000 of credit-card debt, famously bootstrapping with no salespeople (Verified — Wikipedia, SmartCompany, many retellings). Farquhar stepped down as co-CEO in 2024; Cannon-Brookes is sole CEO (Verified — press, Wikipedia).

## Funding

Bootstrapped ~8 years. **$60M secondary from Accel (2010)**; **$150M secondary led by T. Rowe Price (2014)**; **IPO December 10, 2015** on NASDAQ (TEAM) at a ~$4.37B market cap (all Verified — Wikipedia, contemporaneous press). Now funded by revenue; market cap fluctuates in the tens of billions. Recent M&A shows the AI pivot: **Loom** ($975M, 2023 — Reported), **The Browser Company** (Arc/Dia AI browser, ~$610M, Sept 2025 — Verified), **DX** (developer-productivity analytics, $1B cash+stock, closed Nov 2025, largest acquisition ever — Verified — TechCrunch, SEC filing, Businesswire).

## Evidence of real-world use

The base products are among the most-deployed software in the industry — 300,000+ customers, ~52,000 with >$10K cloud ARR (Verified — SEC/earnings). For the AI layer specifically: 2.3M AI monthly active users (company-reported metric; bundling inflates it — treat as adoption of availability, not necessarily of value). Independent signals: the MCP server is in Docker's MCP Catalog, has an active public GitHub repo, and third-party writeups (Medium, MCP tooling vendors, Portkey docs) document actual integration patterns. Anthropic chose Atlassian as a launch partner for remote MCP in Claude — meaningful third-party validation. Rovo Dev's public per-seat pricing indicates a real commercial product rather than a demo.

## Relevance to agentic AI engineering

Atlassian sits at two points in the agent stack. First, **the system-of-record tool that agents call**: Jira/Confluence via MCP is one of the most common real-world tool-use targets, an instance of the multi-tool orchestration trajectory in *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*; its OAuth-scoped, permission-respecting, audit-logged design is a production example of the concerns in *Governance by Construction for Generalist Agents*. Second, **agentic SDLC**: Rovo Dev working from Jira acceptance criteria is the requirements-to-code pattern of *REAgent: Requirement-Driven LLM Agents for Software Issue Resolution* and the plan-compliance question in *From Plan to Action: How Well Do Agents Follow the Plan?*; whether ticket-driven agents actually deliver features is exactly what *FeatureBench* and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* probe. The Teamwork Graph as shared organizational context parallels *Graph-based Agent Memory* and *Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents*. For back-office builders: JSM + Rovo agents is a credible substrate for human-approved workflows (intake queues, approval gates, audit trails) without building your own.

## Use cases & considerations

**Use cases:** (1) wire the Remote MCP Server into Claude/Cursor so coding and ops agents read/write tickets and docs directly; (2) use Jira Service Management as the human-approval queue for back-office agents (e.g., a sub-bill intake or job-packet audit agent filing work items for review); (3) Rovo Studio agents over Confluence for internal knowledge answers; (4) Rovo Dev where the team already lives in Jira/Bitbucket.

**Considerations:** everything assumes you're inside the Atlassian cloud ecosystem — deep lock-in, and the credit-based metering makes heavy agent use hard to cost-predict. Rovo agent quality reports are mixed (third-party analyses note real limitations vs. the marketing). Competitors: Microsoft (GitHub Copilot + Azure DevOps + M365 Copilot), Linear, Notion, Asana/monday.com on work management; Cursor/Claude Code/Windsurf against Rovo Dev; Glean against Rovo Search. Open questions: whether Rovo Dev can compete with frontier coding agents rather than winning purely on Jira adjacency, and how the Browser Company and DX acquisitions integrate.

## Sources

- https://www.atlassian.com/software/rovo
- https://www.atlassian.com/software/rovo-dev
- https://www.atlassian.com/platform/remote-mcp-server
- https://www.atlassian.com/blog/announcements/remote-mcp-server
- https://github.com/atlassian/atlassian-mcp-server
- https://support.atlassian.com/rovo/docs/agents/
- https://developer.atlassian.com/platform/forge/manifest-reference/modules/rovo-agent/
- https://siliconangle.com/2026/05/06/atlassian-opens-teamwork-graph-pushes-rovo-agentic-execution-team-26/
- https://www.businesswire.com/news/home/20250807057757/en/Atlassian-Announces-Fourth-Quarter-and-Fiscal-Year-2025-Results
- https://www.sec.gov/Archives/edgar/data/0001650372/000165037225000028/ex991q4fy25.htm
- https://techcrunch.com/2025/09/18/atlassian-acquires-dx-a-developer-productivity-platform-for-1b/
- https://www.businesswire.com/news/home/20251110683591/en/Atlassian-Completes-Acquisition-of-DX-Advancing-Engineering-Intelligence-for-Enterprises
- https://en.wikipedia.org/wiki/Atlassian
- https://www.smartcompany.com.au/startupsmart/atlassian-story-how-two-indebted-suburban-guys-from-sydney-created-a-us-3-billion-tech-juggernaut/
- https://www.docker.com/blog/atlassian-remote-mcp-server-getting-started-with-docker/
- https://bestagenthub.com/tools/atlassian-rovo
- https://landing.kvasar.tech/articles/atlassian-s-rovo-agents-dissected/
