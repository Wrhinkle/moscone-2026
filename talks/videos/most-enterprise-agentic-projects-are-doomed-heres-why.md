# Most Enterprise Agentic Projects Are Doomed, Here's Why
> Two Accenture practitioners name five enterprise tensions that predict whether an agentic AI project will survive contact with a large organization.

- **Speaker:** Jess Grogan-Avignon & Jack Wang, Accenture
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=AGkzpxMdPn8) (AI Engineer channel; ~21m, released 2026-05-28)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary
Grogan-Avignon and Wang work on agentic deployments inside very large enterprises: telecoms, utilities, government, healthcare. Their opening claim is that the control structures these organizations built for good reasons, layers of process, governance, and sign-off, are now the main drag on AI value. Accenture's research puts only 12% of companies in the "AI achiever" bracket; the rest are stuck piloting. The talk organizes what they have learned into five tensions: speed, value, delivery, trust, and moat.

On speed, Wang argues the bottleneck is the enterprise scaffolding itself, a human operating system running at human pace. His example: an agentic application integrated with a client's centralized AI gateway took about two weeks to build and another twelve months to reach production, because infrastructure, security, AI gateway, data governance, and application teams all had to align. Coding agents make this worse by exploding the supply of deployable code (he cites GitHub reporting 1 billion commits in 2025 and a 2026 pace of 275 million per week, on track for 14 billion) while approval and deployment infrastructure stays unchanged. The prescription: every human process must become adaptable, executable code rather than a sign-off chain, and governance speed should be the CTO's top engineering problem.

On value, Grogan-Avignon attacks the up-front business case. It assumes scope, value, and cost are knowable in advance, when with AI you learn the solution by doing the work. Since prototyping cost is near zero, the right question is what becomes possible, and what not acting costs. She wants CFOs to think like VCs: back a portfolio of bets and expect power-law returns instead of demanding fixed three-year paybacks from each project. AI achievers show about 50% higher revenue growth than peers, which she attributes to new products rather than cost cutting, citing Walmart's trend scanner and generative designer and JPMorgan productizing an internal tool.

On delivery, Wang tells data scientists that agentic delivery belongs to their discipline. Agent behavior is emergent and non-deterministic, so programs should be reshaped around hypothesis-driven work: small loops of build, evaluate, iterate, with statistical confidence as the milestone rather than feature completion.

On trust, Grogan-Avignon lays out an exposure ladder for progressive autonomy. Agents start in shadow mode, running alongside humans without affecting outcomes; move to advisory mode, where they recommend and humans approve; then to controlled autonomy in narrow low-risk scenarios with kill switches; and finally to wider autonomy. Each step is gated by evidence in outcomes, and she frames every release as a deposit or withdrawal in a trust account with stakeholders and customers.

On moat, Wang distinguishes transactional memory (CRM, ERP, SOPs, which every competitor has some version of) from living memory: the edge cases, corrections, and behavioral signals generated when customers touch your product at your scale. Every shipped feature should either generate that feedback signal or act on it; anything else can be cloned. The closing prescription is to bet like a VC, upgrade for machine speed, and engineer for trust with the feedback loop from day one.

## Notable moments
- [0:04:11](https://www.youtube.com/watch?v=AGkzpxMdPn8&t=251s) The AI gateway story: two weeks to build the application, twelve months to get it into production.
- [0:09:14](https://www.youtube.com/watch?v=AGkzpxMdPn8&t=554s) "Your CFO needs to think like a VC," the portfolio argument against per-project business cases.
- [0:15:22](https://www.youtube.com/watch?v=AGkzpxMdPn8&t=922s) The exposure ladder: shadow mode to advisory to controlled autonomy, each step gated by evidence.
- [0:17:24](https://www.youtube.com/watch?v=AGkzpxMdPn8&t=1044s) Transactional memory versus living memory, and why feedback is the only moat.

## Connections
- [Accenture](../../companies/enterprise-adopters/accenture.md), the speakers' employer, whose AI Refinery platform and forward-deployed delivery model is the context for these lessons.
- [Session recaps](../../notes/session-recaps.md), where verification discipline and evals-gated trust recurred as an in-person theme across unrelated sessions.
