# Architecture Without Architects: How AI Coding Agents Shape Software Architecture

- **Status:** Located — [arXiv:2604.04990](https://arxiv.org/abs/2604.04990) (cs.SE, cs.AI)
- **Area:** planning-architecture
- **Authors / venue / date:** Phongsakon Mark Konrad, Tim Lukas Adam, Riccardo Terrenzi, Serkan Ayvaz — arXiv preprint, submitted 2026-04-05

## Problem
Coding agents pick frameworks, scaffold infrastructure, and wire integrations in seconds — real architectural decisions — but almost nobody reviews them as architecture. The paper names this "vibe architecting": system structure shaped by prompt wording rather than deliberate design, with no feedback loop connecting agent decisions to established architectural knowledge.

## Approach
Analytical paper plus a controlled demonstration. It identifies five mechanisms by which agents make implicit architectural choices: (1) model selection (each model has a distinct "coding personality"), (2) task decomposition (sub-agents/worktrees set module boundaries), (3) default configuration (training-data priors stand in for design), (4) scaffolding/single-prompt generation (collapses many decisions into one interaction), (5) integration protocols (MCP vs. hardcoded access). It then proposes six prompt-architecture coupling patterns mapping prompt features to required infrastructure — structured output, few-shot examples, RAG, and context reduction are *contingent* (may weaken as models improve); function calling and ReAct-style orchestration are *fundamental* (persist regardless of capability). Demo: the same customer-service chatbot task, three prompt wordings, same agent (Claude Code) and model.

## Key findings
- Prompt wording alone changed system structure: Variant A ("answer FAQ questions") → 141 LoC, 2 files; Variant B ("return structured JSON with schema validation") → 472 LoC (Zod + retry + fallback), 4 files; Variant C ("agent with tool access") → 827 LoC (SQLite, tool registry, agent loop), 6 files.
- That is a 5.9× code and 3× file spread for identical functional requirements, with different dependency graphs and failure modes.
- Contingent vs. fundamental split gives a lens for which prompt-driven infrastructure to expect to become obsolete.

## Limitations & open questions
Authors concede "vibe architecting" is an unvalidated analytical construct; each prompt was run once, with one agent/model (no variance estimate, no cross-agent generalization); patterns were drawn from LangChain/LlamaIndex/provider docs and are admittedly non-exhaustive as of early 2026. A skeptic would ask whether more LoC/components is actually worse, and whether AGENTS.md-style constraints already tame this in practice.

## Why builders should care
Treat prompts and agent config files as architectural artifacts: review them, record them in ADRs, and set complexity thresholds that trigger review when scaffolding balloons. Before greenlighting agent-generated services, demand an impact statement (new components, new failure modes) — the paper shows one clause in a prompt can add 330 LoC of infrastructure you now own.

## Related companies in this landscape
- **Qodo / Sonar / Greptile / Baz** — code-review products are the natural home for the "review architectural decisions, not just diffs" practice the paper calls for.
- **Cognition / Factory / OpenHands / Cline / Cursor-class agents (Zed, Warp, Coder)** — the tools doing the vibe architecting; mechanism 2 (task decomposition) directly describes their sub-agent/worktree designs.
- **Tessl** — spec-centric development is essentially the paper's "prompt as reviewed architectural artifact" turned into a product.
- **Sourcegraph / Unblocked** — codebase-context tools address the missing feedback loop between agent decisions and existing architectural knowledge.
- **LangChain / LlamaIndex** — their docs are the source corpus for the coupling patterns; the contingent/fundamental split predicts which of their abstractions erode as models improve.

## Sources
- https://arxiv.org/abs/2604.04990
- https://arxiv.org/html/2604.04990v1
