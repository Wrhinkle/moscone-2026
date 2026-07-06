# Recursive Coding Agents

> Raymond Weitekamp applies the recursive language model (RLM) pattern to coding agents: let the agent treat its own prompt as data, decompose problems in code, and call copies of itself.

- **Speaker:** Raymond Weitekamp, OpenProse
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=3hXJI2q0Jz8) (AI Engineer channel; ~24m, released 2026-06-25)
- **Program:** Online Track 2026

## Summary

Weitekamp's thesis is that today's agents are "mismanaged geniuses," a phrase he credits to Alex Zhang, Zhi Li, and Omar Khattab at MIT, authors of the original recursive language models paper. The bottleneck to reliable agents is orchestration rather than raw intelligence: one day a single long prompt gets him a nearly working SaaS app, the next day Claude Code empties his Solana wallet. The missing layer is how work gets specified, managed, reused, and verified.

In an RLM, the context itself is the object of computation. The full prompt is externalized as a variable, possibly spanning many files, and the model interacts with it through a REPL (Python in the original paper), operating on it symbolically and delegating pieces to sub-LLMs or sub-RLMs rather than reading everything into its window. Weitekamp cites three results. RLMs can process inputs orders of magnitude larger than the context window, tens of millions of tokens. His own work showed the unmodified RLM harness performs like a top-10 memory system, competitive with purpose-built products he estimates attract billions in investment. And on the LongCoT benchmark, where problems require more reasoning steps than frontier models can sustain, a small Qwen model around 9B parameters running as an RLM beat Opus and GPT-5.4 running as plain LLMs. He also describes the pattern as "too hot to benchmark": within hours of ARC-AGI-3's release, when frontier models scored around 2 to 3 percent, the Symbolica team's Agentica RLM harness posted scores in the thirties, and the Arc Prize team declined to run the private evaluation because tool calling violated the benchmark's intent.

He offers a rubric for what counts as an RLM: an executable environment, an externalized prompt, code as the thing calling the model, the model choosing the decomposition, and state that stays symbolic. Hardcoded map-reduce pipelines fail the decomposition test. He then surveys implementations: Zhang's original package, which Weitekamp wrapped as a CLI tool for coding agents; dspy.RLM, his benchmarking workhorse; Ax, a TypeScript DSPy variant whose agents write TypeScript interfaces to other Ax agents; a pure-bash "Unix RLM" by Dan at OpenProse where the environment is the file system; and his own ypi, which makes Mario Zechner's minimal pi coding agent literally call itself to arbitrary depth, now achievable as a pure pi extension.

On the recurring question of whether Claude Code is an RLM, Weitekamp says the answer flipped from no to arguably yes when dynamic workflows shipped a few weeks before the talk, a change Khattab publicly endorsed. Weitekamp wrote two Claude Code workflows for the companion repo, one deliberately not an RLM (a hardcoded map reduce) and one that is (deep research over a file system). OpenProse generalizes the idea beyond Claude Code: a markdown-spec programming language in logical English, compiled by the coding agent itself, that can turn any agent with a file system and subagents into an RLM. Prose programs can declare subagent work explicitly, verify it in the parent session, and wire skills and CLI tools in as dependencies per subagent. His favorite recent addition captures a "golden session" and deconstructs it into a reusable prose workflow, turning one good day into repeatable behavior. Companion material lives at recursivecodingagents.com.

## Notable moments

- [0:01:01](https://www.youtube.com/watch?v=3hXJI2q0Jz8&t=61s) The trust problem in one anecdote: a near-complete SaaS app from one prompt, then Claude Code drains his Solana wallet.
- [0:06:08](https://www.youtube.com/watch?v=3hXJI2q0Jz8&t=368s) A roughly 9B Qwen model as an RLM beats Opus and GPT-5.4 as LLMs on LongCoT reasoning tasks.
- [0:07:11](https://www.youtube.com/watch?v=3hXJI2q0Jz8&t=431s) Agentica posts 30-plus percent on ARC-AGI-3 within hours of release; the Arc Prize team refuses the private eval.
- [0:21:29](https://www.youtube.com/watch?v=3hXJI2q0Jz8&t=1289s) Golden-session capture: OpenProse deconstructs a good agent session into a reusable workflow.

## Connections

- [Session recaps](../../notes/session-recaps.md): the in-person DSPy session covered the same "AI programs as composable functions" framing Weitekamp builds on with dspy.RLM.
- [Effective Strategies for Asynchronous Multi-Agent Collaboration](../../papers/swe-agents/effective-strategies-for-asynchronous-multi-agent-collaborat.md): studies the parent-subagent decomposition question that RLM harnesses hand to the model.
- [Are We Ready For An Agent-Native Memory System?](../../papers/memory-research-agents/are-we-ready-for-an-agent-native-memory-system.md): frames the memory-system question behind Weitekamp's claim that a stock RLM harness already ranks among the best memory systems.
