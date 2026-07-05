# CaMeLs Can Use Computers Too: System-level Security for Computer Use Agents

- **Status:** Located — [arXiv:2601.09923](https://arxiv.org/abs/2601.09923) (v3, 2026-06-04; first submitted 2026-01-14); also on [OpenReview](https://openreview.net/forum?id=uD8ZLoi44s)
- **Area:** tool-use-governance
- **Authors / venue / date:** Hanna Foerster, Tom Blanchard, Kristina Nikolić, Ilia Shumailov, Cheng Zhang, Robert Mullins, Nicolas Papernot, Florian Tramèr, Yiren Zhao. arXiv preprint (cs.AI), Jan 2026 (v3 June 2026).

## Problem
Prompt injection is the standing failure mode of computer-use agents (CUAs): anything rendered on screen — a cookie banner, an ad, injected DOM — can hijack the agent. The only defense with real guarantees is architectural isolation (CaMeL-style: trusted planner never sees untrusted data), but CUAs seem to require continuous observation of UI state to decide each next action, which appears incompatible with that isolation.

## Approach
Single-shot planning with a dual-LLM split, structured as Observe–Verify–Act:
- A **privileged planner (P-LLM)** compiles the user query into a complete Python-like execution graph with conditional branches *before* any screenshot is taken. It never sees UI content.
- A **quarantined perception model (Q-VLM)** reads screenshots/DOM at runtime but can only fill in values and return booleans (`verify_hypothesis`) that select among pre-approved branches — it cannot alter control flow.

This yields provable control-flow integrity: injected instructions cannot execute anything outside the pre-written plan. Evaluated on OSWorld.

## Key findings
- Retains up to 57% of frontier-model CUA performance while adding the security guarantee; boosts small open-source CUAs by up to 19%.
- UITars-1.5-7B + CaMeL: 29.0% on all OSWorld tasks vs 24.4% for UITars alone — the security wrapper *improved* the small model, matching a 32B baseline (OpenCUA-32B: 28.7%).
- Planner quality dominates: with GPT-5 as P-LLM, 70.6% pass@5 on a 17-task subset vs 58.8% (Grok-4) and 29.4% (Claude Sonnet as planner).
- Cookie-popup injection: 100% success against undefended agents; blocked by design here.
- Overhead: 1.88x tokens for CaMeL alone (vs 29.6x for Fides, a competing isolation approach); 6.57x with multi-modal consensus checks.
- New attack class identified: **branch steering** — adversarial pixels or fake DOM elements fool the Q-VLM into taking a valid-but-malicious branch; gradient-based pixel attacks evaded even DOM-enhanced verification.

## Limitations & open questions
Authors concede: underspecified tasks force exponentially many branches (cost and performance degrade); data flow can't be fully isolated without making the agent useless; branch steering remains unsolved; OSWorld tasks are often ill-defined and data-independent, so the benchmark undertests the hard cases. A skeptic asks: does single-shot planning survive genuinely open-ended tasks ("find me the cheapest flight") where the state space can't be pre-enumerated? And pass@5/pass@20 gains require parallel sampling — real deployments pay that cost.

## Why builders should care
If you ship browser or computer-use agents, "the model will notice the injection" is not a defense — plan-before-observe architectures with constrained perception are the current best answer with guarantees. Practically: compile plans with a strong planner model, run execution with a cheap grounding model (it may even outperform the small model alone), and treat perception-layer spoofing (branch steering) as your residual threat model.

## Related companies in this landscape
- **Browserbase** — hosted browser infrastructure for agents; its customers are exactly who needs control-flow integrity against injected page content.
- **Cua** — computer-use agent infrastructure; this paper is a direct architectural blueprint/challenge for its runtime.
- **Runlayer / Keycard** — agent governance and least-privilege agent permissions; CaMeL-style plans are the enforcement artifact these products could gate on.
- **WorkOS / Descope / Auth0** — agent identity, audit logs, approval gates; a pre-approved execution graph is auditable in a way free-form agent loops aren't.
- **E2B / Daytona / Modal** — secure sandboxes for agent execution; complementary containment for the data-flow gap the paper admits it can't close.
- **The Browser Company / Yutori** — consumer-facing browsing agents that face cookie-banner-style injection (the paper's 100%-success undefended attack) daily.

## Sources
- https://arxiv.org/abs/2601.09923
- https://arxiv.org/html/2601.09923v2
- https://openreview.net/forum?id=uD8ZLoi44s
- https://huggingface.co/papers/2601.09923
