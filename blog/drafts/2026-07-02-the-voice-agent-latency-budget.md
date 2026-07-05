---
title: "The Voice Agent Latency Budget: Where Your 800 Milliseconds Go"
date: 2026-07-02
description: "Voice agents live or die on a mouth-to-ear latency budget, and every architectural choice — RAG, tool calls, turn-taking — is a withdrawal from it. Reading this year's voice-agent papers as one engineering story: an itemized budget, one paper-backed trick per line item, and a phone-line build for the job packet auditor."
tags:
  - voice-agents
  - latency
  - realtime
  - streaming
  - rag
  - tool-calling
  - evals
  - construction
  - aiewf-2026
draft: true
sources:
  - briefs/2026-07-02-aiewf-batch-01.md
  - notes/conference-notes-raw.md
  - notes/source-map-aiewf-2026.md
  - papers/voice-realtime/building-enterprise-realtime-voice-agents-from-scratch-a-te.md
  - papers/voice-realtime/voiceagentrag-solving-the-rag-latency-bottleneck-in-real-ti.md
  - papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md
  - papers/voice-realtime/building-interactive-real-time-agents-with-asynchronous-i-o.md
  - papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md
  - papers/voice-realtime/tau-voice-benchmarking-full-duplex-voice-agents-on-real-wor.md
  - papers/voice-realtime/provoice-bench-assessing-the-proactivity-of-voice-agents.md
  - papers/voice-realtime/from-text-to-voice-a-reproducible-and-verifiable-framework.md
  - companies/voice-realtime/daily.md
  - companies/voice-realtime/livekit.md
  - companies/voice-realtime/vapi.md
  - companies/voice-realtime/deepgram.md
  - companies/voice-realtime/assemblyai.md
  - companies/voice-realtime/telnyx.md
  - companies/voice-realtime/twilio.md
  - companies/voice-realtime/plivo.md
  - companies/evals-observability/hamming-ai.md
---

