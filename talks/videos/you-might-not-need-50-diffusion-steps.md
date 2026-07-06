# You Might Not Need 50 Diffusion Steps

> Nvidia's Ziv Ilan surveys three stackable techniques, quantization, caching, and step distillation, for pushing image and video diffusion models toward real-time generation.

- **Speaker:** Ziv Ilan, Nvidia
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=gHs5ZiY80PM) (AI Engineer channel; ~19m, released 2026-06-16)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Ilan works in Nvidia's AI labs team in Paris with frontier model builders, and his premise is that diffusion inference is where LLM inference was a few years ago. Diffusion models typically denoise over 20 to 50 steps, and while the past year brought strong open models (Flux 2 for images, LTX 2 for video, Google's Nano Banana line), the ecosystem lags autoregressive LLMs in speed, maturity, and scalability. The goal he keeps returning to is real-time image and video, which unlocks world models for robotics, games, and streaming content generation. His toolkit borrows LLM concepts and adapts them, ordered from simple to complex.

Quantization comes first. Post-training quantization is the easy path but preserving image and video quality is harder than in LLMs, and because diffusion models are attention-heavy the gains are smaller, though Ilan still calls it low-hanging fruit for exploiting Blackwell-class hardware features like FP4 attention. He describes work with Black Forest Labs on Flux 2 using dynamic quantization, where part of the value range is computed on the fly to match the data distribution rather than fixed statically up front. The payoff is both memory (running on consumer or lower-end data-center GPUs) and speed, and Nvidia publishes pre-quantized checkpoints on Hugging Face plus an open-source example in the TRT LLM visual gen repository.

Caching has no direct KV-cache analog since diffusion does not emit tokens one at a time. TeaCache is his teaching example: it compares consecutive denoising steps and skips recomputation when the change falls below a threshold. More modern variants work chunk-wise, recomputing only the regions of a frame that changed, like the moving speaker against a static audience. He shows expected speedups but warns that careless caching visibly damages quality; the technique ships as a flag in TRT LLM visual gen and in serving stacks like vLLM Omni.

Distillation he saves for last as the most impactful and the most demanding. Unlike LLM distillation, the student keeps the same parameter count; the compression is in steps, from 50 down to 8, 4, or even 1, which is what makes real-time generation reachable at good quality. Two families exist, trajectory-based (student imitates the teacher's denoising path) and distribution-based (student only matches the output distribution), with distribution-based currently stronger and hybrids like the latest FastGen video release combining them for training stability. Distillation is post-training, so it needs data, compute, and skill, but not extreme compute: Hopper-class GPUs suffice, and a GTC demo a few weeks earlier reached near real-time video on a single Blackwell B200. FastGen, from Nvidia research, is the open-source scaffolding for this process, handling sharding and structure as video models grow from 20 to 40 billion parameters toward hundreds of billions. His closing point is that all of it is incremental: start with quantization, add parallelism and caching, and reach for distillation when you need real time.

## Notable moments

- [0:03:07](https://www.youtube.com/watch?v=gHs5ZiY80PM&t=187s) The roadmap: quantization, caching, and distillation as the bridge to real-time generation.
- [0:07:09](https://www.youtube.com/watch?v=gHs5ZiY80PM&t=429s) TeaCache and chunk-based caching: skip recomputing what barely changed between denoising steps.
- [0:09:10](https://www.youtube.com/watch?v=gHs5ZiY80PM&t=550s) Step distillation: same parameter count, 50 steps down to 4, 8, or a single shot.
- [0:14:13](https://www.youtube.com/watch?v=gHs5ZiY80PM&t=853s) GTC result: near real-time video generation on one Blackwell B200.

## Connections

- [Nvidia](../../companies/models-inference/nvidia.md): the speaker's company; TRT LLM visual gen and FastGen are the open-source vehicles for everything in the talk.
- [Google DeepMind](../../companies/models-inference/google-deepmind.md): its Nano Banana image models are among the releases Ilan cites as driving practical diffusion use cases.
