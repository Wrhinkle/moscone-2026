# Inth

> A YC-backed enterprise privacy-governance startup, built around the open-source consent SDK c15t, that automates cookie-consent, data-subject-request, and privacy-compliance workflows for fast-shipping engineering teams.

- **Category:** security-identity (category note: Inth's actual product is privacy/consent/compliance governance, not identity/access management in the IAM sense — see Use cases & considerations)
- **AIEWF 2026 tier:** supporting
- **Founded:** 2026 (YC Spring 2026 batch), San Francisco area (Verified via YC)
- **Website / GitHub:** https://inth.com/ · https://www.ycombinator.com/companies/inth · c15t: https://c15t.com/

Disambiguation note: searched for other "Inth" AI companies to rule out collision — none found. This is the only identifiable company matching the name in the AI/dev-tools space.

## What they do
Inth builds code-native privacy governance: consent management, data subject request (DSAR) handling, vendor oversight, and audit-ready compliance evidence, aimed at engineering teams (not legal/GRC teams) shipping fast, including where AI systems or agent-written code moves user data. Its entry point is c15t, an open-source, performance-focused consent/cookie-banner SDK that developers drop into a codebase instead of using slow third-party consent-management platforms; Inth then layers enterprise workflow/governance tooling on top.

## Founders & funding
Founded by Christopher Burns (Reported, via YC company page). Backed by Y Combinator (Spring 2026 batch) (Verified); no seed/Series A amount disclosed publicly beyond YC membership — treat specific dollar figures as Not found in public sources.

## Evidence of real-world use
c15t reports 3M+ npm downloads and is used by named developer-tools companies Zed, Infisical, and Expo (Reported, per YC/company materials), plus unspecified "luxury hotel chains and online supermarkets." npm download counts and named OSS-adjacent dev-tool customers are reasonably strong usage signals, though total figures are company-sourced.

## Relevance to agentic AI engineering
Positioned at the intersection of privacy/compliance and AI: explicitly calls out "agent-written changes that move user data" as a risk surface, i.e., as agentic coding tools autonomously touch data pipelines, someone needs automated guardrails/audit trails around consent and data rights — relevant to teams pairing coding agents with production systems that handle user data, and adjacent to security/observability tooling elsewhere in this repo.

## Use cases & considerations
Use cases: (1) drop-in performant cookie/consent banner without CMP latency hit; (2) automating DSAR fulfillment across vendors; (3) audit trail generation for privacy compliance in fast-moving codebases. Considerations: category placement here as "security-identity" is imprecise — Inth is privacy/compliance governance, closer to legal-tech/GRC than IAM or non-human-identity security (compare Entro Security, Persona, Veza, which are true identity-security plays surfaced during this research but are not "Inth"). Main competitors are traditional consent-management platforms (OneTrust, Cookiebot) which Inth positions itself against on performance/dev-ergonomics grounds. Very early-stage (2026 YC batch); pricing not published.

## Sources
- https://www.ycombinator.com/companies/inth
- https://inth.com/
- https://c15t.com/
