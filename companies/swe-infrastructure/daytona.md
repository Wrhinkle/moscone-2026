# Daytona

> API-provisioned sandboxes — isolated, stateful mini-computers that spin up in under ~100ms — so AI agents can run untrusted generated code, use desktops, and do RL rollouts without touching your infrastructure.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, New York City (Verified — Tracxn, Series A press release; the founding team is Croatian and the origin traces to Codeanywhere)
- **Website / GitHub:** https://www.daytona.io · https://github.com/daytonaio/daytona

## What they do

Daytona sells **execution infrastructure for AI-generated code**. The unit is the **sandbox**: an isolated environment with its own kernel-level separation, filesystem, and network stack, created via API in **sub-90ms** (their claim; LangChain's case study reports <100ms in production). Sandboxes are **stateful and composable** — an agent can create one, install dependencies, run code with real-time output streaming, snapshot the environment, pause it, and resume later — which is the property that matters for long-horizon agent tasks, versus fire-and-forget lambda-style execution. CPU, memory, storage, GPU (H100/H200-class), and OS are configurable per-sandbox on demand.

The API surface an engineer actually integrates: process/code execution, filesystem ops, git operations with credential handling, LSP support, shared volumes across sandboxes, and human escape hatches (web terminal, SSH, VS Code in browser, VNC). SDKs ship for Python (`pip install daytona`), TypeScript, Ruby, Go, and Java. Beyond code execution, they offer **computer-use sandboxes** — full Linux, macOS, and Windows desktops for GUI agents — and pitch **reinforcement-learning environments at scale** as a third workload. Multi-region (US, EU, Asia), SOC 2/HIPAA/GDPR claims, and a public pay-per-second pricing page (vCPU/GiB/GPU-second, $200 free credit) — a real self-serve commercial product, not enterprise vaporware.

Notable history: Daytona began as an open-source **development environment manager** (the "works on my machine" problem, building on the founders' Codeanywhere experience), then pivoted in mid-to-late 2024 when it became obvious the same fast-isolated-environment tech was what agents needed; the direction was formalized December 2024 (Verified — company's own pivot post). The GitHub repo (**~72k stars, ~5.7k forks** — much of it accrued in the dev-environment era) states that as of **June 2026 core development moved to a private codebase**; the public repo stays forkable but unmaintained. So treat Daytona today as closed-core SaaS, not an OSS project.

## Founders & origins

**Ivan Burazin (CEO)**, **Vedran Jukic (CTO)**, and **Goran Draganić (Chief Architect)** (Verified — Tracxn, press, company blog). Burazin and Jukic previously co-founded **Codeanywhere**, a browser IDE dating to 2009; Burazin also founded the **Shift Conference** in Croatia, acquired by Infobip, where he was Chief Development Experience Officer (Reported — interviews, Tracxn).

## Funding

- **Seed, June 2024: $5M** led by **Upfront Ventures** with 500 Global; total funding then reported at **$7M** including earlier pre-seed money (Verified — PRNewswire, Tracxn; angels reported to include founders of Postman, Netlify, Supabase).
- **Series A, Feb 5, 2026: $24M** led by **FirstMark Capital** (Matt Turck joined the board), with Pace Capital, Upfront, E2VC, Darkmode, plus strategic checks from **Datadog and Figma Ventures** (Verified — PRNewswire, company blog, multiple press).
- **Total raised: ~$31M** (computed from the above).

## Evidence of real-world use

Strong for a 20-person company. **LangChain** is a documented, quantified case study: their production coding agent runs on Daytona at ~4,000 sandboxes/month and 660+ hours of runtime/month, and there's an official **`@langchain/daytona`** integration package plus Daytona coverage in LangChain's deepagents sandbox docs — vendor-published but corroborated by LangChain's own reference docs. Series A press names **Turing, Writer, SambaNova** as customers, from YC startups to Fortune 100 (Reported); the site adds logos including Mintlify, Clay, Mastra, Snorkel, CoreWeave (logo-wall grade). Revenue signal: **$1M forward run rate in under three months post-launch, doubled six weeks later**, and the company describes itself as hardware-constrained (Reported — company PR, so promotional but unusually specific). Public pricing plus a $50K startup-credits program indicate genuine self-serve volume.

## Relevance to agentic AI engineering

Daytona is the **secure code-execution substrate** the agentic-SWE literature quietly assumes: long-horizon benchmarks like *SWE-EVO* and *SlopCodeBench*, and feature-level ones like *FeatureBench* and *ProdCodeBench*, all require reproducible, isolated, resumable environments per trajectory — exactly the snapshot/resume primitive here. The computer-use desktops connect to *Verifiable Software Worlds for Computer-Use Agents*, and environment-level isolation (vs. prompt-level guardrails) is the infrastructure counterpart of *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too*. Parallel sandbox fleets are the substrate for *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*, and the RL-environment pitch aligns with production-derived eval/training loops.

## Use cases & considerations

Use cases: (1) execution layer for a coding or data-analysis agent that must run untrusted generated code; (2) per-task ephemeral CI-like environments for agent fleets with snapshot-based caching of warm dependency states; (3) GUI/computer-use agent runtimes on real desktops; (4) RL rollout environments for training/evals.

Considerations: the June 2026 closed-sourcing removes the self-host option the OSS repo implied — you're buying managed SaaS with per-second metering, so model costs for long-running stateful sandboxes carefully. Young company (~20 people, Series A, self-described capacity-constrained). Competitors: **E2B** (closest, also AIEWF partner), **Modal**, **Cloudflare** sandboxes/containers, **Runloop**, **Coder** (self-hosted governance angle), **Morph**; hyperscalers could commoditize the primitive. Open question: whether "sandbox" stays a standalone layer or gets absorbed into agent frameworks and model-provider platforms.

## Sources

- https://www.daytona.io/
- https://github.com/daytonaio/daytona
- https://www.prnewswire.com/news-releases/daytona-raises-24m-series-a-to-give-every-agent-a-computer-302680740.html
- https://www.prnewswire.com/news-releases/daytona-secures-5m-to-simplify-development-environments-302181407.html
- https://www.daytona.io/dotfiles/daytona-raises-24m-series-a-to-give-every-agent-a-computer
- https://www.daytona.io/dotfiles/from-dev-environments-to-ai-runtimes
- https://www.daytona.io/customers/langchain
- https://reference.langchain.com/javascript/langchain-daytona
- https://tracxn.com/d/companies/daytona/__TzaXWUoUzJqHEQmWu6SWgVcuHYFltYtBs_uhDgw84Ss
- https://read.unicorner.news/p/daytona
- https://cerebralvalley.beehiiv.com/p/daytona-composable-computers-for-ai-agents
- https://pulse2.com/daytona-24-million-series-a/
