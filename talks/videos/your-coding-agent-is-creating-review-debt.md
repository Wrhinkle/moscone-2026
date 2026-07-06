# Your Coding Agent Is Creating Review Debt

> Defines review debt as the gap between code agents produce and code humans actually review, and proposes a deterministic 0-100 score to measure it.

- **Speaker:** Sachin Gupta, software engineer
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=TJPInBjhE4Q) (AI Engineer channel; ~25m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Sachin Gupta opens with the gap he says nobody is measuring. GitHub's October 2025 report shows commits up 25 percent year over year while review comments dropped 27 percent in the same year. Faros AI's 2026 benchmark of 22,000 developers across 4,000 teams shows median PR review time up 441.5 percent, reviewed PRs taking 5.4 times longer than they used to, and 31 percent more PRs merged with no review at all. A DX study of 400 organizations over 16 months adds that median PR size grew from 44 to 72 lines while throughput grew only about 8 percent against 65 percent growth in AI usage. Gupta calls the headline numbers real but vanity metrics: PR count rises when one change splits into seven, and cycle time falls when reviewers stop pushing back. His definition of review debt is the accumulating gap between code an agent has produced and code humans have reviewed, trusted, and understood, and he argues it compounds through three loops: unreviewed code grounds tomorrow's agent suggestions, reviewer attention contracts to syntax, and leadership resets velocity expectations so no slack remains to pay the debt back.

The measurement proposal is five signal families with ten deterministic checks, deliberately avoiding an LLM judge because a model-scored PR becomes a moving target and is not defensible to leadership. The families: diff size and coupling (agents fix at the call site and sprawl across files where a human routes to the root cause), test evidence gap (test lines over production lines, with the caveat that agent tests often assert what the code does rather than what it should do), directory and ownership spread (cross-team diffs multiply approvals and mental models), AI authorship indicators (co-authored footers, codex or copilot branch prefixes, generated-by phrases, treated as an attention amplifier rather than a penalty), and evidence and rationale gaps (an 18-character PR body saying "updates" versus a body with symptom, diagnosis, change, and benchmark link). The checks roll into one 0-100 score with four bands, from low burden through needs-evidence at 50-74 to high at 75 plus, and Gupta advises calibrating weights against your last 200 merged PRs.

His scanner demos make the framing concrete. A clean PR scores 0 with an estimated 6 review minutes and an empty report. A high-debt PR scores 60 with 86 estimated minutes, and the AI indicator contributes only 5 of those 60 points; the rest is diff size, claim mismatch, and missing tests. A well-shaped AI-authored PR scores 7, which is his answer to teams asking whether the tool penalizes agent use.

The cross-repo scan covers 524 PRs across three public repos over 27-to-90-day windows. AI authorship stayed flat at 5 to 20 percent of PRs weekly, but burden did not track authorship: one repo accumulated 186 senior reviewer hours in 27 days, the scan total was 228 hours, and a single PR carried an estimated 5,036 minutes, about 84 hours, of review effort. All four PRs landing in the top bands were structural changes such as migrations and SDK rewrites. Gupta's conclusion is that complexity drives burden and AI-driven volume creates the conditions for it to accumulate. His prescriptions need no new tooling: one logical change per PR, tests shipped with the change and confirmed by the human author, staying in one owner's territory, the author writing the why, and identical review standards for AI and human PRs. He closes predicting that 2027 shifts this conversation to governance, where review debt becomes the audit trail question when an AI-authored change causes an incident.

## Notable moments

- [0:01:00](https://www.youtube.com/watch?v=TJPInBjhE4Q&t=60s) Commits up 25 percent, review comments down 27 percent in the same year, plus the Faros AI review-time numbers.
- [0:06:03](https://www.youtube.com/watch?v=TJPInBjhE4Q&t=363s) Why the ten checks are deterministic and no LLM judge is used.
- [0:14:06](https://www.youtube.com/watch?v=TJPInBjhE4Q&t=846s) The high-debt PR: 60 out of 100, 86 estimated review minutes, with structured advice for reviewer and author.
- [0:17:07](https://www.youtube.com/watch?v=TJPInBjhE4Q&t=1027s) The 90-day scan of 524 PRs: burden climbs even where AI authorship stays flat.

## Connections

- [Baz](../../companies/coding-agents/baz.md): sells agentic PR review and plan-stage checks aimed at exactly this review bottleneck.
- [Greptile](../../companies/coding-agents/greptile.md): AI code review with full-repo context, a vendor answer to the burden Gupta measures.
- [Session recaps](../../notes/session-recaps.md): Sonar's session framed reviewing AI-written code as zero trust with multilayer verification, the in-person version of this argument.
