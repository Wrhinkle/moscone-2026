# Your Agent Failed in Prod. Good Luck Reproducing It.
> Why temperature zero cannot make agents reproducible, and Chronicle, a boundary-recording proof of concept that turns failed production runs into replayable test cases.

- **Speaker:** Tisha Chawla & Susheem Koul, Microsoft
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Lc8zRh9muoY) (AI Engineer channel; ~14m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary
Chawla and Koul, who run agents against production backends at Microsoft, open with the on-call scenario every agent team knows: an agent called the wrong tool in production, you pull the prompt from telemetry, replay it locally with the same model, and it works perfectly ten times in a row. The failing run is gone. If you cannot reproduce it you cannot debug it, and you cannot promise it will not happen to the next customer.

Their running example is a broker agent told to sell $1,000 of stock. The model drops the raw number 1,000 into the quantity field and sells 1,000 shares at $190 each, a $190,000 mistake, while the API returns a clean 200 in 30 milliseconds and every dashboard stays green. The reflexive fix, setting temperature to zero, is a misconception on two levels. First, greedy decoding just makes the model repeat the same logical error the same way. Second, temperature zero is not even bitwise deterministic on hosted APIs: the same prompt run a thousand times can return dozens of different responses. Chawla walks through why from first principles: argmax sampling does not guarantee identical underlying scores; floating point addition is not associative, so tiny ordering shifts flip the winning token; the real culprit is batch invariance, since your request is grouped with whatever else hits the server that millisecond; and mixture-of-experts routing has capacity limits, so whether your token makes the cut into an expert depends on co-batched traffic.

The reframe: the wrong question is how to make the model deterministic, the right one is how to debug and retest a run you cannot reproduce. They distinguish bitwise determinism (same input, same output, controllability you will not get from a hosted API and do not actually want) from replayability (recording a run well enough to re-validate and debug it, which is observability). Record at the boundary of each node, not at the network layer, since local retrieval, in-process tools, and memory never touch the network and streaming shreds packet captures.

Koul demos Chronicle, their proof of concept. A boundary annotation wraps any method in the agent graph, whether tool call, LLM call, or RAG retrieval, and records every input-output pair plus state like model version, sampling parameters, and code version, freezing the run as a trace. The stock demo shows the trace pinpointing the planning LLM emitting a tool call for quantity 1,000. The fix is a guardrail on the tool, and Chronicle tests it by replaying the recorded trace with the LLM node stubbed to its recorded output while the fixed tool runs live; an assertion confirms the order is now blocked. Because replays never call the model, they are deterministic, rerunnable, and free, giving agents something like deterministic CI. Their takeaways: stop chasing bitwise determinism, log your session variables, capture the full envelope beyond the prompt, use replays as regression tests, and keep generation-time variation alive because that is what gives the agent its agency.

## Notable moments
- [0:01:02](https://www.youtube.com/watch?v=Lc8zRh9muoY&t=62s) The $1,000 order that sells 1,000 shares, a $190,000 error behind a green dashboard.
- [0:03:05](https://www.youtube.com/watch?v=Lc8zRh9muoY&t=185s) Why temperature zero fails: floating point non-associativity, batch invariance, and MoE routing.
- [0:07:11](https://www.youtube.com/watch?v=Lc8zRh9muoY&t=431s) Chronicle's boundary annotation and the recorded trace of the bad tool call.
- [0:10:14](https://www.youtube.com/watch?v=Lc8zRh9muoY&t=614s) Replay mode: stub the LLM node from the trace, run the fixed tool live, assert the order is blocked.

## Connections
- [Microsoft](../../companies/cloud-compute/microsoft.md): the speakers' employer, whose agent platform work frames the production stakes described here.
- [Braintrust](../../companies/evals-observability/braintrust.md): commercializes the same core move of turning production traces into datasets and regression tests.
- [Reproducible, Explainable, and Effective Evaluations of Agents](../../papers/swe-agents/reproducible-explainable-and-effective-evaluations-of-agen.md): the research-side case for the reproducibility discipline this talk implements with trace replay.
