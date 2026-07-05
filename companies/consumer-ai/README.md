# Consumer AI

Consumer-facing AI products and apps that do not fit the tooling categories. This is the repo's deliberately small "end of the pipeline" folder: while nearly every other category sells infrastructure, models, or dev tools *to* AI engineers, these companies ship LLM-powered products directly to end users, from chat companions to relationship coaching to automated video editing. The real-world problem they solve is not "how do I build an agent" but "what do ordinary people actually pay for when an agent does the work." For an AI engineering audience they matter as case studies in inference economics at consumer scale, in guardrailed persona design, and in agentic pipelines hidden behind a one-tap UX.

Note on scope: this folder started with ~24 candidates and was intentionally pruned. Most turned out to be B2B/infra companies and were re-filed to better categories after research (see [Re-filed companies](#re-filed-companies-expected-here-found-elsewhere) below). What remains is pure B2C.

## How to read this category

Start with **[Character.ai](character-ai.md)**, the load-bearing profile. It is the canonical consumer-LLM story: Transformer-paper co-author founders, a $1B a16z valuation, ~50K requests/sec on custom models, and then the ~$2.7B Google licence-and-rehire deal that became the template for the "reverse acquihire." It is also a cautionary tale: no API, no B2B surface, and MAUs declining as free frontier chatbots improved.

The other two profiles split on the axis that differentiates consumer AI products: **conversation as the product vs. output as the product**. [CoupleWork AI](couplework-ai.md) is the conversation side, a single tightly guardrailed coaching persona ("Maxine") constrained to clinical therapy frameworks, with an explicit coaching-not-therapy legal boundary. [Reelful](reelful.md) is the output side: the agent is invisible; the user hands over a camera roll and gets a finished narrated video ten minutes later.

## Profiles

| Company | One-liner | Tier | Funding posture | Standout fact |
|---|---|---|---|---|
| [Character.ai](character-ai.md) | Persona-driven consumer chat platform on its own fine-tuned LLMs; pure B2C subscription, no developer API | supporting | ~$193M raised at $1B (a16z, 2023); Google licence-and-rehire deal ~$2.7B-equivalent (2024, Verified) | Served reportedly ~50K requests/sec at peak on custom-trained models, an early proof point for cost-efficient high-QPS LLM serving |
| [CoupleWork AI](couplework-ai.md) | Voice-and-text AI relationship coach ("Maxine") for couples, built on Gottman Method / EFT clinical frameworks | supporting | Bootstrapped/undisclosed; no rounds found in public sources | Explicitly positioned as coaching rather than therapy, a deliberate product/legal boundary that keeps it out of telehealth regulation |
| [Reelful](reelful.md) | iOS app that turns a raw camera roll into an edited, narrated short-form reel in ~10 minutes via an agentic editing pipeline | supporting | $18M+ raised per one newsletter source (single-sourced, treat as Reported) | Solo ex-Snap ML engineer founder built and launched it in ~6 months on Convex.dev's real-time backend |

All three profiles are AIEWF 2026 **supporting** tier. None is a headline sponsor; expect them on stage as case studies rather than booth anchors.

## Re-filed companies (expected here, found elsewhere)

The original candidate list for this category included 21 more companies. All were re-filed after research revealed a B2B/infra core, and none is missing from the repo:

- **B2B agents & automation:** [Bem](../back-office-automation/bem.md), [Extend](../back-office-automation/extend.md), [Modem](../back-office-automation/modem.md) → back-office-automation; [Band](../agent-orchestration/band.md), [Zero](../agent-orchestration/zero.md) → agent-orchestration
- **Dev tools:** [Factory](../coding-agents/factory.md), [Kimchi](../coding-agents/kimchi.md) → coding-agents; [Superconductor](../swe-infrastructure/superconductor.md) → swe-infrastructure
- **Evals & observability:** [Cleric](../evals-observability/cleric.md), [Traversal](../evals-observability/traversal.md), [RelAI](../evals-observability/relai.md)
- **Voice:** [Daily](../voice-realtime/daily.md), [Gradium](../voice-realtime/gradium.md) → voice-realtime
- **Security & identity:** [Keycard](../security-identity/keycard.md), [Runlayer](../security-identity/runlayer.md)
- **Data & models:** [Merge](../data-infrastructure/merge.md), [PromptQL](../data-infrastructure/promptql.md) → data-infrastructure; [Venice](../models-inference/venice.md), [Prior Labs](../models-inference/prior-labs.md) → models-inference; [Ref](../memory-rag-search/ref.md) → memory-rag-search
- **Other:** [Circle](../fintech-payments/circle.md) → fintech-payments; [SonderMind](../enterprise-adopters/sondermind.md) → enterprise-adopters

## Related papers

- [Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation](../../papers/memory-research-agents/memory-for-autonomous-llm-agents-mechanisms-architectures.md): the retention problem behind Character.ai's long-running persona memory. Near-perfect recall systems collapse to 40–60% on multi-session tasks, and the 200–500ms retrieval tax bites hardest in interactive consumer chat.
- [LTS-VoiceAgent: A Listen-Think-Speak Framework for Real-Time Voice Agents](../../papers/voice-realtime/lts-voiceagent-a-listen-think-speak-framework-for-real-time.md): sub-400ms time-to-first-speech for cascaded voice pipelines; directly relevant to whether a voice product like CoupleWork's Maxine can feel conversational without sacrificing reasoning depth.
- [Adaptive Turn-Taking for Real-Time Multi-Party Voice Agents](../../papers/voice-realtime/adaptive-turn-taking-for-real-time-multi-party-voice-agents.md): treats "is it my turn, given my role?" as a modeling problem. A couples-coaching session is exactly the multi-party setting (two partners + one agent) where naive VAD-based agents interrupt or go silent.
- [ProVoice-Bench: Assessing the Proactivity of Voice Agents](../../papers/voice-realtime/provoice-bench-assessing-the-proactivity-of-voice-agents.md): measures when an agent should speak at all. Over-triggering is the dominant failure mode, which is the core UX risk for any always-listening consumer coach or companion.

## Open questions

1. **Can consumer AI defend against free frontier chatbots?** Character.ai's MAU decline (~28M → ~20M) as ChatGPT/Gemini improved suggests generic conversation is a melting asset. Do narrow, framework-constrained products (CoupleWork) or output-first products (Reelful) hold up better?
2. **What is the durable moat: model, persona, or workflow?** Character.ai bet on custom models and its founders were bought back by Google; the survivors here bet on clinical frameworks and editing pipelines instead. Nobody in this folder has demonstrated a retention moat with public numbers.
3. **Where is the liability line for AI coaching?** CoupleWork's coaching-not-therapy framing is a product decision doing legal work. No profile in this category yet documents how these boundaries survive regulatory scrutiny or a safety incident.
4. **Do consumer apps ever grow an API?** All three are closed, no-API products. The category's relevance to this repo's engineer audience stays limited to case studies unless one of them opens a developer surface.
