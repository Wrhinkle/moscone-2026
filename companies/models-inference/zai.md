# zAI (Z.ai / Zhipu AI)

> Beijing frontier lab spun out of Tsinghua University that ships MIT-licensed open-weight GLM models tuned for agentic coding, sold via an API platform and a flat-fee "Coding Plan" that plugs into Claude Code and 20+ other harnesses — the first major LLM developer to IPO anywhere (HKEX, January 2026).

- **Category:** models-inference
- **AIEWF 2026 tier:** labs
- **Founded:** 2019, Beijing — spun out of Tsinghua University's Knowledge Engineering Group (Verified — Wikipedia, ChinaTalk, Turing Post)
- **Website / GitHub:** https://z.ai · https://docs.z.ai · https://github.com/zai-org · https://huggingface.co/zai-org

*Naming note:* the AIEWF sponsor list says "zAI"; this is Z.ai, legally Knowledge Atlas Technology (智谱, formerly branded Zhipu AI internationally, rebranded 2025). Not to be confused with Elon Musk's xAI.

## What they do
Z.ai builds the **GLM (General Language Model) family** and monetizes it three ways: a pay-per-token **API platform** (docs.z.ai; also resold via OpenRouter), the **GLM Coding Plan** flat subscription, and open-weight releases on Hugging Face under `zai-org` — flagships included, under MIT license since mid-2025 (Verified — HF, VentureBeat).

The current line is squarely aimed at coding agents. **GLM-5** (Feb 2026) is a 745B-parameter MoE with ~44B active, positioned in its own tech report as moving "from vibe coding to agentic engineering"; vendor-reported 77.8% on SWE-bench Verified (vs. Claude Opus 4.6's 80.8%) and Terminal-Bench 2.0 results comparable to Opus 4.5 — notably evaluated *inside Claude Code* as the harness (Reported — GLM-5 report, arXiv 2602.15763). **GLM-5.2** (June 17, 2026) is a ~753B open-weight release with a 1M-token context window that ranks first among open-weight models on Artificial Analysis' Intelligence Index v4.1 (score 51) and, per VentureBeat, beats GPT-5.5 on several long-horizon coding benchmarks at roughly 1/6 the price (Reported — VentureBeat, Interconnects, Artificial Analysis-derived).

The **GLM Coding Plan** is the commercially interesting wedge: $18/mo Lite, $72/mo Pro, $160/mo Max (promo pricing lower) for quota-based use of GLM-5.x inside Claude Code, Cline, Roo Code, Kilo Code, OpenCode, Factory and 20+ other clients — i.e., a drop-in cheaper backend for Anthropic-style coding-agent workflows (Verified — Z.ai docs, AI Pricing Guru). Other products: ChatGLM consumer assistant, **AutoGLM** phone/computer-use agent, GLM-Voice, Ying text-to-video, and GLM-5V multimodal-agent models.

## Founders & origins
Spun out of Tsinghua's Knowledge Engineering Group in 2019 by professors **Tang Jie** (the lab's defining scientific figure) and **Li Juanzi**; **Zhang Peng** is CEO (Verified — Wikipedia, ChinaTalk, Ginger River interview). The KEG lineage predates ChatGPT: GLM-130B and ChatGLM (2022–23) were among the first credible open bilingual LLMs.

## Funding
- Eight pre-IPO rounds totaling RMB 8.36B (~US$1.19B); other tallies say ~$1.5B (Reported — SCMP vs. aggregate press; exact total varies by source). Backers: Alibaba, Tencent, Ant Group, Meituan, Xiaomi, Hillhouse, Qiming (co-led Series B1, 2022), Chinese local-government funds.
- 2023: ~RMB 2.5B (~$350M) round (Verified — Wikipedia, press).
- May 2024: ~$400M led by Saudi Aramco's Prosperity7, ~$3B valuation (Verified — Wikipedia, Reuters-sourced).
- **IPO:** HKEX ticker 02513, January 8, 2026 — priced HK$116.20, raised ~US$558M, opening market cap ~HK$52.8B; ~70% of proceeds earmarked for model R&D through 2028 (Verified — Bloomberg, CNBC, Qiming).

