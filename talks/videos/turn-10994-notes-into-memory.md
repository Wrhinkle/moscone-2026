# Turn 10,994 Notes Into Memory

> Two educators show an open-source "AI research OS" that turns a 10,000-note second brain into an agent-queryable wiki built from plain markdown files, no vector database required.

- **Speakers:** Paul Iusztin, Decoding AI, and Louis-François Bouchard, Towards AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ZRM_TfEZcIo) (AI Engineer channel; ~40m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Iusztin, founder of Decoding AI and co-author of the LLM Engineer's Handbook, opens with the problem: 18 months spent turning his second brain, over 5,000 Obsidian notes plus another 5,000 in Readwise and more in Notion and Google Drive, growing 250 files a month, into something that surfaces high-signal notes when he starts an article, project, or codebase. Bouchard, co-founder and CTO of Towards AI and creator of the What's AI channel, frames the tool-selection logic: quick questions go to ChatGPT, one-off coding tasks go to Codex or Claude Code, NotebookLM digests content well but you do not own it, it is not agent native, and it is weak for coding. Production RAG stacks with vector databases are powerful at scale but hard to inspect by hand and heavy for a personal system. Their answer is a personal research OS, shipped as an AI Research OS workshop repo of Claude Code plugins and skills that also work in Codex, with connectors for Obsidian, Readwise, NotebookLM, GitHub repos, YouTube transcripts, and web links.

Iusztin walks the system's three versions and why each added complexity. V1 was scoped to generating lessons for their agent engineering course: a topic plus hand-picked golden links seeds a classic deep research loop, an orchestrator spawns sub-agents that query Google through Gemini grounding, three rounds of six queries yield 40 to 50 links, a ranking step scores each source against the topic, only the top K get fully scraped, and everything compiles into a static research markdown file. It generated 35 lessons quickly. V2 aims the same loop at the second brain itself, so the golden links come organically from sources the authors already filtered, alongside the public web. V3 addresses the remaining flaw, that a static research file forces a full expensive rerun for every follow-up question, by adding a wiki layer.

The V3 architecture is deliberately database-free. Iusztin tells the audience to forget vector databases, knowledge graphs, and semantic search for personal systems: everything is files and references. An index.yaml catalogs every source with summary and metadata and serves as the agent's entry point. Raw files are immutable. The wiki folder holds LLM-generated derivatives: per-source executive summaries, extracted concepts and entities, comparisons, and open questions. Querying follows a token-efficient hierarchy, index first, then the source wiki page, then wiki derivatives, and only as a last resort the full raw source. Every question leaves a trace, since answers can spawn new concept, note, or comparison files, so the wiki evolves through conversation as well as ingestion. The wiki sits apart from the second brain itself; Iusztin organizes his vault with Tiago Forte's PARA method and treats Obsidian as an immutable snapshot the LLM never edits.

The demos cover three scales: building a wiki on agentic harness engineering from a brain dump plus references, with light mode running one round of three queries in 10 to 20 minutes; ingesting the opencode, Pi, and Hermes harness repos and generating per-repo architecture notes plus cross-repo comparisons of permission flows and memory systems; and a minimal three-link ingestion needing nothing but git and curl. Bouchard closes with the known gaps, missing connectors, weak source provenance and staleness detection, terminal-only UX, and says they are by design, since the repo exists to teach memory and context management, with the polished version taught in their roughly 60-hour Agent Engineering course.

## Notable moments

- [0:12:07](https://www.youtube.com/watch?v=ZRM_TfEZcIo&t=727s) The three-layer design named: raw content, index, and a wiki of synthesized derivatives
- [0:18:10](https://www.youtube.com/watch?v=ZRM_TfEZcIo&t=1090s) Why static research files fail and V3 adds the wiki layer
- [0:19:12](https://www.youtube.com/watch?v=ZRM_TfEZcIo&t=1152s) The case against personal vector databases: plain files and an index.yaml instead
- [0:31:22](https://www.youtube.com/watch?v=ZRM_TfEZcIo&t=1882s) Demo of auto-extracted concepts, entities, and comparisons from ingested harness repos

## Connections

- [Towards AI](../../companies/vc-community/towards-ai.md): Bouchard's company, whose Academy hosts the Agent Engineering course this system feeds
- [Bright Data](../../companies/memory-rag-search/bright-data.md): named in the talk as the tool for parsing single-page applications and arbitrary public URLs into the wiki
- [Are we ready for an agent-native memory system](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): the research framing of the same question this talk answers with files and indexes
- [Session recaps](../../notes/session-recaps.md): memory beyond vector similarity was a recurring in-person theme, from GraphRAG traversal to world models
