# How We Built Zeta2: Training an Edit Prediction Model in Production

> Zed's edit predictions lead compresses the full Zeta2 training pipeline into ten minutes: distillation from frontier teachers, a repair step, settled-state filtering, and live traffic experiments.

- **Speaker:** Ben Kunkle, Zed
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=phchDt63qAA) (AI Engineer channel; ~11m, released 2026-05-30)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Kunkle leads edit predictions at Zed, and Zeta2 is the small specialized model behind the feature: given a region of code around the cursor plus recent edits, cursor position, nearby type and variable definitions, and diagnostics, predict the user's next edit. It runs on every keystroke, so it has to be fast, which makes a small fine-tuned model doing exactly one task the right shape.

The training pipeline starts from opt-in production data, captured as snapshots so all the surrounding context (related types, definitions, diagnostics) comes along. Zed distills from a frontier model: feed the teacher the same inputs and ask what edit it would predict. Kunkle notes this is harder than it sounds, since asking a frontier model 100,000 times gets you 100,001 answers, so the teacher prompt is finely tuned. Static offline heuristics catch bad teacher predictions, such as undoing what the user just typed or ignoring the editable region boundary, and failures go to a repair step where another frontier model is told how the prediction failed and asked to fix it. Everything up to that point is cached and reused across experiments. Experiment-specific prompt formatting then decides what the student sees, for example whether diagnostics are included and how much edit history, before training and a final round of offline evals. The whole pipeline is JSONL, one giant JSON object per line, with each stage adding or moving fields. Peak training runs use about 100,000 examples; smaller experiments use 10,000 to 50,000.

The most interesting section covers settled data. Because Zed is the editor, the team can wait until the user stops editing the editable region (a 10-second pause serves as the heuristic), snapshot it, and treat that as what the user actually wanted. It is noisy, since the user may change their mind or an agent may rewrite the region entirely. The filter: generate many predictions from the same input and check whether any come close to the settled state using a Levenshtein-style distance. Doing that with 10 teacher predictions per example means a million frontier model requests per 100,000 examples, which is prohibitively expensive, but the student checkpoints now approach teacher quality, so Zed runs the student 50 times instead at essentially no cost. The distance distribution then sorts examples into three bands: far means noise, very close means trivially predictable, and the middle band is the ideal training data, including code past the student's training cutoff, like new functions the model has never seen. They train on the closest prediction rather than the settled state itself, which stays noisy. Offline evals run on a held-out set against three distinct teacher predictions (many edits have no single right answer), tracking an n-gram edit distance metric, a reversal ratio for predictions that undo the user's typing, and diagnostic error counts before versus after the prediction. Experiments then ship behind a live traffic page, with a new checkpoint sampled at 15 percent of production traffic and dashboards for acceptance rate and latency; the checkpoint shown at 15 percent, built on a Seed-Coder base, is what shipped as Zeta2.

## Notable moments

- [0:01:07](https://www.youtube.com/watch?v=phchDt63qAA&t=67s) The distillation problem: ask a frontier model 100,000 times and you get 100,001 answers, hence the tuned teacher prompt and repair step.
- [0:04:11](https://www.youtube.com/watch?v=phchDt63qAA&t=251s) Settled data: because Zed is the editor, it can wait for the user to stop editing and snapshot the code they actually wrote.
- [0:05:11](https://www.youtube.com/watch?v=phchDt63qAA&t=311s) Swapping the teacher for the student in settled-state filtering, turning a million frontier calls into essentially free checkpoint inference.
- [0:07:13](https://www.youtube.com/watch?v=phchDt63qAA&t=433s) The offline eval suite: held-out data, three teacher references per example, reversal ratio, and production kept rate.

## Connections

- [Zed](../../companies/swe-infrastructure/zed.md) is the speaker's company; Zeta2 is the edit prediction model shipped in the editor.
- [Sourcegraph](../../companies/coding-agents/sourcegraph.md) ships competing in-editor code assistance, the market where keystroke-level prediction quality gets compared.