## Evidence of real-world use
Strong developer-side signals: GLM models are top-trending on Hugging Face (Chinese open-weight models held 5 of the top 10 trending slots in June 2026); GLM-5.x is listed on OpenRouter with live commercial pricing ($0.60–$0.975/M input across versions); the Coding Plan's public pricing page and 20+ supported harnesses indicate a real subscription business; Interconnects called GLM-5.2 "the step change for open agents" (Verified/Reported mix — OpenRouter, HF, Interconnects). Named Western enterprise customers: **not found in public sources** — adoption evidence is developer/self-host-shaped, not logo-shaped. Counter-signal: added to the **US Commerce Entity List in January 2025** (Verified — Wikipedia, press), which constrains its US enterprise sales motion even as its weights circulate freely.

## Relevance to agentic AI engineering
Z.ai is a direct supplier to the agentic-SWE stack and arguably the strongest open-weight coding-agent backend as of mid-2026. Its SWE-bench/Terminal-Bench positioning maps onto this repo's benchmark thread — *ProdCodeBench*, *FeatureBench*, *SWE-EVO*, and the vendor-number skepticism argued in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering*; the 1M-context long-horizon claims are exactly what *SlopCodeBench* stress-tests. Its evaluate-inside-Claude-Code posture makes harness portability (see *The Evolution of Tool Use in LLM Agents*) a live integration question, and Entity List status makes the agent-governance thread (*Governance by Construction for Generalist Agents*) practically relevant. GLM-Voice/AutoGLM connect loosely to the voice-agent papers (*LTS-VoiceAgent*, *From Text to Voice*).

## Use cases & considerations
Use cases: (1) cheap Claude Code-compatible backend via the Coding Plan for high-volume agent loops; (2) self-hosted MIT-weights coding model for data-sensitive orgs (GLM-5.2 needs ~8xH100); (3) OpenRouter fallback/router tier for cost arbitrage; (4) computer-use/multimodal agent experiments with GLM-5V/AutoGLM.

Considerations: Chinese jurisdiction plus **US Entity List** status — compliance review is mandatory for US enterprises; headline benchmarks are vendor-reported; flat-plan quotas ("prompts per 5 hours") are opaque units; self-hosting the 700B+ flagships is capital-intensive. Competitors: DeepSeek, Moonshot/Kimi, MiniMax, Qwen (open-weight); Anthropic and OpenAI (agentic coding incumbents).

## Sources
- https://en.wikipedia.org/wiki/Z.ai
- https://z.ai/company
- https://docs.z.ai/guides/overview/pricing
- https://www.chinatalk.media/p/the-zai-playbook
- https://www.turingpost.com/p/zhipu
- https://www.gingerriver.com/p/zhipu-ceo-zhang-peng-on-taking-chinas
- https://www.cnbc.com/2026/01/08/china-ai-tiger-goes-ipo-zhipu-hong-kong-debut-openai-knowledge-atlas-hsi-hang-seng-listing.html
- https://www.bloomberg.com/news/articles/2026-01-07/china-s-openai-rival-zhipu-debuts-in-hk-after-558-million-ipo
- https://www.qimingvc.com/en/news/china%E2%80%99s-agi-pioneer-and-leader-zai-listed-onhong-kong-stock-exchange
- https://www.scmp.com/business/article/3337171/chinese-ai-tiger-zhipu-edges-towards-hong-kong-listing-expected-raise-us300-million
- https://github.com/zai-org/GLM-5
- https://arxiv.org/pdf/2602.15763 (GLM-5: From Vibe Coding to Agentic Engineering)
- https://arxiv.org/pdf/2508.06471 (GLM-4.5 ARC report)
- https://huggingface.co/zai-org/GLM-5
- https://openrouter.ai/z-ai
- https://venturebeat.com/technology/z-ais-open-weights-glm-5-2-beats-gpt-5-5-on-multiple-long-horizon-coding-benchmarks-for-1-6th-the-cost
- https://www.interconnects.ai/p/glm-52-is-the-step-change-for-open
- https://www.aipricing.guru/z-ai-subscription-pricing/
