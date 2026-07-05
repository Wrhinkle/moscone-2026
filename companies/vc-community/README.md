# VC & Community

Venture firms, accelerators/communities, media, universities, foundations, and government bodies sponsoring AIEWF 2026. Nothing in this folder is a tool you'd wire into an agent stack. The category exists because the agent ecosystem runs on more than code: VCs, PE firms, and philanthropies fund the startups, while media outlets, communities, and universities train and connect the practitioners, and government regulates the money. This is the folder for founders scoping investors and for anyone tracking where institutional capital thinks agents are headed; the learning channels live here too.

## How to read this category

Eleven profiles, one load-bearing axis: **capital-as-signal vs. non-capital community nodes**. Six entries write checks (Acrew, Amplify, Gradient, Untapped, Venrock, Carlyle); five don't: a philanthropy (Gates Foundation), a university (UC Berkeley), a media/education business (Towards AI), a practitioner community (The Velocity Room), and a state regulator (DFPI).

Start with these three:

1. **[UC Berkeley](uc-berkeley.md)** is the only entry whose output you might actually run in production: vLLM (serving), Gorilla/BFCL (tool-calling benchmarks), Chatbot Arena (evals). Its lab output underpins several other areas of this repo.
2. **[Untapped Capital](untapped-capital.md)** is the most agent-native investor here: co-founded by Yohei Nakajima, creator of BabyAGI, one of the earliest autonomous-agent open-source projects. The fund is small (~$15M) but unusually relevant to this event.
3. **[Amplify Partners](amplify-partners.md)** has the clearest portfolio-as-map: LangChain, Modal, Temporal, Datadog. If you want to know which infra layers institutional capital believes in, read Amplify's bets, then cross-check with [Gradient](gradient.md) ($220M AI-only seed fund, freshly spun out of Google).

Two oddities worth knowing before you're confused by them: **The Velocity Room** is a practitioner community, not a fund, despite the name (and the only silver-tier sponsor in this folder); the **DFPI** is a California regulator that landed in a VC category because it now runs the state's VC diversity-reporting program.

## Profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Acrew Capital](acrew-capital.md) | Seed/Series A firm across fintech, security, data infra, applied AI | Supporting | ~$1.7B AUM; $700M fund (2024) | Repeat agent-infra backer: Veris AI (fellow AIEWF sponsor), Protect AI, Writer; added ex-OpenAI sales head as GP |
| [Amplify Partners](amplify-partners.md) | Early-stage VC for technical founders in dev tools and AI/ML infra | Supporting | $900M across three funds (June 2025) | Portfolio doubles as this repo's index: LangChain, Modal, Temporal, Runway, Datadog |
| [DFPI](dfpi.md) | California's financial regulator, policing AI-linked fraud and VC reporting | Supporting | N/A (state agency) | Regulator for California's VC founder-diversity disclosures (FIPVCC); enforcement suspended March 2026 pending rulemaking |
| [Gates Foundation](gates-foundation.md) | World's largest private philanthropy funding AI for global health | Supporting | Endowed foundation deploying grant capital (no equity positions) | $200M/4-year Anthropic partnership (May 2026): grant funding, API credits, shared tools for health/education/agriculture |
| [Gradient](gradient.md) | AI-only seed fund, ex-Google Gradient Ventures, independent since Oct 2025 | Supporting | ~$1.2B managed; $220M Fund V (2026) | Spun out of Google to escape cap-table conflicts; profile carries a disambiguation note vs. unrelated Gradient Labs (London) |
| [The Carlyle Group](the-carlyle-group.md) | $477B global PE firm investing in and internally adopting AI | Supporting | Public (NASDAQ: CG) | Named, in-production internal use: agentic RAG pipelines over financial documents via LlamaParse for investment research |
| [Towards AI](towards-ai.md) | AI education publisher: newsletter, courses, Discord | Supporting | No external funding found; revenue-run | 130,000+ newsletter subscribers; published "Building LLMs for Production" (self-stated audience numbers) |
| [The Velocity Room](the-velocity-room.md) | Free-membership practitioner community for AI infra/security/governance | **Silver** | Undisclosed; no founders or funding in public sources | Highest sponsor tier in this folder, yet zero public founder/funding info; profile flags this rather than guessing |
| [UC Berkeley](uc-berkeley.md) | Research university whose labs built core agentic/LLM infrastructure | Supporting | N/A (university) | BAIR/Sky Computing Lab shipped vLLM, Gorilla + the Berkeley Function-Calling Leaderboard, and Chatbot Arena |
| [Untapped Capital](untapped-capital.md) | Data-driven pre-seed/seed fund sourcing ~90% of deals via outbound | Supporting | ~$15M fund (reported) | Co-founder Yohei Nakajima built BabyAGI; co-founder Jessica Jackley co-founded Kiva.org |
| [Venrock](venrock.md) | The Rockefellers' VC arm, funding early-stage tech/health/AI since 1969 | Supporting | ~$3B AUM (reported) | Early Intel and Apple backer; recently led Archetype AI's $13M seed alongside Amazon and Hitachi |

All 11 profiles expected in this category are present; none are missing or re-filed elsewhere.

## Related papers

Capital and community entries connect to the research corpus more loosely than product categories do, so only the genuinely load-bearing links are listed:

- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md): the tool-calling → orchestration research arc that UC Berkeley's Gorilla and the Berkeley Function-Calling Leaderboard helped start; useful context for why Berkeley's output matters so much.
- [Governance by Construction for Generalist Agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md): policy-as-code enforcement for enterprise agents; the technical counterpart to the governance concerns DFPI regulates from outside and The Velocity Room's community discusses from inside.
- [Do Agents Need Semantic Metadata?](../../papers/memory-research-agents/do-agents-need-semantic-metadata-a-comparative-study-in-age.md): evidence that retrieval-corpus structure drives agent precision; directly relevant to Carlyle-style agentic RAG over complex financial documents (their LlamaParse deployment is the industrial version of this problem).

## Open questions

- **Who is behind The Velocity Room?** A silver-tier sponsor with no discoverable founders, parent, or business model is the folder's biggest unverified entity. Worth resolving before treating it as a neutral community.
- **Which Gradient is the sponsor?** The profile covers Gradient (ex-Google Ventures fund) per the category assignment, but flags that Gradient Labs (London, agentic customer-ops fintech) is a plausible alternate referent. The sponsor page should settle it.
- **Does grant capital change what gets built?** Gates ($200M + API credits) and Berkeley (open-source lab output) fund agent work without equity. No profile yet answers whether non-dilutive capital produces different agent infrastructure than the VC-backed track.
- **What happens to DFPI's VC reporting rules?** Enforcement of the founder-diversity disclosure program was suspended in March 2026 pending rulemaking, so the compliance burden on every fund in this folder with a California nexus is currently undefined.
- **Overlap signal untested:** Acrew backs fellow sponsor Veris AI; Amplify backs LangChain; Carlyle uses LlamaIndex tooling. Nobody has yet mapped sponsor-to-sponsor investment edges across this repo; that small graph exercise would show which "community" ties are actually cap-table ties.
