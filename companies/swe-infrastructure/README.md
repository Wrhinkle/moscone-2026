# SWE Infrastructure

CI/CD, merge queues, sandboxes and dev environments, code quality & security scanning, code intelligence, editors/terminals, and engineering analytics. This is the plumbing of software delivery: the layer that decides whether code builds, tests, merges, and ships. The problem it solves has changed shape. For a decade these tools removed friction for *human* developers; as of 2025–26 nearly every company in this folder has repositioned around a single thesis: when coding agents write most of the code, the scarce layer shifts to sandboxed execution and deterministic verification, plus the governed pipelines that land the result. AI can write the code, but someone still has to trust, run, and land it.

## How to read this category

Three profiles carry most of the weight. **[Sonar](sonar.md)** is the incumbent-scale anchor ($4.7B valuation, >75% of the Fortune 100, platinum sponsor) and the cleanest statement of the verification thesis: "vibe, then verify." **[E2B](e2b.md)** and **[Daytona](daytona.md)** define the newest primitive, the API-provisioned agent sandbox, and their rivalry (open-source self-hostable vs. recently closed-core, supporting-tier vs. gold-tier sponsor) is the category's best head-to-head. **[Warp](warp.md)** is the growth story: a terminal that became an "Agentic Development Environment," reportedly adding $1M ARR every week.

The axis that differentiates the rest is *where in the agent SDLC they sit*:

- **Execution substrate** (where agent code runs): [E2B](e2b.md), [Daytona](daytona.md), [Coder](coder.md) (self-hosted/governed), [Flox](flox.md) (reproducible environments)
- **Verification & gating** (whether agent code is trusted): [Sonar](sonar.md), [CircleCI](circleci.md), [Buildkite](buildkite.md), [Meticulous](meticulous.md), [Mesa](mesa.md)
- **Landing & provenance** (how agent code merges and is accounted for): [Aviator](aviator.md), [Entire Inc.](entire-inc.md)
- **Human-agent interface** (where developers steer agents): [Warp](warp.md), [Zed](zed.md), [Superconductor](superconductor.md)
- **Context & runtime intelligence** (what agents know): [Unblocked](unblocked.md) (org knowledge), [Lightrun](lightrun.md) (live production state)
- **Measurement** (whether any of it worked): [Jellyfish](jellyfish.md)

A second useful axis is **self-hosted vs. managed**: Buildkite, Coder, and Flox win where code can't leave the building; CircleCI, Daytona, E2B, and Meticulous sell the managed convenience of the same primitives.

## Start here

1. **[sonar.md](sonar.md)**: the scale end of the category and the purest "deterministic verification gates AI code" bet (AI Code Assurance, AutoCodeRover acquisition, MCP server for agent self-remediation).
2. **[e2b.md](e2b.md)**: the sandbox primitive explained, with the strongest third-party corroboration in the folder (Hugging Face runs tens of thousands of E2B sandboxes for Open-R1; Perplexity and Manus in production).
3. **[coder.md](coder.md)**: the enterprise/governance counterweight, with egress firewalls, audited tool calls, air-gapped agent fleets, and the memorable KKR investor-as-customer datapoint.
4. **[entire-inc.md](entire-inc.md)**: the newest and loudest signal about where the category is going. GitHub's ex-CEO raised a record $60M seed to build provenance/audit infrastructure for agent-generated commits.

