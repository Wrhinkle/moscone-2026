# OpenAI

> The maker of ChatGPT, the GPT model family, and the Codex coding agent — the most valuable private AI company in history and the default first API most teams try.

- **Category:** models-inference
- **AIEWF 2026 tier:** labs
- **Founded:** December 2015, San Francisco, as a nonprofit AI research lab (Verified — Wikipedia, Britannica). Restructured October 28, 2025 into **OpenAI Group PBC**, a for-profit public benefit corporation controlled by the OpenAI Foundation nonprofit (Verified — CNBC, openai.com statement).
- **Website / GitHub:** https://openai.com · https://developers.openai.com · https://github.com/openai

## What they do
OpenAI ships frontier models and sells them three ways: the **ChatGPT** consumer/enterprise app, the **API** (Responses API on developers.openai.com), and **Codex**, its agentic coding product (CLI, IDE extension, cloud agent, and an SDK/MCP server you can embed in your own harness). For an engineer, "integrating OpenAI" in mid-2026 means calling the GPT-5.x family over the API, building agent loops with the **Agents SDK / AgentKit** (which now includes configurable memory, sandbox-aware orchestration, Codex-style filesystem tools, and ChatKit for UI), or wiring Codex into CI and multi-agent dev workflows.

Model lineup as of 2026-07-02 (Verified — OpenAI model release notes and API docs): **GPT-5.5** and **GPT-5.5 Pro** (released April 23, 2026; in API April 24), the **GPT-5.4** family (Thinking/Pro/mini/nano) and GPT-5.3 Instant still serving, **GPT-5.3-Codex** as the dedicated agentic coding model, and a limited preview of the **GPT-5.6 series** — Sol (flagship), Terra (mid-tier, claimed GPT-5.5-competitive at half the cost), Luna (cheapest) (Reported — OpenAI announcement pages; preview-stage claims are vendor-reported). Sora (video) and the Realtime voice stack round out the multimodal surface.

## Founders & origins
Founded December 2015 by a large group: **Sam Altman** and **Elon Musk** as co-chairs, with **Greg Brockman** (ex-Stripe CTO), **Ilya Sutskever** (ex-Google Brain), **John Schulman**, **Wojciech Zaremba**, **Andrej Karpathy**, **Durk Kingma**, **Vicki Cheung**, **Pamela Vagata**, and **Trevor Blackwell** (Verified — Wikipedia, MIT Technology Review). Launched with a $1B pledge from Musk, Altman, Thiel, Hoffman, Livingston, AWS, and Infosys — of which only ~$133M had actually been collected by 2021 (Verified — Wikipedia; the gap is documented in the Musk litigation record). Musk left the board in 2018. Of the founders, only Altman (CEO) and Brockman (President) remain; Sutskever, Schulman, and Karpathy all departed 2024–2025 (Verified).

## Funding
- 2019–2023: Microsoft invested ~$13B cumulatively starting with $1B in 2019 (Verified — widely reported).
- March 2025: **$40B** SoftBank-led round at **$300B** post-money — largest private round on record at the time (Verified — CNBC, OpenAI).
- Feb–March 2026: announced $110B (SoftBank $30B, NVIDIA $30B, Amazon $50B), closed at **$122B** committed capital and an **$852B post-money valuation**, co-led by SoftBank with a16z and D. E. Shaw Ventures participating (Verified — CNBC, OpenAI announcement).
- Post-restructuring, Microsoft holds ~27% (~$135B) with model/product IP rights through 2032; the deal reportedly voids if OpenAI reaches AGI (Verified stake — CNBC; AGI clause Reported).
- WSJ-reported groundwork for a Q4 2026 IPO, possibly at $1T+ (Reported — CMC Markets, PitchBook commentary).
Total primary capital raised exceeds ~$180B (computed from the above; Reported).

