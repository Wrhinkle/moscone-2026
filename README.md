<div align="center">

# The Moscone Landscape

### Company research, paper notes, and essays from the AI Engineer World's Fair 2026

<p>
<img alt="263 company profiles" src="https://img.shields.io/badge/company_profiles-263-2f81f7?style=flat-square">
<img alt="17 categories" src="https://img.shields.io/badge/categories-17-2f81f7?style=flat-square">
<img alt="40 paper notes" src="https://img.shields.io/badge/paper_notes-40-2f81f7?style=flat-square">
<img alt="5 essays" src="https://img.shields.io/badge/essays-5-2f81f7?style=flat-square">
<img alt="built by 252 agents" src="https://img.shields.io/badge/built_by-252_agents-8957e5?style=flat-square">
</p>

Jump to: [the company landscape](#the-company-landscape) · [the papers](#the-papers) · [if you're building X, read Y](#if-youre-building-x-read-y) · [the essays](#the-essays) · [how this was built](#how-this-was-built)

</div>

## Why this exists

The AI Engineer World's Fair ran June 30 to July 2, 2026, across three floors of Moscone West in San Francisco. 263 companies sponsored it. I came home with notes like "lights-off software factory," "Memex," and "tool calls for every aspect of computer usage," and no reliable memory of which of the four document-parsing vendors on the expo floor had actual customers.

That memory problem is normal after a conference. The fix I tried this year: turn the notes into a source list and have research agents work through the whole thing. One agent per company, digging up founders, funding history, what the product actually is, and whether anyone verifiably uses it. One agent per paper from my reading list. Then a pass to build navigation and a pass to draft essays about the ideas worth arguing over. 252 agents ran over about three days, interrupted twice by hotel wifi and once by a rate limit.

This repo is what they produced.

## How to read the profiles

Claims in company profiles carry labels. **Verified** means multiple independent sources agree. **Reported** means a single source, often the vendor. When an agent couldn't confirm something, the profile says "not found in public sources" instead of guessing, and a few profiles for startups with un-Googleable names just describe the ambiguity and list the candidates.

Profiles weight usage evidence above funding news, because a published customer case study says more about a product than a Series B does. Where a research paper contradicts a vendor pitch, the profile links the paper. Everything was researched in the first week of July 2026, so treat funding figures and headcounts as a snapshot.

One idea kept showing up in the notes, the papers, and the booth demos: the systems that work are loops. Observe, condense, decide, act through tools, check the result, hand risky calls to a human. Most category READMEs point back to whichever part of that loop their vendors sell.

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

## If you're building X, read Y

Each trail walks from vendors to research to an essay.

**A back-office automation** (document intake, invoice or packet auditing, approval workflows). Start at [back-office-automation](companies/back-office-automation/README.md) for the extraction layer ([Reducto](companies/back-office-automation/reducto.md) vs. [Extend](companies/back-office-automation/extend.md) vs. [Bem](companies/back-office-automation/bem.md)) and the regulated-vertical pattern ([Anterior](companies/back-office-automation/anterior.md)). Wire the approval gate with [HumanLayer](companies/agent-orchestration/humanlayer.md) plus [Temporal](companies/agent-orchestration/temporal.md) or [Inngest](companies/agent-orchestration/inngest.md). The research backbone is [Governance by Construction](papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) and [REAgent](papers/planning-architecture/reagent-requirement-driven-llm-agents-for-software-issue-re.md). The essays: [Stop Building Chatbots for the Back Office](blog/drafts/2026-07-02-stop-building-chatbots-for-the-back-office.md) and [Agents Should Prepare Decisions, Not Make Them](blog/drafts/2026-07-02-agents-should-prepare-decisions-not-make-them.md).

**A voice agent.** [voice-realtime companies](companies/voice-realtime/README.md) covers the stack layers: telephony, then [LiveKit](companies/voice-realtime/livekit.md) or [Daily](companies/voice-realtime/daily.md) for transport, [Deepgram](companies/voice-realtime/deepgram.md) or [AssemblyAI](companies/voice-realtime/assemblyai.md) for speech, and [Vapi](companies/voice-realtime/vapi.md) if you'd rather buy the whole loop. Then [papers/voice-realtime](papers/voice-realtime/README.md) for the Salesforce reference architecture (a ~755ms budget) and the τ-Voice result that voice keeps only 30 to 45% of text capability. QA with [Hamming AI](companies/evals-observability/hamming-ai.md). The essay: [The Voice Agent Latency Budget](blog/drafts/2026-07-02-the-voice-agent-latency-budget.md).

**Adopting coding agents.** [coding-agents](companies/coding-agents/README.md) for the generate/verify split, then [swe-infrastructure](companies/swe-infrastructure/README.md) for what makes the output shippable: sandboxes ([E2B](companies/swe-infrastructure/e2b.md), [Daytona](companies/swe-infrastructure/daytona.md)), verification ([Sonar](companies/swe-infrastructure/sonar.md)), codebase context ([Unblocked](companies/swe-infrastructure/unblocked.md)). Calibrate expectations with [papers/swe-agents](papers/swe-agents/README.md), especially the benchmark-misalignment position paper, and read how [Optiver](companies/enterprise-adopters/optiver.md) and [Block](companies/enterprise-adopters/block.md) did it in production. The essay: [Your Coding Agent Has Never Seen a Codebase Like Yours](blog/drafts/2026-07-02-your-coding-agent-has-never-seen-a-codebase-like-yours.md).

**A memory system.** [memory-rag-search](companies/memory-rag-search/README.md) lays out the stack: stores, memory layers, web acquisition, enrichment. [Zep AI](companies/memory-rag-search/zep-ai.md) and [Cognee](companies/memory-rag-search/cognee.md) are the purpose-built memory layers, with [Qdrant](companies/memory-rag-search/qdrant.md) and [Neo4j](companies/memory-rag-search/neo4j.md) underneath. Before committing to an architecture, read the agent-native memory survey in [papers/memory-research-agents](papers/memory-research-agents/README.md) and LinkedIn's production memory paper. The essay: [Building the Memex, 80 Years Late](blog/drafts/2026-07-02-building-the-memex-80-years-late.md).

**An eval stack.** [evals-observability](companies/evals-observability/README.md): [Arize](companies/evals-observability/arize.md) vs. [Braintrust](companies/evals-observability/braintrust.md) for the core loop, [Datadog](companies/evals-observability/datadog.md) for the incumbent argument. From the papers, take the eval-hygiene checklist in [swe-agents](papers/swe-agents/README.md), the verifier-beats-LLM-judge result (94.2% vs. 79.2% human agreement) in [tool-use-governance](papers/tool-use-governance/README.md), and the plan-compliance metrics in [planning-architecture](papers/planning-architecture/README.md).

**Securing an agent deployment.** [security-identity](companies/security-identity/README.md), with [WorkOS](companies/security-identity/workos.md) for MCP OAuth and [Keycard](companies/security-identity/keycard.md) plus [Runlayer](companies/security-identity/runlayer.md) as the agent-native pair. Then all of [papers/tool-use-governance](papers/tool-use-governance/README.md): enforcement at the loop, architecture, or syscall layer.

**Agents that spend money.** [fintech-payments](companies/fintech-payments/README.md) for the protocol fight ([Stripe](companies/fintech-payments/stripe.md), [PayPal](companies/fintech-payments/paypal.md), [Circle](companies/fintech-payments/circle.md), [Coinbase](companies/fintech-payments/coinbase.md)) and the budget-enforcement layer ([Stigg](companies/fintech-payments/stigg.md), [Revenium](companies/fintech-payments/revenium.md)).

## The essays

Five drafts written from this research. Each bridges several categories and at least one paper. They carry `draft: true` honestly; `TODO: verify` flags mark claims still being checked.

| Essay | The argument |
|---|---|
| [Stop Building Chatbots for the Back Office](blog/drafts/2026-07-02-stop-building-chatbots-for-the-back-office.md) | Back-office AI works better as an evaluator: messy context in, structured state and missing items and human-approvable next actions out. Chat is a poor interface for work that has a checklist. |
| [Agents Should Prepare Decisions, Not Make Them](blog/drafts/2026-07-02-agents-should-prepare-decisions-not-make-them.md) | The approval gate is an engineering primitive. Durable-workflow engines built for microservices turn out to be the right substrate for human-speed decisions. |
| [Your Coding Agent Has Never Seen a Codebase Like Yours](blog/drafts/2026-07-02-your-coding-agent-has-never-seen-a-codebase-like-yours.md) | Benchmarks are greenfield and your codebase isn't. The gap is codebase comprehension, and a whole vendor tier exists because of it. Includes a self-benchmark recipe. |
| [Building the Memex, 80 Years Late](blog/drafts/2026-07-02-building-the-memex-80-years-late.md) | Vannevar Bush's 1945 associative-trails machine is now a weekend build from commodity parts. The hard part is deciding what deserves memory. |
| [The Voice Agent Latency Budget](blog/drafts/2026-07-02-the-voice-agent-latency-budget.md) | Voice agents live or die inside roughly 800ms mouth-to-ear, and every architectural choice spends part of that budget. Five papers read as one debugging checklist. |

The unwritten backlog is in [`briefs/`](briefs/2026-07-02-aiewf-batch-01.md): ten idea briefs with theses, outlines, and demo tie-ins. The raw inputs are in [`notes/`](notes/), including the [source map](notes/source-map-aiewf-2026.md) and the [original pocket notes](notes/conference-notes-raw.md), typos included.

## How this was built

A fleet of Claude Code agents worked from one seed document. Their definitions live in [`.claude/agents/`](.claude/agents/), so the repo documents its own construction. Point the same agents at a different source map (next year's sponsor list, a reading list, your own market) and you get a different landscape.

| Agent | Role | Output |
|---|---|---|
| [company-researcher](.claude/agents/company-researcher.md) | Researched each sponsor: founders, funding, product, verified vs. reported claims | `companies/<category>/<company>.md` |
| [paper-analyst](.claude/agents/paper-analyst.md) | Located and annotated each paper, with evidence-strength grades | `papers/<area>/<paper>.md` |
| [landscape-curator](.claude/agents/landscape-curator.md) | Built the category and area READMEs and this page | the `README.md` files |
| [blog-ideator](.claude/agents/blog-ideator.md) | Turned the source map into ranked blog briefs | [`briefs/`](briefs/) |
| [blog-drafter](.claude/agents/blog-drafter.md) | Grew briefs into full drafts, grounded in the profiles and paper notes | [`blog/drafts/`](blog/drafts/) |

One deterministic workflow script drove all 252 agents. It broke three times: hotel wifi died mid-run, the host session restarted, and a rate limit killed 102 agents at once. Each time it resumed from a journal of completed work without repeating any research. The one real bug was a classifier that matched companies by name and filed 21 of them in the wrong folder. A cleanup agent re-read those profiles and re-filed them by what the companies actually do.

### Caveats

Research dates: July 2 to 5, 2026. The agents had web search and explicit rules against fabrication, but agents miss things and sources disagree. Some profiles say "could not disambiguate" or "not found in public sources," which is working as intended. If you find an error, open an issue or a PR.