755 milliseconds. That's the measured time-to-first-audio for the best fully self-hosted voice agent pipeline published this year — Salesforce AI Research's nine-chapter tutorial that builds the whole thing from scratch: Silero VAD into Deepgram Nova-3 streaming, into a vLLM-served Qwen2.5-7B on an H200, into ElevenLabs streaming TTS, over WebSockets ([arXiv:2603.05413](https://arxiv.org/abs/2603.05413)). Best case 729ms. That is a state-of-the-art number, achieved by a team that instrumented every hop — and it spends nearly the entire budget before the agent has retrieved a single document or called a single tool.

That's the thing to internalize about voice agents: the budget is small, everything you add is a withdrawal, and most architectural decisions people make casually — "let's ground it in RAG," "let's have it check the CRM" — are three-figure-millisecond decisions.

I spent June 30 through July 2 at the AI Engineer World's Fair at Moscone West. My raw notes from the floor include "Pipecat re eval," "Daily.co," and "Gemini S2S" — the voice-and-realtime tier was thick on the ground: Daily, LiveKit, AssemblyAI, and Telnyx at gold, Deepgram and Vapi below them, Hamming AI in the eval corner. Meanwhile, over the past eighteen months, a wave of papers landed that look like separate topics — voice RAG, speculative tool calling, turn-taking, semantic triggering, full-duplex benchmarks. Read together, they are one paper: **every one of them is about buying back milliseconds from the same budget.** This post reads them that way — as an itemized bill, with one paper-backed trick per line item — and ends with the phone line I want to put in front of a real back-office tool.

## Why dead air is a hard budget, not a preference

Humans hand off conversational turns fast — the gaps in natural conversation are a few hundred milliseconds, and the VoiceAgentRAG authors frame natural voice interaction as demanding roughly a 200ms response budget across STT, retrieval, generation, and TTS ([arXiv:2603.02206](https://arxiv.org/abs/2603.02206)). Nobody's production agent hits 200ms end-to-end today; the working practitioner consensus is that somewhere around 800ms of mouth-to-ear silence, a phone call stops feeling like a conversation and starts feeling like an IVR system — the caller talks over the agent, repeats themselves, or hangs up. <!-- TODO: verify — find a citable source for the ~800ms perceptual threshold specifically; the repo supports "humans expect a few hundred ms" (VoiceAgentRAG's 200ms framing) and "755ms is achievable" (Salesforce tutorial), but the 800ms figure itself is practitioner folklore in my notes -->

Two facts make this budget unusually cruel.

First, it's *serial by default*. A naive cascade waits for the caller to finish, then transcribes, then thinks, then retrieves, then calls tools, then synthesizes. Every stage's latency stacks. The LTS-VoiceAgent paper measured this in its worst configuration: a serial cascade with model reasoning turned on took 43 to 212 *seconds* to first speech on reasoning-heavy queries ([arXiv:2601.19952](https://arxiv.org/abs/2601.19952)). Nobody ships that, but it's the honest baseline every trick below is fighting.

Second, the biggest line items are ones people don't think of as latency at all. The Salesforce tutorial's turn-taking is a VAD state machine that waits for **700ms of silence** before it even decides the caller is done. That 700ms of endpointing sits *in front of* the 755ms pipeline. The clock the caller experiences starts when they stop talking, not when your pipeline starts.

## The budget, itemized

Here's the bill, using the best measured or vendor-published numbers in my research notes. P50s where available; treat everything as directional.

| Line item | Typical cost | Source |
|---|---|---|
| Endpointing (deciding the caller finished) | ~700ms (fixed silence threshold) | Salesforce tutorial's VAD state machine |
| Streaming STT (final transcript) | 337–402ms P50 | Deepgram Nova-3 in the tutorial's measured budget |
| LLM time-to-first-token | 337ms self-hosted (Qwen2.5-7B, vLLM, H200); 278–784ms observed on cloud APIs | Salesforce tutorial |
| Retrieval (if RAG) | 50–300ms network + query per hop | VoiceAgentRAG, measuring Qdrant Cloud at 110.4ms |
| Tool calls (if any) | one full round-trip each, serially stacked | Berkeley speculative-tool-calling paper ([arXiv:2605.13360](https://arxiv.org/abs/2605.13360)) |
| Streaming TTS time-to-first-byte | 219–221ms | ElevenLabs eleven_turbo_v2_5 in the tutorial |
| Transport/telephony | tens of ms (WebRTC) to more (PSTN codec paths) | platform-dependent |

Add the naive cascade up — endpointing, STT, one retrieval, TTFT, TTS — and you're at roughly 1.7–2.0 seconds *before any tool call*, double the budget. Every serious voice-agent architecture is a scheme for making these lines overlap or disappear. The papers, one line at a time:

## Line 1: Endpointing — stop waiting for silence

The 700ms silence threshold is the crudest possible answer to "is it my turn?" — and it's a pure, unrecoverable withdrawal on every single turn.

LTS-VoiceAgent's answer is that "when to start thinking" is a *learnable classification problem*. They train a lightweight DistilBERT classifier on 100k synthetic samples to watch the evolving transcript and fire the LLM only when a prefix is "semantically saturated" (probability > 0.65) — not on fixed time or VAD boundaries. Combined with a background Thinker that maintains structured JSON state across transcript revisions and a foreground Speaker that answers from that state, they get **time-to-first-speech of 332–415ms** across four benchmarks. The contrast with blind speculation matters: the speculative baseline they compare against (PredGen) has 98–99% of its inferences interrupted and rolled back — 59 to 177 wasted forward passes per query — while the semantic trigger runs about 2.0 evaluations with under 10% interruption.

The vendors have converged on the same conclusion from production data. Deepgram's Flux model folds turn-taking and endpointing decisions into the recognizer itself instead of leaving them to VAD heuristics; LiveKit ships its own turn-detector model in its Agents framework. If your stack's endpointing is still "wait N milliseconds of silence," this is the cheapest big win available.

The honest caveat from the paper: the speed is bought with an accuracy tax on hard reasoning — LTS-VoiceAgent scores 62.57% vs. the serial cascade's 76.34% on their own Pause-and-Repair benchmark, and drops from 18.54% to 6.88% on VERA. Fast first-speech and deep reasoning are still a trade, not a solved pair. Their implied pattern for hard turns — say a verbal filler, route to the slow path — is the voice equivalent of a spinner.

## Line 2: Retrieval — take it off the hot path entirely

VoiceAgentRAG (Salesforce again) is the cleanest single-trick paper of the wave. The problem: a production vector-DB query costs 50–300ms of network latency per hop, which can eat the entire conversational budget before the LLM starts. The trick: a dual-agent memory router. A background **Slow Thinker** watches the last six turns, predicts the most likely follow-up topics *as document-style descriptions* (not as questions — their embeddings land closer to actual chunks), and pre-fetches matching chunks into an in-memory FAISS semantic cache during the natural 3–7 second pauses between turns. The foreground **Fast Talker** serves retrieval from cache lookups.

The numbers: retrieval drops from 110.4ms (Qdrant Cloud baseline) to 0.35ms on cache hits — a 316× speedup — with a 75% overall hit rate, rising to 86% by turns 5–9 as the cache warms. The transferable design details are worth stealing verbatim: index the cache by document embeddings rather than predicted-query embeddings, lower the similarity threshold to ~0.40 (query-to-doc cosine similarity with text-embedding-3-small runs 0.30–0.55), TTL of 300 seconds with LRU eviction.

Two honest caveats, both flagged by the authors. The eval is tiny — a 12-document synthetic knowledge base, 10 scripted conversations — so treat the hit rates as an existence proof, not a production forecast. And the 110ms saving is invisible if your LLM generation takes 500–8000ms, which it did in their GPT-4o-mini setup. Retrieval tricks only cash out on top of fast inference; hiding the vector hop behind a slow model is rearranging deck chairs.

## Line 3: Tool calls — start them before the sentence ends

Tool calls are the worst line item because they stack serially and each one is a full round-trip: the agent waits for the caller to finish, reasons, calls a tool, waits, reasons again, then finally speaks. The Berkeley group's speculative-tool-calling paper attacks the whole wait chain with two mechanisms: **asynchronous I/O** (partial utterances stream into the reasoning loop as they arrive, and generation is interruptibly restarted when new input lands) and **speculative tool calling** (the agent launches tool calls on partial information, tracked as a dependency DAG, cancelling stale ones as the utterance completes).

The design pattern that makes this safe is the one to copy even if you copy nothing else: **only read-only tools run speculatively; state-modifying tools commit only after the final utterance arrives.** A side-effect firewall. `get_job_status` can fire while the caller is mid-sentence; `send_customer_email` cannot.

Measured results on OpenAI's Realtime API, no fine-tuning required: 1.3× speedup on HotpotQA (accuracy 71.6% → 71.0%) and 1.7× on TinyAgent (54.9% → 53.2%) — near-zero accuracy cost. End-to-end latency on the cloud path fell from 4.5–7.6s to 3.6–4.4s. Fine-tuned 3B edge models got 1.6–2.2× at a 1–3 point accuracy cost. The known weak spot: naturalistic disfluent speech (fillers, mid-utterance self-corrections) degrades the small models badly — the same failure surface LTS-VoiceAgent's Pause-and-Repair benchmark targets. Real callers hesitate; synthetic training data mostly doesn't.

## Line 4: The pipeline itself — realtime is streaming plus pipelining

The Salesforce tutorial's core thesis deserves to be pulled out and framed: **realtime = streaming + pipelining, not one fast model.** Their 755ms is achieved by making stages overlap — a sentence buffer bridges the LLM's token stream into streaming TTS, so the caller hears the first sentence while the second is still being generated. STT streams partials; TTS streams audio; the LLM never waits for a complete thought before the mouth starts moving. The audio plumbing is unglamorous and specific: 20ms PCM chunks at 16kHz in, 24kHz out, WebSocket transport, an interruption path in the state machine for barge-in with echo gating.

Their comparison shopping is also useful for anyone tempted by speech-to-speech models: locally-served Qwen2.5-Omni came in at ~13.2 seconds time-to-first-audio (unusable), while the cloud-hosted Qwen3-Omni hit ~702ms but can't be self-hosted and only partially supports function calling. For self-hosted enterprise deployment, the cascaded pipeline still wins — spend your effort on pipelining and sentence-boundary buffering, not model hunting.

## Line 5: Turn-taking — the budget's other currency is *when*, not just *how fast*

Two more papers complete the picture by pointing at a failure mode speed can't fix: speaking at the wrong time. Amazon's ModeratorLM work on multi-party turn-taking ([arXiv:2606.13544](https://arxiv.org/abs/2606.13544), Interspeech 2026) shows that "is it my turn, given who I am in this conversation?" is a modeling problem, not a VAD threshold — role-conditioning a streaming speech LLM cut false-positive interruptions to a rate of 0.01 on real meeting recordings, versus >40% worse precision without role conditioning. And ProVoice-Bench ([arXiv:2604.15037](https://arxiv.org/abs/2604.15037)) measured proactive voice agents and found over-triggering is the dominant failure across every model tested — false-positive rates up to 0.934 on intent capture. Models fire constantly rather than wait.

For a phone agent this matters because an agent that responds in 400ms *to the wrong turn boundary* is worse than one that responds in 900ms correctly. τ-Voice's provider comparison makes it concrete: xAI's voice agent had the best task completion but an 84% interrupt rate; OpenAI's was fastest (0.90s latency, 100% responsiveness) but interrupted with only 6% selectivity. Latency and turn-taking discipline are separate axes, and the budget conversation has to hold both.

## Who handles which line for you

The platform tier at the World's Fair maps cleanly onto the budget:

- **Daily/Pipecat** (framework) and **LiveKit** (transport + framework) give you the pipelining machinery — frame-level orchestration, interruption handling, streaming glue — and leave the architecture choices (retrieval, tools, models) to you. Pipecat targets sub-second voice-to-voice and is vendor-neutral across ~80–100 integrations; LiveKit ships its own turn-detector model and is the stack ChatGPT's Advanced Voice Mode runs on. These are the "own your budget" options.
- **Vapi** (managed platform) sells the whole loop at a $0.05/min platform fee (realistic all-in ~$0.15–0.40/min once STT/LLM/TTS/telephony providers stack), claiming sub-600ms responses. You trade budget ownership for speed-to-ship — a dashboard assistant is demoable in an afternoon.
- **Deepgram** and **AssemblyAI** own the STT line (Nova-3 streams at ~$0.0048/min; Universal-Streaming at $0.15/hr with immutable partial transcripts — finality semantics matter because transcript revisions are what trigger speculative-execution rollbacks). Deepgram's Flux moves the endpointing line into the recognizer.
- **Telnyx** attacks the transport line structurally: telephony PoPs and inference GPUs co-located in the same data halls, claiming sub-200ms audio round-trips versus 500ms+ for stitched stacks (vendor benchmark — unverified, but the architecture argument is sound). **Twilio's ConversationRelay** and **Plivo's** `<Stream>` verb are the bring-your-own-brain versions: they run the latency-critical audio pipeline and hand your server a WebSocket of text.

The build-vs-buy question is really "which budget lines do you want to own?" — and the Salesforce tutorial's value is that it prices every line so you can hold vendors to it.

## The build: a phone line for job status

Here's the demo I want to exist, connecting this thread to the back-office one. To be clear: this is a build plan, not shipped work.

I already have a Job Packet Readiness Auditor — a local tool that takes messy roofing job notes and produces a readiness verdict plus structured JSON: `READY / NOT READY / READY WITH RISKS`, blocking items, office vs. production tasks. Its output is a small, typed state object. That makes it a nearly perfect voice-agent backend, because the hard part of voice — grounding — is already solved by structure.

The build: a phone number (Vapi for the fast version; Pipecat + Twilio ConversationRelay for the owned version) fronting the auditor's JSON. A coordinator or crew lead calls the office line: "Is the Johnson job ready to roll?" The agent's tools are three read-only functions: `list_jobs()`, `get_job_readiness(job_id)`, `get_blocking_items(job_id)`. The agent reads the verdict and blockers back in one sentence.

The budget math is why this specific demo works. There is no RAG line — state lives in pre-computed JSON, so "retrieval" is a local lookup at effectively 0ms, which is VoiceAgentRAG's endgame achieved by schema instead of caching. The tool calls are all read-only, so every one of them is speculatively fireable under the Berkeley safe/unsafe split — the agent can be fetching the Johnson packet while the caller is still saying "ready to roll." The response is a verdict plus a short list, so generation is a sentence or two — minimal tokens between TTFT and TTS. Almost the entire naive-cascade overrun is designed out before tuning anything.

The one line item the papers say to worry about: argument values. The From Text to Voice evaluation ([arXiv:2605.15104](https://arxiv.org/abs/2605.15104)) found that the dominant voice tool-calling failure — 54–57% of paired failures for the leading models — is *misheard or misinterpreted argument values*, not wrong tool selection. "Johnson job" vs. "Johnston job" is exactly that failure. So the design carries a read-back confirmation on the job name before answering, and the STT layer gets keyterm prompting (Deepgram and AssemblyAI both support biasing recognition toward a supplied vocabulary — feed it the active job names). That costs one turn of latency budget, spent deliberately, on the one line where the research says voice actually breaks.

## Scoring it: the part that keeps you honest

The reason to be sober about all of this is τ-Voice ([arXiv:2603.13686](https://arxiv.org/abs/2603.13686)). They took 278 verifiable customer-service tasks where GPT-5 scores 85% pass@1 in text, and ran full-duplex voice agents on the identical tasks: **31–51% under clean studio audio, 26–38% under realistic conditions** (accents, background noise, interruptions). Voice agents currently retain 30–45% of their own model's text capability. Accents alone cost about 10 points on average, and the degradation is provider-specific — xAI lost 38% while Google was nearly unaffected. And 79–90% of failures traced to agent behavior — logic errors, transcription failures during authentication, hallucinated completions — not to the simulator.

So the eval plan for the job-status line is not optional garnish; it's half the build. Three layers, smallest first: (1) a paired text/voice golden set in the From Text to Voice style — take twenty scripted job-status calls with known correct verdicts, run them as text and as TTS-generated audio, and track the text-to-voice gap as a first-class metric (for top models it should be under ~5 points; if it's larger, the problem is the pipeline, not the model); (2) accent and noise variants of the same twenty, because τ-Voice says that's where providers diverge; (3) Hamming-style simulated calls — Hamming AI's whole product is synthetic voice characters with configurable accents, interruptions, and background noise placing concurrent calls at your agent and scoring the audio, with failed production calls converting to regression tests. That last loop — production call fails, becomes a test case — is the voice version of the trace-to-dataset discipline the eval tier was selling all over the expo floor.

One more τ-Voice finding worth carrying: they only tested speech-to-speech models, and cascaded pipelines with a strong reasoning LLM may still beat them on task completion — the From Text to Voice data agrees, showing cascade-vs-direct within ~1.5 points either way for top models. Benchmark before betting on speech-to-speech. For a tool-calling agent over a structured backend, the cascade you can instrument is probably still the right default.

## The open question

Every trick above buys milliseconds by *predicting* — predicting the follow-up topic, predicting the utterance's end, predicting which tool will be needed. The budget is increasingly balanced not by faster components but by speculative work that's usually right and cheap to throw away. What nobody has published yet is the aggregate economics: LTS-VoiceAgent counts wasted forward passes, VoiceAgentRAG concedes its prediction fan-out has an embedding-and-LLM cost it doesn't price, and the Berkeley paper doesn't total up the discarded speculative tool calls. At 1–5 million calls a day — Vapi's reported volume — the difference between 2 speculative evaluations per turn and 60 is an infrastructure bill, not a rounding error. Someone is going to write the paper that treats the latency budget and the compute budget as one optimization problem. Until then, the experiment I can actually run is the twenty-call golden set against a phone line that answers "is the Johnson job ready?" in under a second — and the first number I'll publish is where my 800 milliseconds went.
