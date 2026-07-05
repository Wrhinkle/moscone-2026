# Arize

> AI observability and evaluation platform: trace, evaluate, and monitor LLM apps and agents in production, with an open-source core (Phoenix) and an enterprise platform (Arize AX).

- **Category:** evals-observability
- **AIEWF 2026 tier:** platinum
- **Founded:** 2020, Berkeley, CA (Verified — multiple profiles and press agree)
- **Website / GitHub:** https://arize.com — https://github.com/Arize-ai/phoenix — https://github.com/Arize-ai/openinference

## What they do

Arize builds the instrumentation-to-evaluation loop for production AI systems. The core workflow: your app emits OpenTelemetry traces via **OpenInference** (Arize's open semantic conventions for LLM/agent spans — prompts, tool calls, retrievals, token counts), those traces land in either **Phoenix** (open source, self-hostable, runs locally/Docker/notebook) or **Arize AX** (enterprise SaaS), and you then run evaluations — LLM-as-judge, code-based checks, human annotation queues — over those traces, both offline against curated datasets and online against sampled production traffic.

AX extends this into an "agent engineering" platform: agent-trace debugging, tool-calling and planning/goal-achievement evals, prompt playground and experiments comparing changes on identical inputs, datasets/curation, cost tracking, and dashboards/monitors with alerting. It also covers the company's pre-LLM roots: drift and performance monitoring for classic ML and computer vision models. **Alyx** (formerly Arize Copilot) is an in-product assistant with 50+ skills for navigating traces, writing evals, and surfacing anomalies (Reported — Arize docs/blog).

Practically, what you integrate is: an OpenInference/OTel instrumentor for your framework (OpenAI, LangChain, LlamaIndex, LiteLLM, AWS Strands, etc.), a collector endpoint, and eval jobs. Phoenix keeps you vendor-neutral at the tracing layer since it's plain OpenTelemetry underneath.

## Founders & origins

- **Jason Lopatecki (CEO)** — previously co-founder/Chief Innovation Officer at TubeMogul (IPO'd, acquired by Adobe); UC Berkeley EECS. (Verified)
- **Aparna Dhinakaran (Chief Product Officer)** — ML engineering at Uber (Michelangelo ecosystem era), Apple, and TubeMogul; Forbes 30 Under 30. (Verified)

Origin story: both saw firsthand how models degrade silently in production and founded Arize in 2020 to be the "observability layer" for ML, pivoting the same machinery hard into LLM/agent evaluation from 2023 onward as Phoenix took off. (Verified across TechCrunch, Cerebral Valley, company blog.)

## Funding

- **Series A:** $19M, Sept 2021, led by Battery Ventures; Foundation Capital, Trinity Ventures, The House Fund, Swift Ventures participating. (Verified — PRNewswire, TechCrunch)
- **Series B:** $38M, Sept 2022, led by TCV; Battery, Foundation, Swift participating. (Verified — PRNewswire)
- **Series C:** $70M, Feb 2025, led by Adams Street Partners; M12 (Microsoft), Sinewave, OMERS Ventures, Datadog, PagerDuty, Industry Ventures, Archerman Capital, plus existing investors. Billed as the largest single investment in AI observability at the time. (Verified — Arize blog + PRNewswire. Note: one aggregator claims NEA led; the primary sources say Adams Street.)
- **Total:** ~$131M+ including earlier seed (seed amount not confirmed in public sources).

Strategic investors Datadog and PagerDuty are notable — incumbents buying visibility into the category rather than building against it (interpretation, not verified intent).

## Evidence of real-world use

- **Phoenix OSS:** crossed 10,000 GitHub stars (company milestone post; repo confirms ~10.2k+); Arize claimed 2M+ monthly downloads at Series C. (Verified/Reported respectively)
- **Named customers:** Booking.com (with an attributed quote from an ML engineering manager describing use for testing/evaluating/tracing GenAI workflows — stronger than a logo), Duolingo, Uber, PepsiCo, Priceline, TripAdvisor, Hyatt, Condé Nast, Wayfair; plus unnamed government agencies. (Reported — Arize's own announcements; Booking.com quote is documented usage)
- **Ecosystem pull:** AWS published an official blog on Strands Agents SDK + Arize AX; Mistral's cookbook includes a Phoenix RAG-eval notebook; listed on AWS and Microsoft marketplaces. Third-party integration docs are good evidence of organic adoption.
- **Public pricing:** free tier (25k spans/mo), AX Pro, and Enterprise (third-party reporting puts enterprise deals at ~$50–60k/yr median — Reported, single source).

## Relevance to agentic AI engineering

Arize sits at the evals/observability chokepoint of the agent stack — the layer every serious agent deployment eventually needs. Direct connections to this repo's landscape: agent-trajectory evaluation is the operational counterpart to benchmarks like *SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution*; its tool-calling evals and OTel-based audit trails line up with the tool-use/governance thread (*Governance by Construction for Generalist Agents*); RAG/retrieval eval workflows relate to the memory-evaluation questions in *Memory for Autonomous LLM Agents: Mechanisms, Architectures, and Evaluation*; and voice-agent evaluation methodology (*From Text to Voice: A Reproducible and Verifiable Framework for Voice Tool-Calling Evaluation*, *τ-Voice*) is exactly the kind of eval harness teams end up operationalizing on platforms like this.

## Use cases & considerations

Use cases:
1. Instrument a multi-step agent (tool calls, retrievals, sub-agents) with OpenInference and debug failures span-by-span.
2. Gate deployments: run LLM-as-judge + code evals on a curated dataset per prompt/model change (experiments API).
3. Online eval sampling of production traffic with drift/quality monitors and alerting.
4. Start free/self-hosted with Phoenix, graduate to AX when you need retention, RBAC, and scale.

Considerations: crowded category — LangSmith, Langfuse, Braintrust, Galileo, W&B Weave, Datadog LLM Observability all compete. Phoenix mitigates lock-in (OTel-native, self-hostable) but the eval/dataset workflows are stickier. Enterprise pricing is opaque beyond the free tier. Open question: whether "agent engineering platform" breadth (Alyx, prompt optimization) beats the neutral-infrastructure positioning as frameworks ship their own eval tooling.

## Sources

- https://arize.com/blog/arize-ai-raises-70m-series-c-to-build-the-gold-standard-for-ai-evaluation-observability/
- https://www.prnewswire.com/news-releases/arize-ai-secures-70m-series-c-to-fix-ais-biggest-problem-making-llms-and-ai-agents-work-in-the-real-world-302381601.html
- https://www.prnewswire.com/news-releases/arize-ai-raises-19-million-series-a-financing-led-by-battery-ventures-for-machine-learning-observability-301385881.html
- https://www.prnewswire.com/news-releases/arize-ai-raises-38-million-series-b-to-scale-machine-learning-observability-platform-301620603.html
- https://techcrunch.com/2021/09/28/battery-ventures-leads-arize-ais-19m-round-for-ml-observability/
- https://github.com/Arize-ai/phoenix
- https://github.com/Arize-ai/openinference
- https://arize.com/blog/phoenix-10k/
- https://arize.com/docs/phoenix
- https://arize.com/docs/ax/arize-copilot
- https://arize.com/pricing/
- https://arize.com/customers/
- https://aws.amazon.com/blogs/machine-learning/observing-and-evaluating-ai-agentic-workflows-with-strands-agents-sdk-and-arize-ax/
- https://www.cekura.ai/blogs/arize-ai-pricing
- https://cerebralvalley.beehiiv.com/p/arize-expanding-field-ai-observability
