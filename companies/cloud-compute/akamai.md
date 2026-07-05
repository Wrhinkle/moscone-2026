# Akamai

> The original CDN company, now selling a distributed cloud (built on Linode) and pitching itself as the low-latency edge for AI inference and agent traffic — plus security products aimed specifically at LLM apps and AI agents.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** platinum
- **Founded:** Incorporated August 20, 1998, Cambridge, MA, out of MIT (Verified). Public company, NASDAQ: AKAM.
- **Website / GitHub:** https://www.akamai.com · https://www.linode.com · https://github.com/akamai · https://github.com/linode

## What they do

Three product families matter to an AI engineer:

1. **Akamai Cloud (ex-Linode) + Inference Cloud.** Akamai acquired Linode in March 2022 for ~$900M (Verified) and rebuilt it into "Akamai Cloud": VPS/Kubernetes/object storage compute with straightforward pricing, wired into Akamai's edge network of 4,200+ points of presence. In February–March 2025 they launched **Akamai Cloud Inference** (inference on that footprint), and in October 2025 the bigger bet: **Akamai Inference Cloud**, co-built with NVIDIA — RTX PRO 6000 Blackwell Server Edition GPUs plus BlueField-3 DPUs and NVIDIA AI Enterprise, deployed at edge locations rather than centralized regions (Verified, Akamai/NVIDIA press + independent coverage). In 2026 they announced **AI Grid**, orchestration for distributed inference across ~4,400 edge locations (Reported, Akamai press release). Their benchmark claim of up to 1.63x higher inference throughput vs. an H100 is vendor-published (Reported). The pitch in engineer terms: run open-model inference physically near users so multi-call agentic workflows and voice agents don't pay 100ms+ per hop to a hyperscaler region.
2. **AI-specific security.** **Firewall for AI** (launched April 2025) sits in front of LLM apps and inspects both inbound prompts and outbound responses for prompt injection, data leakage, model-extraction, and AI-targeted DoS; deploys via Akamai edge, REST API, or reverse proxy (Verified). **API LLM Discovery** auto-discovers GenAI/LLM API endpoints in your estate. Their bot-management line is being repositioned for the "agentic era" — intent/identity-based classification of AI agents rather than good-vs-bad bots, with support for emerging standards like Web Bot Auth and Know Your Agent (Reported, Akamai blog).
3. **The classic business**: CDN delivery and enterprise security (WAF, DDoS, segmentation), which still funds everything.

## Founders & origins

Founded by **Tom Leighton** (MIT applied-math professor, Princeton BSE '78, MIT PhD '81) and his graduate student **Danny Lewin** (Technion, then MIT), with Jonathan Seelig and Randall Kaplan on the founding team (Verified). The origin: a challenge from Tim Berners-Lee at MIT to fix web congestion, answered with consistent-hashing algorithms for distributing content across servers — work that put Leighton and Lewin in the National Inventors Hall of Fame (2017). Lewin was killed aboard American Airlines Flight 11 on September 11, 2001 (Verified). Leighton has been CEO since 2013 and still runs the company.

## Funding

- Seed/Series A 1998–99: $8.3M from Polaris Ventures and Baker Communications Fund (Verified, FundingUniverse/Encyclopedia.com).
- Second round May 1999: $35M — Polaris, Baker, Battery Ventures, TCW (Verified).
- IPO October 29, 1999 at $26/share, raising ~$234M; shares opened ~$114 in dot-com mania (Verified).
- Today: FY2025 revenue roughly $4B (Reported); compute portfolio $708M in 2025, +12% YoY, with Cloud Infrastructure Services +45% YoY in Q4 2025 and a stated ~$400M cloud run rate (Reported, earnings/Morgan Stanley TMT coverage).

## Evidence of real-world use

The CDN/security business serves a large fraction of global web traffic and most major brands — decades-verified. For the newer AI compute story, evidence is thinner but real: named case studies include **Harmonic** (AI inference on Blackwell GPUs on Akamai Cloud), **Bloomfield Robotics** (crop-imaging deep learning), and **FreshToHome** (Indian grocery platform running its cloud on Akamai) (Reported, Akamai customer stories — vendor-published). Linode retains a genuine developer community with public pricing and long-standing usage. The Inference Cloud is months old; independent production adoption evidence is Not found in public sources yet.

## Relevance to agentic AI engineering

- **Agent latency:** their core argument — multi-step agentic workflows compound per-call network latency — is exactly the bottleneck examined in *Building Interactive Real-Time Agents with Asynchronous I/O and Speculative Tool Calling* and *VoiceAgentRAG* (the RAG latency bottleneck); edge inference is an infrastructure answer where those papers offer architectural ones. Relevant to anything judged by *τ-Voice* or built per *LTS-VoiceAgent*.
- **Agent governance/security:** Firewall for AI and identity-based bot management for AI agents are commercial counterparts to *Governance by Construction for Generalist Agents*, *ClawLess: A Security Model of AI Agents*, and *CaMeLs Can Use Computers Too* — Akamai is one of the few sponsors selling the "who is this agent and may it act" layer for the open web.
- **Tool-use:** as agents call third-party sites/APIs at scale (*The Evolution of Tool Use in LLM Agents*), Akamai sits on both sides — protecting the sites and carrying the traffic.

## Use cases & considerations

**Use cases:** (1) cheap, predictable VPS/K8s compute (Linode heritage) for agent backends without hyperscaler egress fees; (2) low-latency open-model inference near users for voice or interactive agents; (3) Firewall for AI in front of a customer-facing LLM app; (4) bot management if your product will be visited *by* other people's agents.

**Considerations:** Akamai Cloud's region count and managed-service catalog are far thinner than AWS/Azure/GCP — no first-party frontier models, limited data services. The Inference Cloud is new and unproven at production scale; throughput claims are vendor benchmarks. Competitors: Cloudflare (Workers AI — the most direct analog), Fastly, Fly.io, plus hyperscalers on compute and GPU-clouds (CoreWeave, Lambda) on inference. Open question: whether edge inference wins real workloads versus simply caching/routing to centralized GPUs, and whether Akamai's enterprise-sales culture can court AI-native developers.

## Sources

- https://www.akamai.com/company/company-history
- https://www.akamai.com/company/leadership/executive-team/tom-leighton
- https://en.wikipedia.org/wiki/F._Thomson_Leighton
- https://www.invent.org/inductees/daniel-lewin
- https://www.fundinguniverse.com/company-histories/akamai-technologies-inc-history/
- https://www.akamai.com/newsroom/press-release/akamai-inference-cloud-transforms-ai-from-core-to-edge-with-nvidia
- https://www.akamai.com/newsroom/press-release/akamai-launches-ai-grid-intelligent-orchestration-for-distributed-inference-across-4400-edge-locations
- https://www.akamai.com/newsroom/press-release/akamai-sharpens-its-ai-edge-with-launch-of-akamai-cloud-inference
- https://www.akamai.com/newsroom/press-release/akamai-firewall-for-ai-enables-secure-ai-applications-with-advanced-threat-protection
- https://www.akamai.com/blog/security/bot-management-agentic-era
- https://www.akamai.com/products/akamai-inference-cloud-platform
- https://www.fierce-network.com/cloud/akamai-gears-edge-ai-new-inference-cloud
- https://betterstack.com/community/guides/web-servers/linode-akamai-review/
- https://finance.yahoo.com/news/akamai-technologies-highlights-400m-cloud-234742043.html
- https://www.akamai.com/resources/customer-story
- https://www.constellationr.com/insights/news/akamai-inference-cloud-deploys-nvidia-ai-grid
