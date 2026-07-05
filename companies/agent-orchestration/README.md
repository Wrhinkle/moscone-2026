# Agent Orchestration

**Category definition:** Agent frameworks, durable workflow/execution engines, tool-integration layers, human-in-the-loop/approval layers, and structured-output tooling.

This is the connective tissue of the agent stack: everything between "the model can call a function" and "an agent runs a multi-day business process in production without a human babysitting it." The real-world problem is that LLM loops are non-deterministic and crash-prone by default, and nothing holds them accountable. Calls fail, context windows overflow, tools need auth, humans need to approve the dangerous steps, and outputs need to be machine-parseable. Every company in this folder sells one slice of the fix. It's the largest category in this repo (21 profiles) because it's where the 2026 money is: Temporal alone raised $300M at a $5B valuation this year on the thesis that agents need a reliability substrate.

## How to read this category

The load-bearing entries are **[Temporal](temporal.md)**, **[LangChain](langchain.md)**, and **[Composio](composio.md)**. Read those three and you understand the category's three distinct businesses: durable execution (the engine that guarantees a workflow survives crashes and week-long waits), the agent framework (the library that defines what the agent does), and the tool/auth layer (the catalog that lets the agent touch real SaaS systems). Almost everything else in the folder competes with or complements one of those three positions. The differentiating axis across the rest is **how low in the stack they sit and who they sell to**: execution engines are language-agnostic infrastructure sold on reliability; frameworks are developer libraries sold on speed-to-build and monetized via observability clouds; tool layers are sold on integration count and auth handling; and a fourth cluster (human-in-the-loop, agent runtimes, structured output) sells the specific missing piece that makes the other three trustworthy.

**Start here:**

- **[temporal.md](temporal.md)**: the durable-execution reference point. OpenAI runs Codex on it, and every other engine in this folder positions against it.
- **[langchain.md](langchain.md)**: the default OSS agent framework (LangGraph) and the $1.25B-valuation template for framework→observability-cloud monetization.
- **[composio.md](composio.md)**: the cleanest example of the managed tool-calling/auth business (1,000+ SaaS toolkits behind one SDK/MCP layer).
- **[humanlayer.md](humanlayer.md)**: the smallest company here with outsized mindshare, via 12-Factor Agents, "context engineering," and the human-approval-first worldview the whole category is converging on.

## Companies

### Durable execution & workflow engines

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Temporal](temporal.md) | Durable-execution engine: ordinary code as crash-proof workflows, now the reliability substrate under production agents | Gold | ~$650M raised; $5B valuation (Series D, Feb 2026, a16z) | OpenAI runs Codex on Temporal at millions-of-requests scale |
| [Orkes](orkes.md) | Managed Conductor (the Netflix workflow engine) repositioned as an "OS for AI agents" with HITL tasks and RBAC | Gold | ~$90M raised (Series B, Apr 2026) | Workflows live as JSON data, so LLMs can generate and modify them at runtime under governance |
| [Inngest](inngest.md) | Durable step functions over plain HTTP (same code on serverless or servers), plus AgentKit for multi-agent networks | Gold | ~$30M raised (Series A led by Altimeter, Sept 2025) | HTTP-as-transport means identical durable code on Vercel, Lambda, or a long-lived server |
| [Prefect](prefect.md) | Python workflow orchestrator ("the anti-Airflow") that pivoted into AI infra by owning FastMCP, the dominant MCP-server framework | Supporting | >$45M raised, but nothing announced since June 2021 | FastMCP v1 was absorbed into Anthropic's official MCP Python SDK; company claims ~70% of MCP servers trace to it |

