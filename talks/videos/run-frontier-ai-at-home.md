# Run Frontier AI at Home

> EXO Labs' Alex Cheema argues local inference is on a 100x price-performance curve and demos a trillion-parameter model split across four Mac Studios plus a DGX Spark.

- **Speaker:** Alex Cheema, EXO Labs
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ESbWpPT_9-o) (AI Engineer channel; ~105m, released 2026-05-26)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Cheema runs EXO Labs, a lab working across models, software, and hardware to drive down the cost of running frontier AI locally. His opening case is part principle, part practicality. He quotes Karpathy's line "not your weights, not your brain," and tells the story of a friend doing legitimate penetration testing who got locked out of three API providers at once. Against that he sets a technical thesis: the current stack was built for training, which is compute bound, while local inference is dominated by the memory-bound decode phase. What matters for decode is fitting the model in memory, memory bandwidth, and energy per byte. Phones fail on the energy test today: 10 to 15 watts of inference against a 10 to 15 watt-hour battery is about an hour of use, and 18 months ago his benchmark phone got too hot to hold.

Cheema argues the stack is full of unclaimed gains. Profiling Qwen 3.5 on Apple silicon, EXO found real throughput 50 percent below theoretical because of unnecessary kernel launches, and recovered 30 percent by fusing kernels. He cites Stanford Hazy Research's intelligence-per-watt metric, up about 5x in two years from hardware with another 3x from models, and he prefers intelligence per joule since what counts is energy per task. Today running the frontier open model, the 1-trillion-parameter GLM 5.1 at roughly 1.5 TB in FP16, takes about $40,000 of Mac Studios and yields maybe 20 tokens per second. Compounding gains across kernels, harnesses, models, and hardware, he claims a 100x price-performance improvement remains, and predicts a $5,000 box with close-to-frontier performance within 18 months to 2 years.

The demo shows the current state. Four Mac Studios connected by Thunderbolt 5 run a 4-bit GLM 5.1 (about 400 GB) under EXO, an app that auto-discovers devices in a mesh network and picks a distribution strategy. The enabling work is RDMA over Thunderbolt: inter-Mac latency dropped from about 300 microseconds to single digits, roughly 100x, which matters because tensor parallelism on a 60-layer model needs 120 synchronizations per token. A second demo pairs a $4,000 DGX Spark with a MacBook, exploiting a 12x difference in compute-to-bandwidth ratios: the Spark (about 4x the compute) runs prefill and streams the KV cache over 10 gigabit Ethernet to the MacBook (546 vs 273 GB/s memory bandwidth), which decodes. On a large paper-summarization prompt the split cuts end-to-end time from about 7 seconds to 4.8, and the win grows with prompt size since prefill scales quadratically.

Cheema also rebuts the claim that cloud batching permanently dooms local unit economics. Multi-agent systems mean a single user already runs at batch size 8, test-time search lets small models match larger ones by spending inference compute, and continual learning via test-time training would give every user distinct weights, which breaks cloud batching entirely. He closes skeptical of local-AI hype: one-bit quantized "Kimi on a MacBook" demos are worse than smaller unquantized models, and auto-research without the scientific method is a slot machine. EXO plans a public benchmark site within a month showing Pareto frontiers of quality versus speed for local setups at a given budget.

## Notable moments

- [0:08:17](https://www.youtube.com/watch?v=ESbWpPT_9-o&t=497s) Kernel fusion on Qwen 3.5 recovers 30 percent of inference performance on Apple silicon.
- [0:21:24](https://www.youtube.com/watch?v=ESbWpPT_9-o&t=1284s) The core thesis: $40,000 to run GLM 5.1 today, a 100x price-performance gain still available, $5,000 near-frontier boxes within about 2 years.
- [1:09:48](https://www.youtube.com/watch?v=ESbWpPT_9-o&t=4188s) RDMA over Thunderbolt 5 cuts inter-Mac latency about 100x, making tensor parallelism viable across four Mac Studios.
- [1:41:11](https://www.youtube.com/watch?v=ESbWpPT_9-o&t=6071s) Heterogeneous split demo: DGX Spark prefill plus MacBook decode runs a large prompt about 2x faster than the MacBook alone.

## Connections

- [Nvidia](../../companies/models-inference/nvidia.md): the DGX Spark in the demo is Nvidia hardware, and Cheema cites Nvidia's data-center co-design moves as the pattern local inference will follow.
- [Z.ai](../../companies/models-inference/zai.md): GLM 5.1, the trillion-parameter model Cheema calls the open-source frontier and runs in the demo, is Z.ai's release.
- [Session recaps](../../notes/session-recaps.md): overlaps the in-person local-agents thread, including the New York Times session on running local models.
