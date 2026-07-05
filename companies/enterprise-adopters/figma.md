# Figma

> The collaborative interface-design tool that's turning itself into a surface AI coding agents can read from and write to.

- **Category:** enterprise-adopters
- **AIEWF 2026 tier:** supporting
- **Founded:** 2012, San Francisco (Verified)
- **Website / GitHub:** https://www.figma.com · https://github.com/figma

## What they do
Figma is the browser-based design tool most product teams use for UI/UX work — vector editing, components, auto-layout, design systems, and Dev Mode for handoff to engineers. For AI engineers, the relevant surface is its **MCP server**: it exposes structured design context (components, variables, layout, styles) to any MCP-compatible agent — Claude Code, Cursor, Copilot, Codex, Warp, etc. — so a coding agent can generate UI code that actually matches the design system instead of guessing from a screenshot. A newer write-capable mode ("Agents, meet the Figma Canvas") lets agents create/update frames and components directly on canvas, not just read them. Figma Make adds prompt-to-prototype generation. One-line note: founders Dylan Field and Evan Wallace started Figma in 2012 (Field via the Thiel Fellowship); Adobe's $20B acquisition was blocked by regulators in 2023, and Figma IPO'd in July 2025 at a ~$68B valuation (Verified).

## Evidence of real-world use
MCP server ships in beta with documented support across Claude Code, Cursor, Copilot CLI/VS Code, Augment, Codex, Factory, Firebender, and Warp — real multi-vendor adoption, not a one-off integration (Verified, Figma docs/blog).

## Relevance to agentic AI engineering
Direct fit for the "design-to-code" and tool-use slice of the agent stack: MCP as the context-passing protocol, Code Connect for grounding generated code in real components, and canvas write access as an emerging agent-computer-use surface for design work.

## Sources
- https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server
- https://developers.figma.com/docs/figma-mcp-server/
- https://www.figma.com/blog/the-figma-canvas-is-now-open-to-agents/
- https://www.figma.com/blog/design-systems-ai-mcp/
- https://en.wikipedia.org/wiki/Dylan_Field
- https://www.bloomberg.com/news/articles/2025-07-31/figma-s-fig-blockbuster-ipo-gives-ceo-dylan-field-a-6-billion-fortune
