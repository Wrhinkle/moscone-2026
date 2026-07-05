# SlopCodeBench: Benchmarking How Coding Agents Degrade Over Long-Horizon Iterative Tasks

- **Status:** Located — [arXiv:2603.24755](https://arxiv.org/abs/2603.24755) (v2, revised 2026-05-07)
- **Area:** swe-agents
- **Authors / venue / date:** Gabriel Orlanski, Devjeet Roy, Alexander Yun, Changho Shin, Alex Gu, Albert Ge, Dyah Adila, Nicholas Roberts, Frederic Sala, Aws Albarghouthi. arXiv cs.SE, submitted 2026-03-25. Code: [SprocketLab/slop-code-bench](https://github.com/SprocketLab/slop-code-bench).

## Problem
Single-shot coding benchmarks (SWE-bench style) hide design debt: an agent can pass the test suite while producing code that is progressively harder to extend. Prior iterative benchmarks constrain the agent's design space so tightly that you can't measure how its own architectural decisions shape future turns. Nobody had quantified whether agent-written code actually rots as the agent keeps building on it.

## Approach
A benchmark of 36 author-written problems with 196 checkpoints. At each checkpoint the spec evolves and the agent must extend *its own prior solution*; specs demand architectural decisions but deliberately leave internal structure to the agent. Scoring is via CLI/API-level tests per checkpoint. Two degradation metrics: **structural erosion** (complexity concentrating in hotspots) and **verbosity** (redundant code), compared against a baseline of 473 open-source Python repos across their git histories. 15 coding agents evaluated across six providers (Claude Opus 4.5–4.7 / Sonnet 4.6, GPT 5.2–5.5 variants, Zhipu, Kimi, Cursor, MiniMax).

## Key findings
- No agent solves any problem end-to-end; the best agent passes only 14.8% of the 196 checkpoints.
- Structural erosion rises in 77% of trajectories; verbosity rises in 75.5%.
- Versus the 473 human OSS repos: agent code is 2.3x more verbose and 2.0x more eroded, and it accumulates verbosity 6.6x faster and erosion 5.0x faster than human git histories do.
- Mean cost per checkpoint grows 2.2x from first to last checkpoint, while the share of code actually modified drops from 97.4% to 29.5% — agents pay more to change less as their own mess compounds.
- Explicit quality-guidance prompting cuts *initial* erosion by up to 62.3% (verbosity/erosion down by up to a third) and raises cost per checkpoint 12.1% — but does **not** change the degradation rate. Prompting shifts the starting point, not the slope.

## Limitations & open questions
Authors concede: only Python implementations evaluated despite language-agnostic design, and problems are manually authored rather than mined from real repos, so real-world evolutionary pressure may differ. A skeptic would ask whether the erosion/verbosity metrics track what actually blocks future extension (the checkpoint-failure correlation is the evidence, but it's indirect), and whether newer agent harnesses with refactoring passes or repo-level memory would bend the slope.

## Why builders should care
If your agent iterates on its own output — long-lived feature work, not one-shot patches — expect compounding quality decay that system prompts alone won't fix. Budget for periodic externally-triggered refactoring/review passes and quality gates in the loop, and treat rising cost-per-iteration with shrinking diff size as a measurable early-warning signal of slop accumulation.

## Related companies in this landscape
- **Sonar** — this is the paper's thesis as a product: static quality gates catching "slop" before it compounds in agentic loops.
- **Qodo** — agentic code review/quality; the finding that prompting alone doesn't stop degradation argues for its dedicated-reviewer approach.
- **Greptile / Baz** — AI code review agents; validated as a necessary counterpart to generation agents on long horizons.
- **Cognition / Factory / OpenHands / Cline** — long-horizon coding agent vendors this benchmark directly stress-tests; end-to-end solve rate of zero challenges "lights-off software factory" claims.
- **Sourcegraph** — repo-wide context and structure awareness is one plausible lever against the path-dependence failures measured here.
- **Braintrust / Arize** — eval platforms; the cost-up/diff-down trajectory signature is exactly the kind of production metric worth tracking.

## Sources
- https://arxiv.org/abs/2603.24755
- https://arxiv.org/html/2603.24755v2
- https://github.com/SprocketLab/slop-code-bench
