# The Evolution of Tool Use in LLM Agents: From Single-Tool Call to Multi-Tool Orchestration

- **Status:** Located — [arXiv:2603.22862](https://arxiv.org/abs/2603.22862) (v1 2026-03-24, v2 2026-04-02)
- **Area:** tool-use-governance
- **Authors / venue / date:** Haoyuan Xu, Chang Li, Xinyan Ma, et al. (15 authors; Harbin Institute of Technology, Harvard, Huawei per search results — affiliations not on the abstract page). arXiv preprint, cs.SE / cs.CL. No peer-reviewed venue yet.

## Problem
Early tool-use research asked one question: can the model pick and format a single correct call? That question is mostly solved and no longer where agents fail. Production agents fail at orchestration — long trajectories with intermediate state, execution feedback, changing environments, and constraints on safety, cost, and verifiability. The field's terminology (tool use vs. calling vs. retrieval vs. orchestration) and its research silos have not caught up.

## Approach
A survey of 200+ works (2023–2026) that first formally separates single-call tool use from long-horizon orchestration, then organizes the literature along six dimensions: (1) inference-time planning/execution (ReAct chains → DAG/topology-aware planning, hierarchical delegation, tree search); (2) training and trajectory construction (synthetic data with validation loops, SFT for orchestration, RL with turn-level credit assignment); (3) safety and control; (4) efficiency under resource constraints; (5) capability completeness in open environments; (6) benchmark design. Catalogues 40+ long-horizon multi-tool benchmarks.

## Key findings
- Benchmark scale has exploded: ToolBench (3,451 tools / 126,486 instances), StableToolBench (16k+ simulated tools), ToolHop (3,912 tools, multi-hop dependencies), TRAJECT-Bench (trajectory-aware, 5,670 instances), τ-bench/τ²-bench (dual-control user interaction).
- Safety is stratified by execution phase: pre-execution policy enforcement (AgentSpec, AARM), in-execution transaction management with rollback/compensation (SagaLLM, Atomix — epoch-based concurrency isolation), post-execution verification (CRITIC, VerifiAgent), plus trajectory-level auditing for long-horizon drift.
- Efficiency levers: parallel dependency-planned execution (LLMCompiler), speculative reasoning (ReWoo, LATS), model routing (FrugalGPT, RouteLLM), semantic caching (GPTCache).
- Dominant failure modes in current systems: tool hallucination, cascade error propagation, poor capability-boundary perception ("blind trial and error" — FAIL-TALMS), and behavioral degradation over extended interactions (Agent Drift). [Counts above read from the paper's tables; affiliation detail inferred from search snippets.]

## Limitations & open questions
Authors concede conceptual confusion in terminology and structural silos between planning/training/safety/efficiency research. Open: credit assignment theory for multi-tool RL, verifiable orchestration in safety-critical domains, scaling to thousands of volatile APIs, tool deprecation/lifelong learning. A skeptic would add: it's a survey — no new experiments — and arXiv-only, so the taxonomy is a lens, not evidence.

## Why builders should care
Stop benchmarking agents on call-level correctness; the failures that matter are state persistence, error recovery, and boundary awareness over long chains. Adopt phase-stratified governance — policy checks before execution, transactional rollback during, verification after — rather than a single guardrail layer. Speculative/parallel tool calling and model routing are now well-mapped cost levers.

## Related companies in this landscape
- **Composio** — tool registries and managed integrations; the paper's dynamic tool retrieval problem is its product.
- **WorkOS / Keycard / Scalekit / Runlayer** — identity, auth, and least-privilege permissions for agents; direct match for pre-execution constraint enforcement.
- **Temporal / Inngest / Orkes** — durable workflow engines; the SagaLLM/Atomix transactional-rollback pattern is their core primitive.
- **Gravitee** — API gateways/governance as the enforcement point for agent tool traffic.
- **HumanLayer** — approval gates for high-risk write operations (the paper's perform-reject-verify mechanism).
- **E2B / Daytona / Docker / Modal** — sandboxed execution environments the survey treats as prerequisite for safe tool RL and runtime isolation.
- **Braintrust / Arize / LangChain / Hamming AI** — agent tracing and evals; the shift to trajectory-level, system-level benchmarks validates their roadmaps.
- **OpenRouter / Not Diamond** — model routing, the survey's flagged cost-management lever.

## Sources
- https://arxiv.org/abs/2603.22862
- https://arxiv.org/html/2603.22862v2
