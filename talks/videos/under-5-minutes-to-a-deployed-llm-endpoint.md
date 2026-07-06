# Under 5 minutes to a deployed LLM endpoint

> A RunPod intro and live demo deploying an open source LLM from the RunPod Hub to a serverless, autoscaling API endpoint in under five minutes.

- **Speaker:** Audry Hsu, RunPod
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ILdE7FaAjVA) (AI Engineer channel; ~13m, released 2026-06-07)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Hsu pitches RunPod as a cloud AI infrastructure company with the GPUs and the tooling to deploy models, whether private or open source from Hugging Face: you bring your code, RunPod brings the rest. The problems it solves are familiar ones. Infrastructure management is work developers happily handed to DevOps and now want abstracted further, GPU access is slow and opaque in what she calls a global supply crunch, comparing GPU buying to pandemic toilet paper hoarding, and builders should spend their time building applications rather than managing hardware.

The company history is unusual. Founders Zenon and Pardeep had crypto mining rigs in their basement in 2022, the mining failed, and they posted the GPUs on Reddit for free use in exchange for feedback. Hsu tells the story to make a point about the company still being community-driven through Reddit and Discord, not to be bootstrappy. By the numbers she cites: over 500,000 developers on the platform, more than 30 data centers worldwide including in Europe and the EU, and a recently passed milestone of 120 million dollars in annual recurring revenue, with some AI cloud-native companies among the customers.

The product tour covers four building blocks. Pods are sandboxed container environments with allocated GPUs where you bring a Dockerfile and code. Serverless is the autoscaling product for bursty and batch workloads, where idle workers spin down and cost nothing. Clusters serve heavy training with multi-node, high-speed networking. The Hub is a repository of preconfigured, vetted AI repos, from RunPod and the community, that you can fork, star, and deploy. She notes CLI support and agent-ready skills exist so your coding agent can work with RunPod without reading the docs, but demos through the console since the room is full of humans.

The demo delivers the title. From the Hub she picks a vLLM listing, shows that the listing is a plain GitHub repo with a preconfigured Dockerfile, bumps the max model length for a larger context window, and deploys; configuration options pass through as flags to vLLM serve. The endpoint defaults to H100s with A100s as backup, priced at a fraction of a cent per second charged only while a worker handles a request, with max workers configurable up to 15, spending caps, and always-on active workers to avoid cold starts. She sends a test request to the provisioned HTTP endpoint and reads the telemetry: the first request sits in the queue about 41 seconds due to cold start, container creation, and model download, but executes in about a second and a half, and subsequent requests skip the cold-start penalty. Total time from Hub listing to working production-style API: under five minutes. She closes by pointing to a companion session on RunPod's Python SDK, deploying code as a remote function on a GPU entirely from the terminal.

## Notable moments

- [0:02:07](https://www.youtube.com/watch?v=ILdE7FaAjVA&t=127s) The origin story: failed basement crypto rigs offered free on Reddit in 2022 became a company now at 120M ARR.
- [0:05:12](https://www.youtube.com/watch?v=ILdE7FaAjVA&t=312s) Why serverless: autoscaling without capacity planning, spending caps, and always-on workers for latency-sensitive endpoints.
- [0:11:16](https://www.youtube.com/watch?v=ILdE7FaAjVA&t=676s) The first request returns: 41 seconds of cold-start queue time, 1.5 seconds of execution, under five minutes end to end.

## Connections

- [RunPod](../../companies/cloud-compute/runpod.md) is the speaker's company; the profile covers the platform this talk introduces.
- [Modal](../../companies/cloud-compute/modal.md) competes directly on serverless GPU deployment with the same cold-start and autoscaling tradeoffs.
- [Hugging Face](../../companies/models-inference/hugging-face.md) is the model source the demo pulls from, the upstream of RunPod's Hub listings.