## Evidence of real-world use
Company-reported but consistent across independent coverage (mark all as self-reported unless noted):
- ChatGPT: 900M+ weekly active users (Feb 2026), ~1B MAU (June 2026); ~$2B/month revenue with roughly half from Team/Enterprise (Reported — aggregator analyses of OpenAI statements).
- **1M+ business customers**, 7M+ enterprise seats (9x YoY), 92% of the Fortune 500 (Reported — OpenAI "1 million businesses" post).
- **Codex: 5M+ weekly active users** (June 2026, Verified via Constellation Research coverage of OpenAI's report); ~20% are non-developers, growing 3x faster than developers. OpenAI's own arXiv paper *The Shift to Agentic AI: Evidence from Codex* documents task-length distribution — by May 2026, 70% of sampled users ran at least one request exceeding an hour of estimated human work.
- Named case studies: **Cisco** (Codex in engineering workflows; claims 50% faster code review — vendor case study), **Morgan Stanley** (eval-driven advisor assistant, 98% adviser adoption), **T-Mobile** (forward-deployed engineering) (Reported — OpenAI case-study pages; figures are customer/vendor claims, not audited).

## Relevance to agentic AI engineering
OpenAI is the reference implementation for most of this repo's agentic threads. Codex and GPT-5.3-Codex are precisely what the agentic-SWE benchmark papers interrogate — *FeatureBench*, *SWE-EVO*, and *SlopCodeBench* test the long-horizon repo work Codex now claims 8-hour tasks on, and *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* is the right lens on those vendor numbers. The Agents SDK's sandboxing and tool orchestration connect to the tool-use/governance thread (*CaMeLs Can Use Computers Too*, *Verifiable Software Worlds for Computer-Use Agents* — Operator-style computer use is OpenAI's product line here). AgentKit's new configurable memory maps to *Memory for Autonomous LLM Agents* and *Agentic Search in the Wild*; the Realtime API makes GPT-5.x a primary engine for the voice-agent stacks evaluated in *τ-Voice* and *LTS-VoiceAgent*.

## Use cases & considerations
Use cases: (1) default general-purpose LLM API with the broadest tooling ecosystem; (2) embedded coding agents — Codex SDK/MCP in CI or internal dev platforms; (3) enterprise assistants via ChatGPT Enterprise + connectors where compliance teams already approved it; (4) realtime voice agents on the Realtime API.

Considerations: fast model churn (four GPT-5.x tiers in twelve months) means eval pinning and deprecation-watching are mandatory; Responses API/AgentKit primitives are proprietary (lock-in vs. open harnesses); pricing pressure is real but preview-tier cost claims are unverified; enormous capital and compute commitments create IPO-driven incentive questions. Competitors: Anthropic, Google DeepMind (Gemini/Antigravity), Meta Llama, xAI, Mistral. Open questions: the Microsoft AGI clause, and whether the nonprofit's control survives a public listing.

## Sources
- https://en.wikipedia.org/wiki/OpenAI
- https://www.technologyreview.com/2020/02/17/844721/ai-openai-moonshot-elon-musk-sam-altman-greg-brockman-messy-secretive-reality/
- https://www.cnbc.com/2025/03/31/openai-closes-40-billion-in-funding-the-largest-private-fundraise-in-history-softbank-chatgpt.html
- https://www.cnbc.com/2026/03/31/openai-funding-round-ipo.html
- https://openai.com/index/accelerating-the-next-phase-ai/
- https://www.cnbc.com/2025/10/28/open-ai-for-profit-microsoft.html
- https://openai.com/index/statement-on-openai-nonprofit-and-pbc/
- https://www.cmcmarkets.com/en-gb/ipo-trading/open-ai-ipo
- https://help.openai.com/en/articles/9624314-model-release-notes
- https://openai.com/index/introducing-gpt-5-5/
- https://openai.com/index/previewing-gpt-5-6-sol/
- https://developers.openai.com/api/docs/models/all
- https://developers.openai.com/codex
- https://openai.com/index/the-next-evolution-of-the-agents-sdk/
- https://openai.com/index/1-million-businesses-putting-ai-to-work/
- https://www.constellationr.com/insights/news/openai-touts-broadening-codex-usage-5-million-weekly-active-users
- https://arxiv.org/html/2606.26959v1
- https://openai.com/index/cisco/
- https://openai.com/index/morgan-stanley/
- https://www.zenml.io/llmops-database/forward-deployed-engineering-bringing-enterprise-llm-applications-to-production
