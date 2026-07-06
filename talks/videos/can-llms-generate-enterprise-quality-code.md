# Can LLMs generate Enterprise Quality Code?

> Sonar ran 4,444 Java assignments through 53+ models and reports that pass rates above 80 percent coexist with hundreds of bugs and security issues per million lines of generated code.

- **Speaker:** Prasenjit Sarkar, Sonar
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=NuePCNMpWGc) (AI Engineer channel; ~15m, released 2026-05-31)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Sarkar opens with the shift from IDE-centric coding to agentic platforms like Codex, Claude, Devin, and Gemini CLI, citing a March 2026 Pragmatic Engineer survey finding 55 percent of developers now use AI agents regularly. His question is whether the generated code is maintainable, secure, and readable. Vendor benchmarks like HumanEval, MBPP, and SWE-bench measure functional correctness on test cases, where leading models score 80-plus percent, but Sarkar argues they miss security, reliability, maintainability, tech debt, and architectural discipline. Sonar built an evaluation framework that runs 4,444 distinct open source Java programming assignments through each model and analyzes the output with SonarQube Enterprise, publishing everything at sonar.com/leaderboard with 53-plus model versions evaluated so far.

The numbers make the argument. Gemini 3.1 Pro High leads on functional pass rate at 84.17 percent, generating about 307,000 lines of code for the assignment set, with 614 bugs and 210 security issues per million lines of code. Claude Sonnet 4.6 shows the highest security risk in the sample he presents, around 300 security issues per million lines, across roughly 627,000 generated lines. GPT 5.4 and GPT 5.4 Pro High generate about 1.2 million lines of code for the same 4,444 assignments, and GPT 5.2 High about a million, against under 250,000 lines for the older GPT-4.0, so verbosity is trending sharply upward along with cyclomatic and cognitive complexity (the latter a Sonar measure of how hard code is for a human to read and maintain). Sarkar's more subtle finding is that as models mature, total bug and vulnerability counts fall, but the issues that remain are finer-grained and harder for a human reviewer to catch. His causal story: training sets mix quality levels and contain insecure examples and subtle logic errors that models absorb, and LLMs are probabilistic, limited in context about your codebase and architecture, and hard to diagnose.

The prescription is Sonar's agent-centric development cycle, ACDC, with three phases. Guide includes Sonar context augmentation, which pushes codebase context into the LLM, and Sonar Sweep (private beta), which treats the data used to train or tune a model on the theory that problematic training data produces problematic code. Verify is SonarQube, including a new agentic analysis in open beta: an MCP-connected check that analyzes code in 1 to 5 seconds before commit, versus 1 to 5 minutes for CI, feeding issues back to the coding agent to fix before the PR exists. Solve is the remediation agent (open beta), which fixes quality-gate failures in a PR or lets teams select tech debt issues from the SonarQube dashboard and assign them to an agent, one PR per issue, for developer review. The remediation agent re-runs analysis and compilation on its own fixes and discards any that would introduce a regression. Sonar supports 40-plus languages and frameworks across the major DevOps platforms and IDEs.

## Notable moments

- [0:02:09](https://www.youtube.com/watch?v=NuePCNMpWGc&t=129s) What pass-rate benchmarks miss: security, reliability, maintainability, and tech debt, and the 4,444-assignment framework built to measure them.
- [0:04:10](https://www.youtube.com/watch?v=NuePCNMpWGc&t=250s) The density numbers: 614 bugs and 210 security issues per million lines for the pass-rate leader, 300 security issues per million for Claude Sonnet 4.6.
- [0:09:15](https://www.youtube.com/watch?v=NuePCNMpWGc&t=555s) The maturity paradox: newer models produce fewer but finer bugs that are harder for humans to detect, while line counts head north.
- [0:10:16](https://www.youtube.com/watch?v=NuePCNMpWGc&t=616s) The ACDC framework: guide, verify, solve, including 1-to-5-second pre-commit agentic analysis.

## Connections

- [Sonar](../../companies/swe-infrastructure/sonar.md) is the speaker's company and the vendor behind SonarQube, the leaderboard, and the ACDC products.
- [Session recaps](../../notes/session-recaps.md) covers Sonar's in-person ACDC session, which adds the zero-trust verification framing and memory-injection ideas this talk skips.
- [Greptile](../../companies/coding-agents/greptile.md) attacks the same trust gap from the review side, with AI code review instead of static analysis.
- [SlopCodeBench](../../papers/swe-agents/slopcodebench-benchmarking-how-coding-agents-degrade-over-l.md) benchmarks the long-horizon quality degradation that Sonar's per-million-lines metrics quantify per model.
