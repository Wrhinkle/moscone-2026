# Enterprise Adopters

Large enterprises, consumer platforms, and institutions that show up at AIEWF 2026 as **AI adopters and hosts, not AI-tooling vendors**. Nothing in this folder is a product you'd `pip install`. These companies are the demand side of the agent economy: retrofitting agents onto decades-old marketplaces, rebuilding SDLCs around coding agents, exposing their product surfaces to other people's agents via MCP, or shipping LLM features to hundreds of millions of consumers. The real-world problem this category answers is the one every builder eventually faces: whether any of this agent stuff survives contact with production, compliance, and an existing business. These profiles are the evidence base, with deployment patterns, published architectures, and hard(ish) business metrics from organizations that had to make it work rather than sell it.

## How to read this category

Start with the three most load-bearing profiles:

- **[Optiver](optiver.md)**: the most concrete public account of an enterprise redesigning its SDLC *around* coding agents (Optiver claims a 75% time-to-market reduction), plus a sober LLM-vs-intern trading evaluation.
- **[DoorDash](doordash.md)**: the best-documented multi-agent reference architecture in the folder, covering its MCP tool surface, deep-agent hierarchies, and A2A adoption in public engineering posts.
- **[LinkedIn](linkedin.md)**: a rare published architecture for a production agent platform (Hiring Assistant) over regulated personal data, with a companion peer-reviewed memory paper in `papers/`.

The axis that differentiates the rest is *what kind of adopter they are*:

1. **Agent-surface providers**: enterprises making their own products tool-callable by external agents via MCP. Automattic (WordPress, write-capable), Adobe (Firefly + AEM/Commerce MCP), Figma (design context + canvas writes).
2. **Internal platform builders**: companies building agent/LLM infrastructure for their own engineers. Optiver, Uber (Michelangelo/GenAI Gateway), Block (goose, open-sourced), DoorDash, LinkedIn, MercadoLibre (Verdi), Bloomberg (BloombergGPT + ACL agent research), Two Sigma.
3. **Customer-facing deployers**: agents/LLMs bolted onto an existing consumer or B2B product. Indeed, Best Buy, Maersk, Lease End (voice closer), SonderMind (clinical scribing), YouTube, Roku, Upside (ML pricing, pre-agentic).
4. **Integrators**: consultancies selling adoption itself. Accenture (AI Refinery, Anthropic JV), ZS Associates (ZAIDYN).

## Profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Automattic](automattic.md) | WordPress steward making ~43% of the web agent-writable via MCP | Gold | Private, ~$986M raised, last round 2021 ($7.5B val) | WordPress.com MCP gained write access (posts, pages, media) for Claude/ChatGPT/Cursor in March 2026 |
| [Optiver](optiver.md) | Options market maker that rebuilt its SDLC around coding agents | Gold | Employee-owned, no outside capital; €4.6B 2025 trading income | Ran frontier LLMs through its 88-question intern exam: theory passed, sequential belief-updating failed |
| [Accenture](accenture.md) | Global SI selling agent adoption at scale via AI Refinery | Supporting | Public (NYSE: ACN) | Joint Anthropic business group training ~30,000 professionals on Claude/Claude Code |
| [Adobe](adobe.md) | Creative giant shipping a Firefly creative agent plus MCP servers for AEM/Commerce/Express/Target | Supporting | Public (NASDAQ: ADBE) | Building a Firefly Assistant to run *inside* third-party chatbots, starting with Claude |
| [Best Buy](best-buy.md) | Retailer with production gen-AI support agents on Google Cloud | Supporting | Public (NYSE: BBY) | Contact-center agent-assist tooling reportedly deployed in six to eight weeks |
| [Block](block.md) | Fintech that open-sourced goose, an Apache-2.0 coding agent | Supporting | Public (NYSE: XYZ) | goose is LLM-agnostic and MCP-native, with external adopters (Databricks, university labs) |
| [Bloomberg LP](bloomberg-lp.md) | Financial data giant behind BloombergGPT and peer-reviewed agent tool-calling research | Supporting | Private (Michael Bloomberg majority) | Eight papers at ACL 2026 spanning agentic systems and financial NLP |
| [DoorDash](doordash.md) | Logistics marketplace with a published multi-agent MCP/A2A architecture | Supporting | Public (NYSE: DASH) | "Managed Agent Services" exposes business logic as typed MCP tools to every internal agent |
| [Figma](figma.md) | Design tool turned agent-readable/writable surface | Supporting | Public since July 2025 (~$68B IPO valuation) | MCP server ships with documented support across Claude Code, Cursor, Copilot, Codex, Warp and more |
| [Indeed](indeed.md) | Job-search incumbent shipping agents on both marketplace sides | Supporting | Recruit Holdings subsidiary (acquired 2012, ~$1B) | Indeed claims Sourcing Assistant applicants are 2.9x more likely to be hired, ~6 days faster |
| [Lease End](lease-end.md) | D2C fintech whose voice agent closes car-lease buyouts autonomously | Supporting | Private; funding undisclosed (unverified) | "Arco" voice agent can complete a buyout with no human rep unless the customer asks |
| [LinkedIn](linkedin.md) | Microsoft-owned network running Hiring Assistant on a purpose-built agent platform | Supporting | Microsoft subsidiary (acquired 2016, $26.2B) | LinkedIn reports 81% fewer profiles reviewed per qualified match; architecture + memory system published |
| [Maersk](maersk.md) | Container-shipping giant with human-in-the-loop GenAI over quoting and support | Supporting | Public (CPH: MAERSK), family-controlled | Maersk claims >$300M annual savings from AI forecasting/routing (self-reported) |
| [MercadoLibre](mercadolibre.md) | LatAm e-commerce/fintech platform with in-house LLM orchestration ("Verdi") and MCP tooling | Supporting | Public (NASDAQ: MELI) since 2007 | Amplitude-reported 126 internal AI agents built with 71% task-completion rate |
| [Roku](roku.md) | Streaming platform running ML across discovery and ad serving | Supporting | Public (NASDAQ: ROKU) | Contextual AI places brand ads next to matching plot moments in real time |
| [SonderMind](sondermind.md) | Behavioral-health network layering AI scribing/navigation on human care | Supporting | Private unicorn; $276M raised ($150M Series C, 2021) | AI Notes cuts clinical session-note time from ~20 minutes to ~4 (company claim) |
| [Two Sigma Investments](two-sigma-investments.md) | Quant fund embedding AI as an operating layer across research/engineering | Supporting | Private, ~$60B AUM, not VC-funded | Its internal tools are becoming "company aware" of its own platforms and incident processes |
| [Uber](uber.md) | Ride-hailing giant whose Michelangelo ML platform grew a full LLMOps/agent stack | Supporting | Public (NYSE: UBER) | 100% of business-critical ML use cases run on Michelangelo; GenAI Gateway proxies all LLM vendors |
| [Upside](upside.md) | Cash-back app pricing per-transaction incentives with real-time ML | Supporting | Private; ~$250M raised, ~$1.5B valuation (reported) | Computes the *minimum* incentive to change one shopper's behavior, margin-guaranteed |
| [YouTube](youtube.md) | Google's video platform rebuilt around Gemini agents | Supporting | Alphabet subsidiary (acquired 2006, $1.65B) | Jan 2026 Gemini recommendation rewrite, the biggest ranking change since watch-time (2012) |
| [ZS Associates](zs-associates.md) | Consulting firm packaging agentic AI into the ZAIDYN life-sciences platform | Supporting | Private, no VC; ~$4.2B est. revenue | Grew from sales-territory models built on early-1980s PCs into a vertical AI platform |

