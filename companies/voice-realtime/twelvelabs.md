# TwelveLabs

> Video-native foundation models (embeddings + video-language) exposed as APIs, so software can search, analyze, and act on video the way LLMs act on text.

- **Category:** voice-realtime
- **AIEWF 2026 tier:** supporting
- **Founded:** 2021, San Francisco (Verified; founded by a Korean team, some databases list Seattle — the company is US-headquartered with strong Korea ties)
- **Website / GitHub:** https://www.twelvelabs.io — docs at https://docs.twelvelabs.io; SDKs/samples under https://github.com/twelvelabs-io

## What they do

TwelveLabs trains video-native foundation models rather than bolting frames onto an LLM. Two model families, three APIs:

- **Marengo** (currently 3.0, launched Dec 2025) is a multimodal embedding model that encodes visuals, motion, speech, and sound over time into a shared vector space. It backs the **Search API** ("any-to-any" retrieval — text/image/audio query to a video moment) and the **Embed API** (raw embeddings for your own vector store, hybrid search, or anomaly detection).
- **Pegasus** (currently 1.5) is a video-language model behind the **Analyze API**: prompt it against indexed video to get summaries, Q&A, chapters, or structured JSON metadata for downstream pipelines.

The practical integration: upload/index video, then query moments semantically ("person in red shirt enters the restaurant") instead of relying on manually logged metadata. Both models are also available on **Amazon Bedrock** (Verified — AWS blog, July 2025; TwelveLabs was the first video-understanding model family on Bedrock), and Elastic documents a Marengo-on-Bedrock integration for video embeddings. Alongside the July 2026 Series B, the company signed a multi-year deal to run inference on AWS Trainium and launch frontier models first on AWS (Verified).

## Founders & origins

Five co-founders (Verified across Tracxn/Crunchbase/press): **Jae Lee** (CEO), **Aiden Lee** (CTO), **Soyoung Lee** (Go-to-Market), **SJ (Sungjun) Kim**, and **Dave Chung**. Jae Lee studied CS at UC Berkeley and conceived the company during Korean military service in the Cyber Command, where searching video archives by hand exposed the gap in machine video understanding (Reported — TechCrunch, company blog). **Yoon Kim** — former SK Telecom CTO, described as an architect behind Siri — joined as President/CSO in late 2024 (Reported — TechCrunch).

## Funding

Total raised ≈ **$207M** (Verified — cited across Bloomberg/PYMNTS/company release, July 2026):

- **Seed, $5M**, led by Index Ventures, announced March 2022 (Verified)
- **Seed extension, ~$12M**, late 2022, Radical Ventures (Reported)
- **Strategic round, ~$10M**, Oct 2023 — NVIDIA's NVentures, Intel Capital, Samsung Next (Reported; NVentures participation confirmed in Series A release)
- **Series A, $50M**, June 2024, co-led by NEA and NVentures (Verified)
- **Strategic, $30M**, Dec 2024 — Databricks, Snowflake, SK Telecom, HubSpot Ventures, In-Q-Tel; total then $107.1M (Verified — TechCrunch)
- **Series B, $100M**, announced July 1, 2026, co-led by NEA and NAVER Ventures, with Amazon, Index, Radical, Korea Investment Partners, Red Bull Ventures (Verified — multiple outlets)

## Evidence of real-world use

- **MLSE (Maple Leaf Sports & Entertainment):** documented case study (TwelveLabs + AWS blog) — semantic search cut a 16-hour highlight retrieval job to ~9 minutes inside a generative video editor. This is real deployment, not a logo wall.
- **NFL Media:** named endorsement from its Senior Director of Media Management & Post Production (Reported — press release quote, not a published case study).
- **30,000+ developers** on the platform as of Dec 2024 (Reported — TechCrunch).
- **Partner ecosystem** (April 2026): Vidispine/Arvato Systems, EMAM, Quickplay, ScorePlay, Mux, Mimir, Nomad Media, MASV and others shipping integrations — MAM vendors embedding a product is stronger evidence than direct-sales claims.
- **In-Q-Tel investment** and reported municipal deployments (threat detection, traffic) signal public-sector traction (Reported).
- Distribution via Bedrock puts them inside AWS's commercial funnel (Verified).

