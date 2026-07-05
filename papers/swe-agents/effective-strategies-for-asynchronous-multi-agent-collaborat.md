# Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering

- **Status:** Located — published on arXiv under the slightly different title "Effective Strategies for Asynchronous Software Engineering Agents" (https://arxiv.org/abs/2603.21489)
- **Area:** swe-agents
- **Authors / venue / date:** Jiayi Geng, Graham Neubig — arXiv (cs.CL), submitted 2026-03-23; companion post on the OpenHands blog (2026-04-27)

## Problem
Splitting a large SWE task across concurrent agents sounds like free parallelism, but in practice concurrent edits silently break each other's assumptions, dependencies are hard to sequence, and merging partial work into a coherent, passing codebase is where runs die. The paper asks which coordination strategies actually make asynchronous multi-agent SWE work better than one strong agent.

## Approach
CAID — Centralized Asynchronous Isolated Delegation. A central manager agent reads the task spec, builds a dependency graph of subtasks, and delegates parallelizable ones (as structured JSON instructions) to 2–4 engineer agents, each running asynchronously in its own **git worktree**. Integration is branch-and-merge with executable-test verification gating each merge. The insight is that ordinary SWE primitives (worktree = isolation, merge = explicit integration, tests = verification, dependency graph = safe scheduling) are the coordination substrate. Evaluated on Commit0-Lite (implement Python libraries from scratch, all tests must pass) and PaperBench (paper reproduction), with Claude Sonnet 4.5, GLM 4.7, and MiniMax 2.5.

## Key findings
- Headline (abstract): up to **26.7pp absolute** improvement on paper reproduction and **14.3pp** on Python library development vs. single-agent.
- Per-model, PaperBench (2 engineers): Claude Sonnet 57.2% → 63.3%; MiniMax 2.5 10.4% → 36.7%; GLM 4.7 38.0% → 45.4%. Weaker models gain most.
- Commit0-Lite (4 engineers): Claude 53.1% → 59.1%; MiniMax 42.3% → 57.0%; GLM 42.8% → 46.5%.
- Physical isolation matters: "soft isolation" (shared workspace, instruction-only constraints) scored **below single-agent** on PaperBench (55.5% vs. 63.3% with worktrees).
- Parallelism is non-monotonic: 4 engineers optimal on Commit0-Lite; 8 degraded performance via integration overhead. PaperBench plateaued past 2.
- More compute for one agent doesn't substitute: doubling single-agent iterations 100 → 200 gave marginal-to-negative deltas.
- Delegation order is high-variance: two CAID runs on minitorch scored 8.7% vs. 34.3% depending on whether the critical `autodiff.py` module was assigned early.
- Stricter merge review buys accuracy at latency cost: round-manager review 60.2% / 3689s vs. efficiency-prioritized 54.0% / 1909s.
- Coordination isn't free: PaperBench Claude cost $3.3 (single) → $9.3 (CAID); runtime did not drop despite parallelism because integration stays sequential and test-gated.

## Limitations & open questions
Authors concede ~3x API cost, no wall-clock win, a manager that relies on prompt heuristics rather than learned delegation policies, and uncertain transfer beyond SWE (the method leans on version control and executable tests existing). A skeptic would add: the huge MiniMax gain suggests CAID partly compensates for weak base models — for frontier models the gain is ~6pp at ~3x cost; and delegation-order variance (8.7% vs. 34.3%) means results are sensitive to a step the paper doesn't solve.

## Why builders should care
If you're building parallel coding agents, use git worktrees per agent and test-gated merges — prompt-level "stay in your lane" instructions demonstrably fail. Cap parallelism low (2–4), invest in dependency-aware task ordering (it's the highest-variance lever), and treat multi-agent as an accuracy play, not a latency play.

## Related companies in this landscape
- **OpenHands** (Bronze sponsor) — co-author Graham Neubig's project; the paper is effectively OpenHands' playbook for its async cloud agents.
- **Cognition** — Devin's multi-agent / parallel-task ambitions are exactly the regime this paper stress-tests; validates isolation-first design.
- **Factory** — sells asynchronous "droid" software agents; the cost/latency findings temper the parallelism pitch.
- **Daytona / Coder / E2B / Modal** — isolated dev environments and sandboxes are the "isolated workspaces" primitive CAID shows is load-bearing.
- **Temporal / Inngest** — durable async workflow engines map to the manager's dependency-graph scheduling layer.
- **Greptile / Qodo / Sourcegraph** — code-review agents fit the paper's finding that stricter merge-time review measurably raises pass rates.

## Sources
- https://arxiv.org/abs/2603.21489
- https://arxiv.org/html/2603.21489v1
- https://www.openhands.dev/blog/asynchronous-software-engineering-agents
