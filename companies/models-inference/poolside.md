# poolside

> Foundation-model lab building coding models you can own outright — trained for agentic software engineering and deployable air-gapped inside enterprise, bank, and defense environments, now also shipping open weights (Laguna) and a terminal agent (pool).

- **Category:** models-inference
- **AIEWF 2026 tier:** supporting
- **Founded:** early 2023; HQ San Francisco, remote-first across US/UK/France with recurring Paris work weeks — often described in press as "Paris-based" (Verified — Wikipedia, French Tech Journal, Contrary Research)
- **Website / GitHub:** https://poolside.ai · https://huggingface.co/poolside · https://aws.amazon.com/bedrock/poolside/

## What they do
poolside trains its own frontier-scale code models from scratch (internal "Model Factory" infrastructure; Laguna M.1 was trained on 30T tokens across 6,144 NVIDIA Hopper GPUs) and sells them in a way no API lab does: customers can receive **full model weights** and run everything in their own VPC, on-prem racks, or fully air-gapped classified environments, with fine-tuning on the customer's private codebase. The earlier commercial lineup was **Malibu** (complex SWE tasks) and **Point** (low-latency completion) plus an IDE assistant; the pitch to a 5,000-developer bank or defense prime is "a sovereign copy of a coding model tuned on your code," including STIG-hardened OS images and DoD Impact Level 5 deployability (Verified — poolside.ai/enterprise, /government, AWS Bedrock listing).

In April 2026 the strategy visibly broadened. The **Laguna** family launched: **Laguna XS.2** (33B MoE, 3B active, Apache 2.0, open weights on Hugging Face, runs on-device) scoring 68.2% on SWE-bench Verified, and **Laguna M.1** (225B MoE, 23B active, via API and OpenRouter) at 72.5% SWE-bench Verified / 46.9% SWE-bench Pro. **Laguna XS 2.1** shipped July 2, 2026 (today), lifting SWE-bench Multilingual to 63.1%. Alongside came **pool**, a lightweight terminal coding agent that doubles as an Agent Client Protocol (ACP) client-server (Verified — poolside blog, VentureBeat, MarkTechPost, Hugging Face).

A December 2024 AWS strategic agreement put poolside models on Amazon Bedrock and EC2 (Verified — PR Newswire, AWS).

## Founders & origins
**Jason Warner** (CEO): GitHub CTO through the Copilot launch, previously VP Engineering at Heroku, then managing director at Redpoint Ventures 2021–2023. **Eiso Kant** (CTO): founded source{d} (code-analysis ML) and Athenian (engineering analytics). They met in 2017 when Warner tried to acquire Kant's company for GitHub; the deal died, the friendship didn't (Verified — Wikipedia, Newcomer, Contrary Research). Founding thesis: AGI arrives through code, so train models specialized for software rather than general chat.

## Funding
- Seed, May 2023: **$26M** led by Redpoint (Verified — Newcomer, Tracxn).
- Series A: **$100M** (Reported — Wikipedia; details thin in public sources).
- Series B, Oct 2024: **$500M** led by Bain Capital Ventures at ~**$3B**; DST Global, eBay Ventures, NVIDIA, Citi Ventures, Felicis, StepStone participating (Verified — multiple outlets).
- Series C attempt, late 2025–early 2026: **~$2B at ~$14B** with NVIDIA slated for up to $1B — **failed to close**; FT-cited investors doubted poolside could train frontier-competitive models (Reported — Yahoo Finance, DCD, mlq.ai; treat details cautiously).
- Total raised: ~$626M across three rounds (Reported — Tracxn).

