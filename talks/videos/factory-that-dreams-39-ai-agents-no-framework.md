# The Factory That Dreams: 39 AI Agents, No Framework
> A thermoforming factory owner in India explains how a 100-person company with no ML team built a multi-agent "company brain" that runs its entire go-to-market for about $30,000.

- **Speaker:** Rushabh Doshi, Machinecraft
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=jtzh-GBXBWc) (AI Engineer channel; ~10m, released 2026-06-23)
- **Program:** Online Track 2026

## Summary
Doshi runs Machinecraft, a 100-person factory in India that makes thermoforming machines for seven distinct markets, from hydroponic farm trays to EV panels to medical casings. His starting problem is institutional memory: for three generations the company's real asset, who each customer is, what was quoted in 2019, why one machine needed a custom tweak, lived in exactly three brains, his grandfather's, his father's, and his own, and every departing employee took a chunk of it with them. His response was to build what he calls a twin of the company, named Eira, rather than hire a sales team.

The construction surprised him with its simplicity. The team fed hundreds of gigabytes of private history (quotes, drawings, payment schedules, email threads) into off-the-shelf models that extracted facts, then stored meaning as vectors and relationships as a graph. Doshi stresses there was no model training at all: no GPUs, no fine-tuning, no training bill. The brain is not a smarter model, it is a well-organized memory.

The architecture is a cast of specialist agents rather than one mega-prompt, 39 in the talk title, 36 in his narration. Each has one job and a Greek name: Athena runs the room and pulls specialists into meetings where they argue to a single answer, Prometheus owns the sale, Plutus prices, Hephaestus knows machine specs, Vera fact-checks, and Memnon guards human corrections so a fix stays fixed forever. The system runs nine daily go-to-market jobs, including outbound emails grounded in real company history, pre-call account briefs, quotations, lead revival, inbound replies, and fit qualification. The operator interface is a single Cursor tab, and the stack is real: vector, graph, and CRM databases, three model providers each picked per task, and 213 tools exposed over one protocol, with the unbroken rule that Eira drafts and a human sends.

Memory is engineered in layers because, in Doshi's phrase, a raw language model is a goldfish. Working memory covers the last few minutes; pinned facts, episodic conversation stories, and relationship warmth scores persist; a salience gate bounces junk at the door; corrections beat conflicting facts. Every night Eira runs a sleep cycle that replays the day, consolidates useful information, hunts contradictions, forgets stale material, and turns the day's work into reusable skills, leaving a dream report for Doshi each morning. Each agent also carries a "soul file" derived from five principles of his Jain family business, turned into engineering rules: cross-check before speaking, never speak in absolutes and cite document and date, do your own job, report ugly truths, and never work alone.

The economics are his closing argument. An agency quoted $230,000 to build the system; Machinecraft built it for around $30,000 and runs it for a couple of thousand dollars a month. He has extracted the architecture as Brain OS, a forkable empty nervous system (agents, memory, dream cycle, soul file, all blank) at forkmybrain.org, on the theory that nobody can outsource building a company's brain, only pour their own history into one.

## Notable moments
- [0:02:01](https://www.youtube.com/watch?v=jtzh-GBXBWc&t=121s) The plot twist: hundreds of gigabytes of company history, and no model was ever trained; off-the-shelf models extracted facts into vectors and a graph.
- [0:04:02](https://www.youtube.com/watch?v=jtzh-GBXBWc&t=242s) The pantheon: one agent per job, with Athena chairing meetings where specialists argue to a single answer.
- [0:07:04](https://www.youtube.com/watch?v=jtzh-GBXBWc&t=424s) The nightly dream cycle that consolidates memory, prunes contradictions, and leaves a morning dream report.
- [0:08:06](https://www.youtube.com/watch?v=jtzh-GBXBWc&t=486s) The cost math: a $230,000 agency quote versus roughly $30,000 to build in-house.

## Connections
- [Cognee](../../companies/memory-rag-search/cognee.md), a vendor building the same graph-plus-vector agent memory pattern Machinecraft assembled in-house.
- [GAM: hierarchical graph-based agentic memory](../../papers/memory-research-agents/gam-hierarchical-graph-based-agentic-memory-for-llm-agents.md), research formalizing the graph memory structure Eira uses for relationships.
- [Are we ready for an agent-native memory system?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md), which asks in general form the question Doshi answers with layered memory, salience gating, and sleep-cycle consolidation.
