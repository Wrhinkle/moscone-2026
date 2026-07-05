# Tool Use & Governance

Papers on the question that decides whether agents ship in production: not "can the model call a tool?" (largely solved) but "what stops it from calling the wrong one — and how would you know?" The area spans the whole enforcement stack: policy checkpoints inside the agent loop, isolation architectures that make prompt injection structurally impossible, syscall-level sandboxing that assumes the agent itself is compromised, and the verification/eval layer that proves any of it actually worked. The through-line across all seven notes: governance enforced *outside* the model beats governance the model is asked to follow, and it often improves task success at the same time.

## How to read this area

Start with three load-bearing papers. **[Governance by Construction](governance-by-construction-for-generalist-agents.md)** is the enforcement blueprint with the strongest numbers — five typed policy checkpoints bought +18–38 pp task success with no fine-tuning, and a cheap model plus policies beat a frontier model without them. **[CaMeLs Can Use Computers Too](camels-can-use-computers-too-system-level-security-for-comp.md)** is the security architecture with actual guarantees — plan before observing, quarantine perception, and injected content provably cannot alter control flow. **[The Evolution of Tool Use](the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md)** is the map: a 200+-work survey that reframes the field around long-horizon orchestration and phase-stratified safety (policy before execution, rollback during, verification after).

The remaining four differentiate by *which layer they enforce or measure at*: ClawLess goes below everything (syscalls, assuming a malicious agent); OpenComputer and the AI Planning Framework attack the verification layer (programmatic state checks and trajectory-level metrics vs. screenshots and pass/fail); WebXSkill governs the capability layer (validated, context-scoped skill registries beat flat libraries).

## Papers

| Paper | One-line finding | Enforcement/measurement layer |
|---|---|---|
| [Governance by Construction for Generalist Agents](governance-by-construction-for-generalist-agents.md) (IBM, May 2026) | Policy-as-code at five agent-loop checkpoints lifted task success +18–38 pp without fine-tuning, at ~1.5–3.3x token cost; defense-in-depth is load-bearing (Intent Guard alone is bypassable by rewording). | Agent loop (policy checkpoints + HITL approval) |
| [CaMeLs Can Use Computers Too](camels-can-use-computers-too-system-level-security-for-comp.md) (Jan 2026) | Single-shot planning with a quarantined perception model gives provable control-flow integrity against prompt injection — and *improved* a 7B CUA by 4.6 pp; residual threat is "branch steering" via adversarial pixels. | Architecture (planner/perception isolation) |
| [ClawLess: A Security Model of AI Agents](clawless-a-security-model-of-ai-agents.md) (Apr 2026) | Treat the agent itself as the adversary: LTL-expressed dynamic policies ("read sensitive → lose network, permanently") enforced at the syscall layer via gVisor/BPF, plus a "Visible" permission letting agents use secrets without reading them. Design paper — no empirical eval. | OS / syscall (below the agent entirely) |
| [The Evolution of Tool Use in LLM Agents](the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) (Mar 2026) | Survey of 200+ works: single-call correctness is solved; production failures are orchestration failures (state, recovery, boundary awareness), and safety should be stratified pre-/in-/post-execution. | Field map (all layers) |
| [OpenComputer: Verifiable Software Worlds](verifiable-software-worlds-for-computer-use-agents.md) (May 2026) | Programmatic state verifiers over 33 real desktop apps agree with humans 94.2% vs 79.2% for LLM-as-judge — screenshot+judge pass rates are partly fiction, and open-source CUA scores crater off their home benchmarks. | Verification (state-based eval / reward) |
| [AI Planning Framework for LLM-Based Web Agents](ai-planning-framework-for-llm-based-web-agents.md) (Mar 2026) | Near-identical success rates hid a 24-pt gap in step-level fidelity between agent architectures; step-by-step agents produce more auditable trajectories, and recovery after deviation is rare (~31–36%) for everyone. | Verification (trajectory-quality metrics) |
| [WebXSkill: Skill Learning for Autonomous Web Agents](webxskill-skill-learning-for-autonomous-web-agents.md) (Microsoft, Apr 2026) | Executable skills paired with step-level guidance gain +8–14 pts on web benchmarks — but the ablation is the governance lesson: unvalidated skills are worse than none, and a context-scoped registry beats a flat library by ~10 pts. | Capability (validated skill/tool registries) |

All seven are located and sourced (arXiv, one with OpenReview/IBM Research corroboration). Caveats worth carrying: ClawLess and the tool-use survey report no experiments; Governance by Construction is a demo paper on two small in-house benchmarks; WebXSkill's skills come from synthetic trajectories on benchmark sites.

## Company categories this area maps to

- **[Security & identity](../../companies/security-identity/)** — the densest mapping. Keycard, Runlayer, WorkOS, Scalekit, Descope, and Auth0 sell the least-privilege permissioning and audit plumbing these papers formalize; ClawLess's "Visible" permission is precisely 1Password's agent-credential problem.
- **[Browser & computer use](../../companies/browser-computer-use/)** — Browserbase, Cua, Yutori, and The Browser Company face every threat model here daily (CaMeL's cookie-banner injection succeeded 100% against undefended agents) and are the natural consumers of OpenComputer-style instrumented environments.
- **[Agent orchestration](../../companies/agent-orchestration/)** — HumanLayer *is* the Tool Approval checkpoint; LangChain's LangGraph is CUGA's substrate; Composio's registries should carry policy annotations per the Tool Guide pattern; Temporal/Inngest/Orkes own the transactional-rollback primitive the survey highlights (SagaLLM/Atomix).
- **[Evals & observability](../../companies/evals-observability/)** — the 94.2%-vs-79.2% verifier-vs-judge result and the five trajectory metrics are direct roadmap items for Arize, Braintrust, and Hamming AI: programmatic checkers and trajectory-level evals over LLM-judge screenshots.
- **[SWE infrastructure](../../companies/swe-infrastructure/)** — E2B and Daytona provide the sandboxes ClawLess argues need dynamic, taint-aware policies rather than bare isolation; Meticulous's deterministic state-based UI testing is validated by OpenComputer's verifier-over-judge finding.
- **[Cloud & compute](../../companies/cloud-compute/)** — Docker and Modal as execution-isolation substrate; Microsoft as WebXSkill's research home feeding Copilot computer use.
- **[API platforms](../../companies/api-platforms/)** — Gravitee's gateway governance is the network-layer analog of the tool-call-boundary enforcement in ClawLess and Governance by Construction.
- **[Models & inference](../../companies/models-inference/)** — OpenRouter and Not Diamond cover the survey's model-routing cost lever; OpenAI, Google DeepMind, and Amazon AGI Labs are the frontier CUA builders that still top out at 68.3% on OpenComputer.

## Open questions the area hasn't answered

- **Who authors the policies?** Every enforcement approach (LTL rules, policy schemas, playbooks) assumes someone writes and maintains dozens of correct policies per domain — none of these papers measure that cost.
- **Perception-layer spoofing is unsolved.** CaMeL's branch steering (adversarial pixels selecting a valid-but-malicious branch) survived even DOM-enhanced verification.
- **Open-ended tasks vs. pre-enumerable plans.** Plan-before-observe and playbook approaches strain when the state space can't be written down in advance ("find me the cheapest flight").
- **Recovery, not planning, is the bottleneck.** Both web-agent papers found agents rarely rejoin the correct path after deviating; almost all governance effort targets preventing bad steps, not recovering from them.
- **What does syscall-level enforcement cost?** ClawLess ships no latency numbers; nobody has measured dynamic policy enforcement on real coding-agent workloads.
