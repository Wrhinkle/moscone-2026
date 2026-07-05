# Tessl

> A package manager and lifecycle platform for AI-agent skills and specs — the "npm for agent context" — from the founder of Snyk.

- **Category:** coding-agents
- **AIEWF 2026 tier:** gold
- **Founded:** 2024, London, UK (Verified — TechCrunch, Calcalist; emerged from stealth November 2024)
- **Website / GitHub:** https://tessl.io · https://github.com/tesslio (CLI: https://github.com/tesslio/cli) · Docs: https://docs.tessl.io

## What they do

Tessl calls itself an "Agent Enablement Platform." Strip the branding and it's two things. First, a **registry + package manager for agent context**: versioned, evaluated bundles ("tiles"/skills) of instructions, library docs, and rules that coding agents consume. You install with `npm i -g @tessl/cli`, then `tessl install <skill>` or `tessl search`; a `tessl.json` manifest pins versions, and an MCP server lets agents themselves search and install tiles mid-task. It works with Claude Code, Cursor, Copilot, Gemini "and others" (Verified — homepage). The registry launched as a "Spec Registry" (open beta, September 16, 2025) holding 10,000+ specs describing how to correctly use open-source libraries — an anti-hallucination layer against API misuse and version mixups. In January 2026 it was repositioned as a **skills registry**, now listing 2,000–3,000+ *evaluated* skills, each run through "review evals" and task evals so you can see whether a skill measurably improves agent performance before adopting it.

Second, the **Tessl Framework**: the original spec-centric bet, where human-authored specifications (not code) are the durable artifact — specs live in the codebase as long-term memory, generated code is tested against them, and code becomes regenerable/disposable. The Framework entered closed beta in September 2025 and, as of July 2026, still does not appear to be generally available (Verified absence — no GA announcement found). In practice the company's center of gravity has shifted from "spec-driven development replaces code" to the more immediately sellable skills/context supply chain, with enterprise governance (security scanning, audit logs, adoption tracking) on top. Registry is free to start; enterprise pricing is contact-sales (Verified — no public pricing page).

## Founders & origins

- **Guy Podjarny (founder/CEO):** founded Snyk (developer-first security; grew to 1,200+ employees, hundreds of millions in ARR) and before that Blaze, acquired by Akamai (Verified — GV interview, Calcalist, tech.eu). No co-founders named in public sources; key early leaders include **Simon Maple** (Head of DevRel, co-host of the *AI Native Dev* podcast, ex-Snyk) and **Ben Galbraith** (joined from Google) (Reported).
- Origin thesis: code is becoming disposable; human intent (specs, guardrails, context) is the durable asset agents need. Tessl also runs the **AI Native Dev** community/podcast (100+ episodes, weekly cadence) as a deliberate community-first wedge, echoing the Snyk playbook (Verified).

## Funding

- **Seed:** $25M, co-led by boldstart ventures and GV — previously unannounced, disclosed November 2024 (Verified).
- **Series A, November 2024:** $100M, led by Index Ventures, with Accel, GV, boldstart (Verified — TechCrunch, Calcalist, tech.eu).
- **Total raised:** $125M. Valuation: $500M+ per TechCrunch headline; $750M reported by Fortune/boldstart (Reported — treat $750M as single-sourced).
- No later rounds found in public sources as of 2026-07-02.

## Evidence of real-world use

- **Named enterprise users:** Cisco (Principal Engineer quoted on homepage) and HashiCorp/IBM (Director of Product, AI quoted) (Verified — tessl.io). Third-party analysis reports registry eval gains: Cisco software-security skill 47%→84% agent success, HashiCorp terraform-stacks 47%→96%, ElevenLabs TTS 72%→95% (Reported — rywalker.com research page; vendor-adjacent numbers, verify methodology).
- **Snyk partnership:** Snyk security-scans skills in the Tessl registry ("Securing the Agent Skills Registry") — an obvious founder-network synergy but a real governance differentiator (Verified — snyk.io blog).
- **Registry scale:** 2,000+ skills with review evals; homepage claims 3,000+ searchable (Verified — company-published).
- **Weak signals to note honestly:** the public CLI repo has only ~69 GitHub stars; the flagship Framework remains in closed beta ~9 months after announcement; no customer case studies with dollar/time outcomes published. Adoption evidence is early-stage relative to the $125M raise.

## Relevance to agentic AI engineering

Tessl sits in the **context/governance layer** of the agent SDLC stack — upstream of generation (Cursor, Claude Code) and orthogonal to review (Qodo, Greptile). Its evaluated-skills thesis is a direct commercial response to the failure modes in this repo's agentic-SWE benchmark thread: *SlopCodeBench*-style long-horizon degradation and the argument of *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* that generic benchmarks miss org-specific correctness — Tessl's per-skill task evals are essentially private micro-benchmarks. Versioned skill distribution with security scanning is a production take on the tool-use/governance thread (*Governance by Construction for Generalist Agents*), and specs-as-long-term-memory in the Framework is applied agent memory in the spirit of *Memory for Autonomous LLM Agents*.

## Use cases & considerations

Use cases: (1) pin correct, versioned library docs into coding agents to kill API hallucinations; (2) distribute internal team conventions/skills across Claude Code/Cursor/Copilot with one manifest; (3) measure whether a skill actually helps via registry evals before rollout; (4) governed, Snyk-scanned skill supply chain for enterprises worried about prompt-injection-via-skills.

Considerations: skills formats are converging on open standards (Anthropic's Agent Skills, plain markdown, MCP) — Tessl's moat must be evals + governance, not the format, and lock-in is currently low (skills are portable files). Competitors: Anthropic's own skills ecosystem, GitHub/Copilot customization, context tools like Unblocked and Sourcegraph, and DIY git-repo-of-prompts. Open questions: does the Framework ever ship GA; can a paid registry win against free GitHub-hosted skills; is eval quality strong enough to be the buying reason.

## Sources

- https://techcrunch.com/2024/11/14/tessl-raises-125m-at-at-500m-valuation-to-build-ai-that-writes-and-maintains-code/
- https://www.calcalistech.com/ctechnews/article/b1pnxlmg1x
- https://tech.eu/2024/11/14/snyk-founders-new-venture-tessl-raises-125m-for-ai-software-development/
- https://boldstart.vc/news/tessl-worth-a-reported-750-million-after-latest-100-million-funding-to-help-it-build-ai-native-software-development-platform-fortune/
- https://tessl.io/ (homepage, customer quotes, agent integrations)
- https://tessl.io/blog/announcing-tessls-products-to-unlock-the-power-of-agents/
- https://tessl.io/blog/skills-are-software-and-they-need-a-lifecycle-introducing-skills-on-tessl/
- https://tessl.io/blog/announcing-our-series-a-for-ai-native-software-development/
- https://tessl.io/registry
- https://docs.tessl.io/ (CLI, MCP tools, distribution)
- https://github.com/tesslio/cli
- https://snyk.io/blog/snyk-tessl-partnership/
- https://rywalker.com/research/agentic-skills-frameworks (third-party eval numbers)
- https://www.gv.com/news/guy-podjarny-interview-tessl-ai-software-development
- https://tessl.io/podcast/ (AI Native Dev)
