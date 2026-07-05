# E2B

> Open-source cloud sandboxes — Firecracker microVMs that boot in ~150ms — so AI agents can execute untrusted generated code, browse, and use a desktop without ever touching your machines.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** supporting
- **Founded:** March 2023, San Francisco (Czech founders; Verified — company blog, Vestbee, VentureBeat)
- **Website / GitHub:** https://e2b.dev · https://github.com/e2b-dev/E2B

## What they do

E2B sells **isolated execution environments for AI agents**, and effectively created the "AI sandbox" category (their Code Interpreter SDK predates most competitors). The unit is a **sandbox**: a Firecracker microVM — the same isolation primitive AWS Lambda uses — with its own filesystem, network, and kernel-level separation, created via API. Startup is **sub-200ms** (~80ms for regionally colocated instances, no cold starts — company claims). An agent gets a real computer: run Python/JS/Ruby/C++ processes, install packages, write files, keep state across a session of up to **24 hours** (Pro plan), and pause/resume.

What you'd actually integrate: Python and JS/TS SDKs (`e2b`, `e2b-code-interpreter`), with documented integrations for OpenAI, Anthropic, Mistral, Llama, LangChain, and LlamaIndex. Beyond code execution, **E2B Desktop** provides a full graphical Linux environment for computer-use agents, and they explicitly pitch **RL training workloads** — tens of thousands of concurrent sandboxes for rollout/verification loops. The core infrastructure is **Apache-2.0 open source and self-hostable** (Terraform guides for AWS/GCP/Azure) — a real differentiator vs. Daytona, which closed-sourced its core in June 2026. Public per-second pricing ($0.000014/vCPU-s, $0.0162/GiB-hr; Pro $150/mo for 24h sessions and 100 concurrent sandboxes) plus a free tier = genuine self-serve product.

## Founders & origins

**Vasek Mlejnsky (CEO)** and **Tomas Valenta (CTO)** — Czech, friends since sixth grade (Verified — Vestbee, founder interviews). Previously built **Devbook**, an interactive documentation tool for developers; after GPT-3.5 launched they repurposed Devbook's sandbox tech to run an autonomous coding agent, the demo took off on Twitter, and they open-sourced and pivoted to sandboxes as the product, founding E2B in March 2023 and relocating to San Francisco (Reported — founder interviews, Deep Acre profile, Latent Space podcast).

## Funding

- **Seed, ~September 2023: $11.5M** led by **Decibel Partners** (Reported — VentureBeat retrospective, Decibel's own writeup).
- **Series A, July 2025: $21M** led by **Insight Partners**, with Decibel, Sunflower Capital, Kaya, and angels including former Docker CEO Scott Johnston (Verified — PRNewswire, Insight Partners, SiliconANGLE, VentureBeat).
- **Total raised: ~$32.5M** (computed).

## Evidence of real-world use

Unusually strong, with quantified vendor case studies corroborated by third parties. **Perplexity** uses E2B for Pro-tier advanced data analysis (integration reportedly one engineer, one week). **Hugging Face** runs tens of thousands of concurrent E2B sandboxes for code verification in **Open-R1**, its public DeepSeek-R1 reproduction — visible in the open-r1 GitHub repo itself, not just marketing. **Manus** runs its agents' virtual computers on E2B (27 tools; claimed half-day integration vs. months in-house). Other named users: Groq, Lindy. The headline claim — **88% of Fortune 100 at Series A, 94% on the current site** — is company-reported and likely counts any signup, so discount it; the harder numbers are **7M+ monthly SDK downloads** and **1B+ sandboxes started** (company-reported) and **~12.8k GitHub stars / ~1k forks** (Verified). Competitors' comparison pages (Vercel, Modal, Northflank, Beam, ZenML) all treat E2B as the default incumbent to displace — a good backhanded signal.

## Relevance to agentic AI engineering

E2B is the execution substrate that agentic-SWE evaluation work presupposes: long-horizon and feature-level benchmarks (*SWE-EVO*, *SlopCodeBench*, *FeatureBench*, *ProdCodeBench*) each need thousands of isolated, reproducible environments per run — the Hugging Face Open-R1 usage is exactly this pattern applied to RL. VM-level isolation is the infrastructure answer to the agent-security line (*CaMeLs Can Use Computers Too*, *Governance by Construction for Generalist Agents*, *ClawLess*): contain the blast radius rather than trust the model. E2B Desktop maps to *Verifiable Software Worlds for Computer-Use Agents*, and long-running research sandboxes to *Deep Researcher Agent* and *Effective Strategies for Asynchronous Multi-Agent Collaboration in Software Engineering*.

## Use cases & considerations

Use cases: (1) code-interpreter/data-analysis feature inside an LLM product (the Perplexity pattern); (2) execution layer for coding agents running untrusted diffs and tests; (3) mass-parallel sandboxes for RL or benchmark evals; (4) desktop environments for computer-use agents.

Considerations: managed-cloud economics — per-second billing on long-lived stateful sandboxes adds up, and 24h max session caps very-long-horizon agents; self-hosting is possible but operationally nontrivial (Firecracker requires bare metal or nested virtualization). Fortune-100 percentage claims should be read as signups, not deployments. Competitors: **Daytona** (closest, gold-tier AIEWF sponsor), **Modal**, **Vercel Sandbox**, **Cloudflare**, **Runloop**, **Morph**, **Northflank/Beam**; hyperscalers and model providers (code execution built into OpenAI/Anthropic APIs) could commoditize the layer. Open question: whether the open-source "sandbox protocol" standard play lands before the primitive gets absorbed upstream.

*Confidence as of 2026-07-02.*

## Sources

- https://e2b.dev/
- https://github.com/e2b-dev/E2B
- https://e2b.dev/blog/series-a
- https://www.insightpartners.com/ideas/e2b-raises-a-21m-series-a-to-offer-cloud-for-ai-agents-to-fortune-100/
- https://www.prnewswire.com/news-releases/e2b-raises-a-21m-series-a-to-offer-cloud-for-ai-agents-to-fortune-100-302514540.html
- https://venturebeat.com/ai/how-e2b-became-essential-to-88-of-fortune-100-companies-and-raised-21-million
- https://siliconangle.com/2025/07/28/e2b-shares-vision-sandboxed-cloud-environments-every-ai-agent-raising-21m-funding/
- https://www.vestbee.com/insights/articles/e2-b-secures-21-m
- https://e2b.dev/blog/how-hugging-face-is-using-e2b-to-replicate-deepseek-r1
- https://github.com/huggingface/open-r1
- https://www.decibel.vc/articles/e2b-the-ai-agents-cloud
- https://www.latent.space/p/e2b
- https://e2b.dev/pricing
- https://www.beam.cloud/blog/e2b-pricing-explained
- https://www.zenml.io/blog/e2b-vs-daytona
- https://vercel.com/kb/guide/vercel-sandbox-vs-e2b
