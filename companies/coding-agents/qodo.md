# Qodo

> AI code review and code-quality platform: agents that review, test, and govern code (increasingly AI-generated code) rather than write it.

- **Category:** coding-agents
- **AIEWF 2026 tier:** platinum
- **Founded:** 2022, Tel Aviv, Israel (Verified; now often described as NYC-based with a large Tel Aviv office)
- **Website / GitHub:** https://www.qodo.ai · https://github.com/qodo-ai (open-source lineage: https://github.com/qodo-ai/pr-agent)

## What they do

Qodo (formerly CodiumAI) sells a "code integrity" layer for the SDLC: instead of competing with Copilot/Cursor on code generation, its agents sit downstream and verify what humans and coding agents produce. The current platform ("Qodo 2.0," released February 2026) is an agentic code review system that fans a pull request out across multiple specialized agents — one for logic errors, one for security, one for performance regressions — and merges their findings into a single review, filtered against the organization's own standards.

Concretely, you integrate it three ways: a Git-host app (GitHub/GitLab, with partial Bitbucket/Azure DevOps support) that reviews PRs automatically; IDE plugins (VS Code, JetBrains) for local review and test generation; and a CLI for wiring review agents into CI or terminal-based agent workflows. Under the hood a "Context Engine" indexes multi-repo codebases so reviews are judged against how a change affects the whole system plus historical decisions, not just the diff. Earlier separately-branded products (Qodo Merge, Qodo Gen, Qodo Command, Qodo Aware, Qodo Cover for test coverage) have been folded into this unified platform. Enterprise options include air-gapped deployment and an AWS Marketplace listing.

Their pitch, post-2025, is explicitly about the AI-slop problem: as agents like Claude Code generate more code, review becomes the bottleneck, and Qodo wants to be the automated verification/governance layer. CEO Friedman's framing: "Quality is subjective. It depends on organizational standards, past decisions, and tribal knowledge" — i.e., the moat is learning org-specific review policy, not generic linting.

## Founders & origins

- **Itamar Friedman (CEO):** previously a director at Alibaba's Israeli AI lab (machine vision). Verified across Wikipedia, TechCrunch, PR.
- **Dedy Kredo (CPO):** previously led product/data-science teams at VMware and Exploriem. Verified.

Founded 2022 as CodiumAI; rebranded to Qodo in September 2024 (partly to avoid confusion with the unrelated Codeium). Origin story: started with AI test generation ("Codiumate"), then expanded into PR review via the open-source PR-Agent, which became the wedge product.

## Funding

- **Seed, 2023:** $11M — TLV Partners, Vine Ventures; angels associated with OpenAI and VMware (Verified).
- **Series A, Sept 2024:** $40M — co-led by Susa Ventures and Square Peg, with Firestreak, ICON Continuity Fund, TLV Partners, Vine Ventures (Verified — TechCrunch, PRNewswire).
- **Series B, March 2026:** $70M — led by Qumra Capital; Maor Ventures, Phoenix, S Ventures, Square Peg, Susa, TLV, Vine, plus angels Peter Welinder (OpenAI) and Clara Shih (Meta) (Verified — TechCrunch, Calcalist).
- **Total raised:** $120M (Verified). Valuation: not disclosed in public sources.

## Evidence of real-world use

- **Named customers (as of 2026):** Nvidia, Walmart, Red Hat, Intuit, Texas Instruments, Monday.com (Verified via TechCrunch Series B coverage); Box, Ford also reported. "500,000+ developers" served (Reported — company/press figures).
- **Documented case studies:** Monday.com — 800+ potential issues caught monthly, 73.8% suggestion acceptance rate, up to 1 hour saved per PR (Reported — Qodo-published case study, so treat numbers as vendor-sourced). Nvidia — collaboration on code-search/RAG for Nvidia's internal "Genie" system, written up on Nvidia's own developer blog (Verified — independent source).
- **OSS:** PR-Agent, ~11.9k stars / 1.6k forks, Apache-2.0; notably Qodo donated it to a community-owned org in 2025-26, signaling a shift to the commercial platform.
- **Analyst/benchmark signals:** Gartner MQ "Visionary" for AI code assistants (2025); #1 on Martian's Code Review Bench at 64.3% (Reported — vendor-cited benchmark; methodology worth checking).

## Relevance to agentic AI engineering

Qodo occupies the verification/governance slot of the agentic SDLC stack — the counterweight to autonomous code generation. It maps directly onto this repo's agentic-SWE benchmark thread: *SlopCodeBench* (long-horizon degradation of coding agents) and *ProdCodeBench* describe exactly the failure modes Qodo monetizes, and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* echoes their argument that quality is org-contextual, not benchmark-generic. Their multi-agent review architecture is a production instance of *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*; the policy-enforcement angle connects to *Governance by Construction for Generalist Agents*; and the Context Engine (multi-repo, historical decisions) is applied agent memory in the spirit of *Memory for Autonomous LLM Agents* and the graph-based memory work.

## Use cases & considerations

Use cases: (1) automated PR review gate for teams drowning in agent-generated PRs; (2) enforcing org-specific coding standards ("tribal knowledge") as reviewable policy; (3) test-coverage generation on legacy code; (4) air-gapped review for regulated enterprises.

Considerations: the open-source escape hatch (PR-Agent) is now community-maintained and diverging from the paid platform, so evaluate lock-in on the commercial tier. Vendor-published metrics dominate the case studies. Crowded market: direct competitors include CodeRabbit, Graphite (Diamond), Greptile, Cursor Bugbot, GitHub Copilot code review, and Claude Code's review features. Open question: whether review can stay a standalone layer or gets absorbed into the generation platforms.

## Sources

- https://en.wikipedia.org/wiki/Qodo
- https://techcrunch.com/2026/03/30/qodo-bets-on-code-verification-as-ai-coding-scales-raises-70m/
- https://techcrunch.com/2024/09/30/qodo-raises-40m-series-a-to-bring-quality-first-code-generation-to-the-enterprise/
- https://www.prnewswire.com/news-releases/qodo-formerly-codiumai-raises-40m-amid-strong-adoption-of-its-quality-focused-ai-coding-platform-302262380.html
- https://www.finsmes.com/2026/03/qodo-raises-70m-in-series-b-funding.html
- https://www.calcalistech.com/ctechnews/article/r1qdnboswx
- https://github.com/qodo-ai/pr-agent
- https://www.qodo.ai/ (product/platform pages)
- https://docs.qodo.ai/code-review
- https://developer.nvidia.com/blog/spotlight-qodo-innovates-efficient-code-search-with-nvidia-dgx/
- https://aws.amazon.com/marketplace/pp/prodview-efyzjxseyzaxi
