# What Lies Beneath the API

> A Modal engineer argues that every differentiated AI product eventually crosses into domain-specific territory where fine-tuning your own model beats renting a frontier API.

- **Speaker:** Benjamin Cowen, Modal
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=HvZXAOZ3iv8) (AI Engineer channel; ~13m, released 2026-06-02)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Cowen, a forward deployed machine learning engineer at Modal, gives the punchline up front: as AI products mature and specialize, more companies turn to fine-tuning for better performance and costs, so the real question is when your application steps over the line into a custom domain. Modal's vantage point is a general purpose serverless compute platform whose customers range from physics simulations and quantum chemistry to voice, LLMs, agents, and, lately, large-scale reinforcement learning.

He frames the choice as a spectrum. On one end sit frontier APIs, which he credits with unlocking an era where anyone can build almost anything fast, but which allow no customization beyond prompt engineering. His running joke is caveman mode: telling the LLM to talk like a caveman cuts tokens substantially, but that trick will not scale if the startup grows 100x, and it does nothing for enterprise contracts with specific latency or throughput requirements or for custom metrics that encode business logic. On the other end sits training your own model the traditional way, which historically meant procuring a cluster, isolating training from production resources, and pulling AI engineers and even scientists into infrastructure work. Cowen's pitch is the emerging middle ground: serverless platforms plus open source training libraries give you algorithm-level control while keeping the fast iteration cycles of the API end of the spectrum.

The evidence he cites is customer results. Intercom beats its frontier API baseline at one fifth the cost, another customer reports gains of orders of magnitude, and he quotes Modal customer Decagon's framing as the summary: frontier labs want their models to win on everything, while you want your model to win at your business logic. His signals that it is time to fine-tune: you have gone to caveman mode and still pay more for the API than customers pay you, you are missing latency or throughput targets, or your evals have plateaued. The counter-signal is data. If you have not been collecting data and lack mature evals, it is not time to train, because garbage in, garbage out still applies.

The takeaway he most wants the room to keep: if you have built a product, you have probably already touched everything you need to train. An agent harness is an RL environment for teaching a model to provide your service, and product evaluations are training data. Supervised fine-tuning fits in about 300 lines of Python using examples from Modal's repository, and RL fits in a similar footprint. He argues serverless is underrated for training, not just inference: hyperparameter sweeps can fan out across on-demand containers and kill unpromising runs early, which he likens to a meta-evolutionary algorithm, and RL rollouts are embarrassingly parallel. One Modal customer scaled to 50,000 to 100,000 sandboxes in a quarter just to run RL rollouts. Serving comes last: vLLM, SGLang, Triton Inference Server, or a custom Python workflow, autoscaled to traffic. His closing calibration is that the answer is not "train a model in 10 years" but possibly in six to twelve months, so start collecting data and building evals now.

## Notable moments

- [0:04:13](https://www.youtube.com/watch?v=HvZXAOZ3iv8&t=253s) The customer evidence: Intercom at one fifth the cost of its frontier API, and Decagon's line that frontier labs do not share your goal.
- [0:06:15](https://www.youtube.com/watch?v=HvZXAOZ3iv8&t=375s) The signals it is time to fine-tune: API costs exceeding revenue, missed latency targets, plateaued evals, and the data-readiness caveat.
- [0:10:18](https://www.youtube.com/watch?v=HvZXAOZ3iv8&t=618s) A customer scales to 50,000 to 100,000 sandboxes for RL rollouts on Modal's unified sandbox and GPU APIs.

## Connections

- [Modal](../../companies/cloud-compute/modal.md) is the speaker's company and the serverless platform the training and rollout examples run on.
- [RunPod](../../companies/cloud-compute/runpod.md) competes for the same GPU workloads with a different serverless deployment model.
- [Baseten](../../companies/models-inference/baseten.md) targets the serving step Cowen describes, hosting fine-tuned models behind production endpoints.
