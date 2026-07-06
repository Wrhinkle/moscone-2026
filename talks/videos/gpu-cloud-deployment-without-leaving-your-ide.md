# GPU Cloud Deployment Without Leaving Your IDE

> A live demo of RunPod Flash, a Python SDK that deploys a decorated function to cloud GPUs straight from the local dev loop, skipping the commit-build-push-allocate cycle.

- **Speaker:** Audrey Hsu, RunPod
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=zDGHt0LB-dA) (AI Engineer channel; ~20m, released 2026-06-09)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Hsu opens with RunPod's positioning: an AI cloud infrastructure company whose job is to absorb the configuration work, CUDA version alignment, PyTorch compatibility, untested GPU SKUs, that teams otherwise spend more time on than their models. She retells the origin story, two founders with spare GPUs from a failed crypto-mining venture posting free access on Reddit in 2022 in exchange for feedback, and cites the current numbers: revenue-generating from the start, 30-plus data centers across 10 countries, and a recent milestone of $120 million in annual recurring revenue. She sketches the product tiers, pods for reserved per-second VMs, serverless for autoscaling variable workloads with no idle cost, clusters for multi-node training, and a hub of pre-vetted open source repos like ComfyUI and vLLM, before spending the session on serverless.

The demo centers on Flash, RunPod's Python SDK. The problem it targets is the iteration loop during development: commit, push to GitHub, build a Docker image, pull it from the registry, load it on a server, allocate a GPU, test, repeat. Flash collapses that to a decorator. You write a normal async Python function, add the flash endpoint decorator, and everything inside the function is packaged onto GPU cloud while the surrounding code runs locally. Hot file reload repackages and pushes changes immediately.

Hsu runs it live. A generate-image function loads Stable Diffusion XL Turbo, and `flash run` spins up a local FastAPI dev server that proxies requests to the cloud GPU. The audience picks the prompt (cats flying over cloudy London), the first output looks rough, and the recovery becomes the point of the demo: she comments out the model, swaps in DreamShaper, a Stable Diffusion 1.5 fine-tune better for illustration styles, bumps inference steps to 25, and re-sends the same request without touching Docker or the console. The decorator itself carries the infrastructure spec: endpoint name, GPU family, max workers (five in the demo), active always-on workers (one), and idle timeout.

She closes with a multi-model pipeline to show the orchestration case: Qwen 3 on a public endpoint rewrites the user's prompt, DreamShaper on her Flash endpoint generates three images, and Nano Banana 2, a Google image model good at composition, composes final photos of RunPod's founders from a reference picture. A brief console detour answers a pricing question: workers bill only while a request runs, an H100 at $0.00116 per second in the demo, with serverless carrying a premium over pods in exchange for autoscaling. Her guidance is to experiment on pods or a low worker count and reach for serverless when you need hundreds of distributed workers.

## Notable moments

- [0:06:11](https://www.youtube.com/watch?v=zDGHt0LB-dA&t=371s) The iteration-loop problem Flash removes, and the one-paragraph explanation of the decorator
- [0:08:12](https://www.youtube.com/watch?v=zDGHt0LB-dA&t=492s) Live `flash run`: local FastAPI server, cloud GPU execution, audience-chosen prompt
- [0:13:21](https://www.youtube.com/watch?v=zDGHt0LB-dA&t=801s) Swapping Stable Diffusion XL Turbo for DreamShaper from the IDE, no rebuild or console visit
- [0:16:23](https://www.youtube.com/watch?v=zDGHt0LB-dA&t=983s) The Qwen 3 to DreamShaper to Nano Banana 2 pipeline, plus per-second pricing in the console

## Connections

- [RunPod](../../companies/cloud-compute/runpod.md): the speaker's company; this talk demos the Flash SDK on its serverless tier
- [Modal](../../companies/cloud-compute/modal.md): the closest competitor pattern, Python-decorator deployment to serverless GPUs
