# PlanetScale

> Managed, horizontally sharded OLTP databases (MySQL via Vitess, now Postgres too) for companies whose transactional workload outgrew a single primary — sold on raw performance and operational discipline rather than serverless novelty.

- **Category:** data-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** February 2018, San Francisco (HQ at 535 Mission St) — Verified
- **Website / GitHub:** https://planetscale.com · https://github.com/planetscale (Vitess itself lives at https://github.com/vitessio/vitess, a CNCF graduated project)

## What they do
PlanetScale's core product is a managed database platform built on **Vitess**, the MySQL sharding/orchestration layer created at YouTube in 2010 to survive YouTube-scale write traffic. Vitess puts a query-routing proxy (vtgate) in front of many MySQL shards, so an application talks to what looks like one MySQL database while the platform handles sharding, failover, and connection pooling. On top of that PlanetScale added a developer workflow layer: **database branching** with **deploy requests** (git-style schema changes with review and non-blocking, revertible DDL), **Insights** (per-query production performance analytics with index/schema recommendations), and an API/CLI (`pscale`).

Two major expansions define the 2025–26 story. **PlanetScale Metal** (March 2025) runs databases on locally attached NVMe instead of network-attached storage (EBS), trading cloud-storage convenience for dramatically higher IOPS at lower cost — "unlimited I/O" priced by instance size, with HA via replication and automatic failover. **PlanetScale for Postgres** (announced July 2025, GA late 2025) brings the same operational model — Metal storage, branching workflow, Insights, a proprietary proxy layer with query buffering and PgBouncer pooling — to Postgres, with entry pricing down to a $50/month M-10 instance and Postgres 18 supported. Sharded Postgres is the stated next step via **Neki**, a Vitess-inspired Postgres sharding project under development — Verified (company blog, InfoQ). They also ship native vector search in their MySQL fork (Reported) and, as of January 2026, an official **MCP server** exposing orgs, databases, branches, schema, and Insights to AI tools, plus an open `database-skills` repo of skills for AI coding agents — Verified.

## Founders & origins
- **Jiten Vaidya** (co-founder, original CEO) and **Sugu Sougoumarane** (co-founder, CTO) — the YouTube/Google engineers who co-created and maintained Vitess; founded PlanetScale in 2018 to sell managed Vitess — Verified.
- **Sam Lambert** — ex-GitHub VP of Engineering; joined PlanetScale 2020 as Chief Product Officer, CEO since mid-2021 and the public face since — Verified.
- Sougoumarane left (sabbatical ~2022) and in 2025 joined **Supabase** to lead **Multigres** ("Vitess for Postgres") — a direct competitive wrinkle worth knowing — Verified (his own site, Changelog #651).

## Funding
- Seed: $3M, April 2018, led by SignalFire; angels incl. Steve Chen, Adam D'Angelo, Max Levchin — Verified
- Series A: $22M, May 2019, led by Andreessen Horowitz — Verified (TechCrunch)
- Series B: $30M, June 2021, led by Insight Partners — Verified
- Series C: $50M, November 2021, led by Kleiner Perkins — Verified
- Total: ~$105M — Verified. No rounds since; in March 2024 the company cut sales/marketing staff, killed the free Hobby tier, and publicly claimed a path to profitability with Deloitte-audited financials — Verified (The Register, company blog). No public valuation since 2021 — Not found in public sources.

## Evidence of real-world use
Strong, with first-person engineering case studies. **Intercom** migrated critical databases (including its AI infrastructure and Inbox) from Aurora, reporting 90%+ query-performance improvement and zero-downtime maintenance, and adopted Metal — Verified (Intercom's own blog + podcast, PlanetScale case study). **Cursor** and **Block/Cash App** are named as customers running "millions of queries per second on hundreds of terabytes" — Reported (company homepage/GA post; Cursor also confirmed independently in press coverage of its infra). Older public users include MyFitnessPal and Barstool Sports — Reported. Vitess itself (the OSS core) runs at Slack, GitHub, Shopify, and formerly YouTube — Verified, though that's adoption of the project, not the paid platform. Public pricing page, active changelog, and the 2024 profitability restructuring all signal a real commercial business rather than a growth-at-all-costs one.

## Relevance to agentic AI engineering
Three genuine hooks. First, **the OLTP layer under agent products**: Cursor — the flagship agentic-SWE company — runs on PlanetScale, and Intercom's AI systems do too; agent memory/state at scale is a sharded-OLTP problem, the operational side of what *Are We Ready For An Agent-Native Memory System?* asks about. Second, **schema changes as a governed agent workflow**: branching + deploy requests give coding agents a reviewable, revertible path to touch production schemas — governance-by-construction in the spirit of *Governance by Construction for Generalist Agents*, and exactly the guardrail long-horizon benchmarks like *SlopCodeBench* suggest agents need. Third, **the MCP server + database-skills repo** make the database an agent-legible tool (schema, branches, Insights as context) — the *Do Agents Need Semantic Metadata?* thesis applied to query optimization, e.g. their promoted pattern of agents reading Insights and opening index-improvement PRs on a schedule.

## Use cases & considerations
1. OLTP backend for an agent product expecting write-heavy growth (sessions, runs, memory records) without a future resharding rewrite.
2. Let coding agents propose schema/index changes via branches + MCP, with deploy requests as the human gate.
3. Migrate a struggling Aurora/RDS MySQL or Postgres workload to Metal for IOPS-bound performance (Intercom's path).

Considerations: no free tier (lowest entry $50/mo Metal Postgres, ~$39 base plans); MySQL side requires Vitess-compatible patterns (historically no foreign-key constraints, though support has been added — verify current status for your workload); Postgres sharding (Neki) is not shipped yet as of 2026-07-02; proxy/branching layer is proprietary even though Vitess is open. Competitors: Neon (now Databricks), Supabase (plus Multigres, led by PlanetScale's own co-founder), AWS Aurora/RDS, TiDB, Vitess self-managed. Open questions: Postgres-line traction vs. incumbents, and whether staying bootstrapped-profitable limits pace against heavily funded rivals.

## Sources
- https://planetscale.com/about
- https://planetscale.com/blog/planetscale-for-postgres-is-generally-available
- https://planetscale.com/blog/announcing-metal
- https://planetscale.com/blog/50-dollar-planetscale-metal-is-ga-for-postgres
- https://planetscale.com/blog/introducing-planetscale-mcp-server
- https://github.com/planetscale/database-skills
- https://planetscale.com/case-studies/intercom
- https://www.intercom.com/blog/evolving-intercoms-database-infrastructure-lessons-and-progress/
- https://techcrunch.com/2019/05/23/planetscale-vitess/
- https://techcrunch.com/2021/11/16/planetscale-raises-50m-series-c-as-its-enterprise-database-service-hits-general-availability/
- https://www.kleinerperkins.com/perspectives/planetscale-series-c/
- https://www.theregister.com/2024/03/11/planetscale_lays_off_staff_and/
- https://www.infoq.com/news/2025/10/planetscale-metal-postgres/
- https://sougou.io/about/
- https://changelog.com/podcast/651
