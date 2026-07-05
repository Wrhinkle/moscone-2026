# .txt (dottxt)

> The company behind Outlines, the open-source library that guarantees LLM output conforms to a schema (JSON, regex, grammar) via constrained/structured decoding, plus a hosted API for the same guarantee without self-hosting GPUs.

- **Category:** agent-orchestration
- **AIEWF 2026 tier:** supporting
- **Founded:** 2023 (pre-seed), Paris/remote (Verified — TechCrunch, Seedcamp)
- **Website / GitHub:** https://dottxt.ai · https://github.com/dottxt-ai/outlines

## What they do
Outlines is a Python library that constrains token-by-token generation so an LLM's output is guaranteed to match a JSON schema, regex, or context-free grammar — used as a dependency inside agent/tool-calling stacks (works with vLLM, Ollama, OpenAI-compatible endpoints, Transformers). ~11.9k GitHub stars. The .txt REST API extends the same guarantee as a hosted, no-GPU service in early access.

**Founders:** Rémi Louf, Dan Gerlanc, Brandon Willard — ex-Normal Computing colleagues with backgrounds in Bayesian statistics/compiler tech (Verified — TechCrunch).
**Funding:** $3.2M pre-seed (2023, led by Elaia) + $8.7M seed (Aug 2024, led by EQT Ventures) ≈ $11.9M total (Verified — TechCrunch, Seedcamp).

## Evidence of real-world use
AWS has published an official blog integrating Outlines for structured output on Bedrock/SageMaker — strong independent adoption signal beyond OSS stars (Verified — AWS ML Blog).

## Relevance to agentic AI engineering
Structured/constrained generation is foundational plumbing for reliable tool-calling and JSON-mode agent loops — directly relevant to this repo's tool-use and agent-reliability research areas.

## Sources
- https://techcrunch.com/2024/10/17/with-11-9-million-in-funding-dottxt-tells-ai-models-how-to-answer/
- https://github.com/dottxt-ai/outlines
- https://dottxt.ai/
- https://aws.amazon.com/blogs/machine-learning/generate-structured-output-from-llms-with-dottxt-outlines-in-aws/
- https://seedcamp.com/views/dottxt-raises-11-9m-to-enable-llms-to-speak-the-language-of-every-application/
