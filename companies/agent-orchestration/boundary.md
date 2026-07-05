# Boundary (BoundaryML)

> Maker of BAML, a small typed language for defining LLM function calls and structured outputs, embedded inside Python/TypeScript/Ruby/Go via a compiler + runtime.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, Seattle (Reported — YC company page; team blog references "5 years, 12 pivots" of prior work before landing on BAML)
- **Website / GitHub:** https://boundaryml.com / https://github.com/BoundaryML/baml

## What they do
BAML ("Basically a Made-up Language") is a DSL you write prompts and output schemas in; a compiler generates typed client code (Python/TS/Ruby/Go) so LLM calls return validated structs instead of raw strings, with built-in retries/fallback across providers and VS Code/JetBrains tooling for live-testing prompts. It targets the reliability gap in tool-calling and structured extraction that ad-hoc JSON-mode prompting leaves open, positioning itself against libraries like Instructor, Pydantic-AI, and raw function-calling APIs. Engineers adopt it as a schema/contract layer sitting between application code and any LLM provider.

## Founders & Funding
Co-founded by CEO Vaibhav Gupta (ex-Google, built Pixel 4 depth/face-unlock; also worked on HoloLens) and CTO Aaron Villalpando (7 years at Amazon on EC2 monitoring and Prime Video/Twitch streaming) — Verified via company site. Y Combinator-backed; no specific funding round amount found in public sources (Unverified beyond YC participation).

## Evidence of real-world use
GitHub repo (BoundaryML/baml) has 8,423 stars at time of research — Verified via direct fetch — indicating meaningful OSS developer interest; no named enterprise customers found in public sources.

## Relevance to agentic AI engineering
Directly on-topic for agent-orchestration: BAML addresses structured-output reliability and tool-calling contracts, a foundational piece of any agent stack alongside MCP-style tool integration.

## Sources
- https://boundaryml.com/who-are-we
- https://github.com/BoundaryML/baml
- https://www.ycombinator.com/companies/boundary
- https://boundaryml.com/blog/5-years-12-pivots
