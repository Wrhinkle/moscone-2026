# Oracle

> The 49-year-old database giant that reinvented itself as one of the largest AI-training cloud providers on earth — home of OpenAI's Stargate capacity — while pushing agentic AI into its database and ERP suites.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** platinum
- **Founded:** 1977, Santa Clara, CA (as Software Development Laboratories) (Verified, common historical record). HQ now Austin, TX.
- **Website / GitHub:** https://oracle.com · https://www.oracle.com/cloud/ · https://github.com/oracle

## What they do

For an AI engineer in 2026, Oracle is three distinct things:

1. **OCI as raw AI compute.** Oracle Cloud Infrastructure sells bare-metal GPU capacity with RDMA cluster networking at frontier-training scale: OCI Superclusters up to 131,072 NVIDIA GPUs (GB200 NVL72), and the announced **OCI Zettascale10** — a multi-datacenter cluster of up to 800,000 NVIDIA GPUs, claimed 16 zettaFLOPS peak, generally available to customers in H2 2026 (Reported, Oracle announcements + press). OCI's pitch versus the hyperscalers is price/performance on bare-metal GPUs and willingness to build dedicated capacity for one customer.
2. **Oracle AI Database 26ai.** The flagship database now converges relational, JSON, graph, and **AI Vector Search** in one engine, adds vector indexing directly over Apache Iceberg tables ("Vectors on Ice"), a standalone **Autonomous AI Vector Database**, and — most relevant here — an **Autonomous AI Database MCP Server** so external agents/MCP clients can query the database with row/column-level security enforced by the database rather than the agent (Verified, Oracle announcement + Constellation Research coverage, March 2026).
3. **Fusion agentic applications.** Oracle ships 600+ prebuilt AI agents inside Fusion Cloud Applications (ERP/HCM/CX), a low-code **AI Agent Studio** for building/extending them, and a marketplace with 100+ certified partner agents (Reported, Oracle/Constellation).

There is also a multicloud angle: Oracle Database@Azure/@Google/@AWS runs Oracle databases inside competitors' datacenters — the "your enterprise data, any cloud" play that feeds RAG/agent workloads.

## Founders & origins

Larry Ellison, Bob Miner, and Ed Oates, 1977 (Verified). Built the first commercial SQL relational database, inspired by Edgar Codd's IBM papers. Ellison remains chairman/CTO and the driving force behind the AI-infrastructure pivot. In September 2025 Safra Catz moved to vice chair and **Clay Magouyrk (ex-OCI head) and Mike Sicilia became co-CEOs** (Verified, widely reported).

## Funding

Public company (NYSE: ORCL), IPO March 1986 — no venture history to report. The material numbers: Q3 FY2026 (reported March 2026) revenue **$17.2B (+22% YoY)**; OCI infrastructure revenue **$4.9B (+84% YoY)**; **RPO $553B, up 325% YoY**, dominated by large-scale AI contracts (Verified, Oracle 8-K/investor release + CNBC). The single biggest driver: the **~$300B, ~4.5 GW OpenAI/Stargate agreement** (Verified, multiple outlets), with the flagship 1.2 GW Abilene, TX campus live on OCI. Note Oracle is funding this partly with tens of billions in new debt; capex intensity and customer concentration (OpenAI) are the standing bear cases (Reported).

## Evidence of real-world use

- **OpenAI trains on OCI** — the Stargate Abilene site is operational (Verified, Data Center Frontier/DCD). Meta, xAI, and NVIDIA have also been named as OCI AI-capacity customers in Oracle earnings materials (Reported).
- Oracle reported **97.5% global GPU utilization** and $67B in new contracts in Q3 FY2026 alone (Reported, Oracle CEO-office blog).
- **TIM Brasil** built call-center AI agents on OCI: 90% workflow accuracy, 30% faster service (Reported, Oracle case study — vendor-published but named and quantified).
- Long-standing at-scale OCI tenants: TikTok/ByteDance, Zoom (Verified, historical reporting).
- RPO of $553B is itself hard evidence of contracted (not aspirational) demand, though heavily concentrated.

## Relevance to agentic AI engineering

- **Tool-use & governance:** the Autonomous AI Database MCP Server is exactly the pattern discussed in *The Evolution of Tool Use in LLM Agents* — standardized tool access — and its database-enforced row/column security is a production instance of the *Governance by Construction for Generalist Agents* argument that guardrails belong in the substrate, not the agent.
- **Agent memory:** 26ai's pitch of "persistent memory + vector/graph/relational in one engine" competes directly with the dedicated stores surveyed in *Memory for Autonomous LLM Agents* and *GAM: Hierarchical Graph-based Agentic Memory*.
- **Voice agents:** TIM Brasil's contact-center deployment is the commercial setting that *LTS-VoiceAgent* and *τ-Voice* benchmark.
- **Compute layer:** if you train or fine-tune, OCI is now a first-tier alternative to AWS/Azure/GCP GPU capacity.

## Use cases & considerations

**Use cases:** (1) bare-metal GPU clusters for training/fine-tuning at better price/performance than hyperscaler on-demand; (2) if your enterprise data already lives in Oracle DB/Fusion, use AI Vector Search + the MCP Server instead of ETL-ing into a separate vector store; (3) prebuilt Fusion agents for finance/HR back-office automation; (4) Iceberg-native vector search over an existing lakehouse.

**Considerations:** deep lock-in on the database/apps side and famously aggressive licensing/audit culture; the AI story is capex- and debt-heavy with revenue concentrated in a few AI labs — counterparty risk cuts both ways; agentic features (26ai, Agent Studio) are new and mostly vendor-benchmarked. Competitors: AWS/Azure/GCP and neoclouds (CoreWeave, Crusoe) on compute; Postgres+pgvector, MongoDB, Pinecone on the data layer; SAP/Salesforce/Workday on agentic apps. Open question: what OCI margins look like on the OpenAI contracts.

## Sources

- https://www.datacenterfrontier.com/machine-learning/article/55316610/openai-and-oracles-300b-stargate-deal-building-ais-national-scale-infrastructure
- https://www.datacenterdynamics.com/en/news/openai-to-use-oci-for-ai-training-oracle-to-build-very-large-data-center/
- https://eu.36kr.com/en/p/3518250228046722 (Zettascale10)
- https://www.oracle.com/news/announcement/oracle-unveils-ai-database-agentic-innovations-for-business-data-2026-03-24/
- https://www.constellationr.com/insights/news/oracle-adds-agentic-ai-tools-oracle-ai-database-fusion-cloud-apps
- https://www.oracle.com/news/announcement/q3fy26-earnings-release-2026-03-10/
- https://www.sec.gov/Archives/edgar/data/0001341439/000119312526265848/orcl-ex99_1.htm
- https://www.cnbc.com/2026/03/10/oracle-orcl-q3-earnings-report-2026.html
- https://blogs.oracle.com/ceo/from-the-q3-earnings-call
- https://futurumgroup.com/insights/oracle-q3-fy-2026-earnings-driven-by-oci-ai-infrastructure-demand/
- https://www.ciodive.com/news/oracle-amd-nvidia-AI-infrastructure/802772/
- https://aimultiple.com/oracle-cloud-infrastructure

*Profile written 2026-07-02.*
