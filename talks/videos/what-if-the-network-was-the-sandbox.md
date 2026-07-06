# What if the network was the sandbox?

> Tailscale's case for moving agent identity and permissions to the network layer, demonstrated with its Aperture AI gateway.

- **Speaker:** Remy Guercio, Tailscale
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=BM2JX9hqsVQ) (AI Engineer channel; ~24m, released 2026-06-01)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Guercio reduces a sandbox to two components, a boundary and a set of permissions, then points out that both common ways of granting an agent permissions put the credential inside the box. API keys go into the sandbox, where models running in long loops get clever with keys in ways they should not. OAuth logins do the same thing: the account sits in the sandbox with the agent. His question is what changes if authentication and authorization move to the network layer instead.

Tailscale is built on WireGuard, which lets every node on a tailnet hold keys, and Tailscale layers identity on top. Every connection carries the user, their synced groups, and, for non-human nodes like a PR review bot in a GitHub Action, a tag or set of tags. Network access itself is governed by that identity, and the service on the other side of the connection receives the identity too, so it can make decisions per caller without an API key riding along.

The demo is Aperture, Tailscale's AI gateway built on these primitives. One provider key, for Anthropic or OpenAI or Gemini or Bedrock, lives on the Aperture node. Everything else on the tailnet reaches models through it with no key at all in the sandbox, so there is nothing to exfiltrate and nothing for a helpful model to route around when access is cut; revocation at the network layer just ends the conversation. Setup in Claude Code is a settings.json with a dash for the API key, since the harness insists one exists, and Aperture's base URL. The same works for Codex and Gemini CLI.

Because every request transits the gateway, Aperture sees everything. Guercio pulls up his own usage: tokens, per-model spend, full request and response bodies, including the complete system payload Claude Code sends on its first request. Asking Claude Code to just say hello costs about 20 cents. He then inspects the dogfood PR review bot's traffic by tag, showing every bash command and MCP tool call it made, with a guarantee the harness cannot give: if a tool call happened, it went through the gateway. He notes that many customers do not even want blocking yet, they just want to know what their agents are doing, and that on Tailscale's internal instance bash dominates every other tool. Budgets and quotas work across providers as one pool rather than per-vendor allocations, grants can scope model access by group or tag, and webhooks fire on tool calls with delivery guaranteed by the same choke point.

In Q&A, Guercio explains why Aperture intercepts at the LLM layer rather than the MCP layer: as agents shift from structured tool calls to writing and executing code, MCP-level visibility misses most of the action, while the LLM layer still sees the commands. He also declines the suggestion of transparently rewriting traffic at the network level, arguing explicit base URLs break less confusingly. Everything Aperture uses is available through tsnet, Tailscale's open source Go library, so teams could build an equivalent gateway themselves; Aperture itself was deliberately built only on public Tailscale primitives.

## Notable moments

- [0:02:07](https://www.youtube.com/watch?v=BM2JX9hqsVQ&t=127s) The two standard permission models, API keys and OAuth, and why both leave the credential inside the sandbox with the agent.
- [0:06:11](https://www.youtube.com/watch?v=BM2JX9hqsVQ&t=371s) Aperture's core trick: one provider key on the gateway node, zero keys in the sandbox.
- [0:08:13](https://www.youtube.com/watch?v=BM2JX9hqsVQ&t=493s) Live inspection of Claude Code's first request, where saying hello costs about 20 cents.
- [0:22:20](https://www.youtube.com/watch?v=BM2JX9hqsVQ&t=1340s) Why interception moved from the MCP layer to the LLM layer, and the admission that internally bash dominates all other tool use.

## Connections

- [Tailscale](../../companies/security-identity/tailscale.md), the speaker's company; Aperture is built on the identity primitives profiled there.
- [CaMeLs can use computers too](../../papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md), a paper making the parallel argument that agent security belongs in the system layer beneath the model.
- [Governance by construction for generalist agents](../../papers/tool-use-governance/governance-by-construction-for-generalist-agents.md), related work on enforcing agent permissions structurally rather than by trusting the harness.
