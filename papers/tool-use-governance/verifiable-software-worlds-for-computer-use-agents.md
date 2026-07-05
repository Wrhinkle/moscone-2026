# OpenComputer: Verifiable Software Worlds for Computer-Use Agents

- **Status:** Located — [arXiv:2605.19769](https://arxiv.org/abs/2605.19769)
- **Area:** tool-use-governance
- **Authors / venue / date:** Jinbiao Wei, Qianran Ma, Yilun Zhao, Xiao Zhou, Kangqi Ni, Guo Gan, Arman Cohan — arXiv (cs.AI, cs.SE), submitted May 19, 2026

## Problem
Computer-use agent benchmarks mostly grade outcomes with screenshots plus LLM-as-judge, which misjudges tasks whose success lives in fine-grained application state (a setting toggled, a file actually saved in the right format). That makes scores unreliable as evidence and useless as reward signals for training. The paper asks: can real desktop software be wrapped in programmatic, auditable verification instead?

## Approach
OpenComputer builds "verifiable software worlds" from four parts: (1) app-specific state verifiers — structured inspection endpoints over 33 real desktop applications (avg 17.7 endpoints/app); (2) a self-evolving verification layer that runs ~15 calibration tasks per app with frontier agents, diffs programmatic verdicts against criterion-level LLM judgments, and repairs verifier code within a bounded budget; (3) a task-generation pipeline (propose from user goals → filter for multi-step workflows → ground in verifier endpoints → materialize files/configs), yielding 1,000 finalized tasks (avg 6.9 checks each); (4) an evaluation harness recording full trajectories with auditable partial-credit rewards.

## Key findings
- Hard-coded verifiers agree with human adjudication at **94.2%** task-level vs **79.2%** for LLM-as-judge (checklist-level: 97.3% vs 92.2%).
- Self-evolution repaired 68 of 76 checker-side errors (**89.4%** repair rate; 47 fixed in round 1), lifting human–verifier agreement from 85.2% to **94.1%** (+8.9 pts).
- Frontier agents still fail end-to-end: GPT-5.4 leads at **68.3%** full success (88.4% avg partial-credit reward); Claude-Sonnet-4.6 **64.4%**; Kimi-K2.6 **58.8%**.
- Open-source computer-use models crater vs their OSWorld-Verified scores: Qwen-3.5-27B 32.3% (from 56.2%), GUI-OWL-1.5-8B 5.7% (from 52.3%), EvoCUA-8B 10.9% (from 46.1%) — suggesting benchmark-specific overfitting (inference: the paper frames this as a robustness gap).

## Limitations & open questions
Authors concede not every desktop task reduces to programmatic checks — visually/geometrically judged tasks (e.g., Draw.io layout) were excluded (17 tasks) pending hybrid executable+visual verification. A skeptic would ask: how much per-app engineering does 17.7 endpoints/app cost to extend to new software, do verifier endpoints leak hints into task design despite the unconditioned proposal stage, and does the calibration loop inherit LLM-judge blind spots it's calibrated against?

## Why builders should care
If you're shipping computer-use automation, don't trust screenshot + LLM-judge evals — a ~15-point human-agreement gap means your pass rates are partly fiction. Invest in state-based checks (APIs, files, DB rows) for your own workflows; partial-credit, trajectory-level rewards also make these environments directly usable for RL/training data. And treat open-source CUA models' benchmark numbers with suspicion until tested on your apps.

## Related companies in this landscape
- **Browserbase** — hosted browser infra for agents; validates the need for instrumented, inspectable environments rather than raw pixels.
- **Cua** — computer-use agent infrastructure; this benchmark is exactly the evaluation substrate its stack needs.
- **E2B / Daytona / Docker** — sandboxed execution environments; OpenComputer's materialized app worlds are a blueprint for verifiable sandboxes.
- **Braintrust / Arize / Hamming AI** — eval platforms leaning on LLM-as-judge; the 79.2% vs 94.2% result challenges judge-only scoring and argues for programmatic checkers.
- **Meticulous** — deterministic state-based testing of UIs; the paper's verifier-over-judge finding validates that approach for agent grading.
- **OpenAI / Amazon AGI Labs / Google DeepMind** — frontier CUA builders; even the best model tops out at 68.3% end-to-end, so the category is not solved.

## Sources
- https://arxiv.org/abs/2605.19769
- https://arxiv.org/html/2605.19769
