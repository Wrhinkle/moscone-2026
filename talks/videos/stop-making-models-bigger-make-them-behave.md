# Stop Making Models Bigger, Make Them Behave

> Kobie Crawford shows how Snorkel and UC Berkeley's rLLM team used RL on expert-built data to make a 4B model beat a 235B model at financial tool use for under $500 a run.

- **Speaker:** Kobie Crawford, Snorkel
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=TNwJ1LMiENk) (AI Engineer channel; ~21m, released 2026-06-10)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Crawford, a developer advocate at Snorkel, presents joint research with the rLLM group at UC Berkeley (the Agentica project) with a single headline objective: make a 4 billion parameter model outperform a 235 billion parameter model on a tool-use task for financial analysis. The talk challenges the default enterprise move of dropping in a bigger model when performance disappoints. Crawford relays the Berkeley team's name for the fallacy, the Terence Tao effect: a financial analyst does not need across-the-board mathematical brilliance to run a SQL query and do some addition, so paying for frontier-scale reasoning to fix a narrow behavioral failure is a sledgehammer cracking a walnut.

The motivating example is damning for the big model. Asked for the year-over-year growth of YouTube ads revenue from 2023 to 2024 inside their FinQA environment, the 235B Qwen3 reasoning model queried a table that did not exist, guessed a second nonexistent table, then hallucinated an answer, never once calling the available get-table-names tool to inspect its environment. Crawford's diagnosis: the failure was not reasoning capacity but tool discipline.

The method follows Snorkel's standard recipe of experts in the loop. PhD-level and industry financial analysts helped build the dataset, followed by a verification pass to confirm each task is queryable and has a verifiable answer. Training used GRPO on the 4B model inside a self-contained FinQA environment built on the rLLM framework, with no external dependencies, so it deploys on premise. The environment is published on PrimeIntellect's infrastructure, in the OpenEnv GitHub repo, and in Hugging Face spaces. The whole training run took about 21 hours and cost under $500, which Crawford frames as a call to action: getting a self-hosted small model to required performance with RL is tractable, "even if Karpathy doesn't like it."

Results: the fine-tuned 4B model beat the 235B model, roughly doubling pass@1. Revisiting the YouTube ads question, the trained model first calls get-table-names to discover tables, inspects the schema with get-table-info, hits an error asking for a nonexistent revenue column, and self-corrects to the right column before producing the correct answer. Two findings surprised the team. First, training on single-table questions only beat both mixed training and curriculum learning that ramped from single-table to multi-table. Second, that single-table-only training still doubled performance on the harder FinQA-reasoning benchmark of 79 multi-table questions, from 13.9 to 26.6 percent, alongside the main 290-sample set. Fixing the core failure mode, tool discipline, generalized to harder questions.

Crawford closes with the methodological takeaway: find the specific behavior that is failing before buying scale. Snorkel's research team increasingly uses rubrics in evals, breaking a response's rightness into many answerable questions, to locate which behavior needs targeted data. The rubric guides dataset decisions while GRPO still consumes its single reward value. A blog post and a partner post from the Berkeley Agentica team carry the details.

## Notable moments

- [0:07:08](https://www.youtube.com/watch?v=TNwJ1LMiENk&t=428s) The 235B model queries two nonexistent tables and hallucinates a YouTube ads revenue answer.
- [0:11:12](https://www.youtube.com/watch?v=TNwJ1LMiENk&t=672s) The cost reveal: a 21-hour GRPO run at under $500 total.
- [0:14:13](https://www.youtube.com/watch?v=TNwJ1LMiENk&t=853s) The trained 4B model discovers tables, inspects schemas, and self-corrects a bad column name.
- [0:16:13](https://www.youtube.com/watch?v=TNwJ1LMiENk&t=973s) Single-table-only training beats curriculum learning and doubles the multi-table benchmark from 13.9 to 26.6 percent.

## Connections

- [Snorkel](../../companies/evals-observability/snorkel.md), the speaker's company and source of the expert-in-the-loop dataset.
- [UC Berkeley](../../companies/vc-community/uc-berkeley.md), home of the rLLM/Agentica group that co-ran the study and built the training framework.
- [Prime Intellect](../../companies/models-inference/prime-intellect.md), one of the platforms hosting the published FinQA RL environment.
