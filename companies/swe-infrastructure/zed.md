# Zed

> Open-source, Rust-native code editor from the Atom creators, rebuilt around real-time collaboration between humans and AI agents.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** 2021, Boulder, CO / remote-first (Verified — Wikipedia, Tracxn, company site)
- **Website / GitHub:** [zed.dev](https://zed.dev) / [github.com/zed-industries/zed](https://github.com/zed-industries/zed)

## What they do

Zed is a from-scratch code editor written in Rust with its own GPU-accelerated UI framework (GPUI), positioned as the performance-first alternative to Electron-based editors (VS Code, Cursor). The core editor is open source (GPL for the editor, with the company monetizing hosted AI services), runs on macOS, Linux, and Windows, and hit 1.0 in April 2026 after roughly five years of development.

The AI story is what makes Zed relevant at AIEWF. Three pieces: (1) an **Agent Panel** that runs model-agnostic agentic coding sessions — Claude, GPT, Gemini via API keys or Zed's hosted plans, plus local models via Ollama — with support for multiple agent threads in parallel; (2) **Zeta**, Zed's own open-weight edit-prediction model (Zeta2.1 shipped May 2026: ~136ms p50, weights on Hugging Face, Rust bindings on PyPI for self-hosting) powering Copilot-style completions; and (3) the **Agent Client Protocol (ACP)** — an open, Apache-licensed JSON-RPC standard co-developed with JetBrains that decouples coding agents from editors, letting external CLI agents (Claude Code, Gemini CLI, Codex CLI, OpenCode) render natively inside the editor. Zed and JetBrains launched a shared ACP agent registry in January 2026, and ACP 1.0 is now treated as a stable surface (Reported — multiple 2026 reviews and Zed's docs).

Longer-term, the Series B money is funding **DeltaDB**: CRDT-based, operation-level version control that tracks edits at character granularity, so conversations and review comments stay durably linked to code as humans and agents rewrite it — an explicit bet that Git's snapshot model is the wrong substrate for agentic development (Verified — Zed's Series B blog post).

## Founders & origins

Nathan Sobo (CEO), Max Brunsfeld, and Antonio Scandurra (Verified — company site, press, Wikipedia). The team previously built **Atom** and **Electron** at GitHub; Brunsfeld also created **Tree-sitter**, the incremental parsing library now used across the industry (including by most code-RAG systems). Zed is essentially "what Atom's authors wished Atom had been" — native performance and collaboration-first — started in 2021 after years of side work on the underlying CRDT tech.

## Funding

- **Seed:** Root Ventures and others, pre-2023 (Reported — Tracxn; amount not found in public sources).
- **Series A:** $10M, March 2023, led by Redpoint Ventures; angels incl. Dylan Field (Figma), Tom Preston-Werner (GitHub), Spencer Kimball (CockroachDB) (Verified — PRWeb, Redpoint).
- **Series B:** $32M, announced August 20, 2025, led by Sequoia, with Redpoint, Root, Matchstick, V1.VC returning (Verified — Businesswire, Sequoia, multiple trackers; note Preqin lists a Nov 2024 close of $32.4M, so the round likely closed before the announcement).
- **Total:** >$42M (Verified).

## Evidence of real-world use

Strong OSS signals: the GitHub repo is one of the most-starred Rust projects (reports in 2026 range 40k–85k+ stars — Unverified exact count as of 2026-07-02); the Series B release cited **150,000+ active developers and 1,100 contributors**; 2026 sources claim "hundreds of thousands of daily users" and 527 unique non-staff contributors merging PRs Jan–May 2026 (Reported). Public pricing exists (free tier with 2,000 Zeta predictions/month; Pro reported at $10–20/month with hosted-model credits — sources conflict on the number). No named enterprise customers found in public sources — adoption is bottom-up individual developers, not logo-driven.

## Relevance to agentic AI engineering

Zed is infrastructure for the human-agent interface layer of the SDLC: ACP is the editor-side analog of MCP (tool side) — a governance/interop standard worth tracking alongside this repo's tool-use/governance thread. Parallel agent threads plus DeltaDB's operation-level history speak directly to the agentic-SWE-benchmark question (SWE-bench-style long-horizon edits) of how humans review and steer agent-generated diffs. Zeta is a rare open-weight, latency-focused edit model — relevant to anyone benchmarking small task-specific models against frontier APIs.

## Use cases & considerations

- Daily driver editor with bring-your-own-key agentic coding (no Cursor subscription lock-in).
- ACP as an integration target if you're building a coding agent and want editor UI for free.
- Self-hosted Zeta for teams wanting local edit prediction.

Considerations: extension ecosystem still far smaller than VS Code's; Windows support is newest and least mature; monetization is early (hosted AI credits) so pricing may shift; DeltaDB is pre-release vision, not product. Competitors: Cursor, VS Code + Copilot, Windsurf, JetBrains (also an ACP partner — coopetition).

## Sources

- https://zed.dev/blog/sequoia-backs-zed
- https://www.businesswire.com/news/home/20250820782241/en/Zed-Raises-$32M-Series-B-Led-by-Sequoia-to-Scale-Collaborative-AI-Coding-Vision
- https://en.wikipedia.org/wiki/Zed_(text_editor)
- https://www.prweb.com/releases/Zed_Announces_10M_Series_A_and_Launches_its_Collaborative_Code_Editor/prweb19217168.htm
- https://github.com/zed-industries/zed
- https://zed.dev/pricing and https://zed.dev/docs/ai/edit-prediction
- https://tracxn.com/d/companies/zed/__3jn1wtnWJjfLtgOSDXECkHFjHmFm7BkEKtVzcAABH3A
- https://www.builder.io/blog/zed-ai-2026 (2026 AI feature review)
- https://baeseokjae.github.io/posts/zed-ai-guide-2026/ (ACP/Zeta2 details)
- https://zed.dev/blog/community-champions
