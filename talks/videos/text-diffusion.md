# Text Diffusion

> A DeepMind research scientist explains how diffusion-based text generation works, why it is roughly 10x lower latency than autoregression, and what self-correction and adaptive compute unlock.

- **Speaker:** Brendan O'Donoghue, Google DeepMind
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=r305-aQTaU0) (AI Engineer channel; ~28m, released 2026-06-04)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

O'Donoghue works on the team behind Gemini Diffusion, the research preview released a year before this talk to about 100k users, and he frames text diffusion as the same idea as image diffusion applied to tokens. Training corrupts clean token sequences at many noise levels, discretely, by replacing tokens with random ones, and teaches the network to repair the damage. Inference starts from pure random tokens and iteratively refines an entire block, hundreds or thousands of tokens at once, over a handful of denoising passes instead of one token at a time. At release, Gemini Diffusion matched its autoregressive sibling Gemini 2.0 Flash-Lite across the board, slightly ahead on code, at much better latency, hitting around 2,000 tokens per second including prefill.

The latency argument is a hardware argument. GPUs and TPUs have abundant flops and scarce memory bandwidth, and autoregressive decoding streams the entire set of weights and KV cache across that narrow channel once per token. Diffusion streams everything once per denoising pass, so generating 256 tokens in 24 passes does roughly ten times fewer memory transfers, and if you are truly memory bound that is roughly a 10x speedup. The trade-off is throughput: multiple forward passes over the same data hit the compute ceiling earlier, so large-batch serving costs more, which O'Donoghue says is the real reason no big model has landed text diffusion yet. The trade favors on-device settings, phones and robots, where nothing is batched anyway, and he notes the model is already in a couple of on-device applications inside Alphabet.

The less discussed advantages get the most time. Bidirectional attention lets the model see tokens it has not settled yet, which enables self-correction: on an arithmetic prompt from Google IO, the model guesses "answer = 60" after one forward pass, revises to 49 after two, completes the reasoning by pass three, and rewrites its own earlier answer to the correct 39. The much larger GPT-4o and Gemini 2.5 Flash both flubbed the same prompt, and Flash stuck with its wrong 42 to the end, folding the error into its reasoning. Quality also climbs roughly monotonically with denoising budget across DeepMind's six internal coding evals. Adaptive computation lets the model decide when it is done: the first 100 digits of pi take 4 passes, FizzBuzz takes 18, a quantum mechanics paragraph takes 31, and harder evals like GPQA Diamond consume more steps than MBPP without anyone scheduling it. In-place editing works like image inpainting, fixing a bug or inserting a middle paragraph directly rather than regenerating token by token.

The demos lean on latency: a fake Wikipedia whose HTML and text generate on the fly per click, a fabricated Reddit with an image model filling in pictures, an entire operating system hallucinated screen by screen, and a Twitter user's voice-driven to-do app built in what he narrates as 15 seconds of work. In Q&A, O'Donoghue confirms training uses the same data as autoregressive models, that bigger diffusion models need fewer passes for the same output, and that long outputs generate block-wise autoregressively. He closes by teasing a next-generation release.

## Notable moments

- [0:07:12](https://www.youtube.com/watch?v=r305-aQTaU0&t=432s) The memory-bandwidth argument: 24 passes for 256 tokens means 10x fewer memory transfers than autoregressive decoding.
- [0:09:13](https://www.youtube.com/watch?v=r305-aQTaU0&t=553s) Self-correction live: the model's answer token goes 60, then 49, then 39 as the reasoning fills in behind it.
- [0:12:14](https://www.youtube.com/watch?v=r305-aQTaU0&t=734s) Adaptive computation: 100 digits of pi in 4 denoising steps, FizzBuzz in 18, quantum mechanics in 31.
- [0:16:16](https://www.youtube.com/watch?v=r305-aQTaU0&t=976s) The on-the-fly demos: generated Wikipedia, generated Reddit, and a whole operating system rendered click by click.

## Connections

- [Google DeepMind](../../companies/models-inference/google-deepmind.md) is the speaker's lab and home of the Gemini Diffusion research preview the talk is built on.
- [Session recaps](../../notes/session-recaps.md) cover an in-person Google DeepMind session on what comes after code, a companion view of the same lab's forward-looking research.
