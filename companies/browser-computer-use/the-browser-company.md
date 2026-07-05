# The Browser Company

> Maker of the Arc and Dia browsers — the consumer/work-facing "agentic browser" bet — acquired by Atlassian in 2025 for $610M and now building Dia as the AI browser for work.

- **Category:** browser-computer-use
- **AIEWF 2026 tier:** supporting
- **Founded:** 2019, New York City — legal name "The Browser Company of New York" (Verified — Wikipedia, Contrary Research, press)
- **Website / GitHub:** https://thebrowser.company · https://www.diabrowser.com · https://arc.net (no significant public GitHub presence — closed-source products)

## What they do

The Browser Company builds Chromium-based browsers with rethought interfaces. Their first product, **Arc** (public 2022–2023, macOS/Windows/iOS/Android), was a power-user browser with Spaces, a sidebar-first UI, and a cult following — over a million users at peak (Reported — Wikipedia/press; earlier reporting said 500K). In 2025 they made an unusual call: Arc was put in maintenance mode (security updates only, no roadmap) and the whole company pivoted to **Dia**, an AI-first browser rebuilt around conversation rather than tabs-and-clicks.

Dia's engineering-relevant pieces, as of 2026-07-02: (1) a **chat pane with cross-tab context** — `@`-mention any open tab or `@history` to inject page content into a prompt without copy-paste; (2) **Skills**, natural-language-authored reusable workflows ("summarize this page and pull out action items") that can chain across tabs, saved and shared via a community **Skills Gallery** (categories include Development, Research, Writing; examples: Fact-Check, YouTube Transcript); the Natural Language Skill Builder shipped v1.2.0, October 2025 (Reported — third-party reviews); (3) **Memory**, a personal-context retrieval system with automatic memory search (v1.4.0, November 2025) that surfaces prior chats/tabs as you type. Dia Pro is $20/month for unlimited AI chat and Skills (Reported — reviews; public pricing = real commercial product). Current limitation: macOS 14+ on Apple Silicon only; Windows, mobile, and enterprise versions are on the post-acquisition roadmap (Verified — Atlassian statements).

Post-acquisition, Atlassian's stated plan is to make Dia "the browser for work": tabs enriched with SaaS-app context, AI skills plus personal work memory connecting apps, tabs, and tasks, distributed into Atlassian's ~300K customer organizations (Verified — Atlassian blog, Computerworld).

## Founders & origins

- **Josh Miller**, co-founder/CEO (Verified). Previously co-founded Branch (acquired by Facebook, 2014), product at Facebook, then director of product in the Obama White House's digital office (Reported — profiles/interviews).
- **Hursh Agrawal**, co-founder/CTO (Verified — note some sources misspell "Harsh"). Also a Branch co-founder.

Founded 2019 in NYC on the thesis that the browser, not the OS, is where modern work happens and deserved re-invention. The 2025 Arc-to-Dia pivot is well documented in Miller's "Letter to Arc members" and podcast interviews.

## Funding

- **Seed:** $5M, 2020 (Reported — Clay/Tracxn)
- **Series A:** $13M, 2021 (Reported)
- **Additional round, 2022** (Reported — Clay; amount unclear in public sources)
- **Series B:** $50M, March 2024, led by Pace Capital at a **$550M valuation** (Verified — TechCrunch, Crunchbase)
- **Total raised:** conflicting — TechCrunch put post-Series-B total at $68M; Clay/Tracxn report $128M. Unresolved in public sources.
- Notable angels: Jeff Weiner (LinkedIn), Ev Williams (Medium), Dylan Field (Figma), Akshay Kothari (Notion) (Reported)
- **Exit:** acquired by **Atlassian for $610M cash** — announced Sept 4, 2025, closed Oct 21, 2025; operates independently within Atlassian (Verified — CNBC, TechCrunch, Businesswire)

## Evidence of real-world use

- Arc reached 1M+ users before sunset (Reported); it was a genuinely loved product — the sunset itself generated significant community backlash, which is its own adoption signal.
- Dia launched in early access mid-2025 (Arc members first), with an active community Skills Gallery — user-generated skills across many categories is real usage, not a logo wall (Verified — diabrowser.com/skills).
- Public $20/mo Dia Pro tier (Reported — multiple 2026 reviews).
- Independent 2026 reviews consistently rank Dia among the top AI browsers alongside OpenAI's Atlas and Perplexity's Comet (Reported).
- No public Dia user counts found in public sources. The strongest forward-looking distribution evidence is Atlassian's 300K-organization base and its Team '26 conference sessions demoing "Dia + Atlassian."

## Relevance to agentic AI engineering

Dia is the consumer/enterprise-facing end of the browser-agent stack — the human-in-the-loop surface, where Browserbase (same category folder) is the headless infrastructure end. Its Skills system is essentially productized, user-authored skill learning for web agents — directly adjacent to *WebXSkill: Skill Learning for Autonomous Web Agents*. The Memory feature is a production test of the questions in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation* and *Are We Ready For An Agent-Native Memory System?* — and Atlassian's "personal work memory across SaaS apps" ambition rhymes with *Hierarchical Long-Term Semantic Memory for LinkedIn's AI Agents*. An AI browser operating with the user's logged-in sessions raises exactly the prompt-injection/authority problems treated in *CaMeLs Can Use Computers Too* and *Governance by Construction for Generalist Agents*. User search behavior inside Dia is the human-side counterpart of *Agentic Search in the Wild*.

## Use cases & considerations

**Use cases:** (1) daily-driver AI browser for research-heavy work — cross-tab synthesis without copy-paste; (2) codifying repeatable browser workflows as Skills for a small team (intake triage, page-level fact extraction); (3) watching Dia + Atlassian as a template for "agentic UX over existing SaaS"; (4) a Skills Gallery entry as lightweight distribution for a niche workflow.

**Considerations:** not a platform you integrate — no public API/SDK for third-party agents found; it's a product you adopt. Apple Silicon-only today. Post-acquisition roadmap risk: priorities now serve Atlassian's enterprise strategy (Arc's sunset shows this team will kill loved products). Data-governance questions around browser-level memory of everything you do. Competitors: OpenAI Atlas, Perplexity Comet, Google's Gemini-in-Chrome, Brave/Edge AI features. Open question: whether "browser as agent surface" wins versus agents living in the OS or in individual apps.

## Sources

- https://en.wikipedia.org/wiki/Arc_(web_browser)
- https://www.atlassian.com/blog/announcements/atlassian-acquires-the-browser-company
- https://www.cnbc.com/2025/09/04/atlassian-the-browser-company-deal.html
- https://techcrunch.com/2025/09/04/atlassian-to-buy-arc-developer-the-browser-company-for-610m/
- https://www.businesswire.com/news/home/20251021473486/en/Atlassian-Completes-Acquisition-of-The-Browser-Company-of-New-York
- https://techcrunch.com/2024/03/21/the-browser-company-raises-50-million-at-550-million-valuation/
- https://www.clay.com/dossier/the-browser-company-funding
- https://research.contrary.com/company/the-browser-company
- https://www.diabrowser.com/skills
- https://browsercompany.substack.com/p/letter-to-arc-members-2025
- https://www.computerworld.com/article/4053130/atlassian-exec-details-the-610m-browser-company-acquisition.html
- https://supasidebar.com/blog/dia-browser-mac-review-2026
- https://efficient.app/apps/dia
- https://www.reworked.co/collaboration-productivity/inside-atlassians-plan-to-make-dia-an-ai-browser-built-for-real-work/
