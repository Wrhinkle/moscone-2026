# Block

> The fintech company (Square, Cash App, Tidal, TBD) behind Jack Dorsey that builds and open-sources "goose," an Apache-2.0 AI coding agent used internally and by outside teams.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** 2009 as Square, San Francisco (Verified — public company, NYSE: XYZ)
- **Website / GitHub:** https://block.xyz / https://github.com/block/goose

## What they do
Block is best known as a payments/fintech company, but for this repo the relevant product is **goose**, an open-source, extensible AI agent built by Block's engineers and released under Apache 2.0. Goose runs as a software-engineering agent inside a dev environment: it searches, navigates, and writes code, then autonomously executes — running code/tests, installing dependencies, and refining outputs — rather than just suggesting snippets. It's LLM-agnostic (Claude, GPT, Gemini, or local Ollama via pasted API key) and integrates with Anthropic's Model Context Protocol (MCP) to connect to external tools/data. Block also runs a "goose grant program" funding outside contributors. Engineer takeaway: a production-grade, self-hostable alternative/complement to Copilot-style agents, notable for coming out of a large non-AI-native enterprise's own internal tooling need.

## Funding
Not applicable — Block is a publicly traded company (formerly Square); goose is an internal open-source project, not a separately funded startup.

## Evidence of real-world use
Deployed AI agents company-wide reportedly within two months (per Aviator podcast); goose grew to "thousands of community members and dozens of external code contributors" within six months of public launch and has been adopted by companies including Databricks, startups, and university labs (Verified — Block's own blog, cross-referenced by VentureBeat/KDnuggets coverage).

## Relevance to agentic AI engineering
Directly relevant to the agent-orchestration / SDLC-agent tracks: goose is a concrete open-source implementation of an autonomous coding agent with MCP tool integration, useful as a reference architecture or as a tool to actually adopt.

## Sources
- https://block.xyz/inside/block-open-source-introduces-codename-goose
- https://github.com/block/goose
- https://block.xyz/inside/introducing-the-goose-grant-program
- https://www.aviator.co/podcast/block--ai-agents-goose
- https://venturebeat.com/programming-development/jack-dorsey-is-back-with-goose-a-new-ultra-simple-open-source-ai-agent-building-platform-from-his-startup-block