## Relevance to agentic AI engineering

TwelveLabs is a **perception tool in an agent's toolbelt**: Search/Analyze/Embed are exactly the kind of typed, high-value tools that multi-tool agents orchestrate (see *The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration*). Pegasus's structured-JSON output turns video into agent-consumable metadata — directly the question posed by *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* — and Marengo embeddings can feed agent memory/retrieval layers of the sort surveyed in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*. The company itself is leaning in: a 2026 blog post, "Video Intelligence is Going Agentic," positions the APIs for retrieval-plus-reasoning agent loops. Note the category caveat: this is **video** understanding, not voice — it sits adjacent to realtime voice/multimodal agents (audio and speech are modeled, but there's no realtime conversational product like the *τ-Voice*/full-duplex work covers).

## Use cases & considerations

Use cases: (1) semantic search over site/jobsite/security footage archives; (2) auto-generating highlight or documentation clips from long recordings; (3) video QA/metadata extraction feeding a RAG or agent pipeline; (4) content moderation and contextual ad placement.

Considerations: proprietary hosted models — no open weights, so embedding lock-in is real (re-indexing cost if you leave). Indexing large archives has meaningful cost/latency; pricing is usage-based via the platform/Bedrock (public playground and self-serve signup exist — a real commercial product, but budget modeling requires testing). Competitors: Google Gemini's long-context video, OpenAI's multimodal models, AWS Nova, and open-source VLMs (Qwen-VL, InternVideo); TwelveLabs' bet is that video-native temporal modeling beats frame-sampled LLMs. Open questions: how defensible that bet stays as frontier LLMs improve on video, and how deep the AWS dependency (Trainium, Bedrock-first) cuts both ways.

## Sources

- https://techcrunch.com/2024/12/12/twelve-labs-is-building-ai-that-can-analyze-and-search-through-videos/
- https://www.globenewswire.com/news-release/2026/07/01/3320545/0/en/twelvelabs-raises-100-million-in-series-b-funding-to-build-video-superintelligence.html
- https://www.pymnts.com/news/investment-tracker/2026/twelve-labs-raises-100-million-to-fund-bet-on-video-ai/
- https://www.bloomberg.com/news/articles/2026-07-01/video-search-startup-raises-100-million-from-amazon-vc-funds
- https://www.prweb.com/releases/twelve-labs-earns-50-million-series-a-co-led-by-nea-and-nvidias-nventures-to-build-the-future-of-multimodal-ai-302163279.html
- https://medium.com/twelve-labs-blog/to-make-the-worlds-videos-searchable-twelve-labs-raises-5m-a77d9f5257ef
- https://tracxn.com/d/companies/twelve-labs/__eZXrk6YPamabNtuA7HzJhUEnE2Tu0OTrBAOris8TVJs
- https://www.twelvelabs.io/product/models-overview
- https://aws.amazon.com/blogs/aws/twelvelabs-video-understanding-models-are-now-available-in-amazon-bedrock/
- https://press.aboutamazon.com/aws/2025/12/twelvelabs-launches-its-most-powerful-video-understanding-model-marengo-3-0-on-twelvelabs-and-amazon-bedrock
- https://www.twelvelabs.io/case-studies/mlse
- https://aws.amazon.com/blogs/media/maple-leaf-sports-entertainment-debuts-generative-ai-video-editor-to-deliver-content-to-fans-faster/
- https://www.prweb.com/releases/twelvelabs-launches-ecosystem-partner-program-to-extend-video-intelligence-in-the-enterprise-302731801.html
- https://www.elastic.co/search-labs/blog/twelvelabs-marengo-video-embedding-amazon-bedrock
- https://www.twelvelabs.io/blog/video-intelligence-is-going-agentic
