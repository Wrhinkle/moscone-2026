# OpenHands

> The leading open-source autonomous coding agent (born as "OpenDevin"), now a company selling a hosted cloud version and enterprise deployment of the same agents.

- **Category:** coding-agents
- **AIEWF 2026 tier:** bronze
- **Founded:** project March 12, 2024; company (as All Hands AI) mid-2024, Boston, MA (Verified; company rebranded to OpenHands around its Nov 2025 Series A)
- **Website / GitHub:** https://www.openhands.dev · https://github.com/OpenHands/OpenHands (formerly All-Hands-AI/OpenHands)

## What they do

OpenHands is a model-agnostic platform for autonomous software development agents: you give it an issue, a task description, or a scheduled trigger, and the agent writes code, runs commands in a sandboxed (Docker-based) runtime, browses the web, and opens pull requests. Three layers matter to a builder: (1) the **MIT-licensed OSS core** — CLI and GUI app you run locally with any LLM key; (2) **OpenHands Cloud** — hosted agents that run continuously, with a $20/month subscription plus pay-as-you-go or bring-your-own LLM, GitHub/GitLab integration, and an "Agent Canvas" workspace for managing many parallel agents; (3) an **Agent SDK** (rebuilt as "V1" in late 2025, described in the arXiv paper *The OpenHands Software Agent SDK*, 2511.03690) for embedding their agent loop in your own products. Enterprise adds self-hosted/VPC deployment, SAML/SSO, RBAC, audit trails, and org-level quotas.

Positioning is explicitly "open standard for autonomous software development": unlike Devin or Copilot's coding agent, everything from the agent loop to the evaluation harness is public, and it works with any model (Claude, GPT, Qwen, local models via the AMD "Lemonade Server" partnership). Typical enterprise workloads are the unglamorous ones — dependency and vulnerability fixes, merge-conflict resolution, refactors fanned out across hundreds of repos.

## Founders & origins

Unusual origin: OpenDevin was started on March 12, 2024 by **Binyuan Hui and Junyang Lin of Alibaba's Qwen team** as an open-source homage to Cognition's Devin demo (Verified — company's own history post). The company was then formed by three early contributors (Verified across company blog, TechCrunch, LinkedIn):

- **Robert Brennan (CEO)** — previously product/engineering at open-source company Fairwinds; earlier ML/infra work at Google reported in some profiles (that Google detail: Reported).
- **Graham Neubig** — associate professor, CMU Language Technologies Institute; prominent NLP/code-LLM researcher.
- **Xingyao Wang** — UIUC PhD student working on interactive language agents; author of the CodeAct agent framework that powers the core loop.

Renamed OpenDevin → OpenHands in 2024 (trademark-safe); company renamed All Hands AI → OpenHands by late 2025.

## Funding

- **Seed, Sept 2024: $5M** — led by Menlo Ventures; Pillar VC, Betaworks, Rebellion; angels incl. Thom Wolf (Hugging Face), Jeff Hammerbacher, Soumith Chintala (Verified — TechCrunch, company press release).
- **Series A, Nov 18, 2025: $18.8M** — led by Madrona; Menlo Ventures, Pillar VC, Obvious Ventures, Fujitsu Ventures, Alumni Ventures (Verified — Businesswire, FinSMEs, company blog).
- **Total raised: ~$23.8M** (Verified). Valuation: not found in public sources.

## Evidence of real-world use

- **OSS adoption:** 65k+ GitHub stars, ~7k forks, 3M+ downloads, 250+ contributors in year one; contributors from AMD, Apple, Google, Amazon, Netflix, NVIDIA, Mastercard (Verified — repo + Series A announcement).
- **Benchmarks:** the standard open harness for agentic SWE evals — 72% on SWE-bench Verified (Claude Sonnet 4.5 + extended thinking, SDK), reported #1 on Multi-SWE-Bench; many labs (e.g. Nebius with Qwen3-Coder) publish results *using* OpenHands as the scaffold, which is stronger evidence than their own numbers. They also publish their own "OpenHands Index" model leaderboard (Jan 2026).
- **Commercial:** public pricing page (real product); enterprise claims of 50% maintenance-backlog reduction are vendor-sourced (Reported). Named enterprise customers: not found in public sources — the AMD partnership is the most concrete logo.

## Relevance to agentic AI engineering

This is the reference open implementation of the agentic-SWE stack this repo's benchmark thread studies: the original OpenHands paper (ICLR 2025) and SWE-Gym sit directly upstream of *FeatureBench*, *OmniCode*, *ProdCodeBench*, and *SWE-EVO*, and OpenHands is often the agent those benchmarks actually run. Long-horizon cloud agents doing continuous maintenance are exactly the regime *SlopCodeBench* and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* critique. Its sandboxed runtime connects to *Verifiable Software Worlds for Computer-Use Agents*; enterprise RBAC/audit-trail features are a commercial take on *Governance by Construction for Generalist Agents*; Agent Canvas's parallel agents echo *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*.

## Use cases & considerations

Use cases: (1) self-hosted autonomous issue-to-PR agent where code can't leave your VPC; (2) fleet-scale maintenance (dependency bumps, CVE fixes) across many repos; (3) building your own coding-agent product on the SDK instead of writing an agent loop; (4) reproducible agent benchmarking.

Considerations: agent quality is largely a function of the LLM you plug in — costs land on your token bill; OSS-to-cloud upsell means the free tier is genuinely capable but ops burden is yours. Competitors: Cognition (Devin), Claude Code, OpenAI Codex, GitHub Copilot coding agent, Cursor background agents, Factory, SWE-agent. Open question: whether an open-core company can hold pricing power when the models do most of the work; $23.8M raised is small against competitors' war chests.

## Sources

- https://www.openhands.dev/blog/one-year-of-openhands-a-journey-of-open-source-ai-development
- https://www.openhands.dev/blog/weve-just-raised-18-8m-to-build-the-open-standard-for-autonomous-software-development
- https://www.openhands.dev/blog/press-release-all-hands-announces-5m-to-scale-ai-agent-for-software-development
- https://techcrunch.com/2024/09/05/all-hands-ai-raises-5m-to-build-open-source-agents-for-developers/
- https://www.businesswire.com/news/home/20251118768131/en/OpenHands-Raises-$18.8M-Series-A-to-Bring-Open-Source-Cloud-Coding-Agents-to-Enterprises
- https://www.finsmes.com/2025/11/openhands-raises-18-8m-in-series-a-funding.html
- https://github.com/OpenHands/OpenHands
- https://www.openhands.dev/pricing
- https://www.openhands.dev/blog/sota-on-swe-bench-verified-with-inference-time-scaling-and-critic-model
- https://www.openhands.dev/blog/openhands-index
- https://arxiv.org/html/2511.03690v1 (OpenHands Software Agent SDK paper)
- https://nebius.com/blog/posts/openhands-trajectories-with-qwen3-coder-480b
