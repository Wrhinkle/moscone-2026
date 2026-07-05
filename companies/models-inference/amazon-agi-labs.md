# Amazon AGI Labs

> Amazon's San Francisco frontier-agents lab — built from the Adept acqui-hire — whose flagship shipping product is Nova Act, an AWS service for reliable browser-automation agents.

- **Category:** models-inference
- **AIEWF 2026 tier:** labs
- **Founded:** December 2024, San Francisco (Verified — Amazon Science announcement, TechCrunch). Corporate lab inside Amazon, not a startup.
- **Website / GitHub:** https://labs.amazon.science · https://aws.amazon.com/nova/act/ · https://github.com/aws/nova-act

*Disambiguation note:* "Amazon AGI Labs" on the AIEWF sponsor list refers to the Amazon AGI SF Lab (labs.amazon.science), the agent-focused research arm within Amazon's broader AGI organization (which also builds the Nova model family). This profile covers the lab and its shipped agent products.

## What they do
The lab's stated mission is foundational capabilities for agents that "take actions in the digital and physical worlds" — computer use, web browsing, code interpretation — with research bets on agents that learn from human feedback and self-correct (Verified: Amazon Science, TechCrunch, Dec 2024).

The concrete product is **Nova Act**: a fine-tuned action model plus Python SDK for browser agents. Research preview March 2025; generally available as an AWS service December 2, 2025, powered by a custom Nova 2 Lite model (Verified: AWS News Blog). The design philosophy is the interesting part for engineers: instead of one long autonomous prompt, you decompose workflows into short, reliable atomic `act()` commands interleaved with ordinary Python (assertions, breakpoints, thread pools for parallel sessions), with escape hatches to direct Playwright manipulation for things like password entry. Amazon claims >90% reliability on enterprise workflows (Reported — Amazon's own figure, no independent benchmark found). Production tooling includes IAM-based auth, S3 session persistence, Bedrock AgentCore Browser Tool for cloud browser execution, "state guardrails" restricting which URLs an agent may act on, human-in-the-loop approval/takeover patterns, MCP server integration, IDE extensions (VS Code, Kiro, Cursor), a no-code playground (nova.amazon.com/act), and Strands Agents interop. GA is US East (N. Virginia) only (Verified: AWS docs/blog).

## Founders & origins
Not a founded company; the origin is the June 2024 **Adept acqui-hire**: Amazon hired Adept CEO David Luan (previously VP of Engineering at OpenAI) and other Adept leaders and licensed Adept's models and datasets; deal size undisclosed (Verified: TechCrunch, CNBC, GeekWire). Adept itself was co-founded in 2022 by Luan with Transformer-paper co-authors Ashish Vaswani and Niki Parmar (who left Adept in late 2022). Amazon formed the AGI SF Lab in December 2024 with Luan as VP of Autonomy, staffed initially by ex-Adept employees, with Pieter Abbeel (via the Covariant deal) working closely with it (Verified: TechCrunch, Amazon Science).

**Leadership churn:** Luan announced his departure in February 2026 ("to cook up something new"); Peter DeSantis, a 27-year Amazon veteran, took over the broader org including the AGI team. Other ex-Adept executives have also exited (Verified: CNBC, Bloomberg, GeekWire). Open question: the lab's post-Luan direction.

## Funding
Internal Amazon lab — no external funding. Predecessor Adept raised **$415M total**: ~$65M seed/early, $65M Series A (April 2022, Addition and Greylock), $350M Series B (March 2023, General Catalyst and Spark Capital; Microsoft, NVIDIA, Workday Ventures participating) at a ~$1B valuation (Verified: Forbes, TechCrunch, Adept press release).

## Evidence of real-world use
- Nova Act reached GA as a paid AWS service with a public pricing page — a real commercial product. Pricing reported around $4.75/agent-hour plus subscription options (Reported — third-party summaries; confirm on aws.amazon.com/nova/pricing).
- The GA announcement names **no customers**; AWS marketing carries anonymous testimonials (e.g., "hundreds of thousands of runs per month" for mission-critical processes) — treat as logos-without-names (Verified absence: AWS News Blog).
- OSS signal: `aws/nova-act` SDK has ~910 stars, 146 forks, Apache 2.0, 23 releases with active development through April 2026 (Verified: GitHub). Modest for the category.
- AWS has published applied walkthroughs (e.g., competitive price intelligence automation) and third-party engineering coverage exists (Caylent).

Net: real product, real distribution via AWS, but public named-customer evidence is thin as of 2026-07-02.

## Relevance to agentic AI engineering
This is the computer-use camp of the tool-use divide: agents adapting to human UIs rather than software adapting to agents — the tension mapped in *The Evolution of Tool Use in LLM Agents* and *Verifiable Software Worlds for Computer-Use Agents* (Nova Act's atomic-command + assertion style is a practical answer to the verifiability problem those papers raise; *WebXSkill* covers the web-skill side). Its state guardrails and human-approval workflows connect to the governance thread (*Governance by Construction for Generalist Agents*, *CaMeLs Can Use Computers Too*). Browser QA automation also touches the agentic-SWE benchmark discussion (*ProdCodeBench*-style production-derived tasks are exactly what Nova Act QA workflows look like).

## Use cases & considerations
Use cases: (1) web QA test suites written as natural-language steps; (2) form-filling/data-entry against legacy portals with no API; (3) search-and-extract across sites (price intelligence); (4) checkout/booking flows behind human approval gates.

Considerations: single-region GA; AWS lock-in (IAM/S3/AgentCore); reliability claims are vendor-reported; leadership departures cloud the roadmap. Competitors: OpenAI Operator/computer-use, Anthropic computer use, Google Project Mariner, Browserbase, Browser Use, Cua.

## Sources
- https://techcrunch.com/2024/12/09/amazon-forms-a-new-ai-agent-focused-lab-led-by-adept-co-founder/
- https://www.amazon.science/blog/amazon-opens-new-ai-lab-in-san-francisco-focused-on-long-term-research-bets
- https://www.cnbc.com/2026/02/24/head-of-amazons-agi-lab-is-leaving-the-company.html
- https://www.geekwire.com/2026/head-of-amazons-agi-lab-is-leaving-in-latest-exit-from-high-profile-adept-deal/
- https://aws.amazon.com/blogs/aws/build-reliable-ai-agents-for-ui-workflow-automation-with-amazon-nova-act-now-generally-available/
- https://labs.amazon.science/blog/nova-act
- https://aws.amazon.com/blogs/machine-learning/amazon-nova-act-sdk-preview-path-to-production-for-browser-automation-agents/
- https://github.com/aws/nova-act
- https://www.forbes.com/sites/kenrickcai/2023/03/14/adept-ai-startup-raises-350-million-series-b/
- https://techcrunch.com/2023/03/15/adept-a-startup-training-ai-to-use-existing-software-and-apis-raises-350m/
- https://aws.amazon.com/nova/act/
