# Agentic Evaluations at Scale, For Everybody

> Two Kaggle team members argue that AI evals are scattered, opaque, and written by too few people, and walk through Kaggle's four answers: hackathons, agent exams, Game Arena, and a community benchmarks platform.

- **Speaker:** Nicholas Kang & Michael Aaron, Google DeepMind (Kaggle)
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Ubwb6NzegyA) (AI Engineer channel; ~20m, released 2026-05-25)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Kang, product manager for Kaggle Benchmarks, opens with three ways evals are broken. First, they scatter and go stale: ten-plus benchmarks drop daily on arXiv, and leaderboards die once authors move to the next paper. Second, they are not transparent or verifiable. He tells an anecdote of publishing a benchmark with one AI lab, after which a competing lab reran it with much better results, the difference being that they had enabled their API's compaction feature for their own model while Kaggle had not for any. Third, roughly 30,000 AI researchers write the evals meant to serve 30 million technical workers and all of humanity, which he says guarantees the jagged cognitive profile of current models will worsen. His counterexample is a Kaggle user in Turkey, a wastewater treatment plant engineer of 20 years, who built a benchmark from his own proprietary safety knowledge after fatal incidents in his country, a dataset no lab would produce because it is not economically interesting to them.

Kaggle's first response is hackathons with guardrails, including a live one with the Google DeepMind AGI team asking participants to build benchmarks for five of the ten cognitive faculties in DeepMind's recent AGI measurement paper. Kang notes unglamorous platform problems: participants from poorer backgrounds cannot afford five API keys for frontier models, and judging creativity still needs human experts who disagree with each other. The second product is standardized agent exams, launched the week before as an MVP: paste a one-line prompt, your agent takes an exam, and it lands on a comparable leaderboard. Kang points at the OpenClaw wave, agents filing over a thousand security advisories while almost nobody tests their agent before letting it run an inbox or an Amazon account, and floats safety-focused baseline exams. Over 500 agents were evaluated in the first week with little promotion, and spin-off posts appeared on the agent social network Moltbook, including an exam prep course.

Aaron covers Game Arena, Kaggle's answer to benchmark saturation: models play PvP games so there is always a winner, making the leaderboard permanently hill-climbable. Games are picked per capability: Werewolf for deception, poker for randomness and risk (Grok loves going all-in, while newer models are more risk-averse and actually worse at poker), and chess. The stack runs OpenSpiel games on Kaggle's old RL simulation platform, uses Bradley-Terry pairwise scheduling to limit game count, and publishes every LLM conversation as an open dataset plus a game visualizer. The cost problem is concrete: statistical significance for poker took about 400,000 hands, each with many turns.

The benchmarks platform closes the talk: not a production eval product but a community one, where anyone builds tasks from assertions and LLM judges, like Paige Bailey's XKCD SVG-reproduction task, and aggregates them into benchmarks such as the wastewater one. Aaron's hardest open problem is ambiguity under test in agentic benchmarks. Citing a Morph blog post, he notes six frontier models land within a couple percentage points of each other on SWE-bench Pro while the choice of harness swings results by 22 percent, so it is unclear whether a benchmark measures the model or the scaffold around it.

## Notable moments

- [0:03:20](https://www.youtube.com/watch?v=Ubwb6NzegyA&t=200s) The compaction anecdote: a rival lab reruns a published benchmark tuned for its own model.
- [0:04:21](https://www.youtube.com/watch?v=Ubwb6NzegyA&t=261s) The Turkish wastewater engineer who built a safety benchmark no AI lab would write.
- [0:14:28](https://www.youtube.com/watch?v=Ubwb6NzegyA&t=868s) Game Arena internals: OpenSpiel, Bradley-Terry pairing, and 400,000 poker hands for significance.
- [0:18:30](https://www.youtube.com/watch?v=Ubwb6NzegyA&t=1110s) The harness problem: frontier models cluster within points on SWE-bench Pro while harness choice moves scores 22 percent.

## Connections

- [Google DeepMind](../../companies/models-inference/google-deepmind.md), the speakers' parent organization and partner on the AGI cognitive-faculties hackathon.
- [Morph](../../companies/coding-agents/morph.md), whose SWE-bench Pro harness-variance analysis Aaron cites as the core agentic eval ambiguity.
- [Snorkel](../../companies/evals-observability/snorkel.md), a commercial take on expert-built eval data where Kaggle bets on open community contribution.
