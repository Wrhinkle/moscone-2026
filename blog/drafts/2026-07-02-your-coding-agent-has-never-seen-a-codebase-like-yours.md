---
title: "Your Coding Agent Has Never Seen a Codebase Like Yours"
date: 2026-07-02
description: "Coding-agent benchmarks are greenfield and task-shaped; real software work is brownfield and history-shaped. The gap is codebase comprehension — and a whole vendor tier at AI Engineer World's Fair exists to patch exactly that."
tags: [coding-agents, benchmarks, brownfield, agentic-swe, aiewf-2026]
draft: true
sources:
  - briefs/2026-07-02-aiewf-batch-01.md (brief 4)
  - companies/coding-agents/cognition.md
  - companies/coding-agents/factory.md
  - companies/coding-agents/qodo.md
  - companies/coding-agents/openhands.md
  - companies/coding-agents/sourcegraph.md
  - companies/coding-agents/greptile.md
  - companies/swe-infrastructure/unblocked.md
  - companies/models-inference/poolside.md
  - papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md
  - papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md
  - papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md
  - papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md
  - papers/planning-architecture/one-developer-is-all-you-need-a-case-study-of-an-ai-augment.md
  - notes/conference-notes-raw.md
---

Here is a number that should change how you shop for coding agents: Claude Opus 4.5 running under Claude Code scores 74.4% on SWE-bench. On FeatureBench, with the same model and the same harness but tasks that ask it to build a feature where SWE-bench asks it to patch a reported bug, it resolves 11.0% ([FeatureBench](https://arxiv.org/abs/2602.10975), ICLR 2026). Between those two numbers sits a 63-point cliff, and every vendor demo you watched this year was filmed on the high side of it.

I spent three days at AI Engineer World's Fair at Moscone West this week, and one word kept ending up in my notes, underlined: **brownfield**. It came up in Cognition's frontier-code talk and again in the StrongDM software-factory war story. I heard it in hallway conversations with people running agents against ten-year-old Rails monoliths. The benchmarks are greenfield and task-shaped. The work is brownfield and history-shaped. The distance between those two is mostly codebase comprehension, and the vendors on the expo floor have reorganized around that fact.

## The benchmark and the Tuesday-morning ticket

Think about what a SWE-bench instance actually is: a GitHub issue, written by a human, for humans, describing a bug in a popular open-source Python repo, with a reference patch that averages around 33 changed lines. The agent gets a clean environment and a well-described problem, plus a test that tells it when it's done.

Now think about the ticket you picked up on Tuesday. It says "signature flow breaks for non-account holders on retry." The relevant behavior spans four microservices and a frontend. The retry logic exists because of an incident two years ago that lives only in a Slack thread. The integration contract with the legacy system was never documented, and the one person who understood it left. Nothing about this is in the issue text, because the issue text was written by someone who assumed the reader had the context. Every human reader did.

Benchmarks measure the first situation, and the second is the one you are paying for. Four papers from the last year, all in my notes from this conference cycle, measure the distance between them, each from a different angle. They land in the same place.

## What the misalignment papers actually measured

Start with the horizon, which collapses scores by 3x. [SWE-EVO](https://arxiv.org/abs/2512.18470) builds tasks from release notes of mature Python repos (scikit-learn, pydantic, dask): the agent must implement a release's worth of interdependent changes, about 21 modified files on average, validated against test suites that average ~874 tests. The best configuration tested, GPT-5.4 with OpenHands, resolves 25.0%, against 72.8% for the same model family on SWE-bench Verified. The mechanically interesting part: patch apply rates are 95–100%. The agents are not fumbling their tools. And for strong models, over 60% of failures are instruction-following, meaning the agent misread what the release notes asked for; implementation errors account for the minority. The failure sits upstream of code generation, in comprehension of intent against an existing system.

FeatureBench isolates a second variable, whether the agent is handed the contract or has to infer it, and its ablations are the sharpest evidence in this whole literature. Its tasks average ~790 lines across 15+ files, roughly 24x the code of a SWE-bench task. Remove explicit function signatures from the task and Gemini-3-Pro drops from 10.0% to 3.3%. Show the agent the ground-truth acceptance tests and GPT-5.1-Codex gains roughly 50 points. Same model, same code to write — the delta is entirely whether the agent has to reconstruct the contract from the codebase or gets handed it. In a mature codebase, the contract is never handed to you. It is distributed across old PRs, naming conventions, and the memory of whoever wrote the adjacent module. Every model tested also burned over 1M input tokens per task, succeed or fail. Comprehension fails here, and it runs up a bill while it fails.

The third paper skips the proxy entirely and goes straight to what developers actually type. [ProdCodeBench](https://arxiv.org/abs/2604.01527) (Meta) mines verbatim developer prompts from a production coding assistant, paired with the committed diffs and fail-to-pass tests, inside a monorepo whose language mix (Hack-heavy) no public benchmark reflects. Frontier solve rates land between 53.2% and 72.2%. The strongest behavioral predictor of success is whether the agent uses work-validation tools, running tests and checking errors before declaring victory; Claude-family models validated more and solved more. One honest caveat the authors flag: ~65% of the retained diffs were themselves AI-authored, so the benchmark partly tests whether a model can reproduce its own family's prior output.

The fourth paper turns on the leaderboard number itself. The Tessl position paper ([Coding Benchmarks Are Misaligned with Agentic Software Engineering](https://arxiv.org/abs/2606.17799)) reports Claude Opus 4.6 varying from 58% to 79.8% on identical tasks depending only on the agent harness, a swing comparable to a model-generation jump. It also catalogs SWE-bench's validity problems: 32.67% of instances have solution leakage in the issue text, 31.08% pass under insufficient tests, and real-world acceptance rates for agent code (35–64%) sit well below headline benchmark figures (>70%). Fair warning on the source: Tessl sells spec-driven development, and this position conveniently supports it. But the harness-variance data is corroborated (practitioners report 4–10 point swings for Opus 4.5 between standardized and custom scaffolds), and the implication stands regardless of who benefits: treat any leaderboard delta smaller than about 10 points as a fact about scaffolds.

Put the four together and the shape is clear. Code generation is roughly solved at the scale benchmarks test it. What remains unsolved is everything that requires knowing *this* codebase. Interfaces have to be inferred. Invariants were never written down. Somewhere there is a reason the retry count is three.

## The expo floor is a market confession

Here is the thing I actually want to argue, because I haven't seen anyone else say it: you don't need the papers to know this. You can read it directly off the sponsor tiers at Moscone West.

The floor split cleanly into two camps. Camp one, agents that write code: Cognition (silver), Factory (gold), OpenHands (bronze), poolside (supporting). Camp two, tools whose entire product is explaining your codebase to camp one. The second camp out-sponsored the first. Qodo took platinum. Unblocked took platinum. Sourcegraph and Greptile took gold.

If coding agents comprehended codebases the way the demos imply, camp two would not exist. Instead it is well funded and sharply differentiated: each vendor patches a different layer of the same wound.

Sourcegraph sells the code graph: definitions, references, cross-repo dependencies across an org's entire estate, now surfaced to agents through Deep Search, an agentic loop where the model queries the graph with a file-finding subagent and sandboxed aggregation scripts. The layer it patches is precise search.

Greptile builds a graph index of the whole repo before reviewing any PR, so its reviews weigh a diff's blast radius and never just the diff itself. Its v3 learns team standards by reading your engineers' own PR comments and ingests `CLAUDE.md` and `.cursorrules` files. Greptile's layer is accumulated review judgment.

Unblocked ingests the stuff that isn't code at all (Slack threads, Jira tickets, Confluence, old PRs) and answers "why does this service retry three times?" with the argument where that decision was made, exposed to Claude Code and Cursor via MCP. Its layer, tribal knowledge, is the one that never reached the repo in the first place.

Even the agent vendors concede the point in their product roadmaps. Cognition ships Devin Wiki and DeepWiki (auto-generated architecture docs) plus SWE-grep, a specialized parallel code-search subagent, because Devin without codebase comprehension is Devin at its March 2024 launch number: 13.86% on SWE-bench. Factory sells an "Agent Readiness" assessment that scores whether your repo is *suitable for agent work at all*, an admission, priced as a service, that most repos aren't. poolside's entire enterprise pitch is fine-tuning a model on your private codebase, the same thesis expressed in weights where the others use retrieval. Qodo's CEO states the premise outright: "Quality is subjective. It depends on organizational standards, past decisions, and tribal knowledge."

Vendors exaggerate; a sponsorship tier is a spending decision. A vendor tier this size, growing this fast, is the industry putting a price on the comprehension gap (the exact gap the papers measure), and the price is in the hundreds of millions of dollars. Treat the existence of that tier as evidence. It points the same direction the four papers do.

## Benchmark it yourself: the five-task recipe

The practical conclusion stops well short of "agents don't work." It is narrower: the only benchmark that predicts your outcomes is one derived from your repo. ProdCodeBench proved the method at Meta scale; you can run a poor man's version in an afternoon. Five tasks:

1. A real closed ticket. Pick a bug your team fixed in the last quarter. Give the agent the *original* ticket text (verbatim, terse, context-assuming) at the commit before the fix. Do not clean up the prompt; the prompt style is part of what you're testing.
2. A cross-file refactor you actually shipped. Rename a core concept, split a god module, anything that touched 10+ files. The agent must find every site, including the ones grep misses.
3. A feature from a real spec. Take a completed feature, hand the agent the planning doc or release note that described it (not the PR), and see what it builds. This is your SWE-EVO instance: it tests spec interpretation against your system, which is where >60% of strong-model failures live.
4. A comprehension question with a checkable answer. "Why does the export job debounce for 30 seconds?" Something whose true answer lives in an old PR or incident. This isolates the context layer from the generation layer; it's the task Unblocked and Sourcegraph exist for, and it tells you whether to buy them.
5. A fix with a regression tripwire. A change where the obvious patch breaks something non-obvious elsewhere. Score it SWE-EVO-style: partial credit for progress, zeroed if any existing test regresses.

Scoring discipline, straight from the position paper: log the harness and model version on every run (the 58-to-79.8% harness swing will otherwise poison your comparisons), and run each task at least twice. Grade against behavior: did the fix hold, did tests pass. Similarity to your historical diff is a bad rubric, because your diff was one valid solution among several. The whole exercise is fifteen runs and one afternoon, and it yields more decision-relevant signal than every leaderboard combined.

I'm going to run exactly this and publish it: OpenHands (MIT-licensed, model-agnostic, and the scaffold most of these benchmarks already use, which makes results comparable) against a small brownfield repo anyone can clone, with the five task definitions and full transcripts in the repo. That's the follow-up post. If you run the recipe on your own codebase before I get there, I want to see your numbers.

## What the one-person squad actually proves

The strongest counter-story to benchmark pessimism is also, read closely, the strongest evidence for this post's thesis. [One Developer Is All You Need](https://arxiv.org/abs/2605.18461) documents a single staff engineer at Itaú Unibanco delivering a regulated digital-signature platform (4 microservices plus frontend, 9 repos, Brazilian Central Bank compliance) that was scoped for a full squad. Results: 50% time-to-market reduction, throughput up 5.4x, 90% of AI-generated code accepted without structural modification, one post-validation defect, zero post-release. (Single case study, subject-as-author, no control group; hold it loosely. But it's brownfield, regulated production software, which is more than any benchmark can say.)

The mechanism was orchestration. The engineer ran four role-specialized agents under spec-driven development, with natural-language specs as the primary artifact: a discovery agent, a specification agent (Devin) grounding specs across all nine repos, a supervised core-logic agent (Copilot), and an autonomous boilerplate agent (Devin again). Oversight scaled with judgment required.

Two findings matter here. First, the top source of rework was **undocumented legacy integration contracts**: the human hit, in production, the exact wall FeatureBench's signature ablation predicts, and the paper is explicit that rework there exceeded the entire upfront cost of writing specs. Second, the paper names the binding constraint directly: specification quality and institutional knowledge. Model capability wasn't it.

For a small team, that converts to a concrete posture. The 5.4x is real and available — but it went to the person who did the comprehension work *for* the agents, who wrote specs that encode the undocumented contracts and grounded them across every repo, then reviewed in proportion to the judgment each change required. The agents in that study never came to understand the codebase. The engineer made understanding cheap for them to consume, which is exactly the product Sourcegraph, Greptile, and Unblocked sell, hand-rolled at spec-writing time and at a different price point.

The open question I keep turning over: the Itaú engineer had eight years of experience and four years of tenure, so the model consumed institutional knowledge it cannot create. Every agent run that substitutes for a junior engineer's grunt work also substitutes for the apprenticeship that produces the next person who *has* that knowledge. If comprehension of history is the scarce input to agentic software engineering, and agents both depend on it and stop us from growing it, who is writing the specs in 2031? I'd like to be wrong about the shape of that loop. The five-task benchmark won't answer it, but it will tell you, this quarter, whether your agent has actually seen a codebase like yours. Mine hasn't. That's what the transcripts are for.
