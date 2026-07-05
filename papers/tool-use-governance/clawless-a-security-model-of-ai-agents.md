# ClawLess: A Security Model of AI Agents

- **Status:** Located — [arXiv:2604.06284](https://arxiv.org/abs/2604.06284)
- **Area:** tool-use-governance
- **Authors / venue / date:** Hongyi Lu, Nian Liu, Shuai Wang, Fengwei Zhang — arXiv (cs.CR), submitted April 7, 2026. No peer-reviewed venue listed.

## Problem
AI agents break the threat models behind classic OS security: they pull data from arbitrary untrusted sources, behave non-deterministically because of LLM inference, and can *reason about* the security mechanisms constraining them well enough to try to subvert them. Sandboxes and allowlists built for deterministic programs assume the program isn't an adversary; ClawLess assumes the worst case — the agent itself may be malicious (e.g., prompt-injected).

## Approach
A formal, fine-grained security model over system entities (files, processes, sockets, devices), three trust scopes (Sandbox, Agent, Monitor), and five permissions (Read, Write, NoExecute, Append, Visible — "Visible" lets an agent reference a credential without ever reading its contents). Policies are *dynamic*, expressed in Linear Temporal Logic (□ always / ◆ eventually), so rules can adapt to runtime behavior — e.g., "if the agent reads sensitive files, permanently revoke outbound socket access." An SMT-based validator checks policies, a compiler translates them into concrete syscall rules, and enforcement runs in a user-space kernel (gVisor) with BPF-based syscall interception — entirely outside the agent, so security holds regardless of the model or scaffold (they cite OpenClaw, OpenCode, and Claude Code as target systems).

## Key findings
- This is a design/position paper: **no empirical evaluation** — no attack-prevention rates, overhead percentages, or SMT validation times are reported.
- Core conceptual contribution: taint-style dynamic policies ("read untrusted → lose network") formalized in LTL and enforced at the syscall layer, not the prompt layer.
- The "Visible" permission is a concrete mechanism for the credential-exfiltration problem: agents can use secrets without holding them.
- Enforcement is agent-architecture-independent (inferred: this is why they enforce below the framework, at syscalls).

## Limitations & open questions
Authors exclude DoS and vulnerabilities in the agent stack, and assume ClawLess's own software/hardware (gVisor, BPF) is bug-free. A skeptical builder would ask: what's the syscall-interception latency on real coding-agent workloads? How hard is it to author correct LTL policies for a messy real task? And does permanent revocation ("read sensitive → no network, forever") make agents unusable for legitimate work?

## Why builders should care
The lesson generalizes even without benchmarks: enforce agent permissions *below* the agent — at the syscall/sandbox layer with dynamic, taint-aware rules — rather than trusting prompts, tool descriptions, or the framework's own guardrails. If you're shipping agents that touch credentials, "usable but not readable" secrets is a pattern worth copying today.

## Related companies in this landscape
- **Docker, Daytona, E2B, Modal** — secure execution sandboxes; ClawLess argues sandboxes need dynamic, semantic policies, not just isolation.
- **Keycard, WorkOS, Descope, Auth0** — agent identity/least-privilege permissioning; the paper is a formal model of what those permissions should mean.
- **Runlayer, Gravitee** — secure tool/MCP access and API gateways; syscall-level enforcement is the OS-layer analog of their network-layer governance.
- **1Password** — the "Visible" permission (use a secret without reading it) is exactly the agent-credential problem their vaults target.
- **HumanLayer** — approval gates are the human-in-the-loop complement to ClawLess's automated revocation policies.

## Sources
- https://arxiv.org/abs/2604.06284
- https://arxiv.org/html/2604.06284v1
