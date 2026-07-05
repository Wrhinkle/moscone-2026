# MiniMax

> Shanghai frontier lab that ships open-weight agentic coding models (M-series), plus commercial video, speech, and music generation APIs — one of China's "AI tiger" labs, publicly listed since January 2026.

- **Category:** models-inference
- **AIEWF 2026 tier:** labs
- **Founded:** December 2021, Shanghai (Verified — Wikipedia, TechNode, SCMP)
- **Website / GitHub:** https://www.minimax.io · https://platform.minimax.io · https://github.com/MiniMax-AI

## What they do
MiniMax builds proprietary and open-weight multimodal models and sells them three ways: an **Open Platform API** (text, video, image, speech/voice-cloning, music, plus an MCP server), consumer apps (Talkie/Xingye character chat, Hailuo AI video, MiniMax Audio, MiniMax Agent/Chat), and open-weight releases on Hugging Face.

For engineers the headline line is the **M-series of agentic LLMs**. MiniMax-M1 (June 2025) was an open-weights reasoning model using a hybrid "lightning attention" architecture for long-context efficiency (Verified — arXiv 2506.13585). **MiniMax-M2** (October 2025) is an MIT-licensed MoE — 230B total / 10B activated parameters — explicitly tuned for coding-run-fix loops and multi-tool chains (shell, browser, code execution), scoring 69.4% SWE-bench Verified and 46.3% Terminal-Bench per the model card; it uses interleaved `<think>` tags that must be preserved in conversation history, a real harness-integration gotcha (Verified — GitHub MiniMax-AI/MiniMax-M2). Successors M2.5 and **M2.7** (April 2026, open-sourced) push agentic benchmarks further — 56.22% SWE-Pro, 57.0% Terminal Bench 2 — and MiniMax claims M2.7 ran 100+ autonomous rounds of its own scaffold optimization ("self-evolving"; Reported — MiniMax/MarkTechPost/VentureBeat, vendor-framed). Weights deploy via vLLM, SGLang, and MLX.

The other pillars: **Hailuo** video generation (2.3 as of late 2025, sold via API and OpenRouter), **Speech 2.x** TTS/voice-cloning (multilingual, sound tags, studio-grade cloning), and **Music** generation.

## Founders & origins
Founded by **Yan Junjie** (chairman/CEO) and **Zhou Yucong**, both ex-SenseTime computer-vision researchers (Verified — Wikipedia, Forbes). Yan (b. 1989, Henan): mathematics at Southeast University, PhD from the CAS Institute of Automation (2015), Tsinghua postdoc, rose to VP at SenseTime. He credits OpenAI's 2019 Dota 2 bots for his pivot from CV to NLP and left to build "general-purpose AI for the public"; the company name comes from the minimax algorithm (Verified — Forbes profile, 36kr interview). The January 2026 IPO made Yan a billionaire (~$3.2B per Forbes).

## Funding
- Angel (late 2021): miHoYo, Hillhouse, IDG Capital, Yunqi Capital (Verified — 36kr, TechNode "miHoYo-backed").
- ~$600M led by Alibaba, March 2024, at ~$2.5B valuation; Tencent and HongShan among other backers (Verified — Wikipedia, SCMP).
- ~$300M Series B extension, July 2025, at ~$4B, led by Shanghai state-owned STVC Group (Reported — Sacra/Tracxn-sourced summaries).
- **IPO:** Hong Kong Stock Exchange, January 9, 2026, raising ~US$618M; shares surged 70–100% on debut, market cap briefly above HK$90B (~US$11.5B) (Verified — TechNode, Forbes, Yicai).
- Total pre-IPO raised ~$850M–$1.1B (Reported — Tracxn vs InforCapital disagree; exact total unverified).

## Evidence of real-world use
Unusually strong, and audited post-IPO: FY2025 revenue **US$79.0M** (+158.9% YoY), >70% from international markets; cumulative **236M users** across 200+ countries and **214,000 enterprise customers/developers**; API-platform revenue tripled to $26.0M (Verified — company FY2025 results via PR Newswire, an exchange-listed filing). M2 was the first Chinese model on OpenRouter to exceed **50B tokens/day** and topped Hugging Face trending (Reported — MiniMax financial-results narrative; OpenRouter lists MiniMax as a rising provider). Talkie logged ~17M downloads in eight months of 2024, though it was at one point pulled from the US App Store — a regulatory-exposure signal (Reported — Statista/Yahoo Tech). Jensen Huang publicly called MiniMax "world-class" (Reported — SCMP).

## Relevance to agentic AI engineering
MiniMax is a direct supplier for the agentic-SWE stack: M2/M2.7 are open-weight alternatives for coding agents, and their SWE-Pro/Terminal-Bench positioning maps onto this repo's benchmark thread — *ProdCodeBench*, *FeatureBench*, *SWE-EVO*, and the caution in *Position: Coding Benchmarks Are Misaligned with Agentic Software Engineering* applies squarely to vendor-reported M2.7 numbers. Long-horizon self-evolution claims invite scrutiny via *SlopCodeBench*. Its multi-tool orchestration focus connects to *The Evolution of Tool Use in LLM Agents*; the Speech 2.x line is relevant to voice-agent builds discussed in *LTS-VoiceAgent*, *τ-Voice*, and *From Text to Voice*.

## Use cases & considerations
Use cases: (1) self-hosted coding-agent backend (MIT weights, 10B activated params = cheap inference); (2) low-cost agent loops via OpenRouter/platform API; (3) TTS/voice-cloning for voice agents; (4) programmatic video (Hailuo) for content pipelines.

Considerations: Chinese jurisdiction — data residency, export/compliance, and the Talkie App Store removal precedent; benchmark claims are largely vendor-reported; `<think>`-tag handling complicates harness portability; consumer revenue still dwarfs API revenue. Competitors: DeepSeek, Qwen (Alibaba), Moonshot/Kimi, Zhipu on the open-weight side; Anthropic/OpenAI for agentic coding; ElevenLabs (speech), Runway/Kling (video).

## Sources
- https://en.wikipedia.org/wiki/MiniMax_Group
- https://en.wikipedia.org/wiki/Yan_Junjie
- https://www.forbes.com/sites/ywang/2026/01/09/founder-of-chinese-ai-model-developer-minimax-becomes-a-billionaire-as-shares-surge-on-listing/
- https://technode.com/2026/01/09/mihoyo-backed-ai-firm-minimax-jumps-on-hong-kong-debut-market-value-tops-11-5-billion/
- https://www.scmp.com/business/banking-finance/article/3318485/minimax-world-class-ai-start-lauded-jensen-huang-applies-hong-kong-ipo
- https://github.com/MiniMax-AI/MiniMax-M2
- https://www.minimax.io/news/minimax-m27-en
- https://www.marktechpost.com/2026/04/12/minimax-just-open-sourced-minimax-m2-7-a-self-evolving-agent-model-that-scores-56-22-on-swe-pro-and-57-0-on-terminal-bench-2/
- https://www.prnewswire.com/news-releases/minimax-announces-full-year-2025-financial-results-302700868.html
- https://www.minimax.io/news/minimax-speech-28
- https://openrouter.ai/minimax
- https://sacra.com/c/minimax/
- https://eu.36kr.com/en/p/3681421130411656
- https://arxiv.org/pdf/2506.13585
