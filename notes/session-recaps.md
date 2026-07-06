# Session recaps — AIEWF 2026

Recaps of talks and conversations from the conference program, June 30 to July 2, 2026,
reconstructed from notes taken in the room. Attributions and details may be imperfect; where a
speaker's name wasn't captured, the recap names the organization. Corrections welcome via issue
or PR.

## Sonar — agent-centric development and whether AI-assisted coding delivers

Referenced a Carnegie Mellon study on whether AI-assisted coding delivers, and drew a distinction
between generating individual code and maintaining software. The proposed working model was an
agent-centric development cycle, guide → verify → solve, built on repo-aware, project-specific
context and constraints. Two ideas stood out. First, lightweight memory injection: agents need
context re-injected as they work, via hooks triggered by tokens consumed, time elapsed, or
specific code being written, rather than one big prompt up front. Second, "zero trust and
multilayer verification" as the framing for reviewing AI-written code. On technical debt: models
purpose-built to analyze existing systems, each holding deep context on the codebase up to a
cutoff, like an engineer frozen in time, so future agents can interrogate them about the legacy
pieces. The through-line of the talk was compounding loops, and that the industry is contracting
back toward rigor after a period of lean, seat-of-the-pants AI coding. Companion material:
sonar.com/acdc. Related folders: [swe-infrastructure](../companies/swe-infrastructure/README.md),
[papers/swe-agents](../papers/swe-agents/README.md).

## AWS Builder Loft — Bedrock AgentCore

Session at the AWS Builder Loft on building with Bedrock AgentCore. Companion samples:
[awslabs/agentcore-samples](https://github.com/awslabs/agentcore-samples). Related folder:
[cloud-compute](../companies/cloud-compute/README.md).

## Google DeepMind — RL, network topology, and what comes after code

Wide-ranging: model and network topology in reinforcement learning; Google X and Project
Pitchfork; inductive thinking, architecture, and security guardrails. On code, the argument was
about complexity and how ingestible a codebase stays over time, with a case for Rust where
precision matters, and an open question worth sitting with: what would a programming language
designed for LLMs look like, given that it doesn't need to be human-readable or human-editable?
On what's next: heavy biology and chemistry, where relationships from drugs and gene therapy are
easier to break down and test, and beyond that, AI exploratory science operating past human
involvement and perception. Related folder:
[models-inference](../companies/models-inference/README.md).

## Stanford PlatformLab — Homa, a transport protocol for AI networks

AI workloads need network performance that TCP and RDMA don't deliver; both carry latency
penalties that matter at datacenter scale. Homa is a message-oriented transport protocol built as
the replacement, with a Linux kernel module at
[PlatformLab/HomaModule](https://github.com/PlatformLab/HomaModule). Presented by the Stanford
group behind it (John Ousterhout's lab; Behnam Montazeri among the authors). Runs on commodity
hardware, including a DGX.

## DSPy — AI programs as functions

The DSPy team on treating AI loops and programs as composable functions rather than prompt
chains, with invoice and tax extraction as the worked examples. Referenced techniques: RLM, GEPA,
and BetterTogether. An honest open question from the audience side: how much of this is already
covered by the skills-and-agent-definitions pattern in agent harnesses? Related folder:
[agent-orchestration](../companies/agent-orchestration/README.md).

## Anthropic — interpretability, and a process for not handing off the work

Two separate Anthropic conversations. The first centered on interpretability
([transformer-circuits.pub](https://transformer-circuits.pub)) and a question-asking process for
working with agents on real problems, six steps: a blindspot pass; brainstorming with four wildly
different prototypes; an interview phase that prioritizes questions capable of changing the
architecture; a references pass to find existing code or ideas equivalent to what you have in
mind; implementation notes; and a quiz after the fact. The summary line: don't hand off the work.
Also memorable: "tradeoffs are not real at Anthropic when tokens are not a factor," and
exploration as the organizing theme.

The second covered product direction: multiplayer as the operative word, persistent artifacts,
closing the gaps between code, chat, and cowork, killing styles in favor of skills, and "project
unship," the periodic question of what's no longer necessary.

## Stephen Chin — GraphRAG and memory beyond vector similarity

The core claim: vector-space similarity is not the same as true relational mapping. Vector
databases (Pinecone, LanceDB) get you semantic nearness; GraphRAG gets you multi-hop queries and,
importantly for agents, a traversal path that is traceable and auditable, which matters when an
orchestration layer needs to audit decision-making. Covered Goose (which treats memory like an
MCP server), Cognee, and the pipeline of extraction and modeling. Companion material: *GraphRAG:
The Definitive Guide* (Stephen Chin, Michael Hunger, Jesús Barrasa) and the Neo4j Graph Academy.
Related folder: [memory-rag-search](../companies/memory-rag-search/README.md).

## Yohei Nakajima — world models for long-running agents

On agent construction: Kafka-style event streams and blackboard architectures beat request-reply
for multi-agent systems. The idea that stuck: experiential and predictive world models are
probably necessary for long-running agents and tasks, not dissimilar to dreaming. Also covered
ActiveGraph Labs work, including running autonomous research loops for writing. Related folders:
[agent-orchestration](../companies/agent-orchestration/README.md),
[papers/memory-research-agents](../papers/memory-research-agents/README.md).

## New York Times engineers — local agents for games

AI and game theory, with reinforcement learning as the historical training method for game
models (EfficientZero; DQN, 2015). Local agents for games, gaze models, and resource and system
management as testbeds. ARC-AGI scores framed as a meaningful signal for complex-systems
capability. Related folder: [browser-computer-use](../companies/browser-computer-use/README.md).

## Vercel — eve, "Next.js for agents"

Vercel's agent framework is called eve ([eve.dev](https://eve.dev)): runtime, channels, SDK,
sandbox, tools, and subagents as the primitives. Theo Browne's argument from the same
conversation: you have to be able to remove your own opinions from the coding process and give
the model space to use its training scope; "delete your darlings." Open questions raised: what
kind of OS and system do agents need for better work, what counts as ambitious with a
frontier-class model, and how you run a sizeable team of agents (1,000-plus) without going broke.
Tool discovery was flagged as an unsolved, useful problem. Related folders:
[coding-agents](../companies/coding-agents/README.md),
[swe-infrastructure](../companies/swe-infrastructure/README.md).

## Garry Tan — the AI-native company

The definition that traveled: an AI-native company creates as much as possible with AI, sees
what the AI cannot or will not do, and only then hires a person to do that work. Plus YC Startup
School as the on-ramp. Related folder: [vc-community](../companies/vc-community/README.md).

## Themes that recurred across unrelated sessions

Reconstructed from the notes, not imposed on them: verification discipline for agent-written
code (Sonar's zero-trust framing, evals everywhere); memory that goes past vector similarity
(GraphRAG's auditable traversal, world models for long-running agents); and agent-native
infrastructure as an open design space (a programming language for LLMs, a transport protocol
for AI networks, an OS for agents, frameworks like eve).
