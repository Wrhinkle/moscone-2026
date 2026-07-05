# G2i

> A vetted-engineer talent network (since 2016) that has repositioned itself as a human-data vendor for frontier AI labs — staffing staff-level software engineers to build evals, RL environments, and code-focused training data.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2016, Miami / Delray Beach, Florida (Verified — company about page, Forbes, CB Insights)
- **Website / GitHub:** https://www.g2i.ai/ (AI training arm), https://www.g2i.co/ (talent platform). No significant public GitHub presence found.

## What they do

G2i runs two connected businesses. The original business (g2i.co) is a video-based hiring platform that vets and places remote software engineers — historically React/JavaScript-focused — with clients like Automattic, Discover Card, and Webflow. The company claims a curated pool of 8,000+ vetted engineers, thousands of placements, over half a million hours of delivered engineering work, and $28M+ paid out to developers (Reported — company site and press; individual figures not independently audited).

The newer arm (g2i.ai), which is what makes them an AIEWF evals-track sponsor, sells "the engineering layer powering AI training" to frontier labs. Concretely: they assemble teams of experienced (they claim staff-level, 10+ years) production engineers to (1) design and review eval tasks and rubrics, turning benchmark results into reliable signal; (2) build custom RL environments with UI/API parity, tool use, scoring, and telemetry; (3) produce expert code-annotation and RLHF training data — engineers ranking and critiquing model-generated code; and (4) build agent workflows. They market against named public benchmarks ("SWE Bench Pro to Terminal Bench 2") and advertise SOC 2 Type II compliance. This is a services/human-data business, not a SaaS product — you engage them as a vendor, not integrate an SDK.

## Founders & origins

Gabe Greenberg, Founder & CEO (Verified — LinkedIn, Forbes, company site). Origin story per Forbes (2021): Greenberg did mission work in Kenya, then built G2i from the open-source JavaScript/React community starting around 2016, with a "developer health" ethos (they fund a Developer Health Fund and run the React Miami conference). The pivot to AI human data appears to date from roughly 2024–2025, when Greenberg publicly shifted focus to RLHF, evals, and RL environments for frontier labs. No co-founders found in public sources.

## Funding

Not found in public sources. Crunchbase lists a "Private Equity" round as the latest event but no public amounts, dates, or investors surfaced (Unverified/Reported — single-source snippet). The company appears to have grown largely bootstrapped off services revenue; treat any funding figure you see elsewhere with suspicion.

## Evidence of real-world use

- Talent-platform customers Automattic, Discover Card, and Webflow are named on G2i's own site and repeated in Forbes coverage (Reported — mostly self-sourced logos, but consistent over years).
- Active, well-paid hiring is strong evidence the AI-training business is real: G2i has been publicly recruiting ~50 software engineers at $100–$200/hour across 150+ countries to evaluate and critique AI-generated code for "frontier labs" (Reported — press coverage and dozens of live listings on Ashby, startup.jobs, Glassdoor).
- The g2i.ai site claims work with "the most ambitious AI labs" but names none — standard for human-data vendors under NDA (Unverified as to which labs).
- Community signal: G2i co-hosted a VIP evals/human-data gathering at AIEWF 2026 (July 1) alongside Orc.ai; Greenberg is visible at NeurIPS and in the human-data community.

## Relevance to agentic AI engineering

G2i sits on the supply side of the eval stack: they are the humans who author the tasks, rubrics, and environments that agentic benchmarks are made of. Their explicit framing around SWE-Bench Pro and Terminal-Bench 2 connects directly to this repo's agentic SWE benchmark papers — the open problem those benchmarks expose (saturation, contamination, weak rubrics) is exactly the gap G2i sells expert task-authorship to fill. Their custom RL environments with tool use, scoring, and telemetry line up with the tool-use/governance research thread (verified tool-call traces as training signal). Less relevant to the agent-memory and voice-agent threads, though their eval-design services could in principle extend there.

## Use cases & considerations

Use cases: (1) commissioning custom evals/rubrics for a domain-specific coding agent when public benchmarks don't fit; (2) building RL environments for agent post-training; (3) sourcing expert human review of agent outputs at scale; (4) plain contract engineering hires.

Considerations: it's a services business — no product to trial, no public pricing, quality depends on which engineers you get. Lab-customer claims are unverifiable. Competitors: Scale AI, Surge AI, Mercor, Turing, Handshake AI, Snorkel — several with far more capital. Open questions: revenue split between staffing and AI-data arms; whether g2i.ai is a separate entity; funding history.

## Sources

- https://www.g2i.ai/
- https://www.g2i.co/
- https://www.g2i.co/about
- https://www.forbes.com/sites/jonyounger/2021/07/12/g2i-and-itarmi-two-purpose-led-tech-freelance-platforms-you-should-know/
- https://www.linkedin.com/in/gabrielgreenberg/
- https://www.crunchbase.com/organization/g2i-0773
- https://www.cbinsights.com/company/g2i
- https://jobbi.org/news/g2i-is-hiring-50-software-engineers-at-up-to-200hour-to-judge-ai-written-code/
- https://jobs.ashbyhq.com/g2i/4af23e04-c31e-4f03-aa9a-8db3c35fbbd7
- https://startup.jobs/software-engineer-for-ai-training-data-school-specific-g2i-inc-5477750