### Agent frameworks

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [LangChain](langchain.md) | LangChain/LangGraph OSS frameworks monetized through LangSmith (tracing, evals, deployment) | Gold | ~$260M raised; $1.25B valuation (Series B, Oct 2025) | Klarna's 85M-user assistant and Replit's coding agent both run on LangGraph |
| [LlamaIndex](llamaindex.md) | Data-to-LLM framework (RAG, event-driven Workflows) monetized through LlamaCloud/LlamaParse document parsing | Gold | ~$27.5M raised, 10x less than LangChain and deliberately capital-light | Customer parsed 4M pages in a weekend on LlamaParse; Salesforce's Agentforce team uses it in RAG pipelines |
| [Mastra](mastra.md) | TypeScript-native agent framework (agents, suspend/resume workflows, evals, voice) from the Gatsby founders | Supporting | $13M seed (Oct 2025, YC W25) | Their book *Principles of Building AI Agents* shipped 70k+ physical copies; distribution via paper |
| [Pydantic](pydantic.md) | Python's validation substrate turned AI stack: Pydantic AI framework + Logfire observability + Evals + Gateway | Supporting | ~$17.2M raised (Sequoia-led seed + Series A) | The pydantic library crossed 10 billion cumulative downloads; it's the type layer inside most other tools in this folder |

### Tool integration & agent-facing services

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Composio](composio.md) | Managed tool-calling: 1,000+ authenticated SaaS toolkits behind one SDK/MCP layer, plus runtime tool routing | Gold | ~$29M raised (Series A led by Lightspeed, Jul 2025) | Tool Router attacks the dump-every-tool-in-context problem with runtime tool search |
| [Ampersand](ampersand.md) | Declarative (YAML) bi-directional SaaS integrations: CRM/ERP read-write as agent-callable actions | Silver | $4.7M seed (2023, Matrix Partners) | Customer 11x cut agent response time from 60s to 5s using its actions layer |
| [Zero](zero.md) | Free CLI "activation layer": agents discover and call ~14k+ APIs pay-per-call, no API-key setup | Silver | Unverified; launched 2026 | HTTP 402-style micropayments per tool call; no accounts or API keys to set up |
| [AgentMail](agentmail.md) | Email inbox API for agents: a real threaded address per agent in milliseconds, SPF/DKIM handled | Supporting | $6M seed (Mar 2026, General Catalyst; YC S25) | 100M+ emails delivered; usage spiked 3–4x after the "OpenClaw" agent launch |

### Human-in-the-loop & agent–human interfaces

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [CopilotKit](copilotkit.md) | Frontend framework + open AG-UI protocol for agent-in-app UX: streaming chat, generative UI, approval interrupts | Bronze | $27M raised (Series A, May 2026) | AG-UI adopted first-party by Google ADK, Microsoft Agent Framework, and AWS Strands/Bedrock AgentCore |
| [HumanLayer](humanlayer.md) | From human-approval API to CodeLayer: an IDE for orchestrating fleets of coding agents with review gates at every phase | Supporting | ~$3M+ (YC F24; company-stated) | Founder Dex Horthy wrote 12-Factor Agents and is widely credited with coining "context engineering" |

### Agent runtimes, control planes & coordination

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Druid](druid.md) | Enterprise agentic platform (Conductor engine): governed fleets of HR/CS/banking agents, on-prem to air-gapped | Gold | ~$80M+ raised (Series C, Sept 2025) | Ships Becus, a proprietary LLM for air-gapped regulated deployments; UiPath resold the platform globally |
| [Band](band.md) | Hosted "Slack for agents": persistent rooms where agents on any framework (plus humans) discover, delegate, and share context | Gold | $17M seed (Apr 2026; Sierra Ventures, Team8) | Founders' prior companies exited for ~$250M (Sygnia) and ~$300M (Ermetic); adoption still unproven (the SDK had 8 GitHub stars at research time) |
| [AgentField](agentfield.md) | OSS Go control plane: agents as REST endpoints with retries, HITL pause/resume, and per-agent cryptographic identity | Supporting | Undisclosed (Panache, Brightspark) | Gives every agent a W3C-style decentralized ID for enforceable permissions and verifiable audit trails |
| [Introspection](introspection.md) | GitOps agent deployment: git-versioned "Pi recipes" run in confidential-computing sandboxes in your own cloud, with A/B evals | Supporting | Not found in public sources | Credentials are injected at the network edge so keys never enter the agent's sandbox |
| [Paper Compute](paper-compute.md) | Agent-ops OSS: zero-instrumentation telemetry (Tapes) + a hardened agent-sandbox Linux (stereOS) | Silver | Unverified | Founded by Brian Douglas, ex-GitHub director of developer advocacy (OpenSauced) |

