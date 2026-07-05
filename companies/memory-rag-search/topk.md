# TopK

> A serverless, object-storage-native search database that unifies vector, keyword (BM25), and metadata-filtered retrieval in one query — built for RAG and agent memory.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** bronze
- **Founded:** 2024, Prague, Czech Republic (Verified — EU-Startups, tech.eu)
- **Website / GitHub:** topk.io; docs at docs.topk.io

## What they do
TopK is a document database purpose-built for search/RAG applications: a single query can combine dense-vector similarity, sparse-vector and keyword (BM25) matching, and structured filters/scoring ("true hybrid retrieval"), with built-in embeddings, OCR, and document parsing so teams don't have to bolt those onto a generic vector store. It runs on object storage for elastic, serverless scaling, and exposes a Postgres wire-protocol-compatible interface alongside native Python/JS/Rust SDKs — so any Postgres client can issue semantic/hybrid queries as ordinary SQL. Headline numbers claimed: sub-100ms latency and >98% recall at billion-document scale, 17ms p99 on 10M docs.

## Founders & funding
Founded by Marek Galovič and Jerguš Lejko, who reunited after separately working on large-scale systems/AI infrastructure (Verified — tech.eu, EU-Startups). Raised roughly $5.5M / €4.6M seed round to build out the enterprise offering (Verified — tech.eu, therecursive.com, techfundingnews).

## Evidence of real-world use
Company materials describe target customers in e-commerce, finance, healthcare, and legal building RAG/search products, and publish an open benchmark ("TopK Bench") comparing accuracy against unnamed competitors; no named production customers were found in public sources (Unverified beyond marketing claims).

## Relevance to agentic AI engineering
Directly a memory/RAG-layer building block — retrieval infrastructure for agents that need accurate, filterable, low-latency lookup over private document/data stores, competing with turbopuffer, Pinecone, and Postgres+pgvector setups.

## Sources
- https://www.topk.io/
- https://docs.topk.io/concepts/vector-search
- https://tech.eu/2025/07/01/topk-raises-55m-to-develop-ai-native-search-engine-for-enterprises/
- https://www.eu-startups.com/2025/07/czech-startup-topk-raises-e4-6-million-to-build-an-ai-native-search-engine-for-enterprises/
