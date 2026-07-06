# The Art & Science of Benchmarking Agents
> A framework for what makes agent benchmarks useful, drawn from Snorkel AI's $3 million Open Benchmarks Grant and the 120-plus proposals it has reviewed.

- **Speaker:** Vincent Chen, Snorkel AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=iNkFlCiij0U) (AI Engineer channel; ~23m, released 2026-06-04)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Vincent Chen, research fellow and co-founder at Snorkel AI, opens with an asymmetry his team sees in deployments: agent capabilities are climbing, but the ability to measure agents in high-stakes settings like finance, insurance, and healthcare lags behind. He argues that open benchmarks remain the most important tool for closing that gap because the best ones set goalposts for the field rather than snapshot progress after the fact. Snorkel recently committed $3 million to an Open Benchmarks Grant, and Chen says the program has reviewed over 120 applications from academia and industry labs. The talk distills what that review process taught his team.

Chen splits the framework into science and art. The science covers four axes. First, individual task quality: tasks need well-posed instructions, verifiable solutions, and expert validation. He points to GPQA, whose appendix describes an adversarial multi-reviewer protocol with authors, reviewers, and adjudicators, plus payouts tied to agreement, as the underrated contribution. Second, distributional diversity: define a taxonomy for the domain and distribute tasks intentionally, the way MMLU spread its questions across 57 academic and professional domains, or the way self-driving evaluation weights rare but disproportionately important scenarios like yellow lights and motorcyclists. Third, difficulty and model headroom: a benchmark should stay unsaturated and separate frontier models. Chen cites ARC-AGI 2 staying unsaturated until the reasoning push of the prior 18 to 24 months, and ARC-AGI 3 launching with frontier models under 1 percent while every task remained human solvable. Fourth, robust eval methodology: measure the axes that matter beyond accuracy, including cost, latency, and reasoning traces. His example is tau-bench, where an agent that books the right flight but violates fare class rules still fails.

The art side covers what separates field-shaping benchmarks. They carry a thesis: Terminal-Bench was a bet that the CLI would become the core interface for general purpose agents, a bet Chen argues has largely paid off as labs built enterprise capabilities on coding and CLI tools. They create roadmaps: SWE-bench spawned a family of variants (lite, verified, pro, multilingual, multimodal) and reshaped how the field thinks about coding agents. And they invest in researcher UX, which Chen calls severely underrated: make it simple to run models against the benchmark, contribute tasks, and reuse signals for RL. He credits Stanford CRFM's HELM with pioneering the standardized harness and notes Terminal-Bench 2.0 shipped with Harbor, now a de facto evaluation harness for agent teams.

Chen closes with Snorkel's roadmap for the next wave of benchmarks along three axes: environment complexity (real codebases have org policies, Slack context, flaky toolchains, and parallel contributors that current benchmarks barely capture), autonomy horizon (how long an agent operates before reliability breaks down, including specs and priorities that change midstream), and output complexity (nuanced reward signals for artifacts like strategic recommendations, plus outputs that express uncertainty and ask for more information). The grant is still accepting proposals.

## Notable moments
- [0:04:16](https://www.youtube.com/watch?v=iNkFlCiij0U&t=256s) The $3 million Open Benchmarks Grant and the 120-plus applications reviewed so far.
- [0:06:18](https://www.youtube.com/watch?v=iNkFlCiij0U&t=378s) GPQA's adversarial multi-reviewer quality control and agreement-based payouts.
- [0:13:23](https://www.youtube.com/watch?v=iNkFlCiij0U&t=803s) Terminal-Bench as a correct early bet on the CLI as the core agent interface.
- [0:18:25](https://www.youtube.com/watch?v=iNkFlCiij0U&t=1105s) The three axes for the next wave: environment complexity, autonomy horizon, output complexity.

## Connections
- [Snorkel AI](../../companies/evals-observability/snorkel.md) is the speaker's company and runs the Open Benchmarks Grant described in the talk.
- [Position: coding benchmarks are misaligned with agentic software engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) makes the academic case for the same environment-complexity gap Chen wants benchmarks to close.
- [Session recaps](../../notes/session-recaps.md) records verification discipline and "evals everywhere" as a recurring theme across in-person sessions.