### Structured output & contracts

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [.txt (dottxt)](txt.md) | Outlines: constrained decoding that *guarantees* LLM output matches a JSON schema/regex/grammar, plus a hosted API | Supporting | ~$11.9M raised (seed led by EQT, Aug 2024) | AWS published an official Bedrock/SageMaker integration blog for Outlines |
| [Boundary](boundary.md) | BAML, a typed DSL for LLM function calls; the compiler emits validated Python/TS/Ruby/Go clients with retries/fallback | Supporting | YC-backed; round size undisclosed | HumanLayer's team merged a ~35k-line agent-written PR into BAML's Rust codebase as a context-engineering proof point |

*Tier = AIEWF 2026 sponsorship tier, a marketing-spend signal, not a quality ranking. Pydantic and Prefect (supporting) are arguably more load-bearing infrastructure than several gold sponsors.*

**Coverage note:** all 19 companies expected in this category are present. Two profiles were re-filed *into* this folder from other categories: **Band** (originally slotted under consumer-ai; the product is B2B agent-coordination infrastructure) and **Zero** (tool-discovery layer). Nothing expected is missing.

## Related papers

The `papers/` research areas this category productizes, most-relevant first:

- **Tool use & governance**: the category's core academic counterpart. [The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) maps directly onto Composio's Tool Router, Prefect's FastMCP, and Mastra's MCP surface. [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) and [CaMeLs Can Use Computers Too](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) argue that approval and permission must be structural, which is precisely what HumanLayer, CopilotKit's AG-UI interrupts, AgentField's identities, and Orkes/Druid's RBAC ship as product.
- **Planning & architecture**: [From Plan to Action: How Well Do Agents Follow the Plan?](../../papers/planning-architecture/from-plan-to-action-how-well-do-agents-follow-the-plan.md) is cited across the frameworks here (Mastra, CopilotKit, HumanLayer) as the problem their suspend/resume, shared-state, and plan-review features address.
- **SWE agents**: durable execution and HITL orchestration matter most on long-horizon coding work. [SlopCodeBench: Benchmarking How Coding Agents Degrade Over Long-Horizon Iterative Tasks](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) is HumanLayer's entire pitch inverted; [Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md) is what Band's rooms and HumanLayer's parallel sessions productize; [Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md) is the eval discipline Pydantic (Logfire + Evals) and LangSmith sell.
- **Memory & research agents**: execution state vs. semantic memory is a recurring boundary here. [Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md) and [Are We Ready For An Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md) frame what Mastra's observational memory, Band's platform-held room context, and LangGraph's persistence layer are each betting on.

Voice/realtime papers are mostly *not* relevant here: durable checkpointing is the wrong tool for low-latency audio (Inngest's profile says so explicitly). Mastra's voice modules are the one crossover.

## Open questions the category hasn't answered

1. **Does the orchestration layer survive model-provider absorption?** OpenAI, Anthropic, and Google keep pulling agent loops, harnesses, and multi-session tooling into their own SDKs. This is the named existential risk in the LangChain, Temporal, and HumanLayer profiles alike.
2. **Framework durability vs. dedicated engines.** LangGraph checkpointing keeps improving; if "good-enough" durability lives in the framework, the case for a separate Temporal/Orkes/Inngest layer shrinks. Yet Temporal's Series D bet $300M the other way.
3. **Does MCP commoditize the tool layer?** Composio, Ampersand, and Zero all sell curated tool access, but MCP makes connectors cheap to build; Prefect's answer (own the MCP framework *and* its hosting) is unproven revenue.
4. **Structured output vs. model-native competence.** As frontier models get reliably schema-faithful, do .txt and Boundary remain products or become features (the same squeeze LlamaParse faces from VLM-native document understanding)?
5. **Who wins the agent↔UI and agent↔agent protocol wars?** AG-UI vs. A2UI vs. MCP Apps at the UI boundary; A2A/ACP at the coordination boundary. CopilotKit and Band are each betting that an independent protocol network beats framework-native integration, with the hyperscalers adopting (and possibly absorbing) both.
6. **Where does governance actually live?** RBAC and audit exist at every layer of this folder: engine (Orkes), platform (Druid), control plane (AgentField), approval UX (HumanLayer, CopilotKit), sandbox (Introspection, Paper Compute). Enterprises will not buy six governance layers; consolidation is coming and nobody knows around which layer.
