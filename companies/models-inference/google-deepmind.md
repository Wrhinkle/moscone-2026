# Google DeepMind

> Alphabet's consolidated frontier AI lab — the team behind the Gemini model family, AlphaFold, and (as of 2026) the Antigravity agent-first developer platform.

- **Category:** models-inference
- **AIEWF 2026 tier:** labs
- **Founded:** DeepMind founded 2010, London (Verified — Wikipedia, Britannica); acquired by Google January 2014 for a reported $400M–$650M, TechCrunch reported ">$500M" (Verified acquisition; price Reported, never officially disclosed). Merged with Google Brain in April 2023 to form Google DeepMind (Verified).
- **Website / GitHub:** https://deepmind.google · https://ai.google.dev · https://github.com/google-gemini · https://github.com/google-deepmind

## What they do
Google DeepMind is Alphabet's unified AI research and model-building organization — it ships the models; Google Cloud (Vertex AI) and the Gemini API/AI Studio are the distribution. For an engineer, "buying Google DeepMind" means calling Gemini models via the Gemini API or Vertex AI, or building on their agent tooling.

Current model lineup (as of 2026-07-02, Verified via deepmind.google and Google blogs): **Gemini 3.1 Pro** (released Feb 19, 2026; 1M-token context, 65K output), **Gemini 3.5 Flash** (May 19, 2026 at I/O; positioned as the fast engine for agentic workflows, with reported scores of 76.2% Terminal-Bench 2.1 and 83.6% MCP Atlas — vendor-reported), **Gemini Omni** (any-combination multimodal video generation/editing), **Nano Banana 2** image generation (Feb 2026), plus Veo video models and Deep Research Max, an autonomous research agent.

The developer-tooling story changed sharply in mid-2026: at I/O, Google announced it is retiring the standalone **Gemini CLI** and Gemini Code Assist IDE extensions (individual/Pro/Ultra tiers stopped serving June 18, 2026) and consolidating everything into **Antigravity** — an agent-first development platform with a desktop app (Antigravity 2.0), a new Antigravity CLI sharing the same server-side agent harness, and Managed Agents in the Gemini API (Verified — Google Developers Blog, The Register, GitHub discussion #27274). The **Jules** async coding agent (clones repo, works in a VM, submits PRs) was likewise folded into Antigravity for consumers.

Beyond LLMs: **AlphaFold** (protein structure prediction) and sibling science models, commercialized for drug discovery through Alphabet's **Isomorphic Labs** spin-out.

## Founders & origins
DeepMind was founded in 2010 by **Demis Hassabis** (chess prodigy, computational neuroscience PhD, ex-games industry), **Shane Legg** (ML researcher, coined the modern usage of "AGI"), and **Mustafa Suleyman** (Verified — Wikipedia, Britannica). Google acquired it in 2014 — Hassabis reportedly rebuffed a higher Facebook offer (Reported — Fortune). Suleyman later left (Inflection, now Microsoft AI); Legg remains as Chief AGI Scientist. In April 2023 Alphabet merged Google Brain (founded 2011 at X; origin of the Transformer) with DeepMind under Hassabis as CEO of Google DeepMind (Verified). Hassabis and John Jumper won the 2024 Nobel Prize in Chemistry for AlphaFold (Verified); Jumper's 2026 departure to Anthropic is Reported (secondary outlets only).

## Funding
Not applicable — wholly owned Alphabet unit since 2014; funded internally. Pre-acquisition DeepMind raised venture money from Founders Fund and Horizons Ventures (Reported). Alphabet does not break out DeepMind financials.

## Evidence of real-world use
Among the strongest usage evidence of any AIEWF sponsor (all figures from Alphabet's June 2026 investor presentation / Q1 2026 earnings unless noted — Verified as company-reported, not independently audited):
- Gemini app: ~900M monthly active users (May 2026).
- ~8.5M developers building with Gemini models monthly; ~2.4M active Gemini API developers (+118% YoY); direct API traffic >16B tokens/minute.
- 330 Google Cloud customers each processed >1T tokens in twelve months; 35 passed 10T.
- AlphaFold: used by 3M+ researchers across 190+ countries; AlphaFold Server has produced 8M+ structure predictions (Verified — DeepMind "Five Years of Impact" blog; self-reported).
- Counter-signal: the 30-day Gemini CLI shutdown drew significant developer backlash (HN thread, The Register) — real adoption, but also a churn warning.

## Relevance to agentic AI engineering
Google DeepMind sits at nearly every layer of the agent stack. Antigravity/Jules and the Terminal-Bench claims for Gemini 3.5 Flash land squarely in the agentic-SWE benchmark conversation — *FeatureBench*, *SWE-EVO*, and *SlopCodeBench* (long-horizon degradation) are exactly the evaluation questions Antigravity's fire-and-forget PR agents raise, and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* is the caveat to reading those vendor scores. On tool-use/governance, DeepMind originated the CaMeL prompt-injection defense that *CaMeLs Can Use Computers Too* extends, and Project Mariner-style computer use connects to *Verifiable Software Worlds for Computer-Use Agents*. Deep Research Max relates to the agentic-search/memory thread (*Agentic Search in the Wild*, *Memory for Autonomous LLM Agents*); Gemini's native real-time audio makes it a candidate engine for the voice-agent stack benchmarked in *τ-Voice* and *LTS-VoiceAgent*.

## Use cases & considerations
Use cases: (1) long-context workloads (1M tokens) — whole-codebase or document-corpus analysis; (2) cheap high-volume agentic loops on Gemini Flash tiers; (3) multimodal pipelines (video/image understanding and generation via Omni/Veo); (4) async coding agents via Antigravity for PR-shaped tasks.

Considerations: rapid product churn and short deprecation windows (Gemini CLI got ~30 days); ecosystem lock-in toward Google Cloud/Antigravity harness; benchmark claims are vendor-reported; org is a division, so priorities follow Alphabet strategy. Competitors: OpenAI, Anthropic, Meta (Llama), Mistral, Amazon AGI Labs/Nova. Open question: whether Antigravity's server-side harness becomes an open standard or a walled garden.

## Sources
- https://en.wikipedia.org/wiki/Google_DeepMind
- https://www.britannica.com/topic/Google-DeepMind
- https://techcrunch.com/2014/01/26/google-deepmind/
- https://deepmind.google/about/
- https://deepmind.google/models/gemini/
- https://deepmind.google/models/gemini-omni/
- https://blog.google/innovation-and-ai/technology/developers-tools/google-io-2026-developer-highlights/
- https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/
- https://github.com/google-gemini/gemini-cli/discussions/27274
- https://www.theregister.com/ai-ml/2026/05/20/bye-bye-gemini-cli-google-nudges-devs-toward-antigravity/5243605
- https://news.ycombinator.com/item?id=48196867
- https://blog.google/alphabet/investor-presentation-june-2026/
- https://blog.google/company-news/inside-google/message-ceo/alphabet-earnings-q1-2026/
- https://deepmind.google/blog/alphafold-five-years-of-impact/
- https://deepmind.google/blog/demis-hassabis-john-jumper-awarded-nobel-prize-in-chemistry/
- https://blog.google/technology/ai/google-deepmind-isomorphic-alphafold-3-ai-model/
- https://fortune.com/article/fortune-500-titans-and-disruptors-of-industry-google-deepmind-demis-hassabis-isomorphic-artificial-intelligence/
