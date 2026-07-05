# AWS (Amazon Web Services)

> The largest public cloud provider, now selling a full agent stack — Bedrock models, AgentCore runtime, Strands SDK, Kiro IDE, Trainium silicon — on top of the compute everyone already runs on.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** platinum
- **Founded:** launched 2006 (S3 in March, EC2 in August), Seattle, WA; subsidiary of Amazon.com (Verified, common historical record). CEO: Matt Garman since June 2024 (Verified).
- **Website / GitHub:** https://aws.amazon.com · https://github.com/aws · https://github.com/strands-agents

## What they do

AWS is the default substrate: compute (EC2), storage (S3), and ~200 other services. For an AI engineer in 2026, the relevant stack is four layers:

1. **Silicon:** Trainium2/3 training-and-inference chips from Annapurna Labs, positioned as the cheaper alternative to NVIDIA. **Project Rainier** — one of the world's largest AI clusters, ~500K Trainium2 chips at activation, built for Anthropic, which now uses 1M+ Trainium2 chips to train and serve Claude (Verified — AWS and Anthropic announcements).
2. **Models:** **Amazon Bedrock**, the managed multi-model API — Anthropic Claude, Amazon's own Nova family, Meta, Mistral, etc. — with guardrails, knowledge bases, and fine-tuning. (Amazon's frontier-agents research arm is profiled separately in `companies/models-inference/amazon-agi-labs.md`.)
3. **Agent infrastructure:** **Bedrock AgentCore**, GA October 13, 2025 (Verified) — framework- and model-agnostic managed services for running agents: Runtime (isolated sessions), Memory, Gateway (turns APIs into MCP-compatible tools), Identity, Browser and Code Interpreter tools, Observability; GovCloud support May 2026 and a built-in Web Search tool June 2026 (Verified, AWS what's-new). Pairs with **Strands Agents**, AWS's open-source, model-agnostic agent SDK.
4. **Developer tooling:** **Kiro**, the spec-driven agentic IDE/CLI (prompts → specs → code/tests). In January 2026 AWS announced Amazon Q Developer closes to new signups May 15, 2026, naming Kiro the successor (Reported — third-party coverage).

What you'd actually buy: pay-as-you-go tokens on Bedrock, AgentCore consumption pricing for agent hosting, Kiro seats, and the EC2/S3 bill you already have.

## Founders & origins

Not a startup: AWS grew from an internal 2003 initiative to sell Amazon's infrastructure as primitives. **Andy Jassy** led the project from its founding vision document and ran AWS until becoming Amazon CEO in 2021; Adam Selipsky ran it 2021–2024; **Matt Garman** (AWS employee since 2006, ex-head of EC2 and sales) is CEO since June 2024 (Verified). Werner Vogels remains Amazon CTO and its public-facing architect.

## Funding

Wholly owned segment of Amazon (NASDAQ: AMZN) — no venture history. The numbers that matter: Q4 2025 revenue **$35.58B, +24% YoY** (fastest growth in 13 quarters), ~**$142B annualized run rate**, order backlog **$244B (+40% YoY)**, inside Amazon's ~$200B 2026 capex plan (Verified — CNBC, TechCrunch, Futurum). The strategic "investment" story is Anthropic: ~$8B invested through 2024, then (April 20, 2026) **$5B additional equity plus up to $20B milestone-based**, with Anthropic committing **$100B+ of AWS spend over ten years** and up to 5GW of Trainium capacity (Verified — Amazon and Anthropic announcements).

## Evidence of real-world use

- The baseline: roughly a third of the public internet runs on AWS; market-share estimates put it around 30%, still #1 ahead of Azure and Google Cloud (Reported — analyst trackers, not independently verified here).
- AgentCore in production with named customers: **Cox Automotive and Druva** (up to 63% autonomous issue resolution, 58% faster responses — Reported, AWS-published case studies), **Epsilon** for marketing-campaign agents (Reported, AWS blog). Vendor-published but named and specific.
- Anthropic training/serving Claude on 1M+ Trainium2 chips is the strongest independent-workload evidence for the silicon layer (Verified).
- The $244B backlog is contractual committed spend — harder evidence than logos (Verified, earnings).
- Kiro and Strands are young; public adoption numbers were not found as of 2026-07-02 (Unverified).

## Relevance to agentic AI engineering

AWS is trying to own every layer of the agent stack this repo maps. AgentCore Gateway's API-to-MCP conversion is a direct commercial instantiation of the "software adapting to agents" trajectory in *The Evolution of Tool Use in LLM Agents*; its Identity/Runtime isolation model speaks to *Governance by Construction for Generalist Agents* and the system-level security argument of *CaMeLs Can Use Computers Too*. AgentCore Memory is the managed-service counterpart to *Memory for Autonomous LLM Agents* and *GAM: Hierarchical Graph-based Agentic Memory*. Kiro's spec-driven workflow is exactly the long-horizon, production-realistic agentic SWE that *ProdCodeBench*, *SWE-EVO*, and *FeatureBench* benchmark. Nova Sonic speech-to-speech on Bedrock touches the voice-agent thread (*LTS-VoiceAgent*, *τ-Voice*).

## Use cases & considerations

**Use cases:** (1) host production agents on AgentCore instead of building session isolation, memory, and tool gateways yourself — works with LangGraph/CrewAI/Strands and non-Bedrock models; (2) multi-model inference through one Bedrock API with unified guardrails and VPC/compliance posture; (3) Trainium for cost-sensitive training/inference if you can tolerate a non-CUDA toolchain; (4) Kiro for spec-first agentic development on codebases already in AWS.

**Considerations:** AgentCore is model-agnostic in theory but the gravity (IAM, VPC, billing) is real lock-in; consumption pricing for agent workloads is hard to forecast; AWS's AI narrative is fragmented across Bedrock/AgentCore/Q/Kiro/Nova with visible product churn (Q Developer sunset one year after heavy promotion); Trainium tooling maturity lags NVIDIA. Competitors: Microsoft Azure + Foundry (see `microsoft.md`), Google Cloud Vertex, and at the agent-infra layer the neocloud/agent-runtime startups. Open question: whether Anthropic's $100B commitment makes AWS the de facto Claude cloud, and how much of the $244B backlog is AI-specific.

## Sources

- https://aws.amazon.com/blogs/aws/introducing-amazon-bedrock-agentcore-securely-deploy-and-operate-ai-agents-at-any-scale/
- https://aws.amazon.com/about-aws/whats-new/2025/10/amazon-bedrock-agentcore-available/
- https://aws.amazon.com/about-aws/whats-new/2026/05/bedrock-agentcore-launch-aws-govcloud-us/
- https://aws.amazon.com/blogs/aws/announcing-web-search-on-amazon-bedrock-agentcore-ground-your-ai-agents-in-current-accurate-web-knowledge/
- https://aws.amazon.com/bedrock/agentcore/
- https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-and-claude-transforming-business-with-agentic-ai/
- https://www.cnbc.com/2026/02/05/aws-q4-earnings-report-2025.html
- https://techcrunch.com/2026/02/05/aws-revenue-continues-to-soar-as-cloud-demand-remains-high/
- https://futurumgroup.com/insights/amazon-q4-fy-2025-revenue-beat-aws-24-amid-200b-capex-plan/
- https://www.aboutamazon.com/news/aws/aws-project-rainier-ai-trainium-chips-compute-cluster
- https://www.aboutamazon.com/news/company-news/amazon-invests-additional-5-billion-anthropic-ai
- https://www.anthropic.com/news/anthropic-amazon-compute
- https://thenewstack.io/anthropic-amazon-aws-investment/
- https://kiro.dev/
- https://github.com/kirodotdev/Kiro
- https://www.digitalapplied.com/blog/amazon-kiro-aws-agentic-ide-complete-guide
