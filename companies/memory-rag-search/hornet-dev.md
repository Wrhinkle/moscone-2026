# Hornet.dev

> A retrieval engine built specifically for AI agents as the querying user — founded by core engineers from Vespa/Yahoo search — currently pre-launch.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** supporting
- **Founded:** 2025 (Reported — company registry/LinkedIn signals; exact incorporation date not found), Trondheim, Norway (Verified — Norwegian company registry, HORNET AS, Ferjemannsveien 10, Trondheim)
- **Website / GitHub:** https://hornet.dev · blog: https://hornet.dev/blog · No public GitHub org found as of 2026-07-02

## What they do

Hornet is building a retrieval engine whose primary "user" is an agent inside a reasoning loop, not a human typing keywords. Their argument (from the founding blog post "The case for a new retrieval engine for agents"): legacy search infrastructure was tuned for short human queries, millisecond latency, and top-ten snippets, while agents issue long structured queries in rapid succession, read whole documents, and trade latency for throughput and recall. Legacy stacks strain under that concurrency, volatile query mixes, and continuous indexing.

Concretely (Verified — company site and blog, though the product is pre-launch so all of this is claimed, not independently testable yet): schema-first, strongly typed APIs designed to cut agent tool-call errors and wasted tokens; a "verifiable API" with three validation layers (syntactic via OpenAPI, semantic across configuration combinations, behavioral via retrieval-quality metrics — "configurations are source files, API validation is the compiler, behavioral metrics are the tests"); support for exact case-sensitive matching (code) alongside semantic search (concepts) over structured and unstructured data together; read-optimized collections plus ephemeral "scratchpad" indexes for iteration; model-agnostic; deployable as managed service or on-premises. The site publishes agent-facing docs conventions (llms.txt, AGENTS.md, skill.md) but says "full capability details arrive at launch." No pricing page, no GA date found — this is a pre-launch infrastructure company (Verified as of 2026-07-02).

They explicitly position as a horizontal engine under agentic products (research tools, coding assistants) rather than competing with vertical agentic-search APIs like Exa, Tavily, Perplexity, or Parallel, which their own blog names as the adjacent web-search layer.

## Founders & origins

The team is the strongest verifiable asset — this is substantially the core Vespa lineage:

- **Jo Kristian Bergum** — CEO & co-founder (Verified — Luma event, The Org, LinkedIn). Formerly distinguished engineer at Vespa.ai and ~two decades at Yahoo/Vespa; one of the most-followed public voices on retrieval/RAG evaluation.
- **Henning Baldersheim** — CTO & co-founder (Reported — LinkedIn/search profiles). 20+ years at Yahoo and Vespa.ai, core Vespa engine committer focused on performance.
- **Erik Dyrkoren** — COO & co-founder (Verified — LinkedIn title). Three-time founder: CEO/co-founder of Blueye Robotics (Trondheim underwater drones), co-founder of Zeabuz; claims ~€28M raised across ventures.
- **Jon Marius Venstad** — named as co-founder in some profiles (Reported — single-source; also a long-time Vespa engineer).

Origin story: the Vespa team that ran web-scale search for billions of users at Yahoo concluding that agentic workloads justify a new engine rather than retrofitting Vespa/Elasticsearch-era infrastructure. Their jobs page claims the team "built search systems that serve billions of users" (company claim, but consistent with verified Vespa/Yahoo histories).

## Funding

Not found in public sources as of 2026-07-02. No Crunchbase/Tracxn/PitchBook round, no press release. A "HORNET TOPCO AS" holding entity exists in the Norwegian registry alongside HORNET AS (Verified), which usually indicates an investment structure, but investors and amounts are Unverified. Do not cite any figure.

## Evidence of real-world use

Essentially none yet — pre-launch. No named customers, case studies, public pricing, or GitHub adoption found. Real signals that exist: an active technical blog (Bergum authoring), a hiring page (11–50 employees per The Org, Reported), and a self-hosted "Retrieval for Agents" evening event in SF on June 29, 2026 co-located with AIEWF (Verified — Luma). Founder credibility is doing the work here, not usage data. Treat every capability claim as unproven until launch benchmarks or design-partner names appear.

## Relevance to agentic AI engineering

Hornet sits in the **retrieval-tool slot** of an agent stack — the internal/scoped-data complement to web-search APIs like Exa. Its thesis maps directly onto this repo's landscape: *Agentic Search in the Wild* (agent-issued query distributions differ from human ones — Hornet's entire founding premise), *The Evolution of Tool Use in LLM Agents* (their schema-first, verifiable-API design is a bet that reliable typed tools beat prompt-glued search), and *Do Agents Need Semantic Metadata? A Comparative Study in Agentic Data Retrieval* (machine-readable scoped context vs. snippets). The scratchpad/ephemeral-index concept touches the agent-memory thread, and their coding-assistant use case (exact-match code retrieval at scale) connects to the agentic-SWE benchmark work (*FeatureBench*, *OmniCode*) as the retrieval layer coding agents would call.

## Use cases & considerations

Potential use cases once launched: (1) retrieval backend for a document-heavy back-office agent (contracts, submittals, RFIs) needing exact + semantic search over one API; (2) code retrieval for repo-scale coding agents; (3) multi-agent systems needing high-concurrency retrieval without an Elasticsearch tuning project; (4) on-prem retrieval where data can't leave.

Considerations: unlaunched product — evaluate, don't adopt; funding/runway opaque; unclear OSS posture (Vespa pedigree suggests possible open core, but nothing published); Norway-based team selling into SF. Competitors: **Vespa.ai itself, Elastic, Turbopuffer, LanceDB, Chroma, Vectara, Pinecone**, plus per-model native retrieval. Open questions: pricing, benchmarks vs. Vespa/Elastic, and whether "agent-native retrieval" is a durable category or a feature the incumbents ship.

## Sources

- https://hornet.dev/
- https://hornet.dev/blog/the-case-for-a-new-retrieval-engine-for-agents
- https://hornet.dev/blog/how-we-build-a-retrieval-engine-for-agents
- https://www.hornet.dev/jobs
- https://luma.com/ypnd3grq (Retrieval for Agents event, SF, June 29 2026)
- https://theorg.com/org/hornet-dev
- https://virksomhet.brreg.no/en/oppslag/enheter/935080185 (Norwegian registry)
- https://www.linkedin.com/company/hornet-dev · https://www.linkedin.com/in/erik-dyrkoren-7741727/
- https://github.com/jobergum · https://github.com/baldersheim
