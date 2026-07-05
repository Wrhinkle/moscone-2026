# Braintrust

> Eval-first platform for building LLM products: log every trace from production, turn traces into datasets, score outputs with code or LLM judges, and gate releases on eval results.

- **Category:** evals-observability
- **AIEWF 2026 tier:** platinum
- **Founded:** 2023, San Francisco (Verified — company blog, press)
- **Website / GitHub:** https://www.braintrust.dev · https://github.com/braintrustdata

**Disambiguation:** not the freelance talent network "Braintrust" (usebraintrust.com). This is Braintrust Data, the AI evals/observability devtool — the AIEWF sponsor.

## What they do

Braintrust is an evaluation and observability platform for LLM applications. The core loop: you instrument your app with their TypeScript/Python SDK (an `Eval()` harness plus tracing), production logs capture full traces — prompts, tool calls, retrieved context, latency/cost metadata — and any trace can be promoted into a dataset with one click. You then run experiments that score outputs against those datasets using ~25 built-in scorers or custom ones, including LLM-as-judge, and diff results across prompt/model versions. A GitHub Action ("Braintrust eval") runs evals in CI so regressions block merges — the "evals as unit tests" posture is their defining pitch.

Around that core: **Playgrounds** for side-by-side prompt/model comparison against real production examples; prompt management with real-time serving; an **AI proxy** (MIT-licensed, open source) exposing an OpenAI-compatible API across providers with caching, deployable to Vercel/Cloudflare/Lambda; **autoevals**, their open-source scorer library (heuristic, statistical, and model-graded metrics); an MCP server that connects coding agents to your eval stack from the IDE. In 2025 they shipped **Loop**, an agent that analyzes production traces from natural-language failure descriptions and generates eval datasets, scorers, and prompt improvements automatically. Enterprise deployments can run hybrid/self-hosted (data plane in your VPC).

Public pricing (Verified, pricing page 2026-07): free Starter (1 GB processed data, 10k scores, 14-day retention), Pro at $249/mo, custom Enterprise with on-prem option.

## Founders & origins

**Ankur Goyal**, founder and CEO (Verified). Dropped out of CMU to join MemSQL/SingleStore's founding team (rose to VP Engineering); founded **Impira** (document/data extraction ML), acquired by Figma in 2022; then led Figma's AI team. He founded Braintrust in 2023 after building internal eval tooling twice — at Impira and Figma — and concluding the problem was universal (Verified across podcasts/press). No other co-founders are prominently documented in public sources.

## Funding

- **Seed, Dec 2023:** $5.1M led by Saam Motamedi (Greylock); Elad Gil, Basecase, SV Angel, Box Group; total then ~$8.3M implying a small pre-seed (Verified).
- **Series A, 2024:** $36M led by Martin Casado (a16z); participants included Greylock, Elad Gil, Databricks Ventures, Datadog, and angels Guillermo Rauch (Vercel), Simon Last (Notion), Bryan Helmig (Zapier), Greg Brockman, Arthur Mensch. Total ~$45M (Verified).
- **Series B, Feb 2026:** $80M led by ICONIQ at **$800M post-money**; a16z, Greylock, Elad Gil returning (Verified — Axios, SiliconANGLE, company blog).
- **Total raised:** ~$121–125M (Verified within rounding).

Notable: Datadog — a direct future competitor in LLM observability — invested in the Series A.

## Evidence of real-world use

Strong. Named customers across independent press and company posts: **Notion, Stripe, Vercel, Zapier, Airtable, Instacart, Coda, The Browser Company, Replit, Cloudflare, Ramp, Dropbox** (Verified for the recurring core set — Notion, Stripe, Vercel, Zapier appear consistently since the Series A; Replit/Cloudflare/Ramp/Dropbox Reported via Series B press). Customer angels (Rauch, Last, Helmig) investing is a usage signal, not just a logo wall. OSS footprint (autoevals, braintrust-proxy, SDKs, cookbook) is real but modest — star counts not confirmed; the proxy is free without an account. Public pricing page with usage-based overages = real self-serve commercial motion.

## Relevance to agentic AI engineering

Braintrust sits at the evals/observability layer of the agent stack — the tooling counterpart to this repo's agentic-SWE benchmark papers (*SWE-EVO*, *SlopCodeBench*, *ProdCodeBench*, and *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*): those papers define what to measure on long-horizon coding agents; Braintrust is where a team would operationalize such trace-level scoring in CI. Its full-trace capture of tool calls connects to *The Evolution of Tool Use in LLM Agents* and the audit-trail needs in *Governance by Construction for Generalist Agents*. Eval-dataset curation from production traces is the same discipline *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation* argues for in voice agents. Loop itself is an agent doing eval engineering — an emerging meta-pattern.

## Use cases & considerations

Use cases: (1) CI eval gates for a coding/back-office agent (e.g., scoring a job-packet auditor's structured JSON against golden datasets); (2) production trace triage → dataset building for multi-step tool-calling agents; (3) model/prompt migration testing via Playgrounds + proxy; (4) LLM-as-judge scoring pipelines with human review queues.

Considerations: SDK/platform lock-in is moderate (proprietary core; proxy and autoevals are open, unlike Arize's OSS-first Phoenix or Langfuse). Competitors: **LangSmith, Arize AX/Phoenix, Langfuse, W&B Weave, Datadog LLM Observability, Galileo**. Usage-based pricing (per-GB, per-score) can climb with high-volume agent traces. Open questions: OTel-standard interop depth, and how defensible eval tooling is as model providers absorb it.

## Sources

- https://www.braintrust.dev/ and https://www.braintrust.dev/pricing
- https://www.braintrust.dev/blog/seed-round · https://www.braintrust.dev/blog/announcing-series-a · https://www.braintrust.dev/blog/announcing-series-b
- https://www.braintrust.dev/blog/loop · https://www.braintrust.dev/blog/open-sourcing-proxy
- https://www.axios.com/pro/enterprise-software-deals/2026/02/17/ai-observability-braintrust-80-million-800-million
- https://siliconangle.com/2026/02/17/braintrust-lands-80m-series-b-funding-round-become-observability-layer-ai/
- https://a16z.com/announcement/investing-in-braintrust/
- https://www.latent.space/p/braintrust · https://review.firstround.com/podcast/what-braintrust-got-right-about-product-market-fit/
- https://github.com/braintrustdata/autoevals · https://github.com/braintrustdata/braintrust-proxy
- https://www.maginative.com/article/braintrust-secures-5m-seed-round-to-build-ai-infrastructure/
