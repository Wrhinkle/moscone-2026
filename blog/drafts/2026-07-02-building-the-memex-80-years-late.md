---
title: "Building the Memex, 80 Years Late, with Off-the-Shelf Parts"
date: 2026-07-02
description: "Vannevar Bush's 1945 Memex is now a weekend assembly problem: crawl, search, extract, graph memory, weekly synthesis. The parts are commodity. The design decisions are not."
tags: [agents, memory, knowledge-graphs, research-agents, memex, aiewf]
draft: true
sources:
  - briefs/2026-07-02-aiewf-batch-01.md (brief #8)
  - notes/conference-notes-raw.md
  - notes/source-map-aiewf-2026.md
  - companies/memory-rag-search/firecrawl.md
  - companies/memory-rag-search/exa.md
  - companies/memory-rag-search/bright-data.md
  - companies/memory-rag-search/apify.md
  - companies/memory-rag-search/oxylabs.md
  - companies/memory-rag-search/zep-ai.md
  - companies/memory-rag-search/cognee.md
  - companies/memory-rag-search/neo4j.md
  - companies/memory-rag-search/falkordb.md
  - companies/memory-rag-search/lancedb.md
  - papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md
  - papers/memory-research-agents/gam-hierarchical-graph-based-agentic-memory-for-llm-agents.md
  - papers/memory-research-agents/hierarchical-long-term-semantic-memory-for-linkedin-s-ai-age.md
  - papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md
  - papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md
  - papers/memory-research-agents/towards-autonomous-memory-agents.md
---

Somewhere on day two of the AI Engineer World's Fair, standing on the Moscone West expo floor, I typed this into my notes, verbatim:

> Firecrawl model that tracks headlines, articles, podcasts, video series for specific engineers or ceos and does a weekly writeup of topics discussed and anything theyre pushing as next step

Two lines below it: "Memex." One line after that: "Knowledge navigator."

That's the whole post, honestly. The idea I scribbled between booths — an agent that follows specific people across the web and tells me every Monday what changed — is the thing Vannevar Bush described in *The Atlantic* in July 1945, in "As We May Think." He called it the Memex: a desk that stores everything its owner reads, lets them tie any two items together into named associative trails, and lets them walk those trails later, the way a mind does. Bush imagined microfilm and dry photography. Eighty years later the parts are HTTP APIs with public pricing pages, and several of them had booths within a hundred feet of where I was standing.

So this is a build post with a 1945 spec sheet. The claim I want to defend: every component of the Memex is now commodity, the assembly is a weekend, and the only genuinely hard problems left are the two Bush couldn't have anticipated — deciding what deserves memory, and keeping that memory from rotting. The research on the second problem is newer than most of the vendors selling around it.

## Trails, not search

It's worth being precise about what Bush proposed, because "the Memex predicted the internet" flattens it into nothing.

Bush's core complaint was that indexing is artificial. Libraries file by alphabet and subject hierarchy; the mind doesn't. "The human mind... operates by association," he wrote — one item snaps to the next because they were linked by the thinking, not because they share a call number. <!-- TODO: verify exact quote wording against the Atlantic original before publishing --> The Memex's central mechanism was therefore not lookup but the **trail**: the owner views two items side by side, taps a key, and they are permanently joined. Follow the trail years later and you retrace the reasoning, not just the sources. Bush even predicted a profession of "trail blazers" — people whose product was useful paths through the record rather than new documents.

Map that onto 2026 vocabulary and the correspondence is uncomfortably tight:

- Storing everything the owner reads → ingestion and crawling
- The record of items → a document store with embeddings
- Trails — typed, durable associations between items → edges in a knowledge graph
- Walking a trail → multi-hop graph traversal
- Trail blazers → the extraction layer that decides which associations are worth making

Notice what's *not* in the spec: search. Bush assumed getting a document was the easy part and connecting it was the hard part. The last twenty-five years of the web inverted that — we got planetary-scale retrieval and almost no durable association. Every "I built a news summarizer" project recapitulates the inversion: great at fetching, amnesiac about structure. The Memex framing is useful precisely because it forces you to build the association layer, which is the part that was missing from my notes app and yours.

## The 2026 parts list

Here's the expo-floor observation that convinced me this is now a build and not a paper: the memory tier showed up as *sponsors*. Zep AI (supporting tier), Cognee (bronze), FalkorDB (bronze), LanceDB (bronze) all bought booths at AIEWF 2026, with Neo4j at platinum repositioning its entire pitch around GraphRAG and agent memory. Companies don't buy conference booths for research topics; they buy them for product categories. Memory crossed that line sometime in the last eighteen months.

The Memex components, slot by slot, with what I verified about each while building out the research repo:

**Acquisition (Bush's camera and microfilm feed).** Firecrawl turns URLs into LLM-ready markdown or schema-driven JSON — its core repo sits around 145k GitHub stars, among the most-starred AI infra projects anywhere, on a comparatively tiny $16.2M raised. For podcast pages, video descriptions, and conference talks, its Extract endpoint ("describe the fields, it finds them") is the workhorse. If you need industrial scale or hostile targets, Bright Data (which won summary judgment against Meta over scraping public data, and ships an MCP server with a 5,000-request free tier), Apify (~48,000 prebuilt scrapers as rentable "Actors"), and Oxylabs occupy the heavy end. For a five-person tracker you won't need them; it's worth knowing the ceiling exists.

**Discovery (the part Bush skipped).** Exa is a search index built for agent callers rather than human clickers — embeddings-based retrieval, an Answer API with citations, and Websets, which returns structured entity tables instead of links. It raised a $250M Series C at a $2.2B valuation in May 2026, which tells you what the market thinks agent-issued queries are worth. Its "instant" tier runs around 180ms, which matters later when we talk latency budgets.

**The record (Bush's storage desk).** LanceDB gives you an embedded, file-based vector store — no server, data on local disk or S3 — which is the right shape for a personal Memex the same way SQLite is the right shape for a personal database. Midjourney and Character.AI run it at scale; you can run it in-process.

**Trails (the actual invention).** This is the graph-memory slot, and it's the crowded one. Zep's open-source engine Graphiti (28.4k GitHub stars) builds a *temporal* knowledge graph: facts carry validity windows, and when new information contradicts an old fact, the old fact is invalidated rather than deleted — current state stays queryable while provenance survives. Cognee (Apache 2.0, ~27.1k stars, $9M raised) runs an ingestion pipeline that extracts entities and relationships into a hybrid graph+vector index, plus a maintenance operation, `memify`, that prunes stale nodes and reweights edges from usage. Underneath either, you need a graph database: Neo4j if you want the incumbent (84 of the Fortune 100, per company claims), FalkorDB if you want latency — it stores graphs as sparse adjacency matrices and compiles traversals to linear algebra, and its one strong public case study (Securin) is exactly this workload: agents doing 7-hop traversals inside a 5-second SLO, query latency cut from 1.5s to 0.3s. Graphiti officially supports FalkorDB as a backend, so the two snap together.

**Synthesis (the trail blazer).** A weekly LLM pass over the graph. No vendor needed; this is a prompt and a cron job.

None of these components existed in usable form three years ago. All of them now have public pricing, MCP servers, and named production customers. That's what "commodity" means.

## The build, stage by stage

Here's the concrete build — the weekly signal-intelligence agent from my backlog. Framed honestly: this is the build plan, not a retrospective. The Job Packet Readiness Auditor got built first because it pays for itself at a construction company; this one is the personal-infrastructure follow-up, and this post is me committing to it in public.

**Scope.** Track five named people — engineers and CEOs whose technical bets I want to follow (the note said "specific engineers or ceos"; pick yours). Sources: their essays, interviews, podcast appearances, conference talks, launch posts. Output: one Monday brief.

**Stage 1 — Acquisition.** A scheduled job (a plain cron hitting a Python script is fine; resist orchestration frameworks at n=5) runs two collectors per person: an Exa search scoped to the trailing seven days for mentions, appearances, and authored pieces, and Firecrawl Scrape against a hand-curated list of each person's home surfaces — blog, podcast feed pages, talk listings. Everything lands in LanceDB with embeddings and raw markdown. Cost at this scale is trivially inside free tiers plus a few dollars.

**Stage 2 — Extraction.** For each new document, one structured-output LLM call produces typed records: `(person, claim, stance, quote, source_url, date)` plus entity mentions (companies, projects, other people). This is the trail-blazer step, and the schema *is* the product decision. I'm deliberately extracting claims-with-stances ("X argues evals are the bottleneck") rather than topics ("X discussed evals"), because stances can contradict each other later and contradictions are the signal.

**Stage 3 — Trails.** Extracted records go into Graphiti running on FalkorDB — self-hosted, both open enough to walk away from. Each person is a subgraph root; claims attach to people; entities attach to claims. Two research findings shape this stage. First, GAM (arXiv:2604.12285) found that consolidating into structured memory *in batches at semantic boundaries* beats writing to the graph on every item — their ablation showed the cheap append-only event buffer was worth −37.4% F1 when removed, the single biggest component. Translated: buffer the week's extractions, consolidate into the graph once per week, don't stream-write. Conveniently, a weekly brief gives you a natural consolidation boundary; the product cadence and the memory-architecture recommendation are the same thing. Second, LinkedIn's production memory paper (KDD 2026) found that structuring the hierarchy around *ownership* rather than semantic clusters got them structural isolation — 0.0% cross-tenant leakage versus 30–92% for baselines — plus cheaper retrieval from precomputed multi-view summaries. My version of ownership topology is person-rooted subgraphs: every fact hangs off the human it belongs to, and "what is Person X pushing" becomes a subtree read, not a global search.

**Stage 4 — Synthesis.** Monday morning, a job walks each person's subgraph and diffs it against last Monday's state: new claims, invalidated claims (Graphiti's temporal mechanism does the bookkeeping), new edges between tracked people, entities rising across multiple subgraphs. An LLM turns the diff into prose. The brief reports the *delta*, which brings us to the design opinion.

## Deltas beat summaries

Most "AI research agent" output is a summary: here's what was published this week, compressed. Summaries answer "what happened?" — but if you're tracking people over months, the question you actually have is "what *changed*?" Did she stop talking about the thing she spent all spring on? Did two people who never overlapped suddenly both start using the same phrase? Is this week's position a repetition, a sharpening, or a reversal?

A summarizer can't answer those, structurally, because it's stateless — each week's output is a function of each week's inputs. Deltas require a persistent representation that supports comparison, which is precisely what the temporal graph provides. Zep's invalidate-don't-delete mechanism means "changed since last week" is a query over validity windows, not an LLM squinting at two summaries. The graph isn't there because graphs are fashionable; it's there because the diff is the product and you can't diff what you didn't persist.

The field-study data says stateless is also the default failure mode of research agents generally. "Agentic Search in the Wild" (SIGIR 2026) analyzed 14.4M real agent search requests: 88.64% were declarative fact-seeking, retrieval depth was hardcoded in 91.64% of sessions, and fact-seeking sessions degenerated into near-duplicate query loops — a 42.68% repetition rate by step nine. Agents grind the same queries because nothing accumulates between steps. The paper's most encouraging number cuts the other way: about 54% of productive new query terms were traceable to evidence the agent had *already retrieved*, with earlier-than-last-step evidence contributing a measurable +5.81 points. Memory isn't a nice-to-have for research agents; it's where their next good query comes from. Bush said the same thing with different units: the trail, not the fetch, is where thinking lives.

## What breaks in a month

Now the part the demo posts skip. The memory literature is blunt about where this build degrades, and the timeline is roughly one month.

**The recall/use gap.** The memory survey (arXiv:2603.07670) collates a brutal result: systems near-perfect on passive recall benchmarks drop to 40–60% task completion when they must *act* on information from prior sessions. My mitigation is architectural modesty — the agent's only cross-session action is producing a diff report for a human. But it means I should evaluate the system on "did the brief catch the change?" not "can it answer questions about the archive?"

**The cost asymmetry.** "Are We Ready For An Agent-Native Memory System?" (arXiv:2606.24775) benchmarked twelve memory systems and found graph-based ones (Zep and Cognee among them) hitting the top utility scores at 116–155 *seconds* per query, while lightweight systems ran 3.67s at two-thirds the utility. At five people and one synthesis run a week, I can afford expensive queries — that's the trick of the weekly cadence. But this number kills any fantasy of the same architecture powering an interactive assistant without a serious latency-engineering pass (the survey's separate 200–500ms retrieval-tax figure is the interactive-path version of the same warning).

**Temporal rot.** The same benchmark found embedding RAG collapsing as the gap between question and evidence grows — 37.1 to 7.4 F1. A tracker whose whole value is longitudinal cannot lean on vector search for time-dependent questions; the graph has to carry them. This is the strongest empirical argument that the trails layer isn't optional for this use case, whatever it costs.

**Forgetting is unsolved.** The survey calls selective forgetting the near-universal failure across memory systems, and recommends shipping expiration policies and human-visible memory audits instead of trusting the system to prune itself. Cognee's `memify` and Graphiti's invalidation are real mechanisms, but both papers' advice converges on the same practice: maintenance should be *localized and incremental* (the agent-native paper found this strictly more cost-efficient than global rebuilds), and a human should periodically see what the graph believes. So the brief gets an appendix: "facts I'm still carrying about you that haven't been reconfirmed in 60 days." Bush's owner pruned trails by hand. Mine will too, just with better tooling.

The honest summary of all four: the components are commodity, but *curation* — what enters memory, what leaves, who checks — is the actual engineering, and it's the one part with no booth at the expo.

## The four-week experiment

Bush ended his essay predicting new encyclopedias "ready made with a mesh of associative trails running through them." <!-- TODO: verify exact quote wording --> What he couldn't predict was that the mesh-building would become the cheap part and the judgment about which trails deserve to exist would stay expensive — because the judgment was always the human contribution, even in his microfilm version. The trail blazer was a *person* in the 1945 spec. In mine, the extraction schema is where that person's judgment got encoded, and it's the component I expect to rewrite most.

So, the experiment, stated falsifiably before I run it: four weeks, five tracked people, one brief per Monday. Metrics — (1) how many brief items I act on (open, forward, or change a decision because of); (2) how many claims in the graph get invalidated by later evidence, which measures whether the temporal machinery is earning its cost; (3) what fraction of week-four's graph is 60-day-stale, which measures the rot rate the papers predict. If the deltas-not-summaries thesis is right, metric (1) should *rise* over the four weeks as the graph accumulates enough history to make comparisons — a summarizer's usefulness would stay flat. If it stays flat anyway, then the Memex's missing ingredient wasn't parts or even curation, and eighty years of waiting taught us less than I think.

Results post in August, either way.
