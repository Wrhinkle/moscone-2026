# One Developer Is All You Need: A Case Study of an AI-Augmented One-Person Squad in a Brownfield Enterprise

- **Status:** Located — [arXiv:2605.18461](https://arxiv.org/abs/2605.18461)
- **Area:** planning-architecture
- **Authors / venue / date:** Marcelo Vilas Boas, Gustavo Pinto, Edward Roberto Monteiro, Vinicius Fernandes Carida, Danilo Ribeiro — arXiv (cs.SE), submitted 2026-05-18 (v2 2026-05-19)

## Problem
Can a single experienced engineer plus AI agents deliver enterprise brownfield work scoped for a full squad — in a regulated setting (Brazilian Central Bank/CVM compliance, WCAG 2.1 AA) with undocumented legacy contracts across nine repositories? Most agentic-coding evidence comes from greenfield or benchmark settings; this is a production case study at Itaú Unibanco (digital signature platform for non-account holders, 4 microservices + frontend).

## Approach
One staff engineer (8 yrs experience, 4 yrs tenure) orchestrated four role-specialized agents under Spec-Driven Development (SDD), where natural-language specs — not code — are the primary engineering artifact:

1. **Product Manager agent** (StackSpot) — discovery, user stories, domain context
2. **Specification agent** (Devin) — detailed specs with multi-repo grounding: architecture decisions, interface contracts, acceptance criteria, compliance constraints
3. **Core developer agent** (GitHub Copilot) — business logic under continuous human-in-the-loop review
4. **Non-core developer agent** (Devin) — autonomous infra, API integrations, queues, boilerplate

Oversight scaled with judgment required; final homologation (performance, UI, acceptance) stayed human by design.

## Key findings
- 5 features / 25 user stories / 890 Business Complexity Points delivered in 3 sprints vs. 6 planned — **50% time-to-market reduction**
- Throughput 0.59 → 3.21 BCP/engineer-hour (**5.4×**); hours per BCP 8.93 → 2.2
- **90% of AI-generated code accepted without structural modification** on first review
- 113 integration tests and 65 e2e tests at 100% pass; coverage 92.8% backend / 90.3% frontend; 32 production deployments; 1 post-validation defect, 0 post-release
- Cost: R$60k actual staffing + ~R$5–7k tooling vs. R$492k budget (**>85% reduction**)
- Undocumented legacy integration contracts were the top source of underspecification — rework there exceeded upfront spec cost

## Limitations & open questions
Single case, single institution; the primary subject is also an author (confirmation-bias risk, no independent observer). Baseline is the same squad's historical projects, not a control. Results are confounded with a strong senior engineer — unknown whether this works with juniors, and the model consumes exactly the institutional knowledge it doesn't create. No full TCO, no security/IP analysis, and a skeptic would ask whether 3 sprints of one project can show long-horizon maintainability effects.

## Why builders should care
The binding constraint was specification quality and institutional knowledge, not model capability. If you're building agentic SDLC tooling, invest in spec generation/validation and multi-repo context grounding, not just codegen. Role-partitioning agents by judgment required (autonomous for boilerplate, HITL for core logic) is a concrete, copyable pattern.

## Related companies in this landscape
- **Cognition** — Devin is literally two of the four agents here; the paper is direct production validation.
- **Microsoft / GitHub** — Copilot as the supervised core-developer agent.
- **Tessl** — spec-driven, specs-as-primary-artifact development is exactly its thesis; this paper is its strongest field evidence.
- **Unblocked / Sourcegraph** — the "undocumented legacy contracts cause rework" finding is the case for institutional-knowledge and multi-repo code-context products.
- **Qodo / Greptile / Sonar / Snyk** — automated quality/review gates were the guardrails that let 90% first-pass acceptance be safe in a regulated bank.
- **Factory** — one-orchestrator-many-agents software delivery is its product model.

## Sources
- https://arxiv.org/abs/2605.18461
- https://arxiv.org/html/2605.18461v2
