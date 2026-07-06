# The Pipeline Is Dead

> An argument that the frozen-artifact software pipeline existed only because producing code was expensive, and a bet on per-user divergences of a canonical stem now that it is not.

- **Speaker:** Iris ten Teije, Sky Valley Ambient Computing
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=bRnoEpoK5m4) (AI Engineer channel; ~20m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Ten Teije, listed under Sky Valley Ambient Computing and speaking as co-founder of a startup she calls Differ in the talk, starts with the entire distribution stack: CI pipelines, packagers, registries, container images, app store reviews. All of it exists to move one frozen artifact from the machine that built it to the machines that run it, safely and once. Her claim is that the stack encodes an assumption nobody ever chose: one version of the software for everyone. That assumption held because producing a correct change took skilled humans hours or days, so changes were rare central events you verified, froze, and shipped. The frozen artifact bought reproducibility, previews, and rollback, and the price was software that fits no one in particular. Per-user versions were never rejected in a meeting; they meant forking and hand-maintaining code bases, so they were never an option. Her co-founder Noam was the first engineer at JFrog and helped build the pipeline she is declaring dead; she spent a decade in fintech, including scaling and exiting a digital bank.

What changed is not just that AI writes code, which she calls table stakes, but that the cost of a correct, scoped change is collapsing toward zero and production no longer has to happen in one place before anyone runs the software. Parts can run on the server, the client, or inside the user's live session. She grounds the demand side in decades of evidence: forward-deployed engineers and professional services for large Salesforce customers, dotfiles and editor configs that engineers rebuild on every machine, and Excel, millions of people building their own programs on top of one product. Feature flags, segmentation, and A/B testing tried to make software diverge but forced divergence into buckets declared in advance.

The bet: when the agent is the runtime, the thing that runs your software can also modify it, and development and distribution stop being phases. Instead of one code base gated by flags, you deploy one canonical stem and every user runs their own divergence of it, individually adapted live. To the CTO who told her she was describing his worst problem multiplied by millions, she answers that the feared brittleness is unmanaged divergence inside a single artifact with no boundaries. Divergences in her architecture are bounded, isolated, and individually reversible; a bad variant cannot corrupt the stem or reach another user, the blast radius is one context, and any divergence rolls back live with no deploy. Developers set what can adapt: a form can be reshaped to improve conversion, but marked fields can never be dropped and auth or payments stay off limits. Her worked example is an investor using a CRM built for salespeople; the system observes that she always logs who made each intro, skips certain fields, and prioritizes deals differently, and it adapts, letting horizontal SaaS serve more personas without more R&D spend.

She closes on the unsolved parts, which she says are the actual business. Source of truth becomes the stem plus immutable, inspectable, attributable divergences, and lineage becomes a graph query instead of a version number. Correctness means testing the stem and every divergence. Desirability means measuring whether a correct change actually improved retention, churn, or support volume. On autonomy she rejects recommendations-only as the end state; the goal is a system legible and reliable enough that humans choose to step back. On coordination across a million versions: don't merge code, merge intent, so everyone converges on the same goal through their own path. Generation, she argues, is the easy 80%; provenance, validation, and coordination are the hard part.

## Notable moments

- [0:02:00](https://www.youtube.com/watch?v=bRnoEpoK5m4&t=120s) The frozen-artifact deal: one unchanging version for everyone, called reliability, priced at software for no one in particular.
- [0:08:04](https://www.youtube.com/watch?v=bRnoEpoK5m4&t=484s) A skeptical CTO's objection, one AI code base is already hard to reason about, and the stem-plus-divergences answer.
- [0:11:06](https://www.youtube.com/watch?v=bRnoEpoK5m4&t=666s) The CRM example: the system observes an investor's habits and reshapes fields and prioritization for her.
- [0:17:15](https://www.youtube.com/watch?v=bRnoEpoK5m4&t=1035s) Coordination across a million versions: don't merge code, merge intent.

## Connections

- [GrowthBook](../../companies/evals-observability/growthbook.md) represents the feature-flag and A/B-testing generation ten Teije frames as the pre-declared-bucket predecessor to adaptive software.
- [Architecture Without Architects](../../papers/planning-architecture/how-ai-coding-agents-shape-software-architecture.md) studies the flip side of agents making live structural decisions, the unreviewed "vibe architecting" her bounded-divergence design tries to contain.
