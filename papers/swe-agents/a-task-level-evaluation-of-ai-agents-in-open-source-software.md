# A Task-Level Evaluation of AI Agents in Open-Source Software Development

- **Status:** Located — published on arXiv as "A Task-Level Evaluation of AI Agents in Open-Source Projects" (https://arxiv.org/abs/2602.02345); the title in our conference notes is a slight paraphrase
- **Area:** swe-agents
- **Authors / venue / date:** Shojibur Rahman, Md Fazle Rabbi, Minhaz Zibran — MSR Mining Challenge 2026, submitted Feb 2, 2026

## Problem
Leaderboard benchmarks (SWE-bench and kin) measure whether an agent's patch passes tests in a lab harness. They say nothing about what happens when agent-authored PRs hit real open-source review: do maintainers merge them, how much review friction do they cause, and is the change history legible? This paper measures agents where the work actually lands.

## Approach
Observational study of five coding agents — OpenAI Codex, Devin, GitHub Copilot, Cursor, and Claude — over **33,549 AI-generated PRs across 2,807 repositories** (≥100 GitHub stars) from the public AIDev-pop dataset, through Aug 1, 2025. PRs are split into 12 conventional-commit task types (feat, fix, docs, ci, refactor, test, perf, etc.) and scored on three lifecycle dimensions: acceptance rate, review-discussion volume (bot + human comments), and commit-message quality via the C-Good classifier (BERT-based BiLSTM requiring both *what* and *why*; 81.6% precision). Differences validated with Mann–Whitney–Wilcoxon tests (e.g., p=4.27×10⁻⁶³ for Codex vs. Cursor acceptance).

## Key findings
- **Acceptance rates:** Codex 0.83 (SD 0.06, most stable), Cursor 0.67, Claude 0.66, Devin 0.55, Copilot 0.45.
- **Review friction:** Copilot PRs draw the most discussion (avg 1.25 bot + 1.31 human comments); Codex the least (0.02 + 0.05; 98.2% of Codex PRs get zero comments).
- **Commit-message quality (high-quality proportion):** Claude 0.68, Cursor 0.63, Devin 0.57, Copilot 0.41, Codex 0.32 — commit quality is *decoupled* from acceptance; the most-merged agent writes the worst histories.
- 90.6% of all PRs have zero recorded review comments — much acceptance happens without documented deliberation.

## Limitations & open questions
Authors concede: acceptance ≠ correctness (merged PRs may harbor defects); comment volume doesn't distinguish praise from pushback; task complexity varies within categories; open-source-only, single temporal snapshot. A skeptic adds: selection effects are unmodeled — Codex's near-silent, high-acceptance profile may reflect users routing it small/safe tasks or rubber-stamping their own agent's output, not superior capability. Repo popularity and prompt quality are confounds.

## Why builders should care
Pick agents per dimension, not per leaderboard: merge rate, review burden, and history legibility are independent axes. If your team maintains code long-term, an agent that merges easily but writes "why-free" commits (Codex here) taxes future maintainers; enforce commit-message quality gates in the agent loop. Also treat "zero review comments" as a red flag in your own metrics, not a win.

## Related companies in this landscape
- **OpenAI** (Labs) — Codex is the acceptance-rate winner here but the commit-quality laggard; direct evidence for and against.
- **Microsoft / GitHub** (Presenting; Supporting) — Copilot's PRs show the lowest acceptance and highest review friction in this sample.
- **Cognition** (Silver) — Devin sits mid-pack on all three axes; most stable commit quality (SD 0.07).
- **Greptile, Baz, Qodo, Sonar** (Gold/Platinum/Silver) — review and code-quality agents; the 90.6% zero-comment finding is the gap their products monetize.
- **Sourcegraph, Factory, OpenHands, Cline** (Gold/Bronze/Supporting) — coding-agent vendors whose differentiation this task-level framing supports: compete on lifecycle outcomes, not benchmark scores.

## Sources
- https://arxiv.org/abs/2602.02345
- https://arxiv.org/html/2602.02345
