# Tigris

> Globally distributed, S3-compatible object storage with zero egress fees, positioning itself as the storage layer for AI workloads and agents.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** bronze
- **Founded:** 2022 (Verified); San Francisco Bay Area (Reported)
- **Website / GitHub:** https://www.tigrisdata.com/ · https://github.com/tigrisdata

## What they do

Tigris is an S3-compatible object storage service where buckets are global by default: instead of picking a region, you get one bucket and an intelligent routing layer that caches and replicates objects to whichever regions traffic comes from. The metadata layer is built on FoundationDB (the same engine behind Snowflake and Apple iCloud), and the system resolves conflicting multi-region writes automatically — a "multi-master" design the founders carried over from Uber's storage platform. It originally launched running on Fly.io's infrastructure, storing data across Fly's NVMe volumes, and has since expanded to its own hardware in Virginia, Chicago, and San Jose, with London, Frankfurt, and Singapore announced as expansion targets after the Series A (Verified).

The commercial pitch is straightforward for an engineer: drop-in S3 API compatibility (point your existing SDK at a different endpoint), $0.02/GB/month standard storage with cheaper infrequent-access and archive tiers, and **zero egress fees** — the explicit wedge against AWS's "cloud tax" and the thing that makes cross-cloud training/inference pipelines economically sane (Verified via public pricing page).

The AI-specific differentiators are **snapshots and bucket forking**: whole-bucket, zero-copy, point-in-time snapshots you can roll back to ("recover from a bad write, a bug, or a hallucinated agent"), and instant GitHub-style forks of production buckets that share objects copy-on-write. The pitched use case is giving each agent or eval run its own isolated fork of the same dataset without duplication (Verified; covered independently by The New Stack).

## Founders & origins

Ovais Tariq (CEO), Himank Chaudhary (CTO), and Yevgeniy Firsov (Chief Architect) — Verified via company site and press. The three spent ~6 years together on Uber's storage team, building Docstore, Herb, and DBEvents at hundreds of billions of requests/day across ~50 data centers (Verified across Tigris, Fly.io, and a16z sources). Team size ~20 (Reported, company site). SOC 2 Type II certified; HIPAA BAA available (Reported, company site).

## Funding

- **Seed (2022):** launched with $6.9M (Reported — single-source; not confirmed by company).
- **Seed round led by Andreessen Horowitz**, announced Feb–Mar 2024; amount not disclosed in public sources (Verified that the round happened; Martin Casado led).
- **Series A: $25M, October 2025**, led by Spark Capital with a16z participating (Verified — company blog, SiliconANGLE, TechCrunch). Basis Set Ventures and General Catalyst also listed as backers (Reported, company site).
- Total raised: ~$32M+ publicly attributable; exact total not computable since the a16z seed amount is undisclosed.

## Evidence of real-world use

- **Fly.io partnership** is the strongest signal: Tigris is Fly.io's documented, first-party object storage offering (fly.io/docs/tigris), with a dedicated customer story — this is "another platform's docs recommend it," not logo-wall marketing (Verified).
- **4,000+ customers** claimed at Series A (Reported — company/press figure).
- **Basic Memory case study**: per-tenant buckets with scoped credentials for an AI memory product, leaning on zero egress (Reported, company blog).
- Public pricing page, active GitHub org (storage SDKs in Go/TypeScript), and independent developer write-ups (benhoyt.com, Peter Ullrich) documenting real migrations from S3 (Verified).
- Countersignal: a Fly.io community thread documents user complaints about 500 errors and reliability during the Fly-hosted era — worth weighing for production use (Reported).

## Relevance to agentic AI engineering

Tigris sits in the **agent infrastructure/state layer**. Bucket forking maps directly onto the isolation problem in multi-agent coding work — the parallel-sandbox pattern discussed in *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering* and the reproducible-environment requirements in *Verifiable Software Worlds for Computer-Use Agents*. Point-in-time snapshot rollback is a storage-level answer to the long-horizon error accumulation measured in *SlopCodeBench*. The Basic Memory case study connects it to the agent-memory literature (*Memory for Autonomous LLM Agents*, *Are We Ready For An Agent-Native Memory System?*): per-agent, credential-scoped buckets are a plausible substrate for agent-native memory. Zero egress matters for eval harnesses that repeatedly pull large datasets across clouds.

## Use cases & considerations

**Use cases:** (1) blob storage for multi-cloud training/inference where egress fees dominate; (2) per-agent sandboxed data via bucket forks for eval runs and agent experiments; (3) global asset serving without a CDN layer for latency-tolerant apps; (4) tenant-isolated storage for agent memory or user artifacts.

**Considerations:** Young company (~20 people) versus S3/R2 durability track records; the documented reliability complaints are dated but real. Main competitors: Cloudflare R2 (also zero egress), Backblaze B2, Wasabi, AWS S3, MinIO (self-hosted). Forking/snapshots are proprietary extensions — using them creates soft lock-in despite the S3-compatible API. Open question: whether its own-hardware buildout maintains the economics that Fly.io-hosted infrastructure enabled.

## Sources

- https://www.tigrisdata.com/about/
- https://www.tigrisdata.com/blog/series-a/
- https://www.tigrisdata.com/blog/a16z-round-press-release/
- https://www.tigrisdata.com/pricing/
- https://www.tigrisdata.com/blog/build-agents-with-bucket-forking/
- https://www.tigrisdata.com/docs/snapshots-and-forks/
- https://www.tigrisdata.com/blog/case-study-basic-memory/
- https://a16z.com/announcement/investing-in-tigris/
- https://fly.io/customers/tigris
- https://fly.io/docs/tigris/
- https://siliconangle.com/2025/10/09/tigris-data-raises-25m-ai-optimized-cloud-storage-service/
- https://techcrunch.com/2025/10/09/this-distributed-data-storage-startup-wants-to-take-on-big-cloud/
- https://thenewstack.io/how-bucket-forking-brings-github-style-forking-to-object-storage/
- https://benhoyt.com/writings/flyio-and-tigris/
- https://community.fly.io/t/our-experience-dealing-with-issues-of-tigris-reliability-500-responses-and-docs-questions-requests/23720
