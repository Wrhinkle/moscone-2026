# Task Fidelity Scaling Laws

> Snorkel's empirical case that the quality of agentic RL training tasks, not just their quantity, drives post-training gains, with a 6% versus 1% uplift result.

- **Speaker:** Kobie Crawford, Snorkel AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=YYH0DMQr30A) (AI Engineer channel; ~21m, released 2026-06-02)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Crawford, a developer advocate at Snorkel AI, presents research testing whether the company's long-standing data quality thesis holds for agentic tasks. Snorkel grew out of a Stanford AI lab and has built datasets for foundation model customers since 2019; the question here is whether task quality, in the sense of terminal-bench style containerized coding tasks used for evaluation and RL, measurably changes training outcomes.

The team defines task quality with four criteria: the task is achievable, non-trivial, functionally correct in its logic, and runs in a reliable environment. Snorkel's research harness tests all four, and tasks that pass go into an accepted bucket while the rest are rejected. Those two buckets become the experimental contrast between high-quality and low-quality tasks.

Crawford first checks that the acceptance criteria correlate with meaningful behavioral differences. Running the tasks with Claude Sonnet 4.5 and OpenAI Codex models, accepted tasks averaged twice as many tool calls, showed lower pass rates, and required more output tokens, all signs of genuinely harder multi-step work rather than trivially passable or broken tasks. He then breaks failures into categories to separate meaningful failures, where the model fails to reach a logical conclusion, from degenerate ones where an environmental problem means no model could complete the task. Accepted tasks produce what he calls cleaner failures, overrepresented in logic errors and incomplete tasks, which is exactly the signal a model can hill-climb on.

The headline experiment is an RL training run with the same base model, same compute budget, and same number of tasks in each condition. Training on the rejected, low-quality tasks improved the base model by about 1%. Training on the accepted tasks improved it by about 6%. Crawford calls the 5x difference from quality alone striking, and takes it as empirical validation that expert-in-the-loop data generation, Snorkel's production approach, is worth its cost.

The audience Q&A adds texture. Asked what makes tasks fail acceptance, Crawford says the most common pattern is underspecification: the task definition does not state the testable outcome, but the backend tests expect specific things anyway, or tests carry implicit dependencies the model was never told about. He also notes that in Snorkel's internal comparisons of public benchmarks, including work with the terminal-bench team on terminal-bench 2, tasks that literally cannot be completed become a noise source that masks whether models are actually improving. On less verifiable domains, he points to Snorkel's open benchmark grants program and rubric-based evaluation that combines expert human annotators with LLM judges, with inter-annotator agreement measured both between humans and between judges and humans.

## Notable moments

- [0:05:17](https://www.youtube.com/watch?v=YYH0DMQr30A&t=317s) Accepted tasks average twice the tool calls, lower pass rates, and more output tokens than rejected ones
- [0:09:19](https://www.youtube.com/watch?v=YYH0DMQr30A&t=559s) The RL result: about 1% improvement training on low-quality tasks versus about 6% on high-quality tasks
- [0:14:23](https://www.youtube.com/watch?v=YYH0DMQr30A&t=863s) Q&A on underspecified tasks, mismatched backend tests, and implicit dependencies as the main rejection causes

## Connections

- [Snorkel AI](../../companies/evals-observability/snorkel.md): the speaker's company; this talk is the research backing for its frontier data lab positioning
- [Position: coding benchmarks are misaligned with agentic software engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md): makes the academic version of Crawford's point that benchmark task construction shapes what models learn
- [Reproducible, explainable, and effective evaluations of agents](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md): overlaps with the containerized, reproducible task-environment discipline Snorkel's acceptance criteria encode