## Evidence of real-world use
- Defense contracts with **RTX Corporation** and other US defense-industrial-base companies; reported sales efforts to Israeli defense firms (Reported — Wikipedia, TipRanks). Claimed traction in large regulated banks is company-sourced, not independently documented.
- Bedrock listing and first-party AWS partnership are real distribution (Verified).
- **Project Horizon**: 2GW AI campus in Pecos County, TX with CoreWeave as anchor tenant (40,000+ GB300 GPUs from Dec 2025) — but **CoreWeave terminated its 250MW lease in late March 2026** when the Series C stumbled; poolside is seeking new partners (Verified — DCD, Yahoo Finance, CoreWeave PR).
- Laguna open weights on Hugging Face + OpenRouter availability are new, checkable adoption surfaces; too early (as of 2026-07-02) for meaningful download/dependents data. No public enterprise pricing page — sales-led.

## Relevance to agentic AI engineering
poolside is a bet that agentic SWE is the economically decisive workload — exactly the territory mapped by this repo's agentic SWE benchmark papers (**SWE-EVO**, **FeatureBench**, **OmniCode**, **ProdCodeBench**); its own headline numbers are SWE-bench Verified/Pro/Multilingual scores. The pool CLI's ACP client-server design is a concrete instance of the interoperability patterns surveyed in **The Evolution of Tool Use in LLM Agents**. For operators in regulated industries (including construction-adjacent enterprise back offices), the full-weights, air-gapped posture is the strongest available answer to data-governance objections against cloud coding agents.

## Use cases & considerations
Use cases: (1) coding agents inside air-gapped/IL5 or bank-regulated networks where Anthropic/OpenAI APIs are prohibited; (2) Laguna XS 2.1 as a free Apache-2.0 local model for on-device agent loops and CI tasks; (3) fine-tuning a code model on a large private monorepo you cannot exfiltrate; (4) Bedrock deployment for AWS-committed shops.

Considerations: 2026 has been rocky — failed $2B raise, CoreWeave lease collapse, and open questions about frontier competitiveness versus Anthropic/OpenAI/Google; Laguna's SWE-bench numbers trail frontier closed models. Competitors: Anthropic/OpenAI/Google (capability), Mistral and Cohere (sovereign/on-prem posture), Qwen-Coder/DeepSeek/Kimi (open weights), Cursor/Cognition/Windsurf (application layer). Open questions: whether the open-weights pivot signals enterprise-sales strength or weakness, and Horizon's financing after CoreWeave's exit.

## Sources
- https://en.wikipedia.org/wiki/Poolside_AI
- https://poolside.ai/ · https://poolside.ai/enterprise · https://poolside.ai/government
- https://poolside.ai/blog/introducing-laguna-xs2-m1
- https://poolside.ai/blog/introducing-laguna-xs-2-1
- https://poolside.ai/blog/announcing-project-horizon
- https://huggingface.co/poolside/Laguna-XS-2.1 · https://huggingface.co/poolside/Laguna-M.1
- https://aws.amazon.com/bedrock/poolside/
- https://www.prnewswire.com/news-releases/poolside-and-aws-announce-strategic-agreement-to-enable-secure-customized-generative-ai-for-software-engineering-on-amazon-bedrock-and-amazon-elastic-cloud-compute-ec2-302322759.html
- https://www.newcomer.co/p/former-github-cto-jason-warner-raises
- https://research.contrary.com/company/poolside
- https://venturebeat.com/technology/american-ai-startup-poolside-launches-free-high-performing-open-model-laguna-xs-2-for-local-agentic-coding
- https://www.marktechpost.com/2026/04/28/poolside-ai-introduces-laguna-xs-2-and-m-1-agentic-coding-models-reaching-68-2-and-72-5-on-swe-bench-verified/
- https://www.datacenterdynamics.com/en/news/poolside-seeks-partners-for-data-center-in-texas-after-coreweave-deal-falls-apart/
- https://finance.yahoo.com/markets/stocks/articles/coreweave-ends-poolside-deal-raising-111152269.html
- https://tracxn.com/d/companies/poolside/___TyiIVKigoCIY2vK3kAkA4q8hMkX0NjBmHM8bBAqQgo
- https://www.tipranks.com/news/private-companies/poolside-highlights-enterprise-ai-transformation-focus-and-defense-use-cases
