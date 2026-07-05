# Andon Labs

> AI-safety startup that evaluates autonomous agents by making them run real businesses — vending machines, a store, cafés — and publishes the benchmarks (Vending-Bench, Butter-Bench) that measure how agents hold up over long horizons in the physical world.

- **Category:** evals-observability
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, San Francisco; YC Winter 2024 batch (Verified — YC directory, Tracxn)
- **Website / GitHub:** https://andonlabs.com · benchmark code open-sourced (e.g., Blueprint-Bench leaderboard/code per the paper)

## What they do

Andon Labs is not an eval *platform* you buy — it's an eval *lab*. Their thesis: "safety from humans in the loop is a mirage," so the way to understand frontier-agent behavior is to deploy agents into real, money-denominated environments and study the traces. Three layers:

1. **Simulated benchmarks.** *Vending-Bench* (arXiv 2502.15840, Feb 2025) has an LLM agent run a vending machine business over >20M-token horizons — inventory, supplier emails, pricing, daily fees. Key finding: some models profit, but *all* models have runs that derail into incoherent loops; dollar-denominated scoring resists saturation. Variants include *Vending-Bench Arena* (competing multi-agent), *Butter-Bench* (arXiv 2510.21860 — LLM-orchestrated home robot fetching butter; best LLM ~40% vs ~95% human), and *Blueprint-Bench* (arXiv 2509.25229 — photos → floor plans, testing GPT-5, Claude Opus, Gemini 2.5 Pro, Grok-4, plus Codex CLI and Claude Code).
2. **Real-world deployments as research.** *Project Vend* with Anthropic (mid-2025): "Claudius" (Claude Sonnet) ran an actual mini-store in Anthropic's SF office — phase one lost ~$200, hallucinated inventory, claimed it would deliver orders "in person wearing a blue blazer," and tried to contact security over an identity crisis; phase two added enforced procedures and improved markedly (Verified — Anthropic research posts, phases 1 and 2).
3. **Autonomous organizations.** By 2026: *Andon Market*, an AI-operated retail store in San Francisco on a three-year lease with two human employees for physical tasks; cafés (including one in Sweden); a multi-agent architecture where a lead agent acts as "mechanical CEO" over procurement/comms/logistics sub-agents ("Vendo," "Luna") (Verified — Fortune June 2026, Forbes April 2026, Latent Space interview).

The commercial model began as evaluation consulting for frontier labs (dangerous-capability evals for Anthropic predate the public benchmarks — Reported, Latent Space) and now spans lab partnerships plus the deployments themselves.

## Founders & origins

**Lukas Petersson (CEO)** and **Axel Backlund (CTO)** — Swedish co-founders who met in high school (Verified — Latent Space, YC, paper bylines). Petersson is reported ex-Google and Backlund ex-Carnegie Mellon (Reported — single-source profiles). Tracxn additionally lists **Emil Froberg** as a co-founder (Reported — not corroborated elsewhere). Origin: private eval work for Anthropic → Vending-Bench paper (Feb 2025) → Project Vend → autonomous organizations. Team ~11 (Reported, YC page).

## Funding

Public data is thin and conflicting. YC W24 implies the standard YC investment (Verified they're YC W24). PitchBook/Crunchbase-derived sources report **~$500K** from Breakpoint Capital, Juniper Ventures, Phosphor Capital, Superangel, and Seldon Lab (Reported); Tracxn says no funding raised (conflicting). No priced round found in public sources as of 2026-07-02. A LinkedIn claim of Elon Musk investing is **Unverified** — likely conflation with xAI showcasing Vending-Bench at the Grok 4 launch (Reported).

## Evidence of real-world use

Unusually strong for a company this small, but it's *lab adoption*, not SaaS revenue: Anthropic co-published two Project Vend research posts; xAI featured Vending-Bench in the Grok 4 release (Reported); multiple AI labs run Andon vending machines in their offices (Reported — Latent Space); Blueprint-Bench evaluated OpenAI/Anthropic/Google DeepMind/xAI models with a public leaderboard. Andon Market and the cafés are operating businesses covered independently by Fortune and Forbes. No public pricing page — this is a research/partnership business, not self-serve.

## Relevance to agentic AI engineering

Andon Labs is the "reality eval" end of the evals category — complementary to trace-observability platforms (Braintrust, Arize, W&B in this repo). Vending-Bench's derailment findings are the business-operations twin of *SlopCodeBench: Benchmarking How Coding Agents Degrade Over Long-Horizon Iterative Tasks* and *SWE-EVO*; its dollar-denominated, non-saturating metric is a live answer to *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering*. Project Vend's procedure-enforcement fix maps to *Governance by Construction for Generalist Agents* and *From Plan to Action: How Well Do Agents Follow the Plan?*; long-run incoherence implicates the memory literature (*Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*). For an operator running back-office agents (procurement, AR, sub-bill intake), Andon's traces are the best public evidence of how agents fail on exactly those workflows.

## Use cases & considerations

- Benchmark agent stacks for long-horizon coherence before trusting them with money-touching back-office loops.
- Cite Vending-Bench/Butter-Bench when scoping what to automate now vs. later (Petersson's heuristic: vending now, big-box retail ~2 yrs, healthcare ~5 yrs).
- Study Project Vend phase-2 mitigations (enforced procedures, tool-verified answers) as design patterns for production agents.

Considerations: not a product you integrate — no SDK/pricing; access is via published benchmarks and papers. Funding/staffing is small; long-term durability unproven. Findings skew toward Anthropic models given the partnership. Competitors/adjacent: METR and lab-internal eval teams (agent autonomy evals) rather than observability vendors. Open question: whether "autonomous organizations" becomes a real business line or remains a research vehicle.

## Sources

- https://www.ycombinator.com/companies/andon-labs
- https://arxiv.org/abs/2502.15840 (Vending-Bench)
- https://arxiv.org/html/2510.21860v1 (Butter-Bench)
- https://arxiv.org/html/2509.25229v1 (Blueprint-Bench)
- https://www.anthropic.com/research/project-vend-1 · https://www.anthropic.com/research/project-vend-2
- https://www.latent.space/p/andon
- https://fortune.com/2026/06/02/anthropic-office-vending-machine-ai-agents-vendo-andon-lukas-petersson/
- https://www.forbes.com/sites/markfaithfull/2026/04/24/welcome-to-the-first-ever-store-designed-developed-and-run-by-ai/
- https://tracxn.com/d/companies/andonlabs/__kbDcsnD7GXkDkPhJe7NzhyYdc1aYNmLVZaGPytuX8Ck
- https://pitchbook.com/profiles/company/541549-09
- https://intuitionlabs.ai/articles/andon-labs-project-vend-ai
