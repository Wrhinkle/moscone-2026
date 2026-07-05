# Factory

> Model-agnostic AI software engineering agents ("droids") that run in your terminal, IDE, CI, Slack, or browser and execute full SDLC tasks — sold hard into large enterprises.

- **Category:** coding-agents
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, San Francisco (Verified; legal name "The San Francisco AI Factory, Inc."). As of 2026-07-02.
- **Website / GitHub:** https://factory.ai · docs: https://docs.factory.ai

## What they do

Factory builds autonomous software-development agents branded **droids**. The core product is **Droid CLI**, a terminal agent comparable to Claude Code or Codex CLI, plus a desktop **Factory App**, **Droid Exec** (a non-interactive mode for CI/CD and scripted automation), and a web platform. Droids can be dispatched from the terminal, VS Code/JetBrains/Zed, Slack, Linear, or the browser, and target the whole lifecycle — feature development, code review (`/review`), migrations/modernization, debugging, testing, incident response — not just code completion.

The deliberate architectural bet is being **model-, IDE-, and interface-agnostic**: droids route across frontier LLMs (with BYOK support for custom endpoints and open-source models) rather than binding to one provider. Extensibility mirrors the emerging agent-config standard set: AGENTS.md project instructions, reusable Skills, MCP integrations, custom subagents, and hook-based policy enforcement. Enterprise features include governance/observability tooling, on-prem/high-security deployment, and an "Agent Readiness" assessment that scores a repo's suitability for agent-driven work. At the September 2025 Droids GA launch, Factory claimed the #1 spot on Terminal-Bench (58.75%) — Verified as their claim across multiple press writeups; the ranking has since been contested territory as competitors leapfrog.

## Founders & origins

- **Matan Grinberg (CEO)** — Princeton string theory, dropped out of a Berkeley physics PhD in 2023 after cold-emailing Sequoia partner Shaun Maguire about string theory (Verified; Fast Company, Sequoia's Training Data podcast).
- **Eno Reyes (CTO)** — ML engineer at Hugging Face, prior LLM work at Microsoft; thesis on deep learning (Verified).

They were 24 and 23 at founding. Mission framing: "bring autonomy to software engineering."

## Funding

- **Seed (2023):** amount not clearly broken out in public sources; Bloomberg put total funding at "over $20M" post-Series A, implying roughly $5M (Unverified as exact figure).
- **Series A, June 2024:** $15M led by Sequoia, ~$120M valuation (Verified: Bloomberg, factory.ai).
- **Series B, September 2025:** $50M from NEA, Sequoia, NVIDIA, and J.P. Morgan, plus Abstract, Mantis, and angels (Frank Slootman, Nikesh Arora, Aaron Levie); ~$300M valuation (Verified: BusinessWire, SiliconANGLE).
- **Series C, April 2026:** $150M led by Khosla Ventures (Keith Rabois joined the board), with Sequoia, Insight Partners, Blackstone, Evantic, 20VC, NEA, Mantis; $1.5B valuation (Verified: TechCrunch, factory.ai).
- **Total raised:** ~$220M (computed from the above).

## Evidence of real-world use

Named enterprise customers with rollouts: **MongoDB, EY (Ernst & Young), Bayer, Zapier, Clari, Bilt Rewards** (Verified across funding announcements and press). Factory additionally claims developer usage at NVIDIA, Adobe, Palo Alto Networks, Adyen, and Morgan Stanley (Reported — vendor claim in Series C materials). Headline metrics — 31x faster feature delivery, 96.1% shorter migrations, 95.8% faster on-call resolution — are vendor-reported and unaudited. Softer but genuine signals: OpenAI published a Factory case study for its reasoning models; TechCrunch cites 200% quarter-over-quarter growth in 2025; developer-community posts (daily.dev, Latent Space's "A-SWE Droid Army" profile) show organic CLI adoption among individuals switching from Claude Code/Gemini CLI for model choice.

## Relevance to agentic AI engineering

Factory sits squarely in the **agentic SDLC** layer of the stack — a direct subject for this repo's agentic-SWE benchmark work. Their Terminal-Bench-led marketing is exactly the phenomenon *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* critiques, and their enterprise migration/modernization pitch is what *SWE-EVO* and *SlopCodeBench* (long-horizon degradation) actually measure. Feature-level delegation maps to *FeatureBench*. Their hooks/policy enforcement and governance tooling connect to *Governance by Construction for Generalist Agents*, and their AGENTS.md/organizational-context approach touches the questions in *Are We Ready For An Agent-Native Memory System?*.

## Use cases & considerations

Use cases: (1) parallel background agents for migrations/refactors across large legacy codebases; (2) Droid Exec in CI for automated review and test generation; (3) Slack/Linear-dispatched fixes for on-call triage; (4) model-agnostic CLI agent when you want per-task model routing rather than single-vendor lock-in.

Considerations: fierce competition from Claude Code, OpenAI Codex, Cursor, Cognition (Devin/Windsurf), and GitHub's coding agent — several with structural distribution advantages; benchmark leadership is transient; efficiency/ROI metrics are self-reported; pricing is enterprise-oriented and not fully public; being model-agnostic means margin and quality depend on upstream labs they also compete with. For a small operator, the CLI is usable today, but the platform's center of gravity is clearly large-org governance.

## Sources

- https://factory.ai/news/series-b
- https://factory.ai/news/series-c
- https://factory.ai/news/series-a-announcement
- https://docs.factory.ai/welcome
- https://techcrunch.com/2026/04/16/factory-hits-1-5b-valuation-to-build-ai-coding-for-enterprises/
- https://www.bloomberg.com/news/articles/2024-06-18/sequoia-backs-ai-startup-that-automates-engineering-tasks
- https://www.businesswire.com/news/home/20250925993478/en/
- https://siliconangle.com/2025/09/25/factory-unleashes-droids-software-agents-50m-fresh-funding/
- https://www.fastcompany.com/91279593/factory-ai-code-generation-matan-grinberg-eno-reyes
- https://openai.com/index/factory/
- https://sequoiacap.com/podcast/training-data-factory/
- https://www.latent.space/p/factory
