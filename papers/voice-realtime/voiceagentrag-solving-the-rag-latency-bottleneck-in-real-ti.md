# VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents Using Dual-Agent Architectures

- **Status:** Located — [arXiv:2603.02206](https://arxiv.org/abs/2603.02206), open-source code on [GitHub](https://github.com/SalesforceAIResearch/VoiceAgentRAG)
- **Area:** voice-realtime
- **Authors / venue / date:** Jielin Qiu, Jianguo Zhang, Zixiang Chen, Liangwei Yang, Ming Zhu, Juntao Tan, Haolin Chen, Wenting Zhao, Rithesh Murthy, Roshan Ram, Akshara Prabhakar, Shelby Heinecke, Caiming Xiong, Silvio Savarese, Huan Wang (Salesforce AI Research). arXiv, submitted 2026-03-02 (v2 2026-03-03).

## Problem
Natural voice conversation demands roughly a 200ms response budget covering STT, retrieval, LLM generation, and TTS. A production vector DB query alone adds 50–300ms of network latency, so grounding a voice agent in a knowledge base via standard RAG can eat the entire budget before the LLM even starts generating.

## Approach
A dual-agent memory router that decouples retrieval from response. A background **Slow Thinker** watches the conversation (sliding window of last 6 turns), uses an LLM to predict the n most likely follow-up topics as document-style descriptions (not questions — their embeddings land closer to actual chunks), and pre-fetches matching chunks into a FAISS IndexFlatIP semantic cache during inter-turn pauses. A foreground **Fast Talker** answers queries from sub-millisecond cache lookups, falling back to the vector store only on misses (and caching those results too). Key design details: index the cache by document embeddings, not prediction-query embeddings; similarity threshold τ=0.40 (query→doc cosine with text-embedding-3-small runs 0.30–0.55); TTL 300s with LRU eviction; dedup at >0.95 similarity.

## Key findings
- Retrieval latency: 110.4ms (Qdrant Cloud baseline) → 0.35ms on cache hits — **316× speedup**.
- **75% overall cache hit rate** (150/200 queries); 79% on warm turns; 86% on turns 5–9.
- Topically focused scenarios (pricing, API deep-dives) hit 80–100%; broad exploration/rapid-fire only 40–65%.
- ~16.5s cumulative retrieval time saved across 200 queries.
- Eval is small: synthetic "NovaCRM" KB of 12 docs / 76 chunks, 10 scripted conversations × 20 turns, GPT-4o-mini, 3–7s inter-turn delays.

## Limitations & open questions
Authors concede end-to-end time is dominated by LLM generation (500–8000ms with GPT-4o-mini via API), so the 110ms saving is invisible without fast inference; TTL caching is only eventually consistent (stale chunks if the KB changes mid-call); benefits vanish with local vector DBs (~0.1ms search anyway), incoherent topics, or <2s turn gaps needed for prefetch. Skeptic's questions: does a 12-document synthetic KB predict behavior on real enterprise corpora? What does 5 predictions × 10 retrievals per turn cost in embedding/LLM spend at scale? No answer-quality metric is reported — only latency.

## Why builders should care
If you're bolting RAG onto a voice agent, don't put a network-hop vector search on the critical path — prefetch speculatively during pauses and serve from an in-memory semantic cache. The two portable tricks: predict follow-ups as document-style text, and index the cache by document embeddings with a lowered similarity threshold (~0.40). But pair this with fast inference (Groq/Cerebras-class), or the win disappears into generation latency.

## Related companies in this landscape
- **Vapi, LiveKit, Daily** — voice-agent infra platforms whose pipelines this directly targets; a memory-router layer slots between their transport and the LLM.
- **Deepgram, AssemblyAI, Gradium** — streaming STT/speech vendors; retrieval savings only matter if the rest of the pipeline (their piece) is also fast.
- **Qdrant** — the paper's baseline vector DB; validates Qdrant Cloud in RAG stacks while showing its network latency must be hidden for voice.
- **Turbopuffer, Pinecone, LanceDB** — challenged: for voice, remote vector search moves off the hot path; local/embedded search (LanceDB's model) already gets ~0.1ms.
- **Cerebras, Fireworks, Baseten, Together AI** — fast-inference providers the authors implicitly point to, since generation dominates end-to-end latency.
- **Twilio, Telnyx, Plivo** — telephony rails where the sub-200ms budget bites hardest on real phone calls.

## Sources
- https://arxiv.org/abs/2603.02206
- https://arxiv.org/html/2603.02206v2
- https://github.com/SalesforceAIResearch/VoiceAgentRAG
- https://www.marktechpost.com/2026/03/30/salesforce-ai-research-releases-voiceagentrag-a-dual-agent-memory-router-that-cuts-voice-rag-retrieval-latency-by-316x/