## Profiles (18)

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Sonar](sonar.md) | SonarQube static analysis, repositioned as the verification layer for AI-generated code | Platinum | ~$457M raised; $4.7B valuation (2022); bootstrapped 8 years first | Claims 750B lines of code analyzed daily; acquired AutoCodeRover, one of the first LLM repair agents |
| [Unblocked](unblocked.md) | Context engine over repos/Slack/Jira so agents and humans get answers grounded in real org decisions | Platinum | ~$30M (Series A, May 2025, B Capital) | Founder's previous company (Buddybuild) was acquired by Apple and fed into Xcode Cloud |
| [Buildkite](buildkite.md) | Hybrid CI/CD (SaaS control plane, self-hosted build agents), now the delivery layer for agent-driven engineering | Gold | ~$40M; profitable and bootstrapped for 7 years pre-Series A | Uber, Airbnb, Canva, Slack standardized on it; ships a "build fixer" reference workflow where Claude reads failure logs and opens a fix PR |
| [Coder](coder.md) | Self-hosted cloud dev environments, repositioned as the governed runtime for agent fleets | Gold | ~$168–175M; $90M Series C led by KKR (Apr 2026) | Investor KKR deployed it to 500+ of its own engineers; code-server has ~78k GitHub stars |
| [Daytona](daytona.md) | API-provisioned stateful sandboxes (sub-90ms spin-up) for agent code execution, computer use, and RL rollouts | Gold | ~$31M; $24M Series A (FirstMark, Feb 2026) with Datadog and Figma Ventures | LangChain runs ~4,000 sandboxes/month on it; closed-sourced its 72k-star core in June 2026 |
| [Lightrun](lightrun.md) | Live production debugging without redeploys, now a runtime-context MCP layer and AI SRE | Gold | $110M (company figure); $70M Series B (Accel + Insight, Apr 2025) | Taboola case study: two-week backend investigations cut to under an hour |
| [Meticulous](meticulous.md) | Replays recorded real user sessions against every PR as a self-maintaining visual E2E test suite | Gold | ~$4.1M seed (Coatue, YC); no Series A found | Deterministic replay engine built at the Chromium level to kill flake; Dropbox and Notion among logos |
| [Warp](warp.md) | Rust terminal turned "Agentic Development Environment" for launching and steering parallel coding agents | Gold | ~$73M (Series B, Sequoia, 2023); no round since despite reported hypergrowth | Reported $1M ARR added every 5–6 days; open-sourced the client in April 2026 with OpenAI's financial support |
| [Zed](zed.md) | Open-source Rust editor from the Atom creators, rebuilt for human-agent collaboration | Gold | >$42M; $32M Series B led by Sequoia (2025) | Co-created the Agent Client Protocol (ACP) with JetBrains, the editor-side analog of MCP |
| [CircleCI](circleci.md) | Original managed CI/CD, repositioning as "autonomous validation" for agent-written code | Silver | ~$315M; $1.7B valuation (2021); no round since | Chunk, its autonomous CI-fixing agent, runs read-only with bring-your-own OpenAI/Anthropic key |
| [Flox](flox.md) | Nix-powered reproducible environments: identical dev/build setups locally, in CI, and in production | Silver | $16.5M Series A (NEA) + $25M Series B (Addition, Sept 2025) | Incubated at D.E. Shaw's venture studio; PostHog collapsed a 16-step local setup into one command |
| [Superconductor](superconductor.md) | Multiplayer cloud workspace for running and comparing parallel coding agents (Claude Code, Codex, Amp...) | Silver | Seed (Volition, Inc.; amount unverified) | Co-founded by Sergey Karayev (Gradescope co-founder); lets PMs and designers launch agents from Slack/iOS |
| [Mesa](mesa.md) | Git-compatible virtual filesystem for parallel agent runs plus multi-agent code review | Bronze | ~$5M seed (Innovation Endeavors; amount reported, single source) | MesaFS: sub-50ms reads/writes with instant branch/fork so agent fleets don't fight over file locks |
| [Aviator](aviator.md) | Merge queues and stacked PRs, repositioned as the "landing layer" for AI-generated code | Supporting | ~$2.3M pre-seed (YC S21) | Runbooks turn agent tasks into spec-driven stacked PRs (one reviewable PR per step), landed via merge queue |
| [E2B](e2b.md) | Open-source Firecracker-microVM sandboxes (~150ms boot) for agent code execution, desktops, and RL | Supporting | ~$32.5M; $21M Series A (Insight, July 2025) | Hugging Face runs tens of thousands of concurrent E2B sandboxes for its Open-R1 DeepSeek-R1 reproduction |
| [Entire Inc.](entire-inc.md) | Git-native provenance/audit infrastructure for agent-generated code, from GitHub's former CEO | Supporting | $60M seed at $300M valuation (Felicis, Feb 2026) | Reported as the largest seed round in developer-tools history; Checkpoints CLI already open source |
| [Jellyfish](jellyfish.md) | Engineering intelligence dashboard, now measuring AI coding-tool adoption and ROI across the org | Supporting | ~$114M (Series C: Accel, Insight, Tiger) | Its 20M+ PR benchmark study: 90% of engineering teams now use AI coding tools, up from 61% a year prior |
| [Programma Labs](programma-labs.md) | Stealth: human oversight, sandboxing, and verification for coding and computer-use agents | Supporting | Unverified; no public funding, founders, or product found | The folder's only true unknown: a one-page site, job ads, and an AIEWF sponsor listing |

**Coverage notes:** all 17 companies expected in this category are present; **Superconductor** is an addition beyond the original expected list (silver tier, filed here as agent-orchestration workspace). The **Programma Labs** profile is largely unverifiable by its own admission; treat it as a placeholder pending public disclosure. Watch for name collisions flagged in the profiles: Warp here is warp.dev (a payroll company also uses the name, at warp.co), Mesa is mesa.dev (distinct from the graphics project and the Python library), and Meticulous is meticulous.ai (distinct from Meticulous Research).

## Related papers

The profiles in this folder cite the repo's paper notes constantly; these are the ones that genuinely map to the category.

