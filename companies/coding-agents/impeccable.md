# Impeccable

> An open-source "design skill" that gives AI coding agents (Claude Code, Cursor, Copilot, Codex, Gemini CLI) a shared design vocabulary so their output stops looking like generic AI slop.

- **Category:** coding-agents
- **AIEWF 2026 tier:** supporting
- **Founded:** 2026, remote/US (Reported — built by Paul Bakaus as a nights-and-weekends project, then spun into a company)
- **Website / GitHub:** https://impeccable.style/ · https://github.com/pbakaus/impeccable

## What they do
Impeccable is a skill/plugin (not a model) that installs into an AI coding harness and exposes ~23 invocable commands mapping to design disciplines — typography, color, motion, layout — plus roughly 45 deterministic anti-pattern rules that catch common AI-generated UI mistakes. It also generates a `DESIGN.md` spec the agent can read back for consistency, supports design-system inheritance, live iteration in dev servers, and PR-check integration. Practically: an engineer installs it alongside Claude Code/Cursor and the agent's frontend output gets checked/steered against these rules rather than free-associating a Tailwind template.

Disambiguation note: "Impeccable" is a generic word with other unrelated uses (fonts, apparel, etc.); this profile is anchored to impeccable.style / github.com/pbakaus/impeccable, the AI-coding-agent design tool, which is the only candidate matching "coding-agents" sponsor context.

## Founders & funding
Created by Paul Bakaus (creator of jQuery UI). He founded a company, Renaissance Geek, around it, which raised a seed round backed by a16z (Reported, led by Anish Acharya per a16z's own newsletter). Renaissance Geek also partnered with GitHub to build Impeccable into GitHub Copilot (Reported).

## Evidence of real-world use
GitHub repo has passed 40,000 stars with "hundreds of thousands of installs" claimed on the site (Reported, self-published); numerous public testimonials from named developers. It's free and open-source (MIT-style), lowering adoption friction. No independent case study or enterprise logo list found beyond self-reported testimonials — treat usage-scale claims as company-sourced.

## Relevance to agentic AI engineering
Directly addresses agent output quality/evals for a specific domain (frontend/UI generation) — relevant to anyone building coding agents or agentic SWE pipelines who needs deterministic guardrails layered on top of a general-purpose model, complementing eval/observability tooling elsewhere in this repo.

## Sources
- https://impeccable.style/
- https://github.com/pbakaus/impeccable
- https://www.a16z.news/p/impeccable-by-design
- https://www.startuphub.ai/ai-news/investors-news/2026/ai-raised-the-floor-now-what
- https://explainx.ai/blog/impeccable-github-copilot-ai-design-quality-renaissance-geek-2026
