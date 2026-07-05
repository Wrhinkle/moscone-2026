# Weco AI

> An AI agent that treats code optimization as a tree-search problem: it iteratively rewrites your code (ML pipelines, GPU kernels, prompts) and keeps the variant that scores best against a metric you define.

- **Category:** coding-agents
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, London, UK. (Reported — Tracxn/PitchBook aggregator data)
- **Website / GitHub:** https://www.weco.ai/ · docs at https://docs.weco.ai/ · OSS core at https://github.com/WecoAI/aideml (MIT license, ~1.3k stars, 197 forks) and CLI at https://github.com/WecoAI/weco-cli

## What they do
Weco AI's core research artifact is AIDE (AI-Driven Exploration in the Space of Code), an LLM-driven agent that frames ML engineering as tree search: it maintains a tree of candidate code solutions, asks an LLM to propose edits to a chosen node, and lets a hard-coded search algorithm decide which branch to pursue next, scored by an automated evaluation the user supplies. On top of the open AIDE research code, Weco ships `weco-cli`, a production CLI/VS Code extension that runs the same loop against arbitrary metrics — latency, accuracy, cost, throughput — across Python, C++, JavaScript, and Rust, including GPU kernel work (CUDA/Triton rewrites of PyTorch ops). Concretely: point it at a repo, define a shell-runnable eval command, and it iterates unattended, functioning as an autonomous performance-engineering agent rather than a chat assistant.

## Founders & origins
Zhengyao Jiang (CEO) and Yuxiang Wu (co-founder/CTO). (Reported — company blog, LinkedIn posts, Tracxn.)

## Funding
$8–9.3M seed, announced July 2025, led by Golden Ventures with Third Kind Venture Capital, BoxGroup, Founder Collective, Night Capital, Twin Path Ventures, Koro Capital, and angel Scott Belsky participating. (Reported — company blog "Weco Raises $8M" + Tracxn/PitchBook corroboration.)

## Evidence of real-world use
AIDE's research results are independently notable: reported 4x-to-5x medal-rate improvement over baseline agents on OpenAI's MLE-Bench (75 Kaggle-style competitions) and strong RE-Bench performance. The OSS repo (MIT, ~1.3k GitHub stars, 197 forks) is cited as a building block in papers/evaluations from OpenAI, METR, Sakana AI, and Meta — real research-community adoption, distinct from unverified customer claims (no named enterprise customer list found in this pass).

## Relevance to agentic AI engineering
Directly relevant to the SDLC/coding-agent corner of the stack — an example of a narrow, metric-driven autonomous agent (propose → run eval → search) rather than a general chat coding assistant, and a concrete instance of evals-as-reward-signal driving agentic iteration (connects to this repo's evals-observability and agent-orchestration categories).

## Use cases & considerations
Use cases: automated GPU kernel/inference-latency optimization, ML feature/model iteration, prompt optimization, general "optimize this against a number" tasks. Considerations: young company (2023, small seed round), no disclosed enterprise customer list, competes conceptually with general coding agents (Cursor, Devin, Claude Code) that are not metric-search-specialized, and with AutoML/NAS tooling; open question whether the tree-search approach generalizes beyond benchmark-style tasks with cleanly defined metrics.

## Sources
- https://www.weco.ai/
- https://docs.weco.ai/
- https://github.com/WecoAI/aideml
- https://github.com/WecoAI/weco-cli
- https://arxiv.org/html/2502.13138v1
- https://www.weco.ai/blog/seed-announcement
- https://tracxn.com/d/companies/wecoai/__iq6siMtSDc2YZH88q-kD9R1OdPgZHvtEFnI9RhCSGeA
