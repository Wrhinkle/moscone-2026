# The AI bugpocalypse is here. Now what?

> A former CISA advisor on frontier models finding and exploiting vulnerabilities at scale, and why secure-by-design rewrites beat whack-a-mole patching.

- **Speaker:** Jack Cable, Corridor
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=7JgIS42mz7U) (AI Engineer channel; ~20m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Cable is co-founder and CEO of Corridor, an 18-month-old company focused on securing AI coding. Before that he was a senior technical advisor at CISA working on the secure-by-design initiative, and he was a top-100 ranked hacker on HackerOne while in high school. His framing: both ends of the equation are shifting at once. Frontier models keep getting better at discovering and exploiting vulnerabilities, especially in the open-source libraries everything depends on, while attack surfaces grow because AI is becoming the default code writer. He cites Stack Overflow figures of roughly 84% of developers using AI coding tools and 30 to 40% of companies encouraging them, and notes the shift from autocomplete to agents launched from Slack running in the background for hours.

Cable's good news is that the vulnerabilities frontier models find are not new classes. The top entries in MITRE's list of classes behind CISA's known-exploited-vulnerabilities catalog are decades old, and defenders have known how to prevent many of them at scale for decades. Buffer overflows were documented more than 30 years ago, and memory-safe languages make that class impossible to introduce. He puts the payoff in numbers: roughly 60 to 70% of vulnerabilities in products written in memory-unsafe languages are preventable with memory-safe languages, and Google's Android data shows memory-safety bugs falling from about 75% of vulnerabilities in 2019 to around 30% in 2022, achieved just by writing new code in memory-safe languages rather than rewriting old code. His policy conclusion follows: rather than pour millions into one-off patches for open-source libraries, do one-time rewrites of critical libraries into a language like Rust, whose guarantees hold no matter how smart future models get.

On the introduction side, Cable argues security is contextual and models often lack the context to know they are creating a bug. He points to a case where Opus 4.6 introduced a smart-contract vulnerability that led to a couple million dollars being stolen, and to BaxBench, from researchers at ETH Zurich and UC Berkeley, which finds even the best models introduce vulnerabilities about 20 to 40% of the time when writing code. What his customers see is a shift away from one-liner bugs toward contextual issues like authorization flaws that require understanding a company's business logic, which no foundation model is trained on. Corridor's position is that within 6 to 12 months the majority of shipped code will be reviewed by AI rather than humans, since code review is now the bottleneck, so the job is preventing vulnerabilities before the pull request and giving security teams visibility so they can approve autonomy with guardrails instead of blocking it.

He closes with policy. Cable joined a letter urging the White House to lift export controls on the newest frontier models, arguing the benefit to defenders outweighs the risk given that distillation is shrinking the gap between closed and open-weight models and adversaries already have powerful models. His recent congressional testimony made three recommendations: prevent vulnerabilities in new code as development accelerates, harden the open-source foundation with systemic rewrites rather than one-off patches, and foster an American ecosystem of frontier open-weight models, which he ties to fine-tuning needs and competitiveness.

## Notable moments

- [0:06:03](https://www.youtube.com/watch?v=7JgIS42mz7U&t=363s) The MITRE top exploited vulnerability classes are decades old, and models like Mythos find the same ones.
- [0:08:04](https://www.youtube.com/watch?v=7JgIS42mz7U&t=484s) Google's Android chart: memory-safety vulnerabilities drop from about 75% to 30% just by writing new code in memory-safe languages.
- [0:11:08](https://www.youtube.com/watch?v=7JgIS42mz7U&t=668s) BaxBench shows top models introduce vulnerabilities in 20 to 40% of coding tasks; an Opus 4.6 smart-contract bug cost a couple million dollars.
- [0:16:09](https://www.youtube.com/watch?v=7JgIS42mz7U&t=969s) Cable's three recommendations from his testimony to the US Congress.

## Connections

- [Snyk](../../companies/security-identity/snyk.md) sells scanning and guardrails for AI-generated code, the incumbent tooling in the space Corridor is entering.
- [Aikido](../../companies/security-identity/aikido.md) is another vendor consolidating code and dependency security for teams shipping AI-written code.
- [Session recaps](../../notes/session-recaps.md) covers Sonar's in-person session on zero-trust, multilayer verification of AI-written code, the review-side complement to Cable's prevention argument.
