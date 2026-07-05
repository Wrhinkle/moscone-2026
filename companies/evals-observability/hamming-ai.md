# Hamming AI

> Automated QA platform for AI voice agents: it places thousands of simulated phone calls at your agent, scores the audio (not just transcripts) against 50+ metrics, and keeps monitoring calls in production.

- **Category:** evals-observability
- **AIEWF 2026 tier:** supporting
- **Founded:** 2024, San Francisco (Verified — YC profile, seed press). YC Summer 2024 batch (Verified via YC company page; a YC LinkedIn post says "W24" — the company's own materials and YC directory say S24).
- **Website / GitHub:** https://hamming.ai · no significant public GitHub presence found (product is closed-source SaaS)

## What they do

Hamming is end-to-end testing and monitoring for voice agents. The core mechanic: you connect your agent (native integrations for LiveKit, Pipecat, ElevenLabs, Retell, Vapi; inbound, outbound, and WebRTC), Hamming's LLM analyzes your system prompt and auto-generates hundreds of test scenarios, then its own synthetic "voice characters" — with configurable accents, interruptions, background noise, DTMF/IVR behavior — place concurrent test calls (they claim 50K+ concurrent) and score the results. Scoring is audio-native rather than transcript-only, measuring latency, hallucination, sentiment, instruction-following, and compliance; the company claims 95%+ agreement with human evaluators (Reported — company site, not independently benchmarked).

The production side closes the loop: call monitoring with real-time tagging, and one-click conversion of a failed production call into a regression test. CI/CD hooks (REST API, webhooks, GitHub Actions/Jenkins) let teams gate deploys on eval results — the same "evals as unit tests" posture Braintrust takes for text agents, applied to telephony. There is also a red-teaming suite (jailbreaks, prompt injection, PII leakage) and compliance surface: SOC 2 Type II, HIPAA with BAA, single-tenant deployment, US/EU/UK data residency (Verified — company site; SOC 2 claim not independently checked). Claimed scale: 4M+ calls tested, 10K+ agents monitored (Reported — company figures). 65+ languages with regional accent coverage.

Pricing is not public — Startup / Agency / Enterprise tiers priced on test volume rather than seats (Verified that no price list exists; tier structure Reported).

## Founders & origins

**Sumanyu Sharma** (CEO) — previously Head of Data at Citizen and Senior Staff Data Scientist at Tesla, where he worked on AI-powered sales; University of Waterloo (Verified — YC profile, seed press). **Marius Buleandra** (CTO) — ran data infrastructure at Anduril, drove user growth at Citizen alongside Sumanyu, founding engineer at Spell (MLOps startup acquired by Reddit) (Verified — YC profile, press). Origin story: manual voice-agent QA — engineers calling their own bots over and over — doesn't scale, so they built agents that phone your agents. Team size ~8 as of the YC listing (Reported).

## Funding

- **Seed, Dec 2024:** $3.8M led by **Mischief** (Lachy Groom's fund), with Y Combinator, AI Grant, Pioneer, Coalition Operators, and angels including Hiten Shah, Ran Makavy, Max Kolysh, Richard Aberman, Kulveer Taggar (Verified — Business Wire, company blog, multiple press).
- **Total raised:** ~$4.3–4.55M including YC's standard investment (Reported — third-party trackers).
- No Series A found in public sources as of 2026-07-02. Note: one tracker (GetLatka) claims Hamming is "bootstrapped with no outside funding" at $1.1M ARR — this directly contradicts the well-documented seed and should be treated as unreliable; the ARR figure is likewise Unverified.

## Evidence of real-world use

Moderate and improving — real named case studies, not just a logo wall. Documented case studies: **Synthpop** (healthcare patient-journey platform; uses Hamming as its agentic QA and proactive-discovery layer) and **Grove AI** (clinical trial recruitment; cites 97% patient satisfaction and audit prep dropping from weeks to hours) (Verified as published case studies; the metrics inside are customer-reported). Landing-page logos include Luma Health, Netomi, Maven AGI, Ellipsis Health, Lorikeet, Smith.ai, Podium, Bland Labs, mdhub, Anima (Reported — logos only). A published partner integration with Retell and native support in the major voice-agent frameworks (LiveKit, Pipecat, Vapi) is a decent ecosystem signal: the platforms builders actually use route to Hamming for QA. Healthcare concentration is notable — HIPAA/BAA posture is clearly a deliberate wedge.

## Relevance to agentic AI engineering

Hamming is the evals layer for the voice corner of the agent stack — the commercial counterpart to this repo's voice-agent papers. *From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation* argues for exactly the audio-native, reproducible evaluation Hamming productizes; *τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains* and *ProVoice-Bench* define the interruption/turn-taking/proactivity behaviors Hamming's synthetic callers exercise (see also *Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents*). Its production-call-to-regression-test loop is the voice analogue of the trace-to-dataset discipline in *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*, and its red-teaming/compliance surface connects to *Governance by Construction for Generalist Agents*.

## Use cases & considerations

Use cases: (1) pre-launch regression suite for a healthcare or scheduling voice agent, gated in CI; (2) load-testing telephony infrastructure with 1000s of concurrent synthetic calls before a seasonal spike; (3) continuous production monitoring with automatic escalation of failed calls into test cases; (4) HIPAA/PII red-teaming before an enterprise security review.

Considerations: closed-source, no public pricing — expect a sales motion. LLM-judged audio evals inherit judge bias; the 95% human-agreement number is self-reported. Small team (~8) and modest funding relative to the observability incumbents. Competitors: **Coval** (YC-adjacent voice-agent simulation, the closest rival), **Vocera/Roark**, generalist eval platforms (Braintrust, Arize, LangSmith) extending toward voice, and built-in testing inside Vapi/Retell/Bland — the open question is whether voice QA stays a standalone layer or gets absorbed by the agent platforms themselves.

## Sources

- https://hamming.ai/
- https://hamming.ai/about
- https://www.ycombinator.com/companies/hamming-ai
- https://www.businesswire.com/news/home/20241218104943/en/Hamming.ai-Announces-$3.8-Million-Seed-Led-by-Mischief
- https://hamming.ai/blog/hamming-ai-seed-funding-to-make-voice-agents-more-reliable
- https://hamming.ai/case-studies/synthpop
- https://hamming.ai/case-studies/grove-ai
- https://hamming.ai/partners/retell
- https://hamming.ai/industry/healthcare
- https://pulse2.com/hamming-ai-ai-based-voice-agent-reliability-company-raises-3-8-million-seed/
- https://getlatka.com/companies/hamming.ai (flagged unreliable — contradicts seed round)
