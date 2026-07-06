# Why Rust is the Ideal Language for Vibe-Coding

> Daniel Szoke argues that the ease with which LLMs write Python and TypeScript is a liability, and that Rust's strict compiler is the deterministic guardrail agentic coding actually needs.

- **Speaker:** Daniel Szoke, Sentry
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=ugUeZ8-b-u0) (AI Engineer channel; ~16m, released 2026-05-27)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Szoke, the Rust SDK maintainer at Sentry, starts from the conventional wisdom: ask ChatGPT for the best vibe-coding language and it names Python first and TypeScript or JavaScript second, and GitHub reported that AI-assisted development pushed TypeScript to the top language on GitHub by contributor count. The standard reasons are familiarity, framework abundance, fast scaffolding of interpreted code, and the fact that LLMs reliably emit runnable Python and TypeScript on the first try because these languages impose few constraints.

His argument is that almost nobody questions whether first-try runnability is the right thing to optimize. The same dynamic flexibility that makes these languages easy for an LLM to write makes mistakes easy too, and optional typing does not save you when the any type and weak type systems undermine it. LLMs are non-deterministic by design, so they will always be fallible, and just as we guard against human error we need to guard against LLM error. Tests, the usual answer, fall short in specific ways: agents prompted casually write tests after the implementation and end up testing implementation details, tests can generally only prove incorrectness when they fail since exhaustive input coverage is impractical, and the LLM writing the tests or reviewing the code is itself fallible. Szoke borrows from Yuval Noah Harari's book Nexus the framing of LLMs as alien rather than artificial intelligence: token-stream prediction is a powerful but nonhuman way of thinking, so failure modes will surprise us, code that looks polished, well named, and well commented can hide a subtle bug or a heuristic where a reliable check existed. Murphy's Law finishes the setup: without a deterministic guard, human review plus agent review plus tests still eventually lets failures through.

Rust is his deterministic guard. He pitches it as compiled, as fast as C and C++, and built so that if code compiles you can be reasonably confident whole classes of bugs are absent: strict type safety with no any-type escape hatch, no universal null (option types force the check), and fearless concurrency, where the compiler verifies that data shared between threads is accessed safely. His worked example spawns 100 threads incrementing a shared counter through Rc and RefCell. In TypeScript the analogous code compiles, runs, and intermittently returns something other than 100, a data race that is miserable to debug inside a larger application. In Rust it simply does not compile, and the error, "future cannot be sent between threads safely," names the offending Rc RefCell i32 type so an agent can immediately swap in a thread-safe alternative.

The trade-off is explicit: Rust is harder for LLMs to get right on the first try, and Szoke calls that a good thing, because we do not ship raw LLM output, we run agents in loops, and agents are well suited to compile, read rich compiler errors, and fix them. Every compile error is potentially a production bug avoided. To the complaint that Rust compiles slowly, he answers that the compiler is still faster than an AI code review agent and guaranteed to find errors the reviewer might miss. He closes with the sponsor slide: Sentry's agent monitoring features and a free three-month business plan offer.

## Notable moments

- [0:03:16](https://www.youtube.com/watch?v=ugUeZ8-b-u0&t=196s) The heresy stated: being easy for models to write is overstated and sometimes actively bad.
- [0:06:21](https://www.youtube.com/watch?v=ugUeZ8-b-u0&t=381s) Harari's Nexus and the case for calling LLMs alien intelligence with unexpected failure modes.
- [0:11:27](https://www.youtube.com/watch?v=ugUeZ8-b-u0&t=687s) The fearless concurrency demo: a 100-thread counter that races in TypeScript and refuses to compile in Rust.
- [0:14:31](https://www.youtube.com/watch?v=ugUeZ8-b-u0&t=871s) Why constraints suit agents: the compile-error-fix loop beats an AI reviewer on speed and guarantees.

## Connections

- [Sentry](../../companies/evals-observability/sentry.md), the speaker's company, whose agent monitoring pitch closes the talk.
- [GitHub](../../companies/coding-agents/github.md), source of the TypeScript-number-one-by-contributors claim that frames the conventional wisdom.
- [Session recaps](../../notes/session-recaps.md), where the Sonar session covers the adjacent question of whether AI-assisted coding delivers reliable code.
