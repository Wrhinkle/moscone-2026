# Every Solo Agent Builder Eventually Reinvents a Worse Version of CI/CD

> A solo builder's case that agent pipelines quietly rebuild regression tests, monitoring, contracts, staging, and audit trails, and that blocking gates are the fix.

- **Speaker:** Sumaiya Shrabony, independent builder
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=WLXxTaPagA8) (AI Engineer channel; ~11m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Sumaiya Shrabony runs a 19-skill Claude Code agent system covering writing, research, vault sync, analytics sync, hooks, and transcripts, and her talk is about what building it alone actually taught her. You think you are building prompts, she says; build long enough and you are building something that looks suspiciously like CI/CD, except worse, because you assemble it from scratch one failure at a time. Her open source content engine runs every other Saturday: it reads a knowledge vault, creates a research brief, builds a content plan, produces 12 content pieces, then runs verify passes, reviewer gates, and deduplication before saving markdown output. What matters for the talk is that this pipeline has seven handoffs, scheduler to command through reviewer to output folder, and every handoff is a place the system can lie to you, with nobody but the solo builder to catch it.

The core pattern is five reinventions arriving in a predictable order. A prompt change breaks something downstream, so you test output shapes: regression testing. A cron job fails silently for a week, so you build alerts: CI monitoring. One skill changes its output schema and three downstream skills break, so you validate at boundaries: contract testing. An artifact looks done but should not ship, so you add a checkpoint before the ready folder: staging. Something goes wrong and you cannot tell which prompt or handoff produced it, so you log everything: audit trails. Shrabony argues agent systems need the exact same operational guarantees as software and give you none of them by default.

Her demo skips the happy path on purpose. She runs a distilled, privacy-safe version of the production pipeline in two modes and shows three ways output that looks ready is not. First, voice drift: a piece opening with "Unlock the power of AI adoption" and generic marketing phrasing has all required sections and a ready status, so naive mode ships it; guarded mode blocks it at a voice contract. Second, missing verification: a piece claims teams "reduce AI rollout rework by 37%," a specific, plausible number with an empty verification log. Naive mode ships it, guarded mode refuses to let claim-bearing content through without a verification trail, because "trust me" is not a verifier. Third, her favorite as the most realistic solo-builder failure: a near-duplicate hook, an opening angle already used in the vault history, caught by the deduplication contract, which also writes an audit record so a 2 a.m. failure can be reconstructed gate by gate.

The prescriptions are deliberately boring: a pre-save output contract, a voice or domain contract, a verification contract for claims, a deduplication check, and an audit trail. No platform or framework required. Her closing sequence: map your handoffs, since every arrow is a corruption point; put the first gate on the most expensive handoff rather than the most complex one, the wrong public claim or the schema break that cascades; and make the gate say no, because a gate that only logs warnings is a suggestion. The dangerous failure is never the obviously bad output, it is the failure the system formats nicely and ships downstream.

## Notable moments

- [0:01:02](https://www.youtube.com/watch?v=WLXxTaPagA8&t=62s) The seven handoffs in her pipeline, each a place the system can lie.
- [0:02:04](https://www.youtube.com/watch?v=WLXxTaPagA8&t=124s) The five reinventions in order, from regression testing to audit trails.
- [0:06:07](https://www.youtube.com/watch?v=WLXxTaPagA8&t=367s) An unverified "37%" claim with an empty verification log, shipped by naive mode and blocked by guarded mode.
- [0:09:09](https://www.youtube.com/watch?v=WLXxTaPagA8&t=549s) Map handoffs, gate the most expensive one, and make the gate block rather than warn.

## Connections

- [CircleCI](../../companies/swe-infrastructure/circleci.md): a mature version of the CI guarantees she argues solo agent builders rebuild by hand.
- [Session recaps](../../notes/session-recaps.md): verification discipline for agent output was a recurring in-person theme, notably Sonar's zero-trust framing.
