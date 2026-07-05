# Governance by Construction for Generalist Agents

- **Status:** Located — [arXiv:2605.20874](https://arxiv.org/abs/2605.20874); demo paper for ACM CAIS 2026 (per IBM Research publications page)
- **Area:** tool-use-governance
- **Authors / venue / date:** Segev Shlomov, Iftach Shoham, Alon Oved, Ido Levy, Sami Marreed, Harold Ship, Offer Akrabi, Sergey Zeltyn, Avi Yaeli, Nir Mashkif (IBM Research). Submitted to arXiv May 20, 2026.

## Problem

Enterprise agents that plan and call tools autonomously fail in production for governance reasons, not capability reasons: hallucinated facts, misused tools, violated procedures, leaked data. The usual fixes — prompt stuffing and post-hoc validation — are brittle, hard to audit, and still probabilistic because compliance depends on the model choosing to follow instructions.

## Approach

The paper presents the policy system of CUGA (IBM's open-source Computer-Using Generalist Agent, LangGraph-based, on-prem deployable). Governance is "policy-as-code": strongly-typed policy schemas stored in a vector DB (Milvus), matched at runtime by a policy agent, and enforced at five structural checkpoints in the agent loop:

1. **Intent Guard** — blocks malicious requests before any reasoning (keyword match + LLM conflict resolution); termination is irreversible.
2. **Playbook** — injects markdown step-by-step workflow guidance (steps, expected outcomes, tool constraints) into the system prompt at planning time.
3. **Tool Guide** — appends compliance/context guidance to tool descriptions at the tool-call boundary (session-scoped, cumulative).
4. **Tool Approval** — human-in-the-loop pause after code generation, before executing sensitive tools (DB writes, third-party APIs).
5. **Output Formatter** — forces final responses into templates, Markdown, or JSON schemas.

Policies fire on typed triggers: natural-language embedding similarity, keyword, application, agent state, or tool events. No fine-tuning anywhere.

## Key findings

- OAK Bench (27 insurance-workflow tasks), with vs. without policies: GPT-OSS-120B 75% → 100%; GPT-4.1 70% → 96%; Claude Opus-4.5 81% → 96%.
- BPO Bench (26 business-operations tasks): GPT-OSS-120B 49.2% → 82.3% (+33.1 pp); GPT-4.1 28.5% → 66.2% (+37.7 pp); Claude Opus-4.5 50.0% → 68.5%.
- Ablation (BPO, GPT-OSS-120B): 0 policies 46.2% → 2 policies 71.8% → 5 policies 78.2%. Single policies flipped whole task clusters from 0/3 to 3/3 (e.g., an "API capability boundaries" policy stopped the agent from treating unanswerable queries as solvable).
- Cost: token usage roughly 1.5–3.3x (e.g., BPO GPT-4.1: 2.7M → 8.8M tokens).
- Notable pattern: the weakest/cheapest model plus policies beat the strongest model without them (inferred from Table 1, not stated as a headline claim).

## Limitations & open questions

Authors concede the token overhead and six still-unsolved BPO tasks (synthesis gaps, tool malformations, trigger patterns that didn't fire). Skeptic's questions: it's a demo paper on two small in-house benchmarks (27 + 26 tasks) with an LLM judge; trigger-based matching can miss paraphrases (their own Scenario 2 shows Intent Guard bypassed by rewording, caught only by the approval gate — defense-in-depth is load-bearing); who authors and maintains dozens of policies per domain?

## Why builders should care

Governance layered outside the model is also a reliability layer: five typed checkpoints bought +18–38 pp task success without fine-tuning. If you're building domain agents, budget for a policy/playbook layer with explicit approval gates on destructive actions rather than ever-longer system prompts — and expect to pay ~2x tokens for it.

## Related companies in this landscape

- **LangChain** — CUGA's enactment layer is LangGraph; validates LangGraph as the substrate for interruptible, checkpoint-gated agent loops.
- **HumanLayer** — Tool Approval checkpoint is exactly their product: HITL gates on high-risk agent actions.
- **WorkOS / Keycard / Scalekit / Descope / Auth0** — the identity, audit-log, and least-privilege plumbing this "auditable by construction" story presumes.
- **Runlayer / Gravitee** — tool-call-boundary enforcement (secure MCP/API gateways) mirrors the Tool Guide/Tool Approval checkpoints.
- **Composio** — agent tool registries; Tool Guide's per-session augmented tool metadata suggests registries should carry policy annotations, not just schemas.
- **Arize / Braintrust** — the ablation methodology (per-policy task deltas) is an eval-platform workflow; policies become testable artifacts.
- **Qdrant / Milvus-style vector DBs** — policy storage/matching here runs on embedding retrieval, a non-RAG vector-DB use case.

## Sources

- https://arxiv.org/abs/2605.20874
- https://arxiv.org/html/2605.20874v1
- https://research.ibm.com/publications/governance-by-construction-for-generalist-agents
