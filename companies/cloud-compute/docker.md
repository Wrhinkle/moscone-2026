# Docker

> The default container toolchain for developers — Docker Desktop, Docker Hub, and Engine — now repositioning as the packaging, runtime, and security layer for AI agents and MCP tools.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** platinum
- **Founded:** 2008 as dotCloud (Paris); incorporated in the US 2010, went through Y Combinator S10; renamed Docker October 2013 (Verified)
- **Website / GitHub:** https://www.docker.com · https://github.com/docker · https://github.com/moby/moby · https://docs.docker.com/ai/

## What they do
Docker's core products are: **Docker Engine/CLI** (open source, the de facto standard for building and running OCI containers), **Docker Desktop** (the commercial macOS/Windows/Linux dev environment — this is the paid product, licensed per-seat for companies over 250 employees/$10M revenue), **Docker Hub** (the world's largest container registry), plus **Docker Build Cloud** (remote builds), **Docker Scout** (supply-chain/CVE analysis), **Testcontainers** (acquired AtomicJar, Dec 2023 — throwaway real dependencies in integration tests), and **Docker Hardened Images** (minimal, patched base images, with a free tier announced Jan 2026).

Since 2025 Docker has built an explicit AI-agent stack on the same primitives: **Docker Model Runner** (pull and run LLMs locally as OCI artifacts, GPU-accelerated, OpenAI-compatible API), the **MCP Catalog and Toolkit** (300+ verified MCP servers — GitHub, Stripe, Elastic, Browserbase, ElevenLabs, etc. — packaged as signed container images with provenance and one-click install from Docker Desktop), the open-source **MCP Gateway** (a single enforcement point between agent clients and MCP servers: containers run isolated with restricted network/privileges, interceptors can verify image signatures, scan payloads for secrets, and log every tool call), **cagent** (open-source declarative YAML multi-agent runtime supporting OpenAI/Anthropic/Gemini/Model Runner, distributable via registries), **Docker Sandboxes** (run coding agents like Claude Code in isolation from host credentials and filesystem), and **Docker AI Governance** for centralized policy over what agents can execute, reach, and call. A partnership with E2B (announced 2025–26) extends this to cloud sandboxes.

## Founders & origins
**Solomon Hykes, Kamel Founadi, and Sébastien Pahl** founded dotCloud, a PaaS; Hykes open-sourced its internal container tooling as Docker at PyCon in March 2013, and the company pivoted entirely (Verified — Wikipedia, TechCrunch, Forbes). Hykes left in 2018 (he later founded Dagger). Leadership since: Ben Golub, Steve Singh, Rob Bearden, then Scott Johnston (CEO 2019–2025), who led the pivotal 2019 restructuring — Docker Enterprise sold to Mirantis, company refocused on developer tooling. **Don Johnson** (founder of Oracle Cloud Infrastructure, ex-AWS) became CEO on Feb 12, 2025 (Verified). Analysts have speculated the CEO swap positions the company for a sale (Reported — TechTarget).

## Funding
- 2019 relaunch round: $35M from Benchmark and Insight Partners (Verified)
- Series B, Mar 2021: $23M led by Tribe Capital (Reported)
- Series C, Mar 2022: $105M led by Bain Capital Ventures at a **$2.1B valuation**; total $163M raised post-restructuring (Verified — Docker press release, GlobeNewswire)
- Lifetime including the pre-2019 dotCloud/Docker era: ~$436M across ~12 rounds (Reported — Crunchbase)
- Revenue: ~$20M ARR 2021 → $165.4M 2023 → ~$207M ARR 2024, 1M+ paid seats (Reported — third-party stats aggregators; Docker is private and doesn't publish audited figures)

## Evidence of real-world use
Unusually strong, and mostly not marketing: Docker Hub has served **~318B lifetime pulls, ~13B/month**, hosting 15M+ images (Reported). Docker ranked **#1 most-used tool in the 2025 Stack Overflow Developer Survey at 92% adoption** among professionals (Verified). Docker Desktop installs ~3.3M, 7.3M Hub accounts; 75% of the Fortune 100 use Docker (Reported — Docker Index). On the AI side: 1M+ pulls from the MCP Catalog within months of the May 2025 beta (Reported — Docker blog). The `docker` CLI is embedded in essentially every CI system and cloud build pipeline in existence.

## Relevance to agentic AI engineering
Docker sits at three points of the agent stack. (1) **Tool-use and governance:** the MCP Gateway/Catalog is a production implementation of exactly the concerns in *Governance by Construction for Generalist Agents*, *CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents*, and *ClawLess: A Security Model of AI Agents* — signed tool provenance, call interception, least-privilege execution. (2) **Agentic SWE:** containers are the standard isolation substrate for coding-agent benchmarks and rollouts (the reproducible environments demanded by *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering* and *Verifiable Software Worlds for Computer-Use Agents* are, in practice, Docker images); Docker Sandboxes targets running agents like Claude Code safely. (3) **Local inference:** Model Runner makes models distributable OCI artifacts, relevant to low-latency local pipelines discussed in the realtime voice-agent papers (e.g., *Building Enterprise Realtime Voice Agents from Scratch*), though Docker itself is not a voice vendor.

## Use cases & considerations
Use cases: (a) sandbox coding agents and MCP servers instead of granting host access; (b) one gateway endpoint aggregating vetted MCP tools with audit logging for enterprise rollouts; (c) Testcontainers for agent integration tests against real databases/queues; (d) ship internal agents as versioned images via cagent + a registry.

Considerations: Docker Desktop licensing costs bite at scale, and past licensing changes (2021) burned goodwill — Podman, Rancher Desktop, OrbStack, and Colima are credible Desktop/Engine alternatives; for MCP governance, competitors include raw MCP + custom proxies and cloud-sandbox players like E2B (now a partner) and Modal. The AI product line is young (mostly 2025 betas) — API stability and long-term commitment are open questions, as is the post-CEO-change strategic direction.

## Sources
- https://en.wikipedia.org/wiki/Docker,_Inc.
- https://techcrunch.com/2018/03/28/solomon-hykes-leaves-docker-the-company-he-founded/
- https://www.docker.com/press-release/accelerate-investments-in-developer-productivity-trusted-content-and-ecosystem-partnerships/
- https://www.globenewswire.com/en/news-release/2022/03/31/2414082/0/en/Docker-Raises-105-Million-to-Accelerate-Investments-in-Developer-Productivity-Trusted-Content-and-Ecosystem-Partnerships.html
- https://www.docker.com/press-release/docker-announces-don-johnson-as-new-ceo-succeeding-scott-johnston/
- https://techcrunch.com/2025/02/13/former-oracle-cloud-exec-don-johnson-takes-over-as-dockers-new-ceo/
- https://www.techtarget.com/searchsoftwarequality/news/366619297/Docker-Inc-CEO-swap-has-analysts-anticipating-a-sale
- https://www.docker.com/blog/docker-mcp-gateway-secure-infrastructure-for-agentic-ai/
- https://docs.docker.com/ai/mcp-catalog-and-toolkit/
- https://www.docker.com/blog/announcing-docker-mcp-catalog-and-toolkit-beta/
- https://www.docker.com/blog/cagent-build-and-distribute-ai-agents-and-workflows/
- https://www.docker.com/blog/docker-e2b-building-the-future-of-trusted-ai/
- https://www.docker.com/blog/2025-docker-state-of-app-dev/
- https://electroiq.com/stats/docker-statistics/
- https://byteiota.com/docker-adoption-hits-92-2025s-biggest-tech-surge/
- https://www.crunchbase.com/organization/docker/financial_details

*Profile compiled 2026-07-02.*