**Folder vs. expectations:** all 20 expected companies are present. One profile beyond the expected list, **SonderMind**, is filed here and fits the category definition (an adopter rather than a vendor), so treat it as a late addition rather than a misfile. Nothing expected is missing.

## Related papers

The `papers/` folders repeatedly cite these companies as the deployment context; the most genuinely relevant reads:

- [Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents](../../papers/memory-research-agents/hierarchical-long-term-semantic-memory-for-linkedin-s-ai-age.md): the peer-reviewed (KDD 2026) memory system inside LinkedIn's Hiring Assistant; the direct companion to the [LinkedIn](linkedin.md) profile and the strongest company-paper pairing in the repo.
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): the orchestration survey that frames what Automattic, Adobe, Figma, and DoorDash are actually building when they expose MCP tool surfaces.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md): policy checkpoints and approval gates; the formal version of the human-in-the-loop patterns Maersk, Automattic, and LinkedIn describe.
- [CaMeLs Can Use Computers Too](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md) and [ClawLess: A Security Model of AI Agents](../../papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md): what "write-capable agents on production systems" (Automattic, Adobe, Figma canvas writes) should worry about, namely prompt injection and below-the-agent enforcement.
- [ProdCodeBench](../../papers/swe-agents/prodcodebench-a-production-derived-benchmark-for-evaluating.md): Meta's production-derived coding-agent benchmark; the eval-side counterpart to Optiver's, Block's, and MercadoLibre's internal coding-agent rollouts.
- [Effective Strategies for Asynchronous Multi-Agent Collaboration in SWE](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md): worktree isolation and test-gated merges; the research analog of Optiver's agentic-SDLC "golden paths."
- [Agentic Search in the Wild](../../papers/memory-research-agents/agentic-search-in-the-wild-intents-and-trajectory-character.md): 14M real agent search requests; relevant to whether agent traffic actually materializes on content surfaces like WordPress and YouTube.
- [Building Enterprise Realtime Voice Agents from Scratch](../../papers/voice-realtime/building-enterprise-realtime-voice-agents-from-scratch-a-te.md): the latency-budget tutorial that frames what Lease End's Arco voice closer had to solve.

## Open questions

- **Self-reported numbers dominate.** Nearly every efficiency claim here (Optiver's 75%, Maersk's $300M, LinkedIn's 81%, Indeed's 2.9x, SonderMind's 80%) is company- or vendor-published. No independent audit of any of them exists yet.
- **Does external agent traffic show up?** Automattic, Adobe, and Figma have built the write-capable MCP surfaces; there is still no named enterprise running third-party agents against them at production scale. The agent-surface bet is live but unproven.
- **Buyable vs. observable.** Half this category (Optiver, Two Sigma, Bloomberg, Uber, DoorDash) sells nothing an AI engineer can adopt; their value is as reference architecture and hiring signal. Sponsorships here are best read partly as recruiting.
- **Platform convergence or fragmentation?** DoorDash (MCP + A2A), Uber (gateway + agent studio), LinkedIn (messaging-based lifecycle service), and Block (goose) each rolled their own agent platform. Whether these converge on shared protocols or stay bespoke is the category's biggest unresolved architecture question.
- **Where's the line between adopter and vendor?** Block open-sourced goose; ZS sells ZAIDYN; Accenture sells AI Refinery delivery. Several "adopters" are quietly becoming tooling vendors; watch whether they get re-filed next cycle.
