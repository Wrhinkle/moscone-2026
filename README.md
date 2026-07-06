<div align="center">

# AI Engineer World's Fair 2026: The Landscape

### Sponsor research, session recaps, and research-paper notes from AIEWF 2026, cross-linked into one reference

<p>
<img alt="263 company profiles" src="https://img.shields.io/badge/company_profiles-263-2f81f7?style=flat-square">
<img alt="17 categories" src="https://img.shields.io/badge/categories-17-2f81f7?style=flat-square">
<img alt="40 paper notes" src="https://img.shields.io/badge/paper_notes-40-2f81f7?style=flat-square">
<img alt="11 session recaps" src="https://img.shields.io/badge/session_recaps-11-2f81f7?style=flat-square">
</p>

Jump to: [companies](#the-company-landscape) · [papers](#the-papers) · [sessions](#the-sessions) · [if you're building X, read Y](#if-youre-building-x-read-y) · [method](#method)

</div>

## What this is

The AI Engineer World's Fair ran June 30 to July 2, 2026 at Moscone West in San Francisco, with 263 sponsor companies and a program dominated by agents: coding agents, evals, memory systems, voice, and the infrastructure underneath all of it. This repo is a reference for anyone trying to understand that ecosystem without having been there:

- [`companies/`](companies/) — a researched profile of every sponsor: founders, funding, what the product actually is, and evidence that anyone uses it, organized into 17 category folders
- [`papers/`](papers/) — notes on 40 recent research papers in agentic AI, graded by evidence strength, organized into 5 areas
- [`notes/`](notes/) — [recaps of conference sessions](notes/session-recaps.md) and the [source map](notes/source-map-aiewf-2026.md) the research started from

The three layers link to each other. Vendor claims sit next to the research that supports or undercuts them, and session recaps point into the company categories they touched.

## How to read the profiles

Every claim in a profile carries a label. **Verified** means at least two independent sources agree. **Reported** means one source, usually the vendor. When a claim couldn't be confirmed, the profile says "not found in public sources" and moves on. A few companies with un-Googleable names (Band, Kimchi, Zero) get profiles that lay out the candidates and admit which one is probably the sponsor.

The labels exist because funding news is easy to find and tells you little. The more useful question about any vendor is: does anyone use this? So profiles rank usage evidence above money. A published case study beats a logo wall. A public pricing page beats a waitlist. "Harvey replaced their OCR layer with Reducto and wrote about it" beats everything.

The research is a snapshot of the first week of July 2026. Funding figures rot in months; the category structure rots slower.

## The company landscape

Seventeen category folders. Each has a README with picks for where to start, a table of every profile (tier, funding posture, standout fact), related papers, and open questions. Counts are profiles per folder.

| Category | Profiles | What it covers |
|---|---:|---|
| [models-inference](companies/models-inference/README.md) | 34 | The supply side: frontier and open-weight labs, serving platforms (Together, Baseten, Fireworks), model routers (OpenRouter, Not Diamond), inference silicon, and training-data vendors. Jurisdiction is now a purchasing criterion, with Chinese open-weight labs (MiniMax, Z.ai) selling against US "sovereign" plays. |
| [evals-observability](companies/evals-observability/README.md) | 26 | Trace capture, evals, production monitoring, and human-feedback data: eval-native platforms (Arize, Braintrust), incumbents extending down (Datadog, Dynatrace), and Andon Labs, which evaluates agents by having them run vending machines. |
| [back-office-automation](companies/back-office-automation/README.md) | 22 | Where agents meet paperwork. Document extraction APIs (Reducto, Extend, Bem), finance and contract operators (Auditoria, Ironclad, Anterior, Wisedocs), and systems of record growing agent surfaces (Atlassian, Notion, ServiceNow). The shared loop: ingest, extract, act, human approval. |
| [agent-orchestration](companies/agent-orchestration/README.md) | 21 | What sits between "the model can call a function" and "an agent runs a multi-day process unattended": durable execution (Temporal, Inngest, Orkes), frameworks (LangChain, LlamaIndex, Mastra), tool and auth layers (Composio), human-approval layers (HumanLayer). |
| [enterprise-adopters](companies/enterprise-adopters/README.md) | 21 | The demand side. Organizations that deploy rather than sell: Optiver's agent-first SDLC, DoorDash's multi-agent reference architecture, LinkedIn's Hiring Assistant. This is the evidence base for whether any of this survives production and compliance. |
| [memory-rag-search](companies/memory-rag-search/README.md) | 19 | How the model gets the right context: vector and graph stores (Qdrant, Neo4j, Turbopuffer), memory layers (Zep, Cognee), live-web acquisition (Bright Data, Exa, Firecrawl, Apify), embeddings and metadata. The most crowded category here, and the one most threatened by commoditization. |
| [swe-infrastructure](companies/swe-infrastructure/README.md) | 18 | Delivery plumbing repositioned for agent-written code: sandboxes (E2B, Daytona), verification and gating (Sonar, CircleCI, Meticulous), governed dev environments (Coder), context engines (Unblocked), agentic editors and terminals (Warp, Zed). |
| [cloud-compute](companies/cloud-compute/README.md) | 16 | The substrate: hyperscaler agent stacks (AWS, Microsoft, Oracle), GPU neoclouds (Crusoe, Nebius, RunPod), Cloudflare's edge-agent bet, containers and sandboxing (Docker, Modal), storage and self-hosted distribution. |
| [coding-agents](companies/coding-agents/README.md) | 16 | Two sides of one trade: agents that generate code (Cognition/Devin, Factory, OpenHands, Cline) and agents that verify it (Qodo, Greptile, Baz). Plus GitHub as the control plane and Tessl's "npm for agent context." |
| [voice-realtime](companies/voice-realtime/README.md) | 14 | The sub-second pipeline: telephony (Twilio, Telnyx), WebRTC transport and agent frameworks (LiveKit, Daily/Pipecat), speech models (Deepgram, AssemblyAI, Gradium), managed orchestration (Vapi), avatars and realtime video. |
| [data-infrastructure](companies/data-infrastructure/README.md) | 12 | The data layer re-pitched at agents: MCP-fronted ELT and context stores (Airbyte, dbt), analytics engines (ClickHouse), databases positioning as agent state and memory (PlanetScale, YugabyteDB, SurrealDB), unified integration APIs (Merge). |
| [security-identity](companies/security-identity/README.md) | 11 | Scoped, short-lived, logged access for non-human actors: MCP OAuth providers (WorkOS, Descope, Scalekit), agent-native IAM (Keycard, Runlayer), and incumbents retrofitting (Auth0, 1Password, Snyk, Tailscale). |
| [vc-community](companies/vc-community/README.md) | 11 | Six check-writers, UC Berkeley (vLLM, Chatbot Arena), media and education, a practitioner community, and one state regulator (DFPI). |
| [fintech-payments](companies/fintech-payments/README.md) | 8 | Agents that pay for things. The protocol fight between ACP, AP2, and x402 (Stripe/PayPal vs. Google vs. Coinbase/Circle), agent wallets, and the metering layer that decides what a request may cost (Stigg, Revenium). |
| [browser-computer-use](companies/browser-computer-use/README.md) | 7 | Infrastructure for agents that click: headless browser fleets (Browserbase), full-OS sandboxes for training and evals (Cua), pixels-to-actions models (Yutori), agentic browsers and devices for humans. |
| [api-platforms](companies/api-platforms/README.md) | 4 | Four vendors making the same bet, that the API gateway becomes the agent gateway: REST-to-MCP conversion, A2A traffic governance, agent and tool catalogs (Postman, Gravitee, Solo.io, WSO2). |
| [consumer-ai](companies/consumer-ai/README.md) | 3 | The small B2C tail. Character.ai is the canonical rise-and-caution story. Intentionally pruned; the category README explains the re-filing. |

## The papers

Forty notes in five areas. Each area README suggests a reading order, grades the evidence strength of every paper, and maps findings back to the company categories they support or undercut.

| Area | Notes | What the papers add up to |
|---|---:|---|
| [swe-agents](papers/swe-agents/README.md) | 9 | Bug-fix leaderboards sit in the 70s, but anything closer to real work (features, releases, iteration) knocks agents down 3 to 7x. Verification discipline moves outcomes more than model choice. |
| [memory-research-agents](papers/memory-research-agents/README.md) | 9 | Agent memory is quietly a data-management problem. No architecture dominates, winners rotate by workload, graph memory pays a 30 to 40x cost premium, and near-perfect recall says little about acting correctly on old information. |
| [voice-realtime](papers/voice-realtime/README.md) | 9 | Realtime voice is an architecture problem before it is a model problem: overlap pipeline stages or lose the latency budget. Models systematically over-trigger, so suppression logic belongs in your application layer. |
| [tool-use-governance](papers/tool-use-governance/README.md) | 7 | Governance enforced outside the model beats governance the model is asked to follow, and it often improves task success at the same time. Policy checkpoints, injection-proof architectures, syscall sandboxing, state-based verification. |
| [planning-architecture](papers/planning-architecture/README.md) | 6 | The binding constraint is upstream of codegen. Plans drift unless re-injected, restructuring the spec beats better tooling, and prompts are unreviewed architectural artifacts. |

## The sessions

[notes/session-recaps.md](notes/session-recaps.md) has recaps of eleven talks and conversations from the program, reconstructed from notes taken in the room: Sonar on agent-centric development and zero-trust verification of AI-written code; Google DeepMind on RL, Rust, and what a programming language designed for LLMs would look like; Stanford PlatformLab on Homa, a transport protocol built for AI network loads; the DSPy team on AI programs as functions; Anthropic on interpretability and a six-step process for not handing off the work; Stephen Chin on GraphRAG and why vector similarity is not relational mapping; Yohei Nakajima on world models for long-running agents; NYT engineers on local agents for games; Vercel on eve ("Next.js for agents"); Garry Tan on the AI-native company; and AWS on Bedrock AgentCore.

Themes that recurred across unrelated sessions, taken from the notes rather than imposed on them: verification discipline for agent-written code, memory that goes past vector similarity, and agent-native infrastructure (languages, transports, operating environments) as a wide-open design space.

## If you're building X, read Y

Each trail walks from vendors to research.

**A back-office automation** (document intake, invoice or packet auditing, approval workflows). Start at [back-office-automation](companies/back-office-automation/README.md) for the extraction layer ([Reducto](companies/back-office-automation/reducto.md) vs. [Extend](companies/back-office-automation/extend.md) vs. [Bem](companies/back-office-automation/bem.md)) and the regulated-vertical pattern ([Anterior](companies/back-office-automation/anterior.md)). Wire the approval gate with [HumanLayer](companies/agent-orchestration/humanlayer.md) plus [Temporal](companies/agent-orchestration/temporal.md) or [Inngest](companies/agent-orchestration/inngest.md). The research backbone is [Governance by Construction](papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) and [REAgent](papers/planning-architecture/reagent-requirement-driven-llm-agents-for-software-issue-re.md).

**A voice agent.** [voice-realtime companies](companies/voice-realtime/README.md) covers the stack layers: telephony, then [LiveKit](companies/voice-realtime/livekit.md) or [Daily](companies/voice-realtime/daily.md) for transport, [Deepgram](companies/voice-realtime/deepgram.md) or [AssemblyAI](companies/voice-realtime/assemblyai.md) for speech, and [Vapi](companies/voice-realtime/vapi.md) if you'd rather buy the whole loop. Then [papers/voice-realtime](papers/voice-realtime/README.md) for the Salesforce reference architecture (a ~755ms budget) and the τ-Voice result that voice keeps only 30 to 45% of text capability. QA with [Hamming AI](companies/evals-observability/hamming-ai.md).

**Adopting coding agents.** [coding-agents](companies/coding-agents/README.md) for the generate/verify split, then [swe-infrastructure](companies/swe-infrastructure/README.md) for what makes the output shippable: sandboxes ([E2B](companies/swe-infrastructure/e2b.md), [Daytona](companies/swe-infrastructure/daytona.md)), verification ([Sonar](companies/swe-infrastructure/sonar.md)), codebase context ([Unblocked](companies/swe-infrastructure/unblocked.md)). Calibrate expectations with [papers/swe-agents](papers/swe-agents/README.md), especially the benchmark-misalignment position paper, and read how [Optiver](companies/enterprise-adopters/optiver.md) and [Block](companies/enterprise-adopters/block.md) did it in production.

**A memory system.** [memory-rag-search](companies/memory-rag-search/README.md) lays out the stack: stores, memory layers, web acquisition, enrichment. [Zep AI](companies/memory-rag-search/zep-ai.md) and [Cognee](companies/memory-rag-search/cognee.md) are the purpose-built memory layers, with [Qdrant](companies/memory-rag-search/qdrant.md) and [Neo4j](companies/memory-rag-search/neo4j.md) underneath. Before committing to an architecture, read the agent-native memory survey in [papers/memory-research-agents](papers/memory-research-agents/README.md) and LinkedIn's production memory paper. The GraphRAG session recap covers why traversal auditability matters for orchestration.

**An eval stack.** [evals-observability](companies/evals-observability/README.md): [Arize](companies/evals-observability/arize.md) vs. [Braintrust](companies/evals-observability/braintrust.md) for the core loop, [Datadog](companies/evals-observability/datadog.md) for the incumbent argument. From the papers, take the eval-hygiene checklist in [swe-agents](papers/swe-agents/README.md), the verifier-beats-LLM-judge result (94.2% vs. 79.2% human agreement) in [tool-use-governance](papers/tool-use-governance/README.md), and the plan-compliance metrics in [planning-architecture](papers/planning-architecture/README.md).

**Securing an agent deployment.** [security-identity](companies/security-identity/README.md), with [WorkOS](companies/security-identity/workos.md) for MCP OAuth and [Keycard](companies/security-identity/keycard.md) plus [Runlayer](companies/security-identity/runlayer.md) as the agent-native pair. Then all of [papers/tool-use-governance](papers/tool-use-governance/README.md): enforcement at the loop, architecture, or syscall layer.

**Agents that spend money.** [fintech-payments](companies/fintech-payments/README.md) for the protocol fight ([Stripe](companies/fintech-payments/stripe.md), [PayPal](companies/fintech-payments/paypal.md), [Circle](companies/fintech-payments/circle.md), [Coinbase](companies/fintech-payments/coinbase.md)) and the budget-enforcement layer ([Stigg](companies/fintech-payments/stigg.md), [Revenium](companies/fintech-payments/revenium.md)).

## Method

A fleet of Claude Code research agents built this repo from the seed document in [`notes/`](notes/source-map-aiewf-2026.md): one agent per company, one per paper, then curation passes for the navigation. The agent definitions are in [`.claude/agents/`](.claude/agents/), so the repo documents its own construction and can be rebuilt against a different source (next year's sponsor list, a different conference, a reading list).

| Agent | Role | Output |
|---|---|---|
| [company-researcher](.claude/agents/company-researcher.md) | Researched each sponsor: founders, funding, product, verified vs. reported claims | `companies/<category>/<company>.md` |
| [paper-analyst](.claude/agents/paper-analyst.md) | Located and annotated each paper, with evidence-strength grades | `papers/<area>/<paper>.md` |
| [landscape-curator](.claude/agents/landscape-curator.md) | Built the category and area READMEs and this page | the `README.md` files |

Caveats, plainly: research dates are July 2 to 5, 2026. The agents had web search and explicit rules against fabrication, but automated research misses things and sources disagree. Some profiles say "could not disambiguate" or "not found in public sources," which is working as intended. Session recaps are reconstructed from notes taken in the room, so attributions may be imperfect. If you find an error, open an issue or a PR.
