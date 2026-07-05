# Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling

- **Status:** Located — [arXiv:2605.13360](https://arxiv.org/abs/2605.13360) (v2 title: "Speculative Interaction Agents: Building Real-Time Agents with Asynchronous I/O and Speculative Tool Calling")
- **Area:** voice-realtime
- **Authors / venue / date:** Coleman Hooper, Minwoo Kang, Suhong Moon, Nicholas Lee, Eric Wen, John Wawrzynek, Michael W. Mahoney, Yakun Sophia Shao, Amir Gholami, Kurt Keutzer (UC Berkeley group). arXiv preprint, May 13–14, 2026.

## Problem
Voice interaction needs sub-second responsiveness, but an agent that reasons and calls tools blocks for seconds: it waits for the user to finish speaking, then reasons, then waits on each tool round-trip. Every one of those waits is dead time stacked serially in front of the spoken answer.

## Approach
Two mechanisms, layered on an event-driven agent loop (vLLM interruptible streaming, or OpenAI's Realtime API for cloud):

1. **Asynchronous I/O** — the reason-and-act thread never blocks on the user or environment. Partial utterances stream in via `<partial_query_update>` tags (with `<final_query_update>` marking end of utterance); if new input lands mid-generation, generation is halted and the update injected with a `</think_interrupted>` marker, so reasoning overlaps with the user still talking and with tool execution.
2. **Speculative tool calling** — the agent launches tool calls on partial information, tracked as a dependency DAG. Only "safe" (read-only) tools run speculatively; stale speculative reads are discarded via `<cancel>`, and calls can be amended or removed (`REMOVE ID`) as the utterance completes. "Unsafe" state-modifying tools only commit after the final query has arrived — a clean side-effect firewall.

## Key findings
- OpenAI Realtime API: **1.3× speedup on HotpotQA (71.6% → 71.0%)**, **1.7× on TinyAgent (54.9% → 53.2%)** — near-zero accuracy cost.
- Fine-tuned 3B edge models (Qwen2.5-3B, Llama-3.2-3B): **1.6–2.2× speedups**, accuracy drops of roughly 1–3 points vs. baseline SFT.
- End-to-end latency: 4.5–7.6s → 3.6–4.4s (cloud); 2.3–5.0s → 1.1–2.5s (open-source).
- On naturalistic speech ("Human Instructions": fillers, hesitations, mid-utterance corrections), small models degrade badly: 22% → 13.6% (Qwen), 19.2% → 15.3% (Llama), with 9.3–14.3s latencies.

## Limitations & open questions
Authors concede the naturalistic-speech gap — synthetic training data doesn't capture real disfluent speech. TinyAgent tool latencies are simulated (uniform 0.5–1s), not production. No STT/TTS component breakdown. A skeptic would ask: what does speculative fan-out cost in wasted tool calls and tokens, and how does the safe/unsafe classification hold up when "read-only" tools are rate-limited or expensive?

## Why builders should care
The serial wait chain (listen → think → call → answer) is not a law of nature: start reading tools while the user is mid-sentence, and gate only side-effecting calls on the final utterance. The safe/unsafe tool split is a directly copyable design pattern for any voice agent, and the 1.3–1.7× cloud speedup requires no fine-tuning.

## Related companies in this landscape
- **LiveKit / Daily** — realtime transport layers where this overlapped-pipeline pattern would live; validates their push into agent-native orchestration.
- **Vapi** — voice-agent platform whose core latency pitch this paper gives an architectural recipe for.
- **Deepgram / AssemblyAI / Gradium** — streaming STT is the input that makes partial-query speculation possible.
- **OpenAI** — the cloud results are built directly on its Realtime API.
- **Telnyx / Twilio / Plivo** — telephony call agents are the highest-volume place these latency wins cash out.
- **Baseten / Fireworks / Together AI / Modal** — the edge-scale (3B) results argue for fast self-hosted inference with interruptible streaming, which is their serving business.
- **Temporal / Inngest** — async, durable tool execution with cancellation semantics maps to speculative-call DAGs with rollback.

## Sources
- https://arxiv.org/abs/2605.13360v2
- https://arxiv.org/html/2605.13360v2
- https://papers.cool/arxiv/2605.13360
