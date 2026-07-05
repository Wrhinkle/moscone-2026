# Hippocratic AI

> Builds "safety-first" generative AI voice agents that make patient-facing healthcare phone calls — post-discharge follow-up, chronic-care check-ins, pre-op prep — at ~$9/hour, on a purpose-built LLM constellation rather than a single frontier model.

- **Category:** back-office-automation
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023, Palo Alto, CA (Verified — company site, Contrary Research, press)
- **Website / GitHub:** https://hippocraticai.com · Polaris paper: https://arxiv.org/abs/2403.13313 (no significant public OSS)

## What they do

Hippocratic AI sells outbound/inbound **voice AI agents for non-diagnostic patient work**: discharge follow-up calls, chronic-care management, medication adherence, pre-op instructions, scheduling, and intake pre-charting. The explicit positioning is "do what health systems can't staff," not "replace clinical judgment" — agents are constrained to low-risk, protocol-driven conversations and escalate to humans.

The technical core is **Polaris**, a "constellation architecture": one large primary conversational model leads the real-time patient call while multiple specialist support models (medication safety, labs, nutrition, escalation/compliance checking) run alongside, with an orchestration layer managing control flow, inter-model messages, and conversation state (Verified — arXiv 2403.13313, March 2024). Polaris 5.0 (late 2025) is described as a 5T+ total-parameter constellation around a ~700B core model, with company-run evals claiming wins over frontier models on medical safety tasks (Reported — company/PRNewswire; benchmarks are theirs). Latency-sensitive voice inference runs on NVIDIA's stack, including work on "empathy inference" for real-time affect (Verified — NVIDIA case study).

Distribution has two unusual pieces: a **~$9/hour per-agent pricing** anchor (versus ~$39/hr median RN wage) and an **AI Agent App Store** where licensed US clinicians design specialty agents and earn royalties (5% of base rate + 70% of premium, capped $5k/agent) after a three-step validation gate (Verified — company pages, Fierce Healthcare, nurse.org). A **Nurse Co-Pilot** inpatient voice assistant was co-developed with nursing leaders at Cincinnati Children's, OhioHealth, and Cleveland Clinic (Reported — Fierce Healthcare).

## Founders & origins

**Munjal Shah** (CEO) — serial founder: Like.com (acquired by Google, 2010) and Health IQ; CS at UCSD, MS Stanford (Verified — multiple bios). Co-founders per Contrary Research and the company team page: **Vishal Parikh** (CPO), **Meenesh Bhimani, MD** (CMO; ex-COO of El Camino Health), **Subho Mukherjee** (Chief Science Officer), **Saad Godil** (CTO, ex-NVIDIA), **Alex Miller** (SVP AI Ops), **Kim Parikh** (SVP Data & Content) (Reported — Contrary Research; the physician/researcher founding group spans El Camino, Johns Hopkins, Stanford, Google, NVIDIA). Origin story: Shah's stated motivation was applying LLMs to healthcare's staffing shortage while making "do no harm" the design constraint — hence the name.

## Funding

- **Launch/seed:** $50M out of stealth, May 2023, a16z + General Catalyst (Verified — press)
- **Series A:** $53M, March 2024, ~$500M valuation, Premji Invest + General Catalyst (Verified)
- **Series B:** $141M, January 2025, $1.64B valuation, led by Kleiner Perkins; NVIDIA's NVentures among backers (Verified)
- **Series C:** $126M, November 2025, **$3.5B valuation**, led by Avenir Growth with CapitalG, General Catalyst, a16z, Kleiner Perkins, Premji Invest, plus health systems (UHS, Cincinnati Children's, WellSpan) and John Doerr (Verified — Businesswire, Fierce Healthcare)
- **Total raised:** ~$404M (Verified — Series C announcements)

## Evidence of real-world use

Stronger than most healthcare AI startups, though most metrics are company-reported. Documented deployments: **Universal Health Services** launched the agents for post-discharge engagement at Summerlin Hospital (Las Vegas) and Texoma Medical Center (TX), with the Summerlin CNO on record (Verified — UHS press release). Health-system investors (UHS, Cincinnati Children's, WellSpan) doubling as customers is meaningful skin-in-the-game. Company claims as of the Series C: **115M+ clinical patient interactions**, 50+ health system/payer/pharma partners, ~1,000 built use cases, and outcome stats (30% readmission reduction, 20% higher pre-charting completion) — all Reported, not independently audited. The Polaris paper's eval used 1,100+ licensed nurses and 130+ physicians; the ongoing validation network is claimed at 6,000+ nurses / 300+ physicians (Reported). No public self-serve pricing page; enterprise sales motion.

## Relevance to agentic AI engineering

This is the most consequential production case study of **real-time voice agents under safety constraints**. The constellation design — a conversational lead model fenced by specialist checker models — is a concrete industrial answer to the problems in this repo's voice-agent papers: *LTS-VoiceAgent* (listen-think-speak latency budgeting), *VoiceAgentRAG* (dual-agent retrieval off the hot path), *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents*, and eval methodology from *τ-Voice* and *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*. Its human-validation gate and escalation rules are a lived version of *Governance by Construction for Generalist Agents*; its self-run "beats frontier models" benchmarks deserve the skepticism argued in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* (same failure mode, different domain). For any business making high-volume outbound calls (in construction: AR follow-up, sub scheduling, homeowner updates), the pattern — cheap per-hour agent + domain checker models + human escalation — transfers.

## Use cases & considerations

**Use cases:** (1) template for regulated/high-stakes voice agents: constellation + escalation + licensed-expert validation loop; (2) the App Store royalty model as a pattern for domain-expert-authored agents; (3) healthcare orgs offloading follow-up call volume; (4) pricing anchor ($/agent-hour vs labor wage) for any labor-substitution agent pitch.

**Considerations:** proprietary, enterprise-only, healthcare-scoped — nothing to self-serve or integrate today outside health systems. Outcome and safety claims are largely self-reported; "115M interactions, no safety issues" is unaudited. Regulatory/nursing-union pushback on "$9/hr AI nurses" is real reputational risk. Competitors: Abridge and Nuance/Microsoft DAX (documentation, adjacent), Notable, Assort Health, Infinitus (healthcare voice calls), and generic voice-agent platforms (Vapi, Retell, LiveKit-based builds). Open questions: independent safety audits, and whether the constellation retains an edge as frontier models add native low-latency voice.

## Sources

- https://hippocraticai.com/ and https://hippocraticai.com/munjal-shah/
- https://hippocraticai.com/hippocratic-ai-announces-series-c-funding-126-million/
- https://www.businesswire.com/news/home/20251103432446/en/
- https://www.fiercehealthcare.com/ai-and-machine-learning/hippocratic-ai-lands-126m-series-c-expand-patient-facing-ai-agents-fuel-ma
- https://www.fiercehealthcare.com/ai-and-machine-learning/hippocratic-ai-rolls-out-2-new-tools-aimed-expanding-clinical-access
- https://arxiv.org/abs/2403.13313 (Polaris paper)
- https://research.contrary.com/company/hippocratic-ai
- https://uhs.com/news/universal-health-services-launches-hippocratic-ais-generative-ai-healthcare-agents-to-assist-with-post-discharge-patient-engagement/
- https://www.nvidia.com/en-us/case-studies/hippocratic-ai/
- https://nurse.org/news/ai-nurses/ and https://www.hippocraticai.com/ai-agent-app-store
- https://www.techtarget.com/healthtechanalytics/news/366634018/Hippocratic-AI-snags-126M-valuation-soars-to-35B
