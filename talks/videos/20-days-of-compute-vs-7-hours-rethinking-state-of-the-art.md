# 20 days of compute vs 7 hours: rethinking what state-of-the-art means

> An argument that "state of the art" is plural: leaderboards and internal benchmarks mislead unless you evaluate per use case, at scale, and with efficiency on the axis next to quality.

- **Speaker:** Bertrand Charpentier, Pruna
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=hqHC6Z_lXyo) (AI Engineer channel; ~20m, released 2026-06-01)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Charpentier opens with the question every team asks before shipping: which model is state of the art? The two common answers, check a public leaderboard or run an internal evaluation, both tend to collapse into the same lazy default of picking a large foundation model. The talk works through why each method breaks and what to do instead, using image editing models as the running example.

The leaderboard critique comes in four parts. First, rankings disagree across boards: LMArena, Design Arena, and Artificial Analysis rank the same image editing models differently, one model sits at rank 10 on Artificial Analysis and rank 5 on Arena, and some models appear on one board but not another. Elo ranges also differ board to board, so relative strength is hard to read. Second, aggregate scores hide task-level variance. When Charpentier breaks the rankings out by use case, removing objects, changing backgrounds, editing text, ChatGPT image is never top of any per-task board even when it tops the aggregate. No model consistently outperforms the others. Third, leaderboards are statistically thin for any one use case: a few thousand samples per board, while some of Pruna's served models handle millions of requests per day, so production traffic carries more signal than the board does. Fourth, win rates show no model near 100 percent; most models lose at least 40 percent of their battles, and your use case may live in that 40 percent.

Internal evaluation gets the same treatment. Charpentier runs a live experiment, showing the room two sets of three generated images and asking for preferences by show of hands. The audience splits both times, and some people switch preferred models between prompts, which is his point: manual inspection is doubly biased, by your own taste and by the handful of samples you happen to look at. Automated metrics have their own failure mode. CLIP score rankings of eight models flip across datasets and the score differences between models are tiny, while a task-specific metric like text rendering produces stable rankings with clear gaps. His rule: understand what a metric measures and use several.

The title comes from the compute cost of evaluation itself. Reproducing a leaderboard's roughly 26,000 battles with ChatGPT image at about 62 seconds per generation takes 20 days of compute, around 5,000 dollars, and roughly 556 kWh, which Charpentier translates into the energy of running 400 marathons. A Pruna-optimized model generating in under one second does the same evaluation in 7 hours for 265 dollars, or four marathons.

His preferred answer to the state-of-the-art question is a Pareto plot: an efficiency metric on the x-axis (latency or price per image), quality on the y-axis, and a front of three or four models rather than a single winner. Quality scores on the front vary little, roughly 1,100 to 1,200 Elo, while latency varies by around 20x. Drawing the front against a task-specific quality metric, he shows Flux models Pruna optimized with Black Forest Labs staying on the text-rendering front while running much faster. In the Q&A he sketches the compression toolbox behind those models: per-module quantization, pruning, and cutting diffusion denoising steps from 20 to 50 down to as few as four via distillation or caching, with open source algorithms in Pruna's package.

## Notable moments

- [0:08:20](https://www.youtube.com/watch?v=hqHC6Z_lXyo&t=500s) The audience preference game begins; the room splits over three images and some people switch models on the second prompt.
- [0:12:21](https://www.youtube.com/watch?v=hqHC6Z_lXyo&t=741s) The cost accounting: 26K evaluation battles equals 20 days of compute, 5K dollars, and 400 marathons of energy versus 7 hours and 265 dollars with a fast model.
- [0:14:21](https://www.youtube.com/watch?v=hqHC6Z_lXyo&t=861s) The Pareto front answer: three or four state-of-the-art models, similar Elo, up to 20x apart on latency.

## Connections

- [Baseten](../../companies/models-inference/baseten.md) sells the same premise commercially, that inference speed and cost are the competitive axis once quality converges.
- [Fireworks](../../companies/models-inference/fireworks.md) competes in fast image and multimodal model serving, the market Pruna's compressed endpoints target.
