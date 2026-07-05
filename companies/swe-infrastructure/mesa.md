# Mesa

> A version-controlled, POSIX-compatible filesystem plus multi-agent code review, built as infrastructure for AI coding agents.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** bronze
- **Founded:** not disclosed on site; launched publicly ~Oct 2025 (Reported — LinkedIn launch post); San Francisco Bay Area (Verified — mesa.dev)
- **Website:** mesa.dev — disambiguated from the unrelated OSS "Mesa" Python agent-based-modeling library and from Phoronix's "Mesa" (the graphics driver project); this is the venture-backed AI-infra startup "Mesa" / mesa.dev

## What they do
Mesa is two tightly linked products: (1) **MesaFS**, a Git-compatible virtual filesystem agents can mount for sub-50ms reads/writes, branch/fork instantly for parallel agent runs, and roll back — aimed at agents that need to read/write skills, memory, and code without file-lock contention; and (2) an **AI code review platform** billed as "the world's first multi-agent code review," where agents learn a codebase's architecture, business logic, and team conventions to catch anti-patterns and architectural drift in AI-generated PRs, rather than issuing generic linter-style comments. Together the pitch is "rethinking the SDLC for AI codegen" — infrastructure to keep AI-written code from silently accumulating tech debt.

## Founders & funding
Oliver Gilan (CEO, previously co-founded Antimetal; ex-Census, ex-Microsoft) and Benjamin Warren (CTO, ex-Census, ex-Microsoft) — Verified via mesa.dev/about. Seed round led by Innovation Endeavors; other investors include Essence VC, South Park Commons, and angels Thomas Wolf (Hugging Face CSO) and Soleio. One source cites a $5M seed (Reported — South Park Commons LinkedIn post); exact amount not confirmed on Mesa's own site.

## Evidence of real-world use
Innovation Endeavors' investment post states Mesa was already in use at multiple companies "in lieu of more established AI code review tools" within six months of founding (Reported, single source).

## Relevance to agentic AI engineering
Core SWE-infrastructure play: storage/versioning primitives for multi-agent coding workflows plus an evals-adjacent review layer for AI-generated code.

## Sources
- https://www.mesa.dev/
- https://www.mesa.dev/about
- https://www.innovationendeavors.com/insights/mesa-code-verification
- https://www.linkedin.com/posts/oliver-gilan_introducing-mesa-the-worlds-first-multi-agent-activity-7391508781278511104-JkJs
