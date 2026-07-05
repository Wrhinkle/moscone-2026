# LinkedIn

> The professional network (Microsoft-owned) that has shipped a production agentic AI system — Hiring Assistant — inside a regulated, large-scale consumer platform.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** 2002, Mountain View, CA; acquired by Microsoft in 2016 for ~$26.2B (Verified — widely documented)
- **Website:** https://www.linkedin.com · Engineering blog: https://www.linkedin.com/blog/engineering

## What they do
For an AI-engineering audience, LinkedIn's relevant surface isn't the social product but its **agentic AI platform** built to run agents like Hiring Assistant at scale. Per LinkedIn's own engineering writeup, the core is an "agent life-cycle service" — a stateless coordination layer between agents, data sources, and applications — built on messaging as the primary abstraction rather than direct RPC, with explicit support for long-running tasks, switching between interactive and batch modes, and role-based authorization/authentication over regulated personal data. Hiring Assistant itself sources candidates, drafts tailored search strategies beyond keyword filters, and handles recruiter back-and-forth conversationally, integrated with Microsoft Teams for feedback loops.

## Founders & funding
Founded by Reid Hoffman and colleagues from PayPal/SocialNet; now a wholly owned Microsoft subsidiary — not independently funded (Verified).

## Evidence of real-world use
Hiring Assistant is globally available (not a demo): LinkedIn reports recruiters using it review 81% fewer profiles per qualified match and see 66% higher InMail acceptance rates, saving ~1.5 hours per role (Reported — LinkedIn/news.linkedin.com).

## Relevance to agentic AI engineering
A rare public architecture writeup of a large-scale agent orchestration layer (state, memory, auth, long-running tasks) running in production against sensitive user data — directly relevant to agent-orchestration and identity/security tracks at AIEWF.

## Sources
- https://www.linkedin.com/blog/engineering/ai/how-we-engineered-linkedins-hiring-assistant
- https://www.infoworld.com/article/4054974/how-linkedin-built-an-agentic-ai-platform.html
- https://news.linkedin.com/2025/hiring-assistant-globally-available
- https://leaddev.com/ai/how-linkedin-built-ai-hiring-agent
