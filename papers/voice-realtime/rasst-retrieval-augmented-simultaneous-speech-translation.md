# RASST: Retrieval-Augmented Simultaneous Speech Translation

- **Status:** Located — [arXiv:2601.22777](https://arxiv.org/abs/2601.22777)
- **Area:** voice-realtime
- **Authors / venue / date:** Jiaxuan Luo, Siqi Ouyang, Jiaxing Xu, Lei Li (Johns Hopkins / CMU affiliations); arXiv v1 2026-01-30, v2 2026-06-13; listed as under review

## Problem
Speech LLMs have gotten good at simultaneous speech translation (SST), but they still botch rare and domain-specific terminology — exactly the words that matter in conference talks, medical calls, or trade jargon. Retrieval augmentation is the standard fix in text RAG, but in streaming speech it's hard: retrieval must run fast over *partial* audio, and the model must decide whether and when to use a retrieved term mid-generation.

## Approach
RASST bolts a lightweight cross-modal retriever onto a Speech LLM (Qwen3-Omni-30B-A3B-Instruct):
- **Dual-encoder retriever:** Qwen3-Omni audio encoder for speech + BGE-M3 for text, both mapped to normalized 1024-d embeddings, trained with multi-positive InfoNCE on speech–terminology pairs from GigaSpeech.
- **Multi-scale sliding-window retrieval:** 1.92s windows with 0.48s stride; top-10 terms per window, re-aggregated to a top-10 per chunk — improves recall on short partial utterances.
- **Injection:** retrieved glossary entries (term + target translation) are appended as context alongside streaming speech features and prior partial translations.
- **Robustness training data:** synthetic examples mix ground-truth terms with retriever-mined hard negatives, empty retrievals, and all-wrong retrievals, so the LLM learns when to *ignore* retrieval.

## Key findings
- Terminology accuracy up ~40% (relative, per abstract); absolute gains of +16% on En→Zh and +10–15% on En→De / En→Ja across latency settings (ACL 60/60 dev, ESO test).
- Overall quality: +2–3 BLEU on En→Zh — modest because rare terms are, by definition, sparse.
- RASST beats even offline MT on terminology accuracy — glossary access matters more than latency budget for these terms.
- Retriever overhead: at most 16% of Speech LLM decoding time at the smallest chunk size; negligible at larger chunks.

## Limitations & open questions
No formal limitations section. Case studies show three failure modes: retrieval misses needed entries; the LLM retrieves correctly but fails to realize the glossary surface form; and over-triggering injects translations not in the reference. A skeptical builder would also ask: how does glossary construction scale beyond curated/paper-extracted sets, and does the 30B backbone fit real-time budgets on commodity serving?

## Why builders should care
If you're building live translation or any voice agent that must say domain terms correctly, a small streaming retriever plus glossary injection is a cheap, validated pattern — and the "teach the model to ignore bad retrievals" training trick is transferable to any voice-RAG pipeline. Don't wait for a bigger speech model to fix jargon; feed it the glossary.

## Related companies in this landscape
- **LiveKit / Daily** — realtime infra where live translation and voice RAG pipelines like this run.
- **Deepgram / AssemblyAI / Gradium** — streaming STT/speech-model vendors; chunkwise retrieval over partial audio pressures their APIs to expose incremental representations.
- **Vapi** — voice-agent platform; terminology-grounded generation directly addresses domain-jargon failures in production call agents.
- **Qdrant / Turbopuffer / Pinecone / LanceDB** — vector stores serving the low-latency top-k retrieval this design depends on.
- **Twilio / Telnyx** — telephony rails where live-translation features would ship.

## Sources
- https://arxiv.org/abs/2601.22777
- https://arxiv.org/html/2601.22777v1
- https://www.emergentmind.com/topics/retrieval-augmented-simultaneous-speech-translation-rasst
