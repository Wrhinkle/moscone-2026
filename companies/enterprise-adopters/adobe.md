# Adobe

> A creative/enterprise software giant now shipping an agentic AI layer — Firefly AI Assistant — that orchestrates multi-step workflows across its Creative Cloud apps, plus MCP servers exposing Experience Manager, Commerce, Express, and Target to external AI agents.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** 1982, San Jose, CA (public record)
- **Website:** https://www.adobe.com · https://developer.adobe.com

## What they do
**Firefly AI Assistant** (public beta, April 2026) is a conversational "creative agent" that takes a natural-language brief and orchestrates multi-step edits across Photoshop, Premiere, Illustrator, Lightroom, and Express, rather than requiring manual tool-by-tool operation (Verified — Adobe/Axios). Separately, Adobe exposes **MCP servers** for Experience Manager (content CRUD, Cloud Manager ops), Commerce (catalog/cart/pricing/checkout), Express, and Target, letting external LLM agents (Claude, ChatGPT, Cursor, Copilot Studio) call Adobe systems as tools — plus an External AI Registry to discover them (Verified — Adobe developer docs).

## Founders & funding
N/A — public company (NASDAQ: ADBE), founded by John Warnock and Charles Geschke.

## Evidence of real-world use
Adobe is explicitly building a lighter-weight Firefly Assistant to work inside third-party chatbots, starting with Anthropic's Claude (Verified — Axios). MCP servers are documented, shipped developer products, not concepts.

## Relevance to agentic AI engineering
Concrete example of a large enterprise exposing its product surface via MCP for agent tool-calling, plus a first-party "creative agent" — relevant to this repo's tool-use, MCP, and enterprise-adopter research areas.

## Sources
- https://blog.adobe.com/en/publish/2026/04/15/introducing-firefly-ai-assistant-new-way-create-with-our-creative-agent
- https://www.axios.com/2026/04/27/adobe-agentic-ai-firefly-claude
- https://developer.adobe.com/express/add-ons/docs/guides/getting-started/local-development/mcp-server
- https://www.paz.ai/blog/adobe-mcp-commerce-default-agent-protocol
- https://developer.adobe.com/internals/mcp-registry-web-app
