# Continual Learning for AI Agents: From Failures to Durable Improvements

> RELAI's founder argues production logs must be lifted into replayable learning environments, and proposes verifiable continual learning where every agent fix is tested for gains and checked against regressions.

- **Speaker:** Soheil Feizi, RELAI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=2IxD9OB3XuQ) (AI Engineer channel; ~23m, released 2026-07-05)
- **Program:** Online Track 2026

## Summary

Feizi, founder and CEO of RELAI and an associate professor of computer science at the University of Maryland, frames continual learning as making agents improve from experience without forgetting, across three layers: the model (weights), the harness (prompts, skills, tools, code, workflow), and memory (session and persistent). Two challenges structure the talk. First, where does feedback come from? During development you have benchmarks and evaluators, but production gives you session logs, which can be scored automatically by other models or annotated by human experts at lower volume. Feizi's central claim is that a log plus feedback is still not enough because it is not testable. You need a replayable learning environment, a simulation inferred from one observation that captures how tools should behave (real or mocked), what synthetic users look like, and what evaluators define success, so candidate agents can be run against the same scenario repeatedly.

Second, how do you act on feedback? He surveys the options per layer. Weight updates (SFT, RL post-training such as DPO and GRPO, LoRA for cheaper and safer changes) need benchmarks and explicit evaluators. In the harness layer, trace-to-harness approaches, where a coding agent reads a log and edits the agent, work on raw logs but are vibe-based: untestable for the sample at hand and prone to hidden regressions elsewhere. Prompt-search methods like GEPA are testable but again need a benchmark. Memory writes (he cites Letta and Mem0-style fact storage plus skill distillation from successful trajectories) are the cheapest and fastest updates but usually unverified. His summary rule: a good learning engine asks for the smallest durable change at the right layer.

From there he defines verifiable continual learning, where every fix is proven to help and proven to break nothing that already worked, via an executable test, a measured before-and-after delta, and regression tests. Four principles carry it: replayability (one-off failures become rerunnable tests), holisticness (one failure has many candidate causes; his example of an agent citing a stale policy and skipping a required escalation could implicate memory, prompt, tool normalization, workflow gates, or the model itself), lifelongness (regression awareness belongs inside the optimization loop as a constraint over past environments, not as a post-hoc check, and must not scale linearly with the number of environments), and efficiency across both the update types and the loop itself.

The last section shows RELAI's implementation: a one-time learning-harness setup, then two commands, one to create learning environments from logs, feedback, or plain instructions, and one to run the holistic lifelong optimizer, which outputs a reviewable pull-request-style version update. The demo uses a fictional support-agent benchmark with deterministic evaluators and deliberate regression traps. From the instruction "caller is rude and adversarial," the system generates an environment with personas, mock tools, and evaluators, finds the agent scoring 78 percent with two weak evaluators, and after one optimize loop reports roughly 10 percent average improvement with the score rising to 97 percent. His three takeaways: continual learning is not necessarily fine-tuning, production logs are not learning environments until transformed, and the frontier is regression-aware improvement.

## Notable moments

- [0:04:01](https://www.youtube.com/watch?v=2IxD9OB3XuQ&t=241s) Production gives you logs, not benchmarks, and why log-plus-feedback is still not testable.
- [0:11:04](https://www.youtube.com/watch?v=2IxD9OB3XuQ&t=664s) Verifiable continual learning defined: executable test, measured delta, regression test.
- [0:12:05](https://www.youtube.com/watch?v=2IxD9OB3XuQ&t=725s) The stale-policy failure walked through five candidate layers, illustrating fix routing.
- [0:19:18](https://www.youtube.com/watch?v=2IxD9OB3XuQ&t=1158s) Demo: a rude-caller learning environment generated from one instruction, then optimized from 78 to 97 percent.

## Connections

- [Relai](../../companies/evals-observability/relai.md): the speaker's company; this talk is the technical argument behind the product and $6.9M raise covered in the profile.
- [Session recaps](../../notes/session-recaps.md): the DSPy session recap covers GEPA, the prompt-search method Feizi positions as testable but benchmark-dependent.
