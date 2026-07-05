# Buildkite

> Hybrid CI/CD platform: Buildkite runs the control plane (UI, scheduling, APIs) while you run the open-source build agents on your own infrastructure — now positioning that architecture as the delivery layer for AI-agent-driven software engineering.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** September 2013, Melbourne, Australia (Verified — Wikipedia, company site, Startup Daily)
- **Website / GitHub:** https://buildkite.com · https://github.com/buildkite (agent: `buildkite/agent`; MCP server: `buildkite/buildkite-mcp-server`)

## What they do

Buildkite's core product, **Pipelines**, splits CI/CD into a SaaS control plane and self-hosted workers. You install the open-source Go **buildkite-agent** on your own machines (cloud, on-prem, Macs for mobile builds, GPU boxes), and Buildkite orchestrates jobs across them — up to ~10,000 agents per account. Code and secrets never leave your network; only metadata goes to Buildkite. This is the architecture teams reach for when GitHub Actions/CircleCI-style hosted runners can't meet security, scale, or exotic-hardware needs.

In October 2024 they repackaged as a "Scale-Out Delivery Platform" (Verified — Businesswire): **Test Engine** (distributed test execution, flaky-test detection and quarantine — evolved from 2022's Test Analytics), **Package Registries** (artifact/package management, built on the 2023 PackageCloud acquisition), and **Mobile Delivery Cloud** (hosted Mac infrastructure).

The 2025–26 agentic turn is concrete, not vaporware: an official open-source **MCP server** exposing pipelines, builds, jobs, and test data to AI tools; **Agent Skills** for Claude Code and Cursor (buildkite-pipelines, buildkite-agent-runtime, buildkite-preflight); pipeline triggers (inbound webhooks) plus model providers so CI jobs can invoke Claude without personal API keys; and richer failure metadata so agents can distinguish infra kills from real test failures instead of blindly retrying. Their published reference workflows include a PR review bot, a "build fixer" where Claude reads failure logs, pushes a fix branch, and opens a PR, and a Linear issue handler — all running agents in Docker containers with scoped tool access. Recent platform additions (Agent Pools for GPU targeting, fine-grained access control restricting which pipelines can invoke which agents) also read as agent-era hardening (Reported — LavX News summary of changelog).

## Founders & origins

**Keith Pitt** founded it (as "Buildbox," renamed after a trademark collision) in 2013, reportedly prototyping in an airport terminal, after working somewhere that couldn't use cloud CI for security reasons. **Tim Lucas** joined as co-founder shortly after launch; **Lachlan Donald** (then CTO of 99designs) also joined as a co-founder and later served as CEO for a stretch (Verified for Pitt/Lucas; Reported for Donald's co-founder framing — Startup Daily). Leadership churn is current-events material: Pitt exited suddenly in March 2025 without public explanation (remains a major shareholder); board chair Barry Crist ran the company until **Kevin Gounden**, a Silicon Valley operator, was named CEO around August 2025, with **James Wilson** (ex-WooliesX) as CTO (Verified — Startup Daily, Businesswire press release).

## Funding

- Seed: ~A$200K, January 2014 (Reported — Startup Daily).
- Series A: A$28M (~US$20M), August 2020, led by OpenView with General Catalyst; ~A$200M valuation. Notably profitable and bootstrapped for 7 years before this; part of the round cashed out early investors at ~42x (Verified — TechCrunch, Globe Newswire).
- Series B: US$21M (~A$32M), November 2022; OneVentures, AirTree, angel Dominic Pym (Verified — Wikipedia, VentureBeat).
- Total raised: ~US$40M (Verified within rounding).

## Evidence of real-world use

Strong, and documented beyond logo walls: TechCrunch cited 1,000+ customers in 2020 including **Shopify, Pinterest, Wayfair**. The 2024 platform launch names **Airbnb, Block, Canva, Cruise, Elastic, Lyft, Rippling, Slack, Tinder, Twilio, Uber** as standardized users, with a direct Uber quote ("we've halved our build times") and a Persona case study (flaky-test disruptions down 50% in four weeks). `buildkite/agent` is a long-running, actively maintained OSS project; the MCP server is young (~49 GitHub stars, Reported). Public pricing page exists; this is a real commercial product with a decade of enterprise production use.

## Relevance to agentic AI engineering

Buildkite is betting CI/CD becomes the execution substrate for coding agents: sandboxed compute, scoped credentials, and verifiable pass/fail signals. That maps directly onto this repo's landscape — *Verifiable Software Worlds for Computer-Use Agents* and *Governance by Construction for Generalist Agents* (CI as the governed, verifiable environment agents act inside); *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering* and *ProdCodeBench* (production pipelines as the honest eval harness benchmarks approximate); and *The Evolution of Tool Use in LLM Agents* (the MCP server + skills are exactly the multi-tool orchestration surface). Their build-fixer pattern is a production instance of the long-horizon iterative loop *SWE-EVO* and *SlopCodeBench* study.

## Use cases & considerations

Use cases: (1) CI for codebases where agents open many parallel PRs — self-hosted agents make burst compute cheap and keep code private; (2) wiring Claude Code into failure triage via the MCP server, using enriched failure metadata to avoid dumb retries; (3) GPU-pool pipelines for model/eval jobs via Agent Pools; (4) flaky-test quarantine (Test Engine) so agent-authored tests don't rot trust in CI.

Considerations: you operate the agent fleet yourself (that's the product and the burden); overkill below serious scale versus GitHub Actions defaults; 2025's founder-CEO exit without explanation plus new CEO/CTO is genuine execution risk to watch; competitors include GitHub Actions, GitLab CI, CircleCI, Harness, and Depot/Namespace on the fast-runner flank. Open question: whether "CI for agents" becomes a defensible category or every CI vendor's default feature set.

## Sources

- https://en.wikipedia.org/wiki/Buildkite
- https://techcrunch.com/2020/08/18/melbourne-based-ci-cd-platform-buildkite-gets-28-million-aud-series-a-led-by-openview/
- https://www.globenewswire.com/news-release/2020/08/18/2080050/0/en/With-Fresh-Funding-and-200-Million-Valuation-Buildkite-Accelerates-Next-Generation-of-CI-CD.html
- https://www.startupdaily.net/advice/buildkite-story-founders-200-million-investment/
- https://www.startupdaily.net/topic/keith-pitt-buildkites-cofounder-and-ceo-exits-suddenly/
- https://www.startupdaily.net/topic/people/buildkite-finally-has-a-new-ceo/
- https://www.businesswire.com/news/home/20241009617062/en/Buildkite-Launches-First-Scale-Out-Delivery-Platform-to-Bring-the-Engineering-Velocity-of-Top-Software-Companies-to-All-Enterprises
- https://www.businesswire.com/news/home/20250302533765/en/Buildkite-Announces-Leadership-Transition
- https://buildkite.com/resources/blog/building-ai-powered-ci-workflows-three-practical-examples/
- https://buildkite.com/docs/apis/mcp-server
- https://github.com/buildkite/agent
- https://github.com/buildkite/buildkite-mcp-server/
- https://venturebeat.com/security/ci-cd-pipeline-buildkite
- https://news.lavx.hu/article/buildkites-self-hosted-ci-cd-platform-gains-momentum-in-2025

*Profile written 2026-07-02.*
