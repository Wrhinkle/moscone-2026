# Mixedbread Inc.

> Open-source embedding/reranking model shop that grew into a hosted multimodal search API — retrieval infrastructure for RAG and agents, wrapped in relentless bakery puns.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023 (Verified). Location conflicting: CB Insights and PitchBook say Berlin, Germany; other directories say San Francisco — likely German-founded with a US presence (Unverified which is formal HQ).
- **Website / GitHub:** https://www.mixedbread.com/ · https://github.com/mixedbread-ai · https://huggingface.co/mixedbread-ai

## What they do
Mixedbread started as one of the best-known open embedding model labs. Their flagship `mxbai-embed-large-v1` (Apache 2.0, ~335M params) hit state-of-the-art for BERT-large-class models on MTEB (64.68 avg across 56 datasets, March 2024) and, per their model card, outperforms OpenAI's `text-embedding-3-large` at roughly 1/20th the size. Technically notable: it supports Matryoshka Representation Learning (truncate dimensions with graceful quality loss) and binary quantization — combining both yields a claimed ~97% storage reduction, which matters when you're embedding millions of documents. They also ship `mxbai-rerank` rerankers (current: `mxbai-rerank-v3-listwise`, a listwise reranker with instruction following), a German/English embedding model co-developed with deepset, the Baguetter Python search library (sparse/dense/hybrid benchmarking), and the BMX lexical algorithm (entropy-weighted BM25 extension, arXiv 2408.06643).

The commercial pivot is Mixedbread Search: a hosted retrieval API over text, PDFs, images, video, and audio in 100+ languages — you point it at your data and get semantic + hybrid search without managing embedding pipelines, chunking, or a vector DB. They claim sub-200ms latency, #1 on the BrowseComp-Plus benchmark, 2.5B+ documents processed, and 10k+ queries/sec in production (all vendor-reported). SOC2 Type II and ISO 27001 certified, with on-prem/region deployment options. Positioning is explicitly agent-first: "your agent is only as smart as its retrieval."

## Founders & origins
Aamir Shakir and Julius Lipp, founded December 2023 (Verified, multiple sources). Both title themselves "Baker." Shakir: research assistant at EPFL (2021–2023), Google SWE intern (2022), teaching at Otto-von-Guericke University Magdeburg (Reported — LinkedIn/TheOrg). Lipp: software developer at crossnative (2019–2023), Google intern (2022) (Reported). Both co-authored the BMX retrieval paper — this is a founder team that publishes IR research, not just wraps APIs.

## Funding
- Pre-seed: ~$855K implied (total $6.355M across 2 rounds minus seed; 4 investors per Crunchbase) — Reported, single aggregator source.
- Seed: $5.5M, February 2025 — Reported (Crunchbase, Seedtable, PitchBook agree on amount/date). **Lead investors: not found in public sources.** (One press hit, SignalBase, is auto-generated garbage describing them as a baked-goods company — disregard.)
- Total raised: ~$6.4M (Reported).

## Evidence of real-world use
- `mxbai-embed-large-v1`: ~5.45M Hugging Face downloads last month and 12.2M pulls on Ollama (Verified) — it's a default local-embedding choice in the Ollama ecosystem. This is genuine, massive OSS adoption.
- Vercel: Mixedbread is a native Vercel Marketplace integration (Search/Agents categories, unified billing) with an official Next.js starter template (Verified via vercel.com). Landing page also lists TinyFish, AnkiHub, Deepset — logos, but the deepset relationship is substantiated by a jointly-trained published model, and there's a maintained Haystack integration.
- No detailed public case studies found; commercial-product traction is thinner than OSS traction.

## Relevance to agentic AI engineering
This is the retrieval layer of an agent stack — the "R" that agent memory and research agents sit on. Directly relevant repo papers: *Agentic Search in the Wild: Intents and Trajectory Characteristics of Autonomous Web-Search Agents* (their BrowseComp-Plus claim targets exactly this workload), *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval*, and the memory-layer work (*Memory for Autonomous LLM Agents*, *Are We Ready For An Agent-Native Memory System?*) where embeddings/reranking are the substrate for semantic recall. For latency-sensitive stacks, *VoiceAgentRAG: Solving the RAG Latency Bottleneck in Real-Time Voice Agents* makes their sub-200ms and binary-quantization story concrete.

## Use cases & considerations
1. Local/self-hosted RAG with zero API cost: `mxbai-embed-large` via Ollama + `mxbai-rerank` — proven, cheap, Apache 2.0.
2. Drop-in hosted search for a doc-heavy agent (construction job packets, PDFs, drawings) without running a vector DB.
3. Two-stage retrieval upgrade: add their listwise reranker behind an existing BM25/vector search.

Considerations: hosted Search is young — pricing page is thin ("free to try"), and named-customer evidence is mostly ecosystem integrations. Small team, ~$6.4M raised: platform-longevity risk, though open weights are the hedge against lock-in. Competitors: Cohere (embed/rerank), Voyage AI (now MongoDB), Jina AI on models; Exa, Elastic, turbopuffer+DIY pipelines on hosted search. Open question: whether an open-model shop can convert OSS goodwill into API revenue against much better-funded rivals.

## Sources
- https://www.mixedbread.com/
- https://huggingface.co/mixedbread-ai/mxbai-embed-large-v1
- https://ollama.com/library/mxbai-embed-large
- https://github.com/mixedbread-ai (incl. baguetter, mxbai-rerank repos)
- https://www.crunchbase.com/organization/mixedbread-ai
- https://pitchbook.com/profiles/company/596394-91
- https://www.cbinsights.com/company/mixedbread
- https://vercel.com/marketplace/mixedbread
- https://vercel.com/templates/next.js/mixedbread-starter
- https://haystack.deepset.ai/integrations/mixedbread-ai
- https://huggingface.co/mixedbread-ai/deepset-mxbai-embed-de-large-v1
- https://theorg.com/org/mixedbread/org-chart/aamir-shakir · /julius-lipp
- https://arxiv.org/html/2408.06643 (BMX paper)
- https://seedtable.com/companies/mixedbread-ai
