# Cua

> Open-source (MIT) infrastructure for computer-use agents: sandboxed full-OS VMs, a cross-platform SDK, and a benchmarking suite for training and evaluating agents that drive real desktops.

- **Category:** browser-computer-use
- **AIEWF 2026 tier:** supporting
- **Founded:** March 2025, San Francisco (Verified — YC profile + company about page; Delaware-incorporated per Tracxn)
- **Website / GitHub:** https://cua.ai — https://github.com/trycua/cua

## What they do

Cua (pronounced "koo-ah", GitHub org `trycua`) builds the runtime layer for agents that operate a computer via screen, mouse, and keyboard instead of APIs. Their positioning is essentially "Docker for computer-use agents": you launch an isolated OS environment with one command or API call, point any VLM/LLM at it, and get back trajectories.

The stack has four parts (Verified — GitHub repo + cua.ai):

- **Cua Driver** — an open-source "background computer-use" driver for native desktop apps on macOS/Windows (Linux in pre-release). Notable engineering detail: agents click, type, and verify *without stealing the user's cursor or focus*. Ships as an MCP server, daemon, or CLI, so it plugs into Claude Code, Cursor, and other MCP clients.
- **Cua Sandbox** — agent-ready VM provisioning, local or cloud, across Linux, Windows, macOS, and Android, with snapshot-native (copy-on-write) rollouts for reproducible environment state.
- **Cua Run / Cloud** — elastic warm pools of machines claimed in milliseconds, aimed at evals, RL rollouts, and batch trajectory generation at fleet scale. SOC 2-ready, BYOC, and on-prem options.
- **Cua-Bench + Lume** — a benchmark harness that runs agents against OSWorld, ScreenSpot, Windows Arena, and custom task sets, exporting trajectories for fine-tuning/RL; Lume is the original CLI for near-native macOS/Linux VMs on Apple Silicon via Apple's Virtualization.Framework (~97% native CPU speed claimed). They also sell "Verified Data": human-QA'd pre-run trajectories with step-level annotations.

The SDK is model-agnostic (Anthropic, OpenAI, Ollama/open models) and OS-agnostic — one API regardless of runtime.

## Founders & origins

**Francesco Bonacci** (product; ex-Microsoft/Xbox AI) and **Dillon DuPont** (research; ex-Microsoft) — Verified via cua.ai/about. At Microsoft they built **Windows Agent Arena**, an early benchmark for screen-acting agents. Francesco left Microsoft in early 2025, launched Lume (hit HN front page), founded Cua the same month, and entered **YC Spring 2025 (X25)**. Note: Tracxn lists a co-founder "Alessandro Puppo," which conflicts with the company's own about page naming DuPont — the company page is treated as authoritative; discrepancy Unverified. Team of ~8 listed (SF, Vancouver, Toronto).

## Funding

- **$500K seed, June 2025** — Y Combinator plus 468 Capital, Orange Collective, Script Capital, Transpose Platform, Vento (Reported — Tracxn/PitchBook; amount is consistent with YC's standard check). No later round found in public sources as of 2026-07-02; total raised ≈ $500K disclosed.

## Evidence of real-world use

- **GitHub: ~19.4k stars, ~1.3k forks, 546 releases** as of 2026-07 (Verified — repo). Sustained trending momentum (~1.3k stars added in a single week per third-party review coverage).
- **Named users on cua.ai:** Google DeepMind (evaluating Gemini 3.5 Flash on Cua) and Qwen Code (Reported — company site testimonials; treat as vendor-claimed until independently corroborated). Site also claims "50,000+ engineers" including at Google, Meta, Apple, NVIDIA (Unverified marketing figure).
- **Launch HN (April 2025)** with substantive discussion; MCP integration means it shows up inside Claude Code/Cursor workflows, a real distribution channel.
- Commercial signals: cloud product with free tier + dedicated fleets by request, active hiring (research intern postings), Discord community. No public per-unit pricing page — enterprise-motion pricing.

## Relevance to agentic AI engineering

Cua is the environment/sandbox layer of the agent stack — the substrate under evaluation, RL training, and production computer-use. It connects directly to this repo's tool-use/governance thread: **Verifiable Software Worlds for Computer-Use Agents** (reproducible, checkable environments is exactly what snapshot-native sandboxes provide) and **CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents** (OS-level isolation is the enforcement point that paper's threat model assumes). Cua-Bench's trajectory export loop is the practical counterpart to the benchmark-design concerns in **Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering** and long-horizon eval work like **SlopCodeBench** — same reproducibility problems, GUI domain. Founders' Windows Agent Arena lineage makes the benchmarking DNA credible.

## Use cases & considerations

Use cases: (1) safe sandboxes for agents automating legacy GUI apps with no API — e.g. insurance-carrier portals or estimating software in a construction back office; (2) eval/RL infrastructure for teams training computer-use models (OSWorld-style rollouts at fleet scale); (3) background desktop automation via MCP from Claude Code/Cursor without hijacking the user's session; (4) Android/mobile agent testing.

Considerations: young company (~1 year old, ~$500K disclosed funding) — cloud-service continuity risk, though MIT license and self-hosting blunt lock-in. Lume's macOS strength is Apple Silicon-specific. Competitors: Browserbase (browser-only, same category folder), E2B and Daytona (code sandboxes), Scrapybara, Anchor Browser, and hyperscalers' own computer-use offerings. Open questions: revenue traction beyond the free OSS tier; whether "Verified Data" becomes the real business.

## Sources

- https://github.com/trycua/cua
- https://cua.ai/
- https://cua.ai/about
- https://www.ycombinator.com/companies/cua
- https://tracxn.com/d/companies/cua-ai/__o8YYWID0aTrulrJn7F3L4KMrye__2TwaEKHVrhpDFjY
- https://pitchbook.com/profiles/company/863187-94
- https://news.ycombinator.com/item?id=43773563
- https://andrew.ooo/posts/trycua-cua-open-source-computer-use-agents/
- https://cua.ai/blog/introducing-cua-cloud-containers
