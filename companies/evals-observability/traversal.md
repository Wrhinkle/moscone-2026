# Traversal

> An AI site reliability engineer for large enterprises: agents that triage alerts, trace production incidents to root cause across sprawling distributed systems, and increasingly remediate them — built by causal-ML academics who turned troubleshooting into a search problem.

- **Category:** evals-observability
- **AIEWF 2026 tier:** gold
- **Founded:** 2023, New York (Verified — Fortune, Sequoia, Cornell Tech all agree)
- **Website / GitHub:** https://www.traversal.com — no significant public GitHub org found (closed-source enterprise product; listed on AWS Marketplace)

## What they do

Traversal sells an "AI SRE" for enterprise incident response. The system ingests the customer's existing telemetry — logs, metrics, traces, alerts, plus git history for code-change correlation — and does the diagnostic work an on-call engineer would do, at machine speed. Two named components anchor the architecture: a **Production World Model**, a continuously maintained dependency map of the production estate (the site cites 1.7M+ nodes across ~30 resource types: pods, services, databases, hosts, load balancers, queues), and a **Causal Search Engine** that traverses that graph during an incident to separate root cause from symptom cascade. The causal framing is not branding: three of the four founders are causal-inference researchers, and the core bet is that RCA is a causal search over a dependency graph rather than a summarization task over dashboards.

Product surface (Verified from company site): autonomous alert triage; incident RCA delivered in minutes; "self-healing" that converts a diagnosis into automated remediation; a natural-language interface for querying live production state; and **Traversal Workers**, proactive agents that act unprompted to prevent incidents. It integrates with Kubernetes, cloud infra (EC2, storage, LBs), Postgres/MySQL/TimescaleDB, message queues, monitoring stacks, and git. No public pricing page — enterprise sales motion, with an AWS Marketplace listing (Verified as of 2026-07-02). CEO Anish Agarwal frames the roadmap as "agentic incident response": diagnose first, then progressively earn write access to remediate (Reported — SiliconANGLE).

## Founders & origins

Four co-founders who met as researchers (Verified — Fortune, Cornell Tech, Sequoia):
- **Anish Agarwal, CEO** — MIT PhD, left a tenure-track faculty position at Columbia to start the company; causal inference/ML researcher, originally from Singapore.
- **Raaz Dwivedi** — assistant professor at Cornell Tech (causal ML/statistics).
- **Raj Agrawal** — MIT PhD, causal ML (Reported spelling varies: "Agrawal" per Fortune, "Agarwal" in some profiles).
- **Ahmed Lone** — former Citadel Securities quant trader; the one founder who lived the on-call problem in industry rather than academia (Reported — Sequoia).

Origin story: the team concluded that the causal-discovery methods they were publishing mapped directly onto the "what changed and what did it break" structure of production troubleshooting, which Agarwal calls one of the most complex workflows in software.

## Funding

- **$48M total across seed + Series A**, announced together when the company left stealth in June 2025 — Sequoia led the seed, Kleiner Perkins led the Series A; NFDG (Nat Friedman/Daniel Gross) and Hanabi Capital participated (Verified — Fortune, SiliconANGLE, company blog).
- **Strategic investment from Amex Ventures**, March 2026, alongside a commercial partnership; total raised reported at roughly $53M after this round (Reported — SiliconANGLE exclusive).

## Evidence of real-world use

Unusually strong for the category, though nearly all numbers are vendor- or customer-reported rather than independently benchmarked:

- **DigitalOcean** — published case study: 38% MTTR reduction, ~3,600 engineering hours/year saved; incidents that took engineers an hour root-caused in under a minute (Verified — Traversal case study + Fortune's independent "37% faster over six months" figure).
- **American Express** — 82% root-cause accuracy and 32% MTTR reduction within six months of deployment, followed by Amex Ventures investing (Verified — SiliconANGLE + Traversal announcement).
- **PepsiCo** — 80% RCA accuracy, ~6,000 engineering hours/year (Reported — company site).
- **Cloudways** — 70% MTTR reduction, 96,000 support-engineering hours/year (Reported — company site).
- **Eventbrite** and unnamed Fortune 100 financial institutions cited at launch, with engineers reporting >90% accuracy on hundreds of high-impact incidents (Reported — launch press).

## Relevance to agentic AI engineering

Traversal is one of the clearest production deployments of long-horizon, tool-using agents operating over real infrastructure. For this repo's threads: the world-model + causal-search design is a live answer to the **agent memory** question — persistent structured environment knowledge instead of per-incident context stuffing (compare Cleric's episodic "operational memory" approach in the same category). The diagnose-first, remediate-later posture is a concrete **tool-use governance** pattern: read-only agents earning write access. And on **agentic SWE benchmarks**: incident diagnosis still has no dominant SWE-bench equivalent — emerging efforts like SREGym and SRE-skills-bench exist, but Traversal's accuracy claims (80–82% RCA) are self/customer-reported, which is exactly the evaluation gap the benchmark papers highlight.

## Use cases & considerations

Use cases: (1) first-line triage for high-alert-volume enterprise environments; (2) MTTR compression on Sev-1s in deep microservice estates where no single engineer holds the dependency graph; (3) reducing escalation load on senior engineers/support orgs (the Cloudways pattern); (4) feeding production failure context back into dev workflows.

Considerations: enterprise-only motion with no public pricing or self-serve tier — evaluation requires a sales cycle; value scales with telemetry quality and system complexity (likely overkill below a few hundred services); the per-environment world model creates real switching costs. Crowded, fast-moving category: **Cleric**, **Resolve.ai**, **Datadog Bits AI**, **incident.io**, and incumbents (Dynatrace Davis) all converge here. Open questions: independent accuracy verification, how much remediation is actually autonomous today versus roadmap, and model/inference dependencies (not publicly documented).

## Sources

- https://www.traversal.com/
- https://www.traversal.com/blog/launch-announcement
- https://www.traversal.com/blog/american-express-announcement
- https://traversal.com/customer-stories/digitalocean
- https://fortune.com/2025/06/18/traversal-emerges-from-stealth-with-48-million-from-sequoia-and-kleiner-perkins-to-reimagine-site-reliability-in-the-ai-era/
- https://siliconangle.com/2025/06/18/traversal-launches-48m-tackle-site-reliability-observability-ai/
- https://siliconangle.com/2026/03/04/exclusive-american-express-partners-invests-ai-operations-startup-traversal/
- https://sequoiacap.com/article/partnering-with-traversal-because-every-engineer-remembers-their-first-time-troubleshooting/
- https://tech.cornell.edu/news/traversal-ai/
- https://www.dash0.com/podcast/33-inside-the-ai-sre-boom-anish-agarwal
- https://aws.amazon.com/marketplace/pp/prodview-76q4p3nhuqgj4
