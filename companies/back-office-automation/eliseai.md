# EliseAI

> Vertical conversational-AI company that automates the front office of US rental housing (and now healthcare clinics) — an agent named "Elise" answers every call, text, and email, books tours and appointments, and pushes results into the property/practice management system.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2017, New York City, originally as "MeetElise"; Y Combinator W19; rebranded to EliseAI in 2023 (Verified — press, CB Insights; YC batch Reported)
- **Website / GitHub:** https://eliseai.com · no public GitHub presence (closed-source vertical SaaS)

## What they do

EliseAI sells a conversational agent platform for two regulated verticals. The housing suite covers the full renter lifecycle: **LeasingAI** answers prospect inquiries 24/7 across voice, SMS, email, and web chat, qualifies leads, and books tours (including AI-guided self-tours with door unlocking); **ResidentAI** handles maintenance requests, renewals, and delinquency follow-up; **EliseCRM** centralizes the conversations; newer modules do lease audits and fee-transparency checks. Written responses in ~51 languages, voice in 7 (Reported — company site). The engineering-relevant part: this is a production voice+text agent doing real tool calls — calendar writes, CRM updates, work-order creation, door access — against property management systems (Yardi, RealPage, Entrata ecosystems), at a scale of over a million conversations monthly (Reported — company/leadership bios).

**HealthAI** (launched with the 2023 rebrand) applies the same stack to clinics: VoiceAI answers 100% of inbound patient calls, schedules against provider calendars, handles reminders/waitlists and insurance intake, integrates with EHR/PMS/RCM systems, and is HIPAA and SOC 2 Type II compliant (Reported — company site; independent verification of clinical claims not found). No public pricing page — enterprise sales only.

## Founders & origins

**Minna Song** (CEO) and **Tony Stoyanov** (CTO). Song has an MIT B.S. in Computer Science, with prior stints at Microsoft and MIT Lincoln Laboratory; Stoyanov came out of Cambridge computer science (Verified — Sapphire Ventures, press). Accounts say the two met at the University of Cambridge (Reported). Origin story, well documented: Song took a job as an office manager at a NYC real-estate firm to learn the domain firsthand, then they bootstrapped an email-based AI leasing assistant before YC W19 — motivated by data that roughly half of rental inquiries go unanswered (Verified — VentureBeat, company blog).

## Funding

- **Seed:** $1.9M led by Avalon Ventures (Reported — Crunchbase-derived history)
- **Series A/B:** Series B July 2021 led by Navitas Capital; amounts not found in public sources
- **Series C:** $35M, June 2023, led by Point72 Private Investments, with Koch Real Estate Investments, Golden Seeds, Navitas, JLL Spark, DivcoWest (Verified — BusinessWire)
- **Series D:** $75M, August 2024, led by Sapphire Ventures — $1B+ valuation, unicorn mark (Verified — multiple outlets)
- **Series E:** $250M, August 2025, led by Andreessen Horowitz with Bessemer, at $2.2B valuation (Verified — SiliconANGLE, Fierce Healthcare, company blog)
- **Total raised:** ~$385M (pre-E total ~$134M per Tracxn + $250M)

## Evidence of real-world use

Strong and unusually documented for vertical AI. Named enterprise customers: **Greystar, AvalonBay, Equity Residential, Brookfield, Bozzuto, Invitation Homes, LeFrak, Cardinal Group** (Verified — site, Forbes June 2026 profile). Third-party analysis (Thesis Driven deep dive) and press put the footprint at 600+ owners/operators covering roughly 1 in 6 US rental units. Documented case results: Equity Residential — 1.5M+ customer interactions/year, 90% of prospect workflows automated, ~$14M payroll savings; Kittle Property Group — 65% faster lead-to-lease, +8% conversion (Reported — company case studies). Surpassed $100M ARR in 2025 (Reported — Series E coverage, Investing.com). OpenAI publicly named EliseAI a trusted partner (Reported — company blog). Healthcare traction is the unproven half — the Series E was explicitly raised to build it out.

## Relevance to agentic AI engineering

EliseAI is a reference case for deployed, revenue-generating voice agents in a regulated domain — exactly the territory of this repo's voice papers: *τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains* (leasing/scheduling calls are the archetypal domain), *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents*, and *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation* (every Elise call ends in tool calls against a PMS/EHR). Fair-housing and HIPAA constraints make it a live instance of the *Governance by Construction for Generalist Agents* problem — constraining what an agent may say/do by design, not prompt. Multi-month renter journeys (inquiry → tour → lease → renewal) are a real-world test of the agent-memory literature (*Memory for Autonomous LLM Agents*). For a construction back office, it's the closest existence proof that vertical conversational + workflow agents can win a trades-adjacent industry.

## Use cases & considerations

**Use cases:** (1) property managers/owners: automate leasing inquiry-to-tour and resident maintenance/renewal comms end-to-end; (2) clinics: AI front desk for scheduling and intake; (3) for builders: study as a design pattern — vertical agent + deep system-of-record integration + compliance moat — rather than something you integrate (no public API/platform play).

**Considerations:** enterprise-only, no public pricing, deep PMS/EHR integration means real lock-in. Sector-wide legal exposure is genuine: the 2023 Open Communities fair-housing suit hit competitor PERQ's chatbot (not EliseAI — no litigation against EliseAI found in public sources), but source-of-income screening liability applies to any leasing agent. Competitors: Funnel Leasing, Knock (RealPage), Zuma, PERQ, Colleen AI in housing; Hyro, Notable, Assort Health, Insight Health in healthcare voice. Open questions: whether the multi-vertical (housing + healthcare) strategy dilutes focus — a critique publicly raised by health-tech analysts — and how defensible the NLP stack is as frontier voice models commoditize.

## Sources

- https://eliseai.com/ and https://eliseai.com/platform-overview
- https://eliseai.com/healthai and https://eliseai.com/health/voiceai
- https://eliseai.com/blog/eliseai-raises-250m-series-e
- https://eliseai.com/blog/eliseai-world-leader-in-ai-enabled-solutions-for-housing-raises-75-million-series-d-round-valuing-company-in-excess-of-1-billion
- https://www.businesswire.com/news/home/20230607005164/en/ (Series C)
- https://siliconangle.com/2025/08/20/property-management-startup-eliseai-nabs-250m-2-2b-valuation/
- https://www.fiercehealthcare.com/ai-and-machine-learning/eliseai-banks-250m-a16z-bessemer-venture-partners-grow-its-healthcare
- https://venturebeat.com/ai/real-estate-tech-firm-eliseai-was-ahead-of-the-curve-now-its-a-unicorn
- https://www.forbes.com/sites/rashishrivastava/2026/06/10/this-22-billion-ai-startup-is-helping-the-countrys-largest-landlords-with-admin-work/
- https://www.thesisdriven.com/letters/deep-dive-eliseai/
- https://www.cbinsights.com/company/meetelise and https://tracxn.com/d/companies/eliseai/__frC_1IDVJYdO6D1sDs1wID8oSQfzoVZH1wRXFipczc8
- https://www.open-communities.org/post/press-release-open-communities-reaches-accord-in-case-addressing-artificial-intelligence-communicat (sector context; PERQ, not EliseAI)
- https://x.com/SapphireVC/status/1823734011874722244
