# Safe Intelligence

> Imperial College London spinout applying formal verification to ML models — and, since 2026, spec-driven black-box testing to AI agents (Spec27).

- **Category:** evals-observability
- **AIEWF 2026 tier:** bronze
- **Founded:** 2021, London, UK (Verified — Imperial College news, company site)
- **Website / GitHub:** https://safeintelligence.ai · https://www.spec27.ai · academic lineage: https://github.com/vas-group-imperial/venus, https://github.com/vas-group-imperial/VeriNet-OpenSource

Note: do not confuse with Ilya Sutskever's Safe Superintelligence Inc. (SSI) — entirely unrelated company.

## What they do

Two product lines, one thesis: testing on held-out data is not enough for models that carry real risk.

1. **Core validation platform** ("Validate / Robustify / Monitor"). Formal verification of neural networks, decision trees, and random forests against defined perturbation classes — mathematically proving (not sampling) that a model's output is stable across a region of input space. "Robustification" then retrains/repairs models where fragilities are found; monitoring tracks drift post-deployment. Delivered as CLI tools plus a platform. This is the productization of the Venus (MILP-based) and VeriNet (symbolic interval propagation) verification toolkits from Lomuscio's Verification of Autonomous Systems group at Imperial. Target workloads: vision and tabular models in finance, mobility, robotics, aviation (Verified).

2. **Spec27** (launched in early access April 8, 2026, at the AI.Engineer Europe Summit in London). A spec-driven validation and monitoring platform for LLM applications and agents. You write a structured specification of expected behavior (capability + input dataset + context + what the agent must be robust to); Spec27 auto-generates test suites — including adversarially amplified variants — and runs them pre-deployment and continuously. Notably it is **black-box, outside-in**: it hits your user-facing endpoint like a user would, testing the whole stack including guardrails and filters, with no SDK, gateway, or model access required (Verified — launch post, spec27.ai).

## Founders & origins

- **Alessio Lomuscio** — founder & CTO. Professor of Safe Artificial Intelligence at Imperial College London, RAEng Chair in Emerging Technologies, ACM Distinguished Member, EurAI fellow, 200+ papers on verification of autonomous/multi-agent systems (Verified).
- **Steven Willmott** — CEO (appointed at the Feb 2025 raise, previously led product/engineering there). Founder/CEO of 3scale, the API-management company acquired by Red Hat; PhD in AI (Verified).
- Panagiotis Kouvaros (co-author of Venus/VeriNet) is also at the company (Reported — LinkedIn).

## Funding

- **Seed: £4.15M, announced Feb 20, 2025.** Led by Amadeus Capital Partners; OTB Ventures (new) and Vsquared Ventures (existing) participated (Verified — company, Imperial, FinSMEs, Amadeus).
- Vsquared being an "existing investor" implies an earlier pre-seed; amount/date not found in public sources (Unverified).
- **Total publicly disclosed: £4.15M.**

## Evidence of real-world use

Thin, publicly. No named customers or published case studies found as of 2026-07-02. Documented signals: an early-access/early-user program targeting safety-critical sectors, with Imperial's announcement citing pilots in financial services (lending models) and aviation (autonomous cargo aircraft control) — sectors, not logos (Reported). Spec27 had a Show HN and conference launch (booth at AI.Engineer Europe 2026; sponsoring AIEWF 2026). The underlying Venus/VeriNet toolkits are established in the academic NN-verification community (VNN-COMP lineage). Treat this as a credible deep-tech team pre-commercial-traction, not a proven vendor.

## Relevance to agentic AI engineering

Sits squarely in the evals/validation layer of the agent stack, from an unusual angle: formal methods rather than LLM-as-judge. Spec27's spec-then-adversarially-test loop is a direct response to the gap this repo's agentic SWE benchmark papers document — static benchmarks don't transfer to your use case, so you need per-application harnesses. Its outside-in testing of tool-using agents (including whether guardrails hold under manipulation) connects to the tool-use/governance line of work here; long-term monitoring of spec adherence is relevant wherever agent memory papers show behavior drifting as context accumulates. Less relevant to voice-agent work today (text/API endpoints first). Lomuscio's academic roots are literally in verification of multi-agent systems — rare pedigree for this niche.

## Use cases & considerations

Use cases: (1) regression-test a customer-facing agent against a behavior spec on every prompt/model change, without instrumenting the stack; (2) adversarial robustness/jailbreak hardening tested through the full deployed pipeline; (3) formal robustness certification of vision/tabular models in regulated settings (lending, avionics); (4) continuous production monitoring against specs.

Considerations: no public pricing (early access — expect sales-led); no named customers yet; formal verification scales poorly to frontier-size models, so the core platform suits smaller task models while Spec27 (empirical, not formal) covers LLM agents — know which guarantees you're actually buying. Competitors: Braintrust, LangSmith, Patronus AI, Galileo, Giskard on agent evals; Lakera/Haize on adversarial testing. Open questions: Spec27 traction post-early-access, and whether spec authoring is tractable for messy real workflows.

## Sources

- https://safeintelligence.ai/
- https://safeintelligence.ai/safe-intelligence-raises-4m-to-deliver-advanced-validation-for-reliable-ai/
- https://www.imperial.ac.uk/news/261320/safe-intelligence-raises-4m-build-safe/
- https://safeintelligence.ai/introducing-spec27-spec-driven-validation-for-ai-applications-and-agents/
- https://www.spec27.ai/
- https://www.finsmes.com/2025/02/safe-intelligence-raises-4-15m-in-seed-funding.html
- https://www.amadeuscapital.com/safe-intelligence-raises-4m-to-deliver-advanced-validation-for-reliable-ai/
- https://vsquared.vc/portfolio/safe-intelligence/
- https://github.com/vas-group-imperial/venus
- https://github.com/vas-group-imperial/VeriNet-OpenSource
- https://news.ycombinator.com/item?id=47959984 (Show HN: Spec27; thread content not retrievable at research time)
