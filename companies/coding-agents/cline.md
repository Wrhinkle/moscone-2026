# Cline

> Open-source, model-agnostic autonomous coding agent (IDE extension, CLI, and SDK) where you bring your own API keys and see every token you spend.

- **Category:** coding-agents
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified — started as a hackathon side project in mid-2024, incorporated after the Nov 2024 seed; founder relocated from Indiana to SF)
- **Website / GitHub:** https://cline.bot · https://github.com/cline/cline

## What they do

Cline is an autonomous coding agent that, unlike autocomplete tools, plans and executes whole tasks: it reads your codebase, creates/edits files across the project, runs terminal commands and reacts to live output, drives a browser, and gates every action behind human approval by default (a "Plan then Act" workflow with per-action-type auto-approve toggles). It began as a VS Code extension and now ships as four surfaces: IDE extensions (VS Code, JetBrains family, plus running inside Cursor/Windsurf), a CLI (`npm i -g cline`, with headless mode, JSON output, and stdin/stdout piping for CI), a TypeScript SDK, and a web "Kanban" board for running parallel agent instances.

Two architectural decisions define it. First, BYO-model: Cline itself is free and takes no margin on inference — you connect Anthropic, OpenAI, Gemini, Bedrock, Vertex, DeepSeek, xAI, Mistral, OpenRouter, local Ollama, or any OpenAI-compatible endpoint, and Cline surfaces per-task token cost in the UI. Second, no server middleman: prompts go straight from your machine to your model provider, which is the wedge into security-sensitive enterprises. Team conventions are encoded in `.clinerules` files, and it was an early, aggressive adopter of MCP for tool integration (including having the agent build its own MCP servers).

In May 2026 the company extracted its internal agent harness into an open-source runtime, `@cline/sdk`, and is rebuilding all its own products on it — CLI and Kanban are already migrated, IDE extensions in progress (Verified — company blog + MarkTechPost). Monetization: Cline Teams (org management, centralized billing, audit logs, access controls; self-hosted option planned) and ClinePass, a $9.99/month subscription for low-cost access to open coding models (Reported).

## Founders & origins

**Saoud Rizwan** (founder/CEO) built the tool as "Claude Dev" for Anthropic's *Build with Claude* hackathon in mid-2024, released it open source, renamed it Cline, and turned it into a company after it went viral (Verified — Forbes, company blog). He raised the seed in November 2024 and moved from Indiana to San Francisco (Verified — Forbes). No public co-founders found; early team drawn heavily from open-source contributors (Reported).

## Funding

- **Seed, Nov 2024:** $5M — Pace Capital (Verified — Forbes, company announcement).
- **Series A, July 2025:** $27M led by Emergence Capital, with Pace Capital and 1984 Ventures; $110M valuation (Verified — Forbes, GlobeNewswire). Other participants across the $32M combined total: Essence VC, Cox Exponential; angels include Jared Friedman (YC), Logan Kilpatrick (Google), Addy Osmani, Eric Simons (StackBlitz).
- **Total raised:** $32M (Verified). No Series B found in public sources as of 2026-07-02.

## Evidence of real-world use

- **OSS adoption:** ~64.3k GitHub stars, ~6.8k forks, Apache-2.0, 250+ contributors (Verified — GitHub, 2026-07-02). Installs grew from 2.7M (July 2025 press) to "8M+ developers across platforms" per the current site (company-reported).
- **Named enterprises:** SAP and Samsung cited in Series A press as customers requiring strict privacy (Reported — company/press); homepage logos add Salesforce, Oracle, Amazon, Microsoft, eBay, Visa, IBM, LG, Globant (Unverified beyond logos — no public case studies found; treat as logo-wall evidence).
- **Community:** ~20k Discord members, active fork ecosystem — Roo Code and Kilo Code are literal forks of Cline, which is strong evidence the codebase is load-bearing infrastructure for the OSS coding-agent scene (Verified).

## Relevance to agentic AI engineering

Cline is a reference implementation of the agentic-SWE loop this repo's benchmark thread studies: long-horizon multi-file tasks are exactly where *SlopCodeBench*-style degradation shows up, and its human-approval gates and `.clinerules` policy files are a shipped, pragmatic version of the control layer argued for in *Governance by Construction for Generalist Agents*. The `@cline/sdk` harness extraction makes it directly comparable to Claude Agent SDK as embeddable tool-use infrastructure, and its early MCP bet ties into the tool-use/governance papers. For evaluation, its transparent per-task token accounting makes it a good substrate for cost-aware agent benchmarking (*ProdCodeBench* territory).

## Use cases & considerations

Use cases: (1) coding agent for enterprises that cannot route code through a vendor's servers (client-to-provider direct); (2) headless CLI agent in CI/cron pipelines; (3) building your own domain agent on `@cline/sdk` instead of writing a harness from scratch; (4) cheap model experimentation — swap providers per task and compare cost/quality.

Considerations: BYO-API-key pricing means costs are transparent but unbounded and can shock (Forbes framed the Series A around AI-spend control for this reason). Business model is young — the free agent is the product; Teams/ClinePass monetization is unproven. Fierce competition: Cursor, GitHub Copilot agent mode, Claude Code, Windsurf, plus its own forks (Roo Code, Kilo Code) which fragment the community. Open question: whether an inference-margin-free company can sustain the R&D pace of Anthropic/OpenAI-subsidized rivals.

## Sources

- https://cline.bot/blog/cline-raises-32m-series-a-and-seed-funding-building-the-open-source-ai-coding-agent-that-enterprises-trust
- https://www.forbes.com/sites/rashishrivastava/2025/07/31/cline-has-raised-27-million-to-help-developers-control-their-ai-spend/
- https://www.globenewswire.com/news-release/2025/07/31/3125274/0/en/Cline-Raises-32M-in-Seed-and-Series-A-Funding-to-Bring-Agentic-AI-Coding-to-Enterprise-Software-Teams.html
- https://github.com/cline/cline
- https://cline.bot/
- https://cline.bot/blog/introducing-cline-sdk-the-upgraded-agent-runtime
- https://www.marktechpost.com/2026/05/14/cline-releases-cline-sdk-an-open-source-agent-runtime-now-powering-its-cli-and-kanban-with-ide-extensions-being-migrated/
