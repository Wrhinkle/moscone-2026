# Road to 5 Million Tokens: Breaking Barriers in Long Context Training

> Max Ryabinin stacks memory optimizations, from FSDP through a chunked rework of Ulysses context parallelism, until 5 million token training sequences fit on ordinary GPU nodes.

- **Speaker:** Max Ryabinin, Together AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=TUnPNY4E2fw) (AI Engineer channel; ~16m, released 2026-06-08)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Ryabinin, VP of research and development at Together AI, presents the company's research on training transformers at extreme sequence lengths. The demand comes from two directions: agents that want to stuff as many tokens as possible into context and actually use them, and video generation, where multiple frames per second consume tokens quickly and temporal consistency requires the model to see minutes into the past. Even teams far below millions of tokens, he adds, benefit from knowing where training memory goes, since freed memory can be reinvested in speed.

Two bottlenecks block naive context extension: quadratic attention computation from pairwise token interactions, and the more insidious linear growth of activation memory. The talk's core is a worked example: fitting a 3 million token training sequence for a Llama-architecture model onto a single 8x H100 node. Model parameters alone overflow one GPU, so step one is fully sharded data parallelism to chunk parameters across the eight GPUs. Attention activations still blow the budget, so step two is DeepSpeed Ulysses context parallelism, Microsoft's technique where each GPU computes full-sequence attention for only its assigned heads, cutting activation memory roughly 8x while staying compatible with the best Flash Attention kernels. Step three, activation checkpointing, recomputes activations during the backward pass for another factor of about eight. Step four offloads transformer block inputs to CPU and prefetches them before backpropagation reaches the layer, an optimization Ryabinin credits Unsloth with implementing first. Step five is Arctic sequence-length training, tiling all element-wise computations, losses and MLPs, so no buffer ever spans the full 3 million token dimension. Only with the whole stack does 3 million tokens fit.

Going past that required Together's own contribution, an extension of Ulysses the talk calls U-Pipe. The team observed that computing even one group of attention heads at a time already saturates a GPU's compute within an iteration. So instead of allocating one huge buffer for all heads scheduled on a GPU, U-Pipe splits the heads into chunks, iterates through them, and reuses the same smaller buffer across iterations, storing partial attention results as it goes. The result is further activation memory savings with no significant throughput cost at small scales. Ryabinin shows measurements at both 8B and 32B model scales: the method matches the most memory-optimized transformer training implementations while scaling to 5 million tokens, and sometimes runs faster at shorter context lengths. The chunk size gives a straightforward dial, larger chunks use more memory but run faster.

His takeaway is that long-context training bottlenecks appear where you least expect, so profiling tools like the PyTorch profiler, which the paper elaborates on, matter as much as the techniques themselves. The paper and results are public. In the question round he restates the core problem plainly: a vanilla attention implementation at 3 million tokens would allocate a tensor 3 million long on one axis, and no single trick escapes that, only the combination does.

## Notable moments

- [0:05:17](https://www.youtube.com/watch?v=TUnPNY4E2fw&t=317s) The worked example begins: 3 million tokens on one 8x H100 node, and why the model alone does not fit.
- [0:08:18](https://www.youtube.com/watch?v=TUnPNY4E2fw&t=498s) CPU offloading of block inputs with prefetch, credited to Unsloth as first implementers.
- [0:10:21](https://www.youtube.com/watch?v=TUnPNY4E2fw&t=621s) The U-Pipe idea: chunk attention heads per GPU and reuse one small buffer across iterations.
- [0:11:22](https://www.youtube.com/watch?v=TUnPNY4E2fw&t=682s) Results at 8B and 32B scale, matching the most memory-optimized baselines while reaching 5 million tokens.

## Connections

- [Together AI](../../companies/models-inference/together-ai.md), the speaker's company, whose training and fine-tuning services this research feeds.
- [Unsloth](../../companies/models-inference/unsloth.md), credited in the talk with first implementing the CPU offloading optimization in the stack.
- [Microsoft](../../companies/cloud-compute/microsoft.md), origin of the DeepSpeed Ulysses technique that U-Pipe extends.
