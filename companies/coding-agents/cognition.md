# Cognition

> Maker of Devin, the autonomous "AI software engineer" you assign tickets to like a junior teammate, plus the Windsurf agentic IDE and its own family of fast coding models.

- **Category:** coding-agents
- **AIEWF 2026 tier:** silver
- **Founded:** 2023, San Francisco (Verified; sources vary between August and November 2023 on the exact date)
- **Website / GitHub:** https://cognition.ai · https://devin.ai · https://windsurf.com · https://github.com/CognitionAI

## What they do

Cognition sells two complementary products. **Devin** is a cloud-hosted autonomous coding agent: you hand it a ticket (from Slack, Jira, or Linear), it plans, edits a real repo in its own sandboxed environment with a shell, editor, and browser, runs tests, and opens a pull request for human review. It is positioned for delegable, well-scoped work — migrations, bug backlogs, test coverage, boilerplate features — running many sessions in parallel rather than replacing an IDE. Devin 2.0 (April 2025) added an agent-native IDE view, Devin Search (codebase Q&A), and Devin Wiki (auto-generated architecture docs); the public spinoff **DeepWiki** generates free wikis for public GitHub repos. **Windsurf**, acquired July 2025, is the synchronous half: an agentic IDE (Cascade agent) for in-editor work, giving Cognition both the "delegate to an agent" and "pair with an agent" form factors.

Underneath, Cognition increasingly ships its own models: **SWE-1.5**, a frontier-size coding-agent model served on Cerebras hardware at up to ~950 tok/s (their pitch: near-SOTA quality at ~13x Sonnet 4.5 speed), a **SWE-1.6** preview, and **SWE-grep / SWE-grep-mini**, specialized parallel code-search subagents that power Windsurf's Fast Context retrieval. Pricing is public and usage-metered: Devin Core at $20/month + ~$2.25 per ACU (an "Agent Compute Unit" ≈ 15 minutes of active agent work); Team at $500/month with 250 ACUs.

## Founders & origins

Scott Wu (CEO), Steven Hao, and Walden Yan — all IOI gold medalists; Wu previously co-founded Lunchclub and won IOI outright in 2014 (Verified — Wikipedia, press). The March 2024 Devin demo ("first AI software engineer," 13.86% unassisted on SWE-bench, then SOTA; methodology published at github.com/CognitionAI/devin-swebench-results) launched the company into public view. CEO Wu has publicly argued coding agents should augment rather than replace engineers (TechCrunch, May 2026).

## Funding

- Early 2024: $21M led by Founders Fund at ~$350M (Verified).
- April 2024: $175M led by Founders Fund at $2B (Verified).
- March 2025: round led by 8VC at ~$4B valuation; amount widely reported as "hundreds of millions" but not officially disclosed (Reported).
- July 2025: acquired Windsurf's team/tech after the $3B OpenAI deal collapsed over Microsoft IP terms; price undisclosed, ~$250M estimated (Reported).
- Sept 2025: $400M led by Founders Fund at $10.2B post (Verified — CNBC), with Lux Capital, 8VC, Bain Capital Ventures.
- May 2026: $1B+ Series D at $25B pre / $26B post (Verified — TechCrunch, 2026-05-27).
- **Total raised:** roughly $1.6B+ (approximate; March 2025 amount unclear).

## Evidence of real-world use

- ARR ~$492M as of May 2026 (Reported — company figure via press); Windsurf brought ~$82M ARR and 350+ enterprise customers at acquisition (Reported).
- Named production customers: Goldman Sachs (CIO Marco Argenti publicly called Devin "our new employee"; reportedly hundreds of instances), Citi, NASA, Mercedes-Benz, Dell, Santander, Elevance, Itaú, U.S. Army and Navy (Verified for Goldman via IBM/press coverage; others Reported via press).
- Dogfooding claim: 89% of code committed at Cognition written by Devin, up from 13% in Dec 2025 (Reported — vendor figure).
- Counterweight: Answer.AI's independent January 2025 evaluation found early Devin completed only ~3 of 20 real tasks (Verified — widely discussed). Capability has clearly moved since, but treat vendor metrics skeptically.

## Relevance to agentic AI engineering

Cognition is the reference case for the async-agent SDLC pattern this repo tracks: long-horizon autonomous tasks, PR-gated human review, parallel agent fleets. Directly relevant papers here: **SWE-EVO** and **SlopCodeBench** (long-horizon degradation is exactly Devin's failure mode), **FeatureBench**, **ProdCodeBench**, and **Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering** (the Devin 13.86%-SWE-bench-to-production gap is that paper's argument in miniature), plus **Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering**. Devin Wiki/Knowledge features connect to the agent-memory thread (**Memory for Autonomous LLM Agents**), and SWE-grep is a production instance of the retrieval-subagent ideas in the search/memory papers.

## Use cases & considerations

Use cases: parallelizing a bug/migration backlog across Devin sessions; test-coverage and dependency-upgrade grunt work; codebase onboarding via DeepWiki/Devin Wiki; Windsurf as the interactive complement.

Considerations: ACU-metered costs are hard to predict on flailing tasks; heavy lock-in to a closed platform and proprietary models; post-acquisition team turbulence (Windsurf buyouts) reported; fierce competition from Cursor, GitHub Copilot's agent mode, Claude Code, OpenAI Codex, and Factory. Open question: how much of the $492M ARR is Devin autonomy vs. Windsurf IDE seats.

## Sources

- https://en.wikipedia.org/wiki/Cognition_AI
- https://en.wikipedia.org/wiki/Scott_Wu
- https://cognition.com/blog/funding-growth-and-the-next-frontier-of-ai-coding-agents
- https://cognition.com/blog/windsurf
- https://cognition.com/blog/swe-1-5
- https://cognition.com/blog/swe-1-6-preview
- https://cognition.ai/blog/swe-bench-technical-report
- https://github.com/CognitionAI/devin-swebench-results
- https://www.cnbc.com/2025/09/08/cognition-valued-at-10point2-billion-two-months-after-windsurf-.html
- https://techcrunch.com/2026/05/27/ai-coding-startup-cognition-raises-1b-at-25b-pre-money-valuation/
- https://techcrunch.com/2026/05/29/cognitions-scott-wu-says-ai-coding-agents-shouldnt-replace-humans/
- https://techcrunch.com/2025/04/03/devin-the-viral-coding-ai-agent-gets-a-new-pay-as-you-go-plan/
- https://venturebeat.com/programming-development/devin-2-0-is-here-cognition-slashes-price-of-ai-software-engineer-to-20-per-month-from-500
- https://venturebeat.com/programming-development/cognition-follows-windsurf-acquisition-with-usd400m-fundraise-showing-strong
- https://www.ibm.com/think/news/goldman-sachs-first-ai-employee-devin
- https://www.cerebras.ai/blog/case-study-cognition-x-cerebras
- https://devin.ai/pricing/
- https://research.contrary.com/company/cognition
