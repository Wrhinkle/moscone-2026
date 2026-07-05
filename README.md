<div align="center">

# The Moscone Landscape

### Every company, paper, and idea from the AI Engineer World's Fair 2026 — researched, verified, and cross-linked

<p>
<img alt="263 company profiles" src="https://img.shields.io/badge/company_profiles-263-2f81f7?style=flat-square">
<img alt="17 categories" src="https://img.shields.io/badge/categories-17-2f81f7?style=flat-square">
<img alt="40 paper notes" src="https://img.shields.io/badge/paper_notes-40-2f81f7?style=flat-square">
<img alt="5 essays" src="https://img.shields.io/badge/essays-5-2f81f7?style=flat-square">
<img alt="built by 252 agents" src="https://img.shields.io/badge/built_by-252_agents-8957e5?style=flat-square">
</p>

**Pick a door:** 🗺️ [The company landscape](#the-company-landscape--17-categories) · 📚 [The research shelf](#the-research-shelf--40-papers-5-areas) · 🧭 [If you're building X, read Y](#if-youre-building-x-read-y) · ✍️ [Five essays](#five-essays-that-connect-the-dots) · 🛠️ [How this was built](#how-this-repo-was-built)

</div>

---

## Why this exists

From June 30 to July 2, 2026, the AI Engineer World's Fair filled three floors of Moscone West with 263 sponsors — frontier labs, eval platforms, voice stacks, document-AI vendors, agent frameworks, GPU clouds, and at least six startups whose names are un-Googleable common nouns. I walked out with a pocket full of notes like *"lights-off software factory," "Memex,"* and *"tool calls for every aspect of computer usage."*

Expo floors are optimized for logo recall, not understanding. A week later you remember the booth swag; you don't remember which of the four document-parsing vendors actually had customers, which "agent memory" company was a database with a new landing page, or which research paper quietly contradicted half the sales pitches on the floor.

So instead of letting the notes rot, I turned them into a source map and pointed a fleet of research agents at it: **one deep-research agent per company** (founders, funding history, actual products, and — most importantly — evidence of real-world use), **one analyst per paper**, a curator pass to build the navigation you're reading, and a drafting pass to write up the ideas worth arguing about. 252 agents, roughly ten million tokens, and one classification bug later, this repo is the result.

The through-line that emerged — from the notes, the papers, and the floor itself — is that the interesting systems of 2026 are **loops, not chatbots**: observe → condense → decide → act through tools → evaluate → escalate to a human → improve the next pass. Coding agents, back-office intake clerks, voice agents, research monitors — same skeleton, different clothes. Every category README ties back to some part of that loop.

### What makes this different from a sponsor list

- **Funding and founder claims are verified**, not vibes. Every profile marks each claim **Verified** (multiple independent sources), **Reported** (single source or vendor claim), or **Unverified** (couldn't confirm — and the profile says so instead of guessing). A few un-disambiguatable startups are flagged outright. Trust the labels, not the prose.
- **Usage evidence is separated from logo walls.** "Raised $75M" is a weaker signal than "Harvey published a case study about replacing their OCR layer." Profiles hunt for the second kind.
- **The papers talk to the products.** Each paper note names the companies it validates or challenges; each category README links back to the research. The eval vendors and the eval literature are two views of one argument.
- **It's a snapshot, on purpose.** Everything was researched in early July 2026. Funding rounds age fast; the loop thesis ages slower.

---

## The company landscape — 17 categories

Every category folder has a README with "start here" picks, a full profile table (tier, funding posture, standout fact), related papers, and the open questions the category hasn't answered. Counts are profiles per folder.

| Category | Profiles | What it covers |
|---|---:|---|
| [models-inference](companies/models-inference/README.md) | 34 | The supply side of everything: frontier and open-weight labs, serving platforms (Together, Baseten, Fireworks), model routers (OpenRouter, Not Diamond), inference silicon, and training-data vendors. Jurisdiction is now a purchasing criterion — the Chinese open-weight labs (MiniMax, Z.ai) vs. US "sovereign" plays. |
| [evals-observability](companies/evals-observability/README.md) | 26 | "Is it actually working, and how would we know?" Trace capture, evals, production monitoring, and human-feedback data — from platinum eval-natives (Arize, Braintrust) to incumbents (Datadog, Dynatrace) to agents evaluated by running vending machines (Andon Labs). |
| [back-office-automation](companies/back-office-automation/README.md) | 22 | Where agents meet paperwork: document extraction APIs (Reducto, Extend, Bem), finance/contract/vertical operators (Auditoria, Ironclad, Anterior, Wisedocs), and systems of record growing agent surfaces (Atlassian, Notion, ServiceNow). One shared loop: ingest → extract → act → human approval. |
| [agent-orchestration](companies/agent-orchestration/README.md) | 21 | The connective tissue between "the model can call a function" and "an agent runs a multi-day process unattended": durable execution (Temporal, Inngest, Orkes), frameworks (LangChain, LlamaIndex, Mastra), tool/auth layers (Composio), and human-approval layers (HumanLayer). |
| [enterprise-adopters](companies/enterprise-adopters/README.md) | 21 | The demand side — organizations that deploy rather than sell: Optiver's agent-first SDLC, DoorDash's multi-agent reference architecture, LinkedIn's Hiring Assistant. The evidence base for "does this survive production and compliance?" |
| [memory-rag-search](companies/memory-rag-search/README.md) | 19 | How the model gets the right context: vector/graph stores (Qdrant, Neo4j, Turbopuffer), memory layers (Zep, Cognee), live-web acquisition (Bright Data, Exa, Firecrawl, Apify), embeddings and metadata. The most crowded, commoditization-threatened category here. |
| [swe-infrastructure](companies/swe-infrastructure/README.md) | 18 | The delivery plumbing repositioned for agent-written code: sandboxes (E2B, Daytona), verification and gating (Sonar, CircleCI, Meticulous), governed dev environments (Coder), context engines (Unblocked), and agentic editors/terminals (Warp, Zed). |
| [cloud-compute](companies/cloud-compute/README.md) | 16 | The substrate: hyperscaler agent stacks (AWS, Microsoft, Oracle), GPU neoclouds (Crusoe, Nebius, RunPod), edge-agent bets (Cloudflare), containers and sandboxing (Docker, Modal), storage and self-hosted distribution. |
| [coding-agents](companies/coding-agents/README.md) | 16 | Both sides of one trade: agents that generate code (Cognition/Devin, Factory, OpenHands, Cline) and agents that verify it (Qodo, Greptile, Baz) — plus GitHub as the control plane and Tessl's "npm for agent context." |
| [voice-realtime](companies/voice-realtime/README.md) | 14 | The sub-second pipeline, wires to face: telephony (Twilio, Telnyx), WebRTC transport and agent frameworks (LiveKit, Daily/Pipecat), speech models (Deepgram, AssemblyAI, Gradium), managed orchestration (Vapi), avatars and realtime video. |
| [data-infrastructure](companies/data-infrastructure/README.md) | 12 | The data layer re-pitched at agents: MCP-fronted ELT and context stores (Airbyte, dbt), analytics engines (ClickHouse), OLTP/multi-model databases as agent state and memory (PlanetScale, YugabyteDB, SurrealDB), unified integration APIs (Merge). |
| [security-identity](companies/security-identity/README.md) | 11 | Scoped, short-lived, logged access for non-human actors: MCP OAuth land-grabbers (WorkOS, Descope, Scalekit), agent-native IAM (Keycard, Runlayer), and incumbents retrofitting (Auth0, 1Password, Snyk, Tailscale). |
| [vc-community](companies/vc-community/README.md) | 11 | Capital and community nodes, not tools: six check-writers, UC Berkeley (vLLM, Chatbot Arena), media/education, a practitioner community, and one state regulator (DFPI). |
| [fintech-payments](companies/fintech-payments/README.md) | 8 | Agents that pay for things: the ACP vs. AP2 vs. x402 protocol war (Stripe/PayPal vs. Google vs. Coinbase/Circle), agent wallets, and the metering layer that decides what a request may cost (Stigg, Revenium). |
| [browser-computer-use](companies/browser-computer-use/README.md) | 7 | The substrate for agents that click: headless browser fleets (Browserbase), full-OS sandboxes for training and evals (Cua), pixels-to-actions models (Yutori), and agentic browsers/devices for humans. |
| [api-platforms](companies/api-platforms/README.md) | 4 | Four vendors, one convergent bet: the API gateway becomes the agent gateway — REST-to-MCP conversion, A2A traffic governance, agent/tool catalogs (Postman, Gravitee, Solo.io, WSO2). |
| [consumer-ai](companies/consumer-ai/README.md) | 3 | The deliberately small B2C tail — what end users actually pay for (Character.ai as the canonical rise-and-caution story). Intentionally pruned; see the category README's re-filing notes. |

---

## The research shelf — 40 papers, 5 areas

Each area README gives a "how to read this area" ordering, a finding-per-paper table with evidence-strength grades, builder takeaways, and a map back to company categories.

| Area | Notes | Through-line |
|---|---:|---|
| [swe-agents](papers/swe-agents/README.md) | 9 | The measurement gap: bug-fix leaderboards sit in the 70s, but anything closer to real work (features, releases, iteration) knocks agents down 3–7x. Verification discipline moves outcomes more than model choice. |
| [memory-research-agents](papers/memory-research-agents/README.md) | 9 | Agent memory is quietly a data-management problem. No architecture dominates — winners rotate by workload, graph memory pays a 30–40x cost premium, and near-perfect recall says little about acting correctly on old information. |
| [voice-realtime](papers/voice-realtime/README.md) | 9 | Realtime voice is an architecture problem, not a model problem: overlap pipeline stages or lose the latency budget. Models systematically over-trigger; suppression logic belongs in your application layer. |
| [tool-use-governance](papers/tool-use-governance/README.md) | 7 | Governance enforced *outside* the model beats governance the model is asked to follow — and often improves task success at the same time. Covers policy checkpoints, injection-proof architectures, syscall sandboxing, and state-based verification. |
| [planning-architecture](papers/planning-architecture/README.md) | 6 | The binding constraint is upstream of codegen: plans drift unless re-injected, restructuring the spec beats better tooling, and prompts are unreviewed architectural artifacts. |

---

## If you're building X, read Y

The cross-cutting trails — each one walks from vendors to research to an opinionated write-up.

- **A back-office automation** (document intake, invoice/packet auditing, approval workflows) → start at [back-office-automation](companies/back-office-automation/README.md) for the extraction layer ([Reducto](companies/back-office-automation/reducto.md) vs. [Extend](companies/back-office-automation/extend.md) vs. [Bem](companies/back-office-automation/bem.md)) and the regulated-vertical pattern ([Anterior](companies/back-office-automation/anterior.md)). Wire the approval gate with [HumanLayer](companies/agent-orchestration/humanlayer.md) + [Temporal](companies/agent-orchestration/temporal.md)/[Inngest](companies/agent-orchestration/inngest.md) from [agent-orchestration](companies/agent-orchestration/README.md). The research backbone is [Governance by Construction](papers/tool-use-governance/governance-by-construction-for-generalist-agents.md) and [REAgent](papers/planning-architecture/reagent-requirement-driven-llm-agents-for-software-issue-re.md); the opinionated syntheses are [Stop Building Chatbots for the Back Office](blog/drafts/2026-07-02-stop-building-chatbots-for-the-back-office.md) and [Agents Should Prepare Decisions, Not Make Them](blog/drafts/2026-07-02-agents-should-prepare-decisions-not-make-them.md).
- **A voice agent** → [voice-realtime companies](companies/voice-realtime/README.md) for the stack layers (telephony → [LiveKit](companies/voice-realtime/livekit.md)/[Daily](companies/voice-realtime/daily.md) transport → [Deepgram](companies/voice-realtime/deepgram.md)/[AssemblyAI](companies/voice-realtime/assemblyai.md) speech → [Vapi](companies/voice-realtime/vapi.md) if you'd rather buy the loop). Then [papers/voice-realtime](papers/voice-realtime/README.md): the Salesforce reference architecture (~755ms budget) and the τ-Voice reality check (voice keeps only 30–45% of text capability). QA it with [Hamming AI](companies/evals-observability/hamming-ai.md). The itemized version is [The Voice Agent Latency Budget](blog/drafts/2026-07-02-the-voice-agent-latency-budget.md).
- **Adopting coding agents** → [coding-agents](companies/coding-agents/README.md) for the generate/verify split, then [swe-infrastructure](companies/swe-infrastructure/README.md) for what makes the output shippable (sandboxes: [E2B](companies/swe-infrastructure/e2b.md)/[Daytona](companies/swe-infrastructure/daytona.md); verification: [Sonar](companies/swe-infrastructure/sonar.md); codebase context: [Unblocked](companies/swe-infrastructure/unblocked.md)). Calibrate expectations with [papers/swe-agents](papers/swe-agents/README.md) — especially the benchmark-misalignment position paper — and see how [Optiver](companies/enterprise-adopters/optiver.md) and [Block](companies/enterprise-adopters/block.md) did it in production. Companion essay: [Your Coding Agent Has Never Seen a Codebase Like Yours](blog/drafts/2026-07-02-your-coding-agent-has-never-seen-a-codebase-like-yours.md).
- **A memory system** → [memory-rag-search](companies/memory-rag-search/README.md) for the four-layer stack (stores → memory layers → web acquisition → enrichment), with [Zep AI](companies/memory-rag-search/zep-ai.md) and [Cognee](companies/memory-rag-search/cognee.md) as the purpose-built memory layers and [Qdrant](companies/memory-rag-search/qdrant.md)/[Neo4j](companies/memory-rag-search/neo4j.md) under them. Before choosing an architecture, read the agent-native memory survey in [papers/memory-research-agents](papers/memory-research-agents/README.md) (no architecture dominates) and LinkedIn's production memory paper (isolation by structure). Companion essay: [Building the Memex, 80 Years Late](blog/drafts/2026-07-02-building-the-memex-80-years-late.md).
- **An eval stack** → [evals-observability](companies/evals-observability/README.md): [Arize](companies/evals-observability/arize.md) vs. [Braintrust](companies/evals-observability/braintrust.md) for the core loop, [Datadog](companies/evals-observability/datadog.md) for the incumbent argument. Steal from the papers: the eval-hygiene checklist in [swe-agents](papers/swe-agents/README.md), the verifier-beats-LLM-judge result (94.2% vs. 79.2% human agreement) in [tool-use-governance](papers/tool-use-governance/README.md), and plan-compliance metrics in [planning-architecture](papers/planning-architecture/README.md).
- **Securing an agent deployment** → [security-identity](companies/security-identity/README.md) ([WorkOS](companies/security-identity/workos.md) for MCP OAuth, [Keycard](companies/security-identity/keycard.md) + [Runlayer](companies/security-identity/runlayer.md) as the agent-native pair), then the whole of [papers/tool-use-governance](papers/tool-use-governance/README.md) — enforcement outside the model, at the loop, architecture, or syscall layer.
- **Agents that spend money** → [fintech-payments](companies/fintech-payments/README.md) for the protocol war ([Stripe](companies/fintech-payments/stripe.md), [PayPal](companies/fintech-payments/paypal.md), [Circle](companies/fintech-payments/circle.md), [Coinbase](companies/fintech-payments/coinbase.md)) and the budget-enforcement layer ([Stigg](companies/fintech-payments/stigg.md), [Revenium](companies/fintech-payments/revenium.md)).

---

## Five essays that connect the dots

Technical, exploratory drafts written from this repo's research — each one bridges several categories and at least one paper. They carry `draft: true` honestly: opinions are the author's, `TODO: verify` flags mark the claims still being checked.

| Essay | The argument |
|---|---|
| [Stop Building Chatbots for the Back Office](blog/drafts/2026-07-02-stop-building-chatbots-for-the-back-office.md) | The useful shape of back-office AI is an *evaluator* — messy context in, structured state + missing items + human-approvable next actions out. Chat is an interface mismatch for work that has a checklist. |
| [Agents Should Prepare Decisions, Not Make Them](blog/drafts/2026-07-02-agents-should-prepare-decisions-not-make-them.md) | The approval gate is an engineering primitive, not a compliance afterthought — and durable-workflow engines built for microservices are accidentally the right substrate for human latency. |
| [Your Coding Agent Has Never Seen a Codebase Like Yours](blog/drafts/2026-07-02-your-coding-agent-has-never-seen-a-codebase-like-yours.md) | Benchmarks are greenfield; your codebase isn't. The gap is codebase comprehension — and a whole vendor tier exists because of it. Includes a self-benchmark recipe. |
| [Building the Memex, 80 Years Late](blog/drafts/2026-07-02-building-the-memex-80-years-late.md) | Vannevar Bush's 1945 associative-trails machine is now a weekend build from commodity parts. The hard part isn't any component — it's deciding what deserves memory. |
| [The Voice Agent Latency Budget](blog/drafts/2026-07-02-the-voice-agent-latency-budget.md) | Voice agents live or die inside ~800ms mouth-to-ear, and every architectural choice is a withdrawal from that budget. Five research papers read as one debugging checklist. |

The unwritten backlog lives in [`briefs/`](briefs/2026-07-02-aiewf-batch-01.md) — ten ranked idea briefs with theses, outlines, and demo tie-ins. The raw inputs are in [`notes/`](notes/): the [source map](notes/source-map-aiewf-2026.md) and the [original pocket notes](notes/conference-notes-raw.md), typos and all.

---

## How this repo was built

This repo was produced by a fleet of Claude Code agents working from one seed document. The agent definitions live in [`.claude/agents/`](.claude/agents/) — meaning the repo documents its own construction and is rebuildable against a new source map (next year's conference, a reading list, your own market).

| Agent | Role | Output |
|---|---|---|
| [company-researcher](.claude/agents/company-researcher.md) | Researched each sponsor: founders, funding, product, verified vs. reported claims | `companies/<category>/<company>.md` |
| [paper-analyst](.claude/agents/paper-analyst.md) | Located and annotated each paper, with evidence-strength grades | `papers/<area>/<paper>.md` |
| [landscape-curator](.claude/agents/landscape-curator.md) | Built the navigation layer: category and area READMEs, this page | the `README.md` files |
| [blog-ideator](.claude/agents/blog-ideator.md) | Turned the source map into ranked blog briefs | [`briefs/`](briefs/) |
| [blog-drafter](.claude/agents/blog-drafter.md) | Grew briefs into full technical drafts, grounded in the profiles and paper notes | [`blog/drafts/`](blog/drafts/) |

The run itself was a small case study in the loop thesis: 252 agents orchestrated by a deterministic workflow script, which survived a mid-run wifi outage, a session restart, and a rate-limit wall by resuming from a cached journal — no completed research was ever repeated. The one quality bug (21 companies whose names the classifier fumbled into the wrong folder) was fixed by a re-filing agent that re-categorized them from their *researched content* rather than their names, which is more than can be said for most conference attendees.

### Caveats, honestly stated

- **Point-in-time:** researched July 2–5, 2026. Funding figures, headcounts, and product claims age; the Verified/Reported labels tell you how solid each claim was *then*.
- **AI-researched:** every profile was written by an agent with web search, working under explicit rules against fabrication — but agents miss things and sources disagree. A handful of profiles say "could not disambiguate" or "not found in public sources," and that honesty is the feature. Corrections welcome via issue or PR.
- **Opinionated by design:** category one-liners and essay theses take positions. The profiles underneath them separate fact from framing so you can disagree with the framing.

---

<div align="center">

*Built from three days at Moscone West, one pocket of notes, and 252 agents that never got to see the expo hall.*

</div>
