# Conductor (Orkes)

> Managed cloud platform for Conductor, the durable, event-driven workflow-orchestration engine originally built at Netflix — now marketed as the runtime for production AI agents.

- **Category:** coding-agents
- **AIEWF 2026 tier:** supporting
- **Founded:** 2021, San Francisco, CA (Orkes the company; Conductor OSS originated at Netflix in 2016) (Verified)
- **Website / GitHub:** https://orkes.io · https://github.com/conductor-oss/conductor

## Disambiguation note
Two unrelated companies share the name "Conductor": (1) **conductor.com**, an enterprise SEO/AEO (answer-engine-optimization) content platform founded 2006; and (2) **Orkes' Conductor**, the open-source agentic-workflow orchestration engine from ex-Netflix engineers. The AIEWF sponsor listing gives no disambiguating description, but the assigned category (coding-agents) and the fact that Orkes is independently hosting an agents-in-production happy hour at this AIEWF ("Harness the Agent," July 1) make Orkes/Conductor the near-certain match; this profile covers that company. If the SEO-platform Conductor was intended instead, disregard this profile.

## What they do
Conductor is a durable execution engine for orchestrating multi-step workflows and AI agents: it externalizes state, error-handling/retries, human-in-the-loop approval steps, and conditional branching outside the agent's own process, so a crashed worker or a long-running tool call doesn't lose progress. It has native LLM/MCP tool-calling integration across 14+ model providers, polyglot workers (Java, Python, Go, JS, C#, Ruby, Rust), and full workflow replay for debugging. Orkes sells the hosted/managed version of the Apache-2.0 OSS project.

## Founders & funding
Founded by Viren Baraiya, Boney Sekh, and Jeu George (co-creators of Conductor at Netflix) with Dilip Lukose (Verified, TechCrunch). Raised $9.3M seed (2022, led by Battery Ventures), $20M (2024, led by Nexus Venture Partners), and $60M Series B (April 2026, led by AVP) — roughly $89M+ total (Verified, BusinessWire/FinSMEs).

## Evidence of real-world use
Conductor OSS has ~32,000 GitHub stars and lists Netflix, Tesla, LinkedIn, and J.P. Morgan as production adopters (Verified via repo). Orkes cites customer growth including a large global retailer, United Wholesale Mortgage, and Quest Diagnostics (Reported, company sources).

## Relevance to agentic AI engineering
Squarely in the agent-orchestration/durable-execution layer this repo tracks: it's the "boring but critical" infrastructure making agents reliable in production (retries, state, human approval) rather than a model or framework itself — complements agent frameworks like LangChain rather than competing with them.

## Sources
- https://github.com/conductor-oss/conductor
- https://orkes.io/
- https://techcrunch.com/2022/02/28/orkes-from-the-creators-of-netflixs-open-source-conductor-workflow-orchestration-tool-comes-out-of-stealth-with-9-3m/
- https://www.businesswire.com/news/home/20260423550324/en/Orkes-Raises-$60M-as-Developers-Increasingly-Use-Its-Platform-to-Deploy-AI-Confidently-in-Production
- https://www.ai.engineer/worldsfair/2026
- https://www.conductor.com/ (the unrelated SEO-platform namesake, for disambiguation)