**Agentic-SWE benchmarks** (the failure modes this category's verification layer is built to catch):

- [SlopCodeBench: how coding agents degrade over long horizons](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md): the quality-decay problem Sonar, CircleCI's Chunk, and Mesa's review layer all claim to gate.
- [ProdCodeBench: a production-derived benchmark for coding agents](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md): production context as the honest eval; cited by Sonar, Lightrun, Meticulous, CircleCI, and Unblocked profiles.
- [Position: coding benchmarks are misaligned with agentic software engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md): the right skeptical lens on vendor benchmark claims (Warp's Terminal-Bench/SWE-bench marketing especially).
- [SWE-EVO: coding agents in long-horizon software evolution](../../papers/swe-agents/swe-evo-benchmarking-coding-agents-in-long-horizon-software.md): long-horizon iteration needs exactly the resumable sandboxes (Daytona, E2B) and CI feedback loops (Buildkite, CircleCI) sold here.
- [FeatureBench: agentic coding for complex features](../../papers/swe-agents/featurebench-benchmarking-agentic-coding-for-complex-featur.md): feature-level evals presuppose isolated, reproducible environments per trajectory.
- [Reproducible, explainable, and effective evaluations of agentic AI for SWE](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md): production pipelines as the eval harness benchmarks approximate (Buildkite's framing).
- [Effective strategies for asynchronous multi-agent collaboration in SWE](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md): the parallel-agent substrate assumed by Coder, Daytona, E2B, Aviator's stacked-PR runbooks, and Superconductor.

**Tool use, governance, and security** (policy enforced by the environment rather than the prompt):

- [Governance by construction for generalist agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md): the single most-cited paper across this folder; Coder's egress firewalls, Buildkite's scoped credentials, Aviator's mandatory review gates, and Sonar/CircleCI MCP loops are all commercial instances.
- [CaMeLs can use computers too: system-level security for computer-use agents](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md): the threat model behind VM-level sandbox isolation (E2B, Daytona, Coder).
- [ClawLess: a security model of AI agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md): companion security framing for agent runtimes.
- [Verifiable software worlds for computer-use agents](../../papers/tool-use-governance/verifiable-software-worlds-for-computer-use-agents.md): maps to E2B/Daytona desktop sandboxes and Meticulous's deterministic replay-as-ground-truth.
- [The evolution of tool use in LLM agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): the MCP-server wave (Sonar, CircleCI, Buildkite, Lightrun, Unblocked all ship one) as multi-tool orchestration surface.

**Memory and context** (what Unblocked and Lightrun are betting on):

- [Are we ready for an agent-native memory system?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): the thesis behind Unblocked's authority-weighted, deduplicated retrieval.
- [Memory for autonomous LLM agents: mechanisms, architectures, and evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md): survey grounding for org-knowledge context engines and Lightrun's cross-incident "knowledge memory engine."
- [Hierarchical long-term semantic memory for LinkedIn's AI agents](../../papers/memory-research-agents/hierarchical-long-term-semantic-memory-for-linkedin-s-ai-age.md): a production analog of structured retrieval over org artifacts.

**Planning and the brownfield reality:**

- [One developer is all you need: a case study of an AI-augmented workflow](../../papers/planning-architecture/one-developer-is-all-you-need-a-case-study-of-an-ai-augment.md): real SWE work is brownfield and context-starved, the gap Unblocked targets directly.

## Open questions

1. **Layer or feature?** Nearly every bet here (sandboxes: E2B/Daytona; context: Unblocked; merge automation: Aviator; CI-for-agents: Buildkite/CircleCI) faces the same absorption risk: does it stay a standalone layer, or do agent vendors, hyperscalers, and GitHub build it in? E2B's own profile asks whether the sandbox primitive gets absorbed upstream into model-provider APIs.
2. **Who owns agent validation?** Sonar (deterministic SAST), CircleCI (CI pipelines), Mesa and the LLM-review crowd (Qodo, Greptile, CodeRabbit) are all claiming the gate on agent-generated PRs. Deterministic analysis and LLM-native review can't both be the canonical checkpoint forever.
3. **Does provenance become mandatory?** Entire's $60M seed prices in a future where audit trails for agent-generated commits are compliance table stakes. Nothing in the folder yet shows a customer *required* to have this.
4. **Do vendor-reported agent-era numbers survive contact with third parties?** Warp's ARR trajectory, Daytona's run-rate, Unblocked's token-savings benchmark, and Jellyfish's 90%-adoption study are all self-published. The strongest independently corroborated datapoint in the folder remains Hugging Face's Open-R1 usage of E2B.
5. **Execution risk at the incumbents and the newborns alike.** CircleCI hasn't raised since 2021 and carries a 2023 breach; Buildkite's founder-CEO exited without explanation in 2025; Daytona closed-sourced its core; Programma Labs has no public product at all. In each case the repositioning story has moved faster than the evidence behind it.

*Curated 2026-07-05 from the 18 profiles in this folder.*
