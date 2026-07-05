# Ref

> An MCP server that gives coding agents token-efficient, search-based access to API/library documentation instead of dumping whole docs into context.

- **Category:** memory-rag-search
- **AIEWF 2026 tier:** silver
- **Website / GitHub:** https://ref.tools · https://docs.ref.tools/ · https://github.com/ref-tools/ref-tools-mcp

## What they do

Ref (`ref-tools-mcp`) is a Model Context Protocol server exposing a documentation-search tool plus a URL-to-markdown fetch tool to any MCP-compatible coding agent. Instead of pasting entire docs pages into the context window, the agent issues iterative, refined searches; Ref deduplicates results already returned in-session (reducing "context rot" and repeat-token spend) and can index public docs/GitHub as well as private repos and PDFs. It also screens fetched public documentation for prompt-injection payloads before returning content to the calling agent (Verified — GitHub repo, docs.ref.tools, ref.tools/blog). This is squarely dev-tooling infrastructure, not a consumer product, despite the category label given.

## Founders & funding

Not found in public sources — no founder names, funding rounds, or investors surfaced in search; treat as **Unverified**.

## Evidence of real-world use

The open-source `ref-tools-mcp` repo has ~1.1k GitHub stars, 66 forks, MIT license (Verified — GitHub). Listed on MCP directories (mcpservers.org, Glama, mcpmarket.com), indicating real adoption within the MCP ecosystem beyond a landing page.

## Relevance to agentic AI engineering

Directly addresses context-window efficiency and grounding for coding agents — a tools/retrieval building block relevant to any agent stack doing tool-calling against external documentation, and a practical mitigation for prompt-injection risk in retrieved web content.

## Sources

- https://ref.tools/
- https://docs.ref.tools/
- https://github.com/ref-tools/ref-tools-mcp
- https://ref.tools/blog/how-does-ref-mcp
- https://mcpservers.org/servers/ref-tools/ref-tools-mcp

*Profile written 2026-07-02.*
