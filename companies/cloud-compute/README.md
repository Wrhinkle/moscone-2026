# Cloud & Compute

General cloud, GPU cloud, edge/CDN, containers, deployment platforms, self-hosted distribution, and object storage. This is the substrate layer: every agent, model, and eval harness in the rest of this repo ultimately runs on something profiled here. The real-world problem the category solves is that agentic workloads look nothing like the web apps clouds were built for. They are inference-heavy and bursty (scale-to-zero economics matter) and long-lived and stateful (session isolation and durable memory matter), and they execute untrusted, model-generated code that has to be sandboxed. In 2025–26 every company in this folder, from $3T incumbents to 20-person startups, repositioned around some slice of that problem.

## How to read this category

Three profiles carry the most weight. **[AWS](aws.md)** and **[Microsoft](microsoft.md)** are the hyperscaler agent-stack plays (Bedrock/AgentCore and Foundry respectively), and between them they define what "managed agent runtime" means commercially; read them first to calibrate everything else. **[Cloudflare](cloudflare.md)** is the strongest non-hyperscaler thesis: agents as hibernating, stateful edge objects that cost nothing when idle. That answer differs from the hyperscalers' in architecture, and the cost profile follows from the architecture.

The rest of the folder differentiates along one main axis, **what layer of the stack they sell**:

- **Full-stack incumbents** (AWS, Microsoft, Oracle, Red Hat, DigitalOcean): general cloud plus an agent/inference platform bolted on top, sold into an existing install base.
- **GPU neoclouds** (Crusoe, Nebius, RunPod, Vast.ai): raw NVIDIA capacity at below-hyperscaler prices, differentiated by how vertically integrated they are: Crusoe owns the power plants; Vast.ai owns nothing but the marketplace.
- **Serverless/edge developer platforms** (Modal, Vercel, Cloudflare, Akamai): abstractions over compute (a Python decorator, a git push, a Worker), with agent sandboxes as the common new product.
- **Distribution and storage specialists** (Docker, Replicated, Tigris): the packaging, self-hosted delivery, and object-storage layers that the other three groups all depend on.

A recurring pattern worth noticing: the same three primitives (sandboxed execution, agent memory/state, and MCP tooling with governance) appear independently at Docker, Modal, Cloudflare, Vercel, AWS, and Microsoft. The vendors have converged on what agent infrastructure *is*; who owns it remains an open fight.

## Profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [AWS](aws.md) | Largest public cloud, now selling a full agent stack: Bedrock, AgentCore runtime, Strands SDK, Kiro IDE, Trainium silicon | platinum | Amazon segment; ~$142B run rate, $244B backlog | Anthropic trains/serves Claude on 1M+ Trainium2 chips; $100B+ ten-year AWS spend commitment |
| [Microsoft](microsoft.md) | Azure + Foundry agent runtime + GitHub Copilot + Agent 365 governance, covering the whole enterprise agent estate | presenting | Public; $281.7B FY2025 revenue, ~$3T cap | Copilot's coding agent reportedly ships ~1.2M PRs/month; holds ~27% of OpenAI with IP rights through 2032 |
| [Oracle](oracle.md) | Database giant turned mega-scale AI-training cloud (home of OpenAI's Stargate capacity), with an MCP server in the database itself | platinum | Public; RPO $553B, +325% YoY | The ~$300B, ~4.5 GW OpenAI/Stargate agreement; OCI Zettascale10 targets 800K-GPU clusters |
| [Akamai](akamai.md) | The original CDN, now selling edge GPU inference (with NVIDIA) and an AI firewall for LLM apps and agent traffic | platinum | Public since 1999; ~$4B revenue, cloud at ~$400M run rate | Inference Cloud puts Blackwell GPUs at edge PoPs, a bet that proximity wins multi-call agent latency |
| [Docker](docker.md) | The default container toolchain, repositioning as the packaging, sandboxing, and MCP-governance layer for agents | platinum | Private; $105M Series C at $2.1B (2022), ~$207M ARR | MCP Catalog/Gateway: 300+ signed MCP servers with call interception; 1M+ pulls within months of beta |
| [Cloudflare](cloudflare.md) | Edge network (~20% of the web) turned agent deployment substrate: Durable Objects, Agents SDK, Workers AI, x402 agent payments | gold | Public; ~$2.8B FY2026 guidance | Agents hibernate to zero cost when idle; "millions of concurrent agents" is architecture, not marketing |
| [Crusoe](crusoe.md) | Vertically integrated energy-first AI cloud; built OpenAI's Stargate Abilene campus, sells GPU clusters and managed inference above it | gold | ~$2.8B equity raised; Series E at >$10B (Oct 2025) | Built the 1.2 GW Stargate Abilene site; when OpenAI dropped an expansion, Microsoft leased the adjacent ~900 MW within weeks |
| [Nebius](nebius.md) | Nasdaq-listed neocloud built from Yandex's non-Russian remains: own data centers, GPU clusters, and the Token Factory inference platform | gold | Public (NBIS); $4.34B convert + $2B NVIDIA warrants, ~$20–25B capex | Meta deal expanded to up to $27B and Microsoft to ~$17.4B; two customers dwarf everything else |
| [Replicated](replicated.md) | Ships a vendor's SaaS as self-hosted/air-gapped installs in the customer's own environment: the delivery rail for "your agent, in my VPC" | gold | ~$85M raised; no round since 2021 | Cohere, Writer, and H2O.ai distribute via Replicated, with model weights gated per customer license |
| [RunPod](runpod.md) | Developer-first GPU cloud: per-second Pods, scale-to-zero Serverless inference, short-commitment training clusters | gold | $122M total; Series A at $1B (Jun 2026) | Bootstrapped from basement Ethereum rigs to ~$120M ARR largely on a $20M seed |
| [DigitalOcean](digitalocean.md) | Simple-cloud provider for SMBs layering an "AI-native cloud" (GPUs, inference, managed agents) on its Droplet/K8s core | silver | Public (DOCN) since 2021 | 600K+ customers as the distribution channel for a five-layer managed-agent stack aimed at non-ML teams |
| [Modal](modal.md) | Serverless Python-native compute: decorate a function, get autoscaling GPUs, plus gVisor Sandboxes for agent-generated code | silver | ~$465M; Series C at $4.65B (May 2026) | Custom Rust runtime cold-starts multi-GB ML containers in under a second; claims 100k+ concurrent sandboxes |
| [Red Hat](red-hat.md) | Enterprise Linux/K8s (IBM subsidiary) positioning OpenShift + vLLM + llm-d as the open-source model/agent serving stack | silver | IBM subsidiary (acquired 2019, $34B) | One of the largest commercial vLLM contributors; llm-d co-founded with CoreWeave, Google, IBM, NVIDIA for agentic inference |
| [Vast.ai](vast-ai.md) | GPU marketplace connecting renters with independent hosts, from gaming rigs to data-center racks, at below-hyperscaler prices | silver | Funding conflicting across sources; not verified | 17,000+ GPUs from 350+ hosts; the purest marketplace model in the category |
| [Tigris](tigris.md) | Globally distributed S3-compatible object storage, zero egress fees, with copy-on-write bucket forking for per-agent data isolation | bronze | ~$32M+; $25M Series A (Oct 2025, Spark + a16z) | GitHub-style bucket forks give each agent or eval run an isolated zero-copy view of production data |
| [Vercel](vercel.md) | Next.js steward moving from "frontend cloud" to "AI cloud": AI SDK, AI Gateway, microVM Sandboxes, v0 | supporting | ~$863M; Series F at $9.3B (Sep 2025) | Vendor-reported: agents now trigger over half of all deployments on the platform, up from <3% in early 2026 |

Caveats worth carrying into any read: adoption numbers in this category are overwhelmingly vendor-published (flagged per-profile), Vast.ai's funding could not be verified at all, and several flagship products (Akamai Inference Cloud, Nebius Token Factory, Vercel's eve, Docker's AI line) are months old with no independent production track record yet.

## Related papers

The profiles cross-reference the papers below repeatedly; they are the research counterparts to what this category sells.

**Tool use, sandboxing, and governance** is the strongest overlap. Docker's MCP Gateway, AWS AgentCore Identity, Microsoft Agent 365, Akamai's Firewall for AI, and Oracle's database-enforced MCP security all commercially instantiate the argument that guardrails belong in the substrate itself:

- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md)
- [CaMeLs Can Use Computers Too: System-Level Security for Computer-Use Agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md)
- [ClawLess: A Security Model of AI Agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md)
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): AgentCore Gateway's API-to-MCP conversion and Cloudflare's Code Mode are this paper's trajectory, productized
- [Verifiable Software Worlds for Computer-Use Agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md): the reproducible environments it demands are, in practice, Docker images and Modal/Vercel sandboxes

