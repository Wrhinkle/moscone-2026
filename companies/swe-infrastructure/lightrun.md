# Lightrun

> Live production debugging without redeploys — dynamic logs/snapshots/metrics injected into running apps — now repositioned as the "runtime context" layer and AI SRE that lets agents see and fix what code actually does in production.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** gold
- **Founded:** 2019, Tel Aviv, Israel (Verified — TechCrunch, CTech, Insight Partners)
- **Website / GitHub:** https://lightrun.com · https://github.com/lightrun-platform/lightrun

## What they do

Lightrun's core technology is a runtime agent (JVM agent for Java; equivalents for Python, Node.js, and .NET) that lets you insert **dynamic logs, snapshots (virtual breakpoints that capture variable state without pausing), metrics, and traces** into a live running application — no code change, no redeploy, no restart. Actions are added from JetBrains IDEs, VS Code/Visual Studio, or a web console, are sandboxed read-only, and run in Docker, Kubernetes, and even AWS Lambda. Security posture is enterprise-grade: TLS 1.3, AES-256 at rest, SOC 2 Type II / ISO 27001, PII redaction (Verified — docs and site).

Since 2024–25 the company has rebuilt its story around AI. Two product lines today (Verified — pricing page): **Lightrun Runtime Context**, which exposes that live instrumentation to AI coding assistants via a **Lightrun MCP server** (Claude, GitHub Copilot, Cursor, Amazon Q, Gemini are named integrations) so an agent can validate its assumptions against real execution state before shipping a change; and **Lightrun AI SRE**, an autonomous incident-resolution agent that triages alerts, places snapshots to capture variable state "at the exact line, as it fails," does root-cause analysis, and — via an "Error Remediation Automation Skill" — can raise a fix PR with runtime evidence attached, human review last. A newer **Runtime-Aware PR Verifier** simulates how a change behaves against live-system context before merge (Reported — company site).

## Founders & origins

Founded mid-2019 by **Ilan Peleg** (CEO; former Israeli 800m running champion) and **Leonid Blouvshtein** (CTO; HPC/debugging background from an elite IDF intelligence unit). The two met at a bus station during military service and had previously co-founded Hommyfood, briefly, before it was acquired (Verified — CTech, Insight Partners profile). Origin story: Blouvshtein's frustration debugging production systems in the military, generalized into "connect developers to live applications."

## Funding

- **Seed, 2019–2020:** led by Glilot Capital Partners; announced as **$4M** in the June 2020 stealth-exit release, while CTech reported **$6.5M** — sources conflict, so treat the exact figure as Reported.
- **Series A, May 2021:** **$23M** led by Insight Partners (Verified — TechCrunch, VentureBeat).
- **July 2024:** **$18M** round alongside launch of the "Runtime Autonomous AI Debugger" (Reported — SiliconANGLE).
- **Series B, April 2025:** **$70M** co-led by **Accel and Insight Partners**, with Citi, Glilot, GTM Capital, and Sorenson Capital (Verified — TechCrunch, company release).
- **Total:** company states **$110M** raised (Verified as the company's own figure; disclosed rounds sum slightly higher, likely due to the seed discrepancy).

## Evidence of real-world use

Stronger than most gold-tier sponsors. Named Fortune 500 customers in the Series B announcement: **ADP, AT&T, Citi, ICE, Inditex, Microsoft, Priceline, Salesforce, SAP** — note Citi is also an investor, so that logo is partly circular (Verified — company/press). Documented case studies with numbers: **Taboola** reclaimed 260+ engineering hours/month and cut two-week backend investigations to under an hour (Verified — published AWS case study); the site claims **AT&T** cut incident resolution from 5 hours to 30 minutes (Reported — vendor-sourced). Earlier customers: Sisense, Tufin, Cisco (Reported — TechCrunch 2021). A public pricing page exists with a free AI SRE tier, though all paid tiers are contact-sales — commercial but enterprise-motion, not self-serve. The GitHub org is docs/helm-charts rather than a real OSS core; community signal is modest.

## Relevance to agentic AI engineering

Lightrun is a direct bet on the biggest gap in agentic SWE: coding agents reason from static code and stale logs, not from what the program actually did. Their own 2026 report claims 44% of AI-SRE investigations fail because execution-level data was never captured. That is precisely the critique in *ProdCodeBench: A Production-Derived Benchmark for Evaluating AI Coding Agents* and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* — production context, not puzzle-solving, is what's scarce. The MCP runtime-context server is a clean example of tool-use grounding for SDLC agents, and the read-only, sandboxed production access is a practical instance of the guardrail pattern argued in *Governance by Construction for Generalist Agents*. The AI SRE's "knowledge memory engine" (persisting learnings across incidents) connects to the repo's agent-memory thread (hierarchical/maintained memory). Long-horizon relevance: runtime evidence as the feedback signal is what benchmarks like *SWE-EVO* say iterative coding agents lack.

## Use cases & considerations

Use cases: (1) wire Lightrun MCP into Claude Code/Cursor so an agent verifies a hypothesis against live variable state before proposing a fix; (2) autonomous alert-to-PR remediation with human review as the only gate; (3) debugging Python ML pipelines / JVM services in Kubernetes where redeploy cycles are expensive; (4) runtime evidence capture for postmortems in regulated environments (audit logs, PII redaction).

Considerations: requires deploying their agent inside your runtime — real production-access trust decision even if read-only; supports only Java/Python/Node/.NET (no Go or Rust found in docs — Unverified beyond that); opaque contact-sales pricing; autonomous-remediation claims are new and thinly evidenced versus the mature debugging core. Competitors: Datadog (Dynamic Instrumentation + Bits AI), Rookout (acquired by Dynatrace), and the AI-SRE crowd (Cleric, Resolve.ai, Traversal); coding agents with log access could erode the moat from the other side.

## Sources

- https://lightrun.com/
- https://lightrun.com/lightrun-secures-70m-series-b/
- https://techcrunch.com/2025/04/28/lightrun-grabs-70m-using-ai-to-debug-code-in-production/
- https://techcrunch.com/2021/05/26/lightrun-raises-23m-for-its-debugging-and-observability-platform/
- https://www.insightpartners.com/ideas/lightrun-leadership-story/
- https://siliconangle.com/2024/07/31/israeli-developer-observability-startup-lightrun-raises-18m-launches-new-ai-debugger/
- https://www.calcalistech.com/ctech/articles/0,7340,L-3898951,00.html
- https://www.prnewswire.com/il/news-releases/lightrun-announces-4m-for-first-complete-continuous-debugging-and-observability-platform-301082753.html
- https://docs.lightrun.com/
- https://lightrun.com/pricing/
- https://lightrun.com/runtime-context/
- https://lightrun.com/blog/ai-sre-agent/
- https://lightrun.com/resources/how-taboola-slashed-mttr-saved-260-debugging-hours-a-month-with-lightrun/
- https://github.com/lightrun-platform/lightrun
