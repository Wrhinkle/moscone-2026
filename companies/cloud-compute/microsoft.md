# Microsoft

> The largest enterprise software and cloud company in the world, now repositioning its entire stack — Azure, GitHub, Microsoft 365 — around building, running, and governing AI agents.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** presenting
- **Founded:** 1975, Albuquerque, NM (Verified); HQ Redmond, WA. Satya Nadella CEO since 2014 (Verified).
- **Website / GitHub:** https://microsoft.com · https://github.com/microsoft · https://azure.microsoft.com

## What they do

For an AI engineer in 2026, "Microsoft" is really four overlapping products:

1. **Microsoft Foundry** (renamed from Azure AI Foundry) — the enterprise agent platform. At Build 2026 it added a managed **agent runtime** (Foundry Agent Service hosted agents, each session in its own sandbox with dedicated compute/filesystem; GA expected ~July 2026), **Foundry IQ** (an SLA-backed retrieval/knowledge layer unifying Work IQ, Fabric IQ, Azure SQL, File Search, and MCP sources, replacing hand-rolled RAG), and **agent memory** in public preview with three scopes — procedural, user, and session — where procedural memory (reusing successful execution patterns) is claimed to lift task success 7–14% (Reported, Microsoft's own numbers). The runtime is framework-agnostic: Microsoft Agent Framework, GitHub Copilot SDK, LangGraph, etc.
2. **Microsoft Agent Framework (MAF) v1.0** — the GA open-source successor consolidating AutoGen and Semantic Kernel: agent harness, skills, middleware, orchestration primitives (Verified, Build 2026 coverage).
3. **GitHub Copilot** — IDE assistant plus an autonomous **coding agent** that takes issues to pull requests.
4. **Copilot Studio / Microsoft 365 Copilot / Agent 365** — the business-user and governance layer: low-code agent building, computer-using agents, real-time voice agents, and Agent 365 as a centralized control plane for agent inventory, permissions, and activity, GA in 2026 (Verified).

Underneath all of it sits Azure — $75B+ revenue in FY2025, growing 34% (Verified, SEC filing/DCD) — which hosts OpenAI's frontier models plus Microsoft's own model efforts. What you'd actually buy: Azure compute + Foundry Agent Service for hosting agents, Foundry IQ for retrieval, Copilot seats for your developers.

## Founders & origins

Bill Gates and Paul Allen, 1975, Albuquerque, to sell a BASIC interpreter for the Altair 8800 (Verified, common historical record). Neither is operationally involved today; Allen died in 2018. The company's current AI posture is defined by Nadella's 2019–2023 OpenAI investments and the 2018 GitHub acquisition ($7.5B).

## Funding

Public company — no venture funding history in the usual sense. IPO March 1986 (Verified). FY2025 revenue **$281.7B** (Verified, 8-K). Market cap ~**$3T** as of May 2026 (Reported). The load-bearing "funding" fact is the **restructured OpenAI partnership (Oct 2025)**: Microsoft holds ~**27%** of OpenAI's new public benefit corporation (down from 32.5%), valued at ~$135B; IP rights to OpenAI models/products run through **2032** (including post-AGI systems, with guardrails); an independent expert panel now adjudicates any AGI declaration; OpenAI committed **$250B** in additional Azure purchases while Microsoft lost right-of-first-refusal on OpenAI compute (Verified — Microsoft blog + multiple independent reports).

## Evidence of real-world use

- GitHub Copilot: **20M all-time users** by July 2025 (Verified, TechCrunch); ~4.7M paid subscribers and ~77K enterprise customers as of Jan 2026 (Reported, third-party stat aggregators — treat precision skeptically); deployed at ~90% of the Fortune 100 (Reported). The coding agent reportedly contributes ~1.2M PRs/month (Reported).
- Copilot Cowork: used by **more than half the Fortune 500** during its Frontier preview; named customers include Accenture, Avanade, Capital Group, Koch, Ooredoo Qatar, Zurich Insurance (Reported, Microsoft 365 blog — vendor-published but named).
- Nadella has stated Copilot is now a bigger business than GitHub was at acquisition (Reported).

This is documented usage at a scale no other AIEWF sponsor approaches; the caveat is that most numbers originate from Microsoft itself.

## Relevance to agentic AI engineering

Microsoft touches nearly every research area in this repo:

- **Agentic SWE:** Copilot's coding agent is the archetypal system that *ProdCodeBench*, *SWE-EVO*, *SlopCodeBench*, and *FeatureBench* evaluate; the *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* critique applies directly to how Copilot's 1.2M PRs/month should be judged.
- **Tool-use & governance:** Agent 365 and Copilot Studio's governance features are a commercial instantiation of the concerns in *Governance by Construction for Generalist Agents* and *CaMeLs Can Use Computers Too* (system-level security for computer-use agents); Foundry's MCP-source support ties into *The Evolution of Tool Use in LLM Agents*.
- **Agent memory:** Foundry's three-scope memory preview is directly comparable to *Memory for Autonomous LLM Agents* and *GAM: Hierarchical Graph-based Agentic Memory*.
- **Voice:** Copilot Studio's May 2026 real-time voice experiences intersect with *LTS-VoiceAgent* and *τ-Voice* full-duplex benchmarking.

## Use cases & considerations

**Use cases:** (1) host production agents on Foundry Agent Service instead of building your own sandbox/runtime; (2) Foundry IQ as a managed retrieval layer over M365 + Fabric + SQL data — relevant to back-office document workflows (e.g., job-packet/invoice auditing on data already in SharePoint); (3) Copilot coding agent for issue-to-PR automation; (4) Copilot Studio computer-using and voice agents for ops teams without engineers.

**Considerations:** deep lock-in — identity (Entra), data (Graph/Fabric), and governance all assume the Microsoft estate; relentless product renaming (Azure AI Foundry → Microsoft Foundry) makes docs churn; metered agent billing (Copilot Cowork credits) is new and hard to forecast; most adoption numbers are vendor-published. Competitors: AWS Bedrock/AgentCore, Google Vertex + Gemini Enterprise, OpenAI selling directly (now less exclusive to Azure), Anthropic's Claude Code against Copilot. Open question: whether the loosened OpenAI exclusivity erodes Azure's frontier-model moat through 2032.

## Sources

- https://devblogs.microsoft.com/foundry/whats-new-in-microsoft-foundry-build-2026/
- https://www.infoq.com/news/2026/06/microsoft-foundry-agents/
- https://thenewstack.io/microsoft-foundry-build-2026-ai-agents/
- https://blogs.microsoft.com/blog/2025/10/28/the-next-chapter-of-the-microsoft-openai-partnership/
- https://openai.com/index/next-chapter-of-microsoft-openai-partnership/
- https://www.computing.co.uk/news/2025/microsoft-takes-27-percent-stake-openai
- https://www.datacenterdynamics.com/en/news/microsoft-loses-ip-exclusivity-rights-and-sees-revenue-payments-capped-in-updated-openai-deal/
- https://techcrunch.com/2025/07/30/github-copilot-crosses-20-million-all-time-users/
- https://www.quantumrun.com/consulting/github-copilot-statistics/
- https://www.microsoft.com/en-us/microsoft-365/blog/2026/03/09/powering-frontier-transformation-with-copilot-and-agents/
- https://www.microsoft.com/en-us/microsoft-copilot/blog/copilot-studio/new-and-improved-computer-using-agents-a-new-workflows-experience-and-real-time-voice-experiences/
- https://www.microsoft.com/en-us/microsoft-365/blog/2026/06/02/announcing-the-new-work-iq-apis/
- https://www.sec.gov/Archives/edgar/data/0000789019/000095017025100226/msft-ex99_1.htm
- https://www.datacenterdynamics.com/en/news/microsoft-azure-brought-in-75bn-for-fy2025-company-deployed-2gw-data-center-capacity/
