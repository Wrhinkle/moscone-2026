# The Miranda Hypothesis: How Hamilton Poisoned Persona Evals

> An argument that persona evals measure fluency and personality consistency while missing the dominant failure mode, anachronistic compositing, plus a pre-registered instrument to catch it.

- **Speaker:** Jacob E. Thomas, Results Gen
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=IJXjTLPzvAU) (AI Engineer channel; ~58m, released 2026-06-25)
- **Program:** Online Track 2026

## Summary

Thomas, a data scientist who runs the analytics lab at a labor market intermediary and trained as a behavioral epidemiologist, opens with role-playing language agents in the wild: Character AI, the Hello History tutor app, and his own open source prompt framework, Companion, running on Claude Opus 4.7. His organizing question is what persona evals actually measure. The in-character style benchmarks he surveys report state-of-the-art systems at 80.7 percent alignment with human-perceived personality, yet the same high-scoring systems render a Hamilton who sounds like he has read his own Broadway musical. His thesis: if the dominant failure mode is anachronistic compositing and your evals measure fluency and personality consistency, your evals cannot detect the dominant failure.

He is careful to credit the field's progress, from rule-based templates to imitation to cognitive simulation, citing systems like CoSER, built from nearly 18,000 characters whose 70B model matches or beats GPT-4 on three benchmarks. But these instruments measure whether a model reproduces a personality profile, and have no mechanism to check whether the character stays within his documentary record at a specific moment of his life. Thomas calls the gap the mask and the mirror, and demonstrates it live: a frontier model's Hamilton delivers the orphan-immigrant ambition arc of the 2015 musical rather than dry Federalist syntax, and answers a slavery question as a clean abolitionist when the scholarly record shows a man who joined the Manumission Society while conducting slave transactions for in-laws and clients.

The Miranda hypothesis names the mechanism. Culturally dominant representations of a figure exceed the primary record in volume and recency, next-token prediction compresses both into parameters with no way to distinguish a 1789 letter from a 2019 viral tweet, and the output is a salience-weighted composite that corresponds to the figure at no verifiable moment. The Federalist Papers total roughly 175,000 words; musical-derived content exceeds that by orders of magnitude. His physical-world evidence is the Schuyler Mansion, where visitation nearly tripled after the musical and staff spent their time unteaching it. Worse, he argues alignment amplifies the problem, because human raters carry the same mythologized composites, a failure he calls algorithmic sycophancy. Time-locked models do not fix it either, since period anchoring is not persona anchoring.

His proposed fourth stage, epistemic simulation, moves the constraint outside the model: corpus-bounded reasoning, a temporal anchor, and expert-in-the-loop evaluation. For role-playing systems he replaces "agent" with role-playing language system, five components where the persona lives in the configuration, not the checkpoint, no more located in the weights than Hamlet is located in Laurence Olivier's body. That favors context-window architectures over fine-tuning, which he argues layers a thin personal signal over cultural sediment and breaks provenance; he cites a 2026 Nature Medicine study where general frontier models beat specialized clinical tools across 12 clinics, and work showing biomedically fine-tuned models underperform their bases through catastrophic forgetting. The context window is also a kitchen-table capability, open to a grandchild with her grandmother's letters, where fine-tuning is institutional.

The instrument is pre-registered with historian Rick Halpern of the University of Toronto and Shawn Martin of Washington College: four temporally distinct Lincolns (1847 Whig congressman, 1858 debater, 1860 constitutional unionist, 1862-65 emancipator), three seeding conditions (bare model, biography, primary sources), five diagnostic questions, 60 responses scored on a rubric weighting anachronism detection 40 percent, documentary consistency 35, contextual plausibility 25, with rhetorical authenticity deliberately excluded. The bare model's 1847 Lincoln already fails, reasoning about inherent executive authority in Spielberg's cadences, while Lincoln's actual 1848 letter to Herndon flatly rejects unilateral war power. The talk ends where the project began, a failed attempt to give language back to a person with advanced dementia that produced a composite instead of the person. His threshold: you want a model that can speak with your mother's documents in the room.

## Notable moments

- [0:04:11](https://www.youtube.com/watch?v=IJXjTLPzvAU&t=251s) The thesis against the 80.7 percent benchmark score: evals built on fluency cannot detect anachronistic compositing.
- [0:19:23](https://www.youtube.com/watch?v=IJXjTLPzvAU&t=1163s) Why alignment makes it worse: raters grew up with the same composite, so post-training rewards the Hamilton you already believe in.
- [0:44:42](https://www.youtube.com/watch?v=IJXjTLPzvAU&t=2682s) The 1848 Lincoln letter to Herndon, the primary-source prism against the bare model's Spielberg Lincoln.
- [0:54:48](https://www.youtube.com/watch?v=IJXjTLPzvAU&t=3288s) The origin story in a hospital room, and the line that a system fabricating your own beloved is a violation, not a limitation.

## Connections

- [Character AI](../../companies/consumer-ai/character-ai.md) is the deployed platform the talk opens with, the commercial scale at which persona fidelity failures ship to millions of users.
