# Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering

- **Status:** Located — [arXiv:2604.01437](https://arxiv.org/abs/2604.01437)
- **Area:** swe-agents
- **Authors / venue / date:** Jingyue Li, André Storhaug (NTNU, Trondheim). ResponsibleSE 2026 workshop, FSE Companion '26 (Montreal, July 5–9, 2026). Submitted to arXiv April 1, 2026. DOI 10.1145/3803437.3805548.

## Problem
SE-agent papers are exploding (7 papers with "agent" in the title at ICSE 2025 → 301 accepted at ICSE 2026), but the evaluations backing their claims are hard to reproduce and harder to explain: LLM backends are black boxes with random outputs, and papers routinely omit the parameters (model version, temperature, prompts) that determine results. Rerunning baselines against commercial APIs is also expensive, which quietly discourages honest comparison.

## Approach
A position paper built on an analysis of 18 agentic-SE papers from ICSE 2025/2026, FSE 2025, ISSTA 2025, and ASE 2025 (selected by "agent" in title + preprint availability as of Jan 12, 2026). The authors catalog evaluation designs, baselines, and reproducibility practices, then propose: (1) mandatory reporting of prompts, temperature, and exact LLM versions; (2) open publication of agents' Thought-Action-Result (TAR) trajectories — or LLM-generated summaries of them — so approaches can be compared qualitatively without rerunning baselines. A proof-of-concept uses Kimi K2.5 to run three-step summarization (summarize each run → compare agents per run → aggregate patterns) over public TAR trajectories from their Favia CVE-fix-detection agent.

## Key findings
- Only 1 of 18 papers compared against a state-of-the-art agentic baseline; most compared against classical tools, deep learning, or naive-prompt LLMs.
- All 18 disclosed which LLMs were used, but only 3 gave precise version identifiers (e.g., GPT-3.5-0125); only 3 reported temperature settings; only 2 ran temperature-sensitivity analyses; only 2 repeated runs and averaged.
- 13 of 18 ran ablation studies; 11 of 18 used multi-agent architectures; 4 papers included cost/token analyses.
- Case study: on 10 runs where a Qwen3-235B agent failed CVE-fix detection, Llama-3.3-70B and Gemma-3-27B agents succeeded on several of the same runs; automated trajectory analysis attributed Llama's edge to "stricter adherence to verification protocols" (check dates/versions/files first) and flagged "pattern matching without validation" as the dominant failure mode across models.

## Limitations & open questions
Authors concede the 18-paper sample is non-exhaustive (title-keyword selection), TAR trajectories can be huge (hence summaries-only sharing), LLM-summarized trajectories can be deceptive or biased (mitigation: cross-validate with multiple analyzer models), and trajectory comparisons mislead when agents run on different benchmark datasets. Skeptics should ask whether an LLM judging LLM traces is itself reproducible, and whether summarized traces survive adversarial cherry-picking.

## Why builders should care
If you ship or buy a coding agent, demand versioned-model + temperature + prompt disclosure in any eval claim — this paper shows most peer-reviewed work fails even that bar. Logging full thought-action-result trajectories is nearly free (they're execution logs) and turns "our agent scored X" into a debuggable, comparable artifact; the case-study finding that verification discipline beats raw model size is directly actionable in agent prompt design.

## Related companies in this landscape
- **Arize / Fiddler / Comet / Weights & Biases (CoreWeave)** — the paper's TAR-trajectory publication is exactly what agent tracing and eval-observability platforms productize; it validates their category.
- **Braintrust / Hamming AI / Snorkel** — LLM-as-judge trajectory summarization is their core eval workflow; the paper's bias caveats are their open problem.
- **Datadog / Sentry / Dynatrace / Lightrun** — agent execution logs as first-class telemetry maps to their agent-monitoring pushes.
- **LangChain / LlamaIndex** — trajectory capture (LangSmith-style) is the artifact format this paper wants standardized.
- **Qodo / Sourcegraph / Factory / Cognition / OpenHands / Greptile / Cleric** — SWE-agent vendors whose benchmark claims this paper challenges: almost nobody compares against agentic SOTA baselines reproducibly.

## Sources
- https://arxiv.org/abs/2604.01437 (abstract page)
- https://arxiv.org/pdf/2604.01437 (full text, read in full)
- Replication package cited by the paper: https://github.com/andstor/agentic-ai-eval-replication-package
- TAR trajectory dataset used in the case study: https://huggingface.co/datasets/andstor/favia_trajectories