**Agent memory and state.** Microsoft Foundry's three-scope memory, AWS AgentCore Memory, Cloudflare Agent Memory, Crusoe's MemoryAlloy KV cache, and Tigris's per-agent buckets each answer this literature at a different layer:

- [Memory for Autonomous LLM Agents: Mechanisms, Architectures](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md)
- [GAM: Hierarchical Graph-Based Agentic Memory for LLM Agents](../../papers/memory-research-agents/gam-hierarchical-graph-based-agentic-memory-for-llm-agents.md)
- [Are We Ready for an Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md)

**Agentic SWE benchmarks.** These cover the workloads that fill this category's GPU clusters and sandboxes (Copilot's PRs, v0, Windsurf training on Crusoe, coding agents in Modal/Docker sandboxes):

- [ProdCodeBench](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md)
- [SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md)
- [FeatureBench](../../papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md)
- [SlopCodeBench: How Coding Agents Degrade Over Long Horizons](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md): Tigris pitches snapshot rollback as a storage-level answer to exactly this error accumulation
- [Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md)
- [Reproducible, Explainable, and Effective Evaluations of Agentic AI for SWE](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md)
- [Effective Strategies for Asynchronous Multi-Agent Collaboration in SWE](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md): the parallel-sandbox pattern Tigris's bucket forking targets

**Voice/realtime latency budgets.** This is the workload class that justifies edge inference (Akamai, Cloudflare) and sub-second cold starts (Modal, RunPod):

- [LTS-VoiceAgent: A Listen-Think-Speak Framework](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md)
- [τ-Voice: Benchmarking Full-Duplex Voice Agents](../../papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md)
- [VoiceAgentRAG: Solving the RAG Latency Bottleneck](../../papers/voice-realtime/voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md)
- [Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling](../../papers/voice-realtime/building-interactive-real-time-agents-with-asynchronous-i-o.md)
- [Building Enterprise Realtime Voice Agents from Scratch](../../papers/voice-realtime/building-enterprise-realtime-voice-agents-from-scratch-a-te.md)

## Open questions

1. **Does edge inference win real workloads?** Akamai and Cloudflare bet that multi-call agent latency is won by proximity; the counter-case is that caching plus routing to centralized GPUs is good enough. No independent production evidence exists yet either way.
2. **Mega-deal concentration vs. self-serve.** Nebius (Microsoft + Meta), Crusoe (OpenAI/Oracle, then Microsoft), and Oracle (OpenAI) all carry extreme counterparty concentration; the March 2026 Abilene expansion cancellation shows the churn risk. Is any neocloud's self-serve business material, or are these data-center developers with a cloud console attached?
3. **Who owns the sandbox primitive?** Docker, Modal, Vercel, Cloudflare, E2B, and now AWS/Microsoft all ship isolated agent-execution environments. Hyperscalers adding first-party sandboxes is the direct threat to Modal's $4.65B valuation and Docker's AI pivot.
4. **Does the OpenAI/Anthropic capital circuit hold?** AWS↔Anthropic ($100B commitment), Microsoft↔OpenAI (through 2032), NVIDIA↔Nebius/Crusoe warrants and stakes: the category's growth numbers rest on circular financing whose margins none of the parties has disclosed.
5. **Do agents change cloud pricing?** Scale-to-zero, per-second, per-token, and metered agent-credit billing (Copilot Cowork, AgentCore consumption) are all young; whether enterprises can forecast agent workloads well enough to buy them is unresolved.
6. **Self-hosted AI as a durable niche.** Replicated's thesis, that enterprise buyers refuse multi-tenant AI clouds, is backed by real AI-vendor logos, but the company hasn't raised since 2021 and GPU-heavy stacks still need a hardware answer at each customer site.
