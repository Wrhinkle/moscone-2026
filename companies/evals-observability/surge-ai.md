# Surge AI

> Human-data infrastructure for RLHF, RL environments, and evals — the labor market that trains frontier models.

- **Category:** evals-observability
- **AIEWF 2026 tier:** supporting
- **Founded:** 2020, San Francisco, CA (Verified)
- **Website / GitHub:** https://surgehq.ai/ · https://github.com/surge-ai (Python SDK: `surge-ai/surge-python`)

## What they do
Surge AI is a data-annotation and human-feedback platform, not a labeling-app clone: it runs a marketplace of vetted expert annotators (physicians, lawyers, mathematicians, coders, 70+ languages) and layers tooling on top for RLHF preference/reward data, SFT demonstration data, rubric/verifier design for RL environments that train agentic models, and raw human evaluation as a "gold standard" check on outputs algorithms can't score well (safety, subtlety, creative quality). Engineers integrate via a Python SDK/API (projects, tasks, bulk CSV task creation) rather than a self-serve labeling UI — it's built for frontier labs running large post-training pipelines, not small teams needing a few thousand labels.

## Founders & origins
Founded by Edwin Chen (ex-ML engineer at Facebook, Google, Twitter), who started Surge after frustration with crowdsourced label quality. (Verified)

## Funding
Bootstrapped with no outside capital through 2024; profitable "from nearly day one" per Chen. In July 2025 Surge began its first external raise, reported by Reuters/Bloomberg at up to $1B at a $15–25B+ valuation. (Reported — press accounts, deal not fully confirmed closed as of writing)

## Evidence of real-world use
Named customers/partners include Anthropic (RLHF platform used to train Claude, per Surge's own blog) and reported work with Google, Microsoft, and Meta; Surge states 2024 revenue of $1.2B driven by ~12 frontier labs. Forbes (Sept. 2025) reported OpenAI no longer works with Surge. (Reported)

## Relevance to agentic AI engineering
Sits upstream of the agent stack: the RLHF/rubric/RL-environment work Surge sells is exactly what produces the reward signals and verifiers agentic models are trained against — directly relevant to eval design and post-training for tool-using agents.

## Sources
- https://en.wikipedia.org/wiki/Surge_AI
- https://surgehq.ai/
- https://surgehq.ai/products
- https://surgehq.ai/blog/anthropic-surge-ai-rlhf-platform-train-llm-assistant-human-feedback
- https://www.forbes.com/sites/phoebeliu/2025/09/17/the-ai-billionaire-youve-never-heard-of/
- https://www.inc.com/sam-blum/bootstrapped-to-1-billion-surge-ai-ceo-edwin-chen-on-how-he-did-it/91207937
- https://github.com/surge-ai/surge-python
