# We Cut 94% of AI Coding Tokens With a Local Code Index

> A local hybrid-search layer between codebase and coding agent that cuts context tokens 94 percent on a public benchmark.

- **Speaker:** Rajkumar Sakthivel, Tesco
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=dRmWYHuIJxM) (AI Engineer channel; ~11m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Sakthivel's story starts with a bill. He and his collaborator Foss were using Claude Code, Cursor, Copilot, and Codex daily on a shared project when their AI spend jumped month over month with no change in behavior. Investigating, they found the money was going to context rather than model reasoning. A typical query on their project sent 45,000 tokens of context of which about 5,000 mattered; his analogy is ordering one pizza and paying for nine you do not eat.

Three fixes failed or fell short before the real one. Shorter prompts did nothing because the 45,000 tokens arrive before the model reads the prompt. Model settings like max tokens and temperature change the output, and the money is in the input. Output compression worked, cutting output 75 percent, but output is only about 10 percent of cost, so the total saving was around 8 percent. His central slide makes the arithmetic explicit: 90 percent of AI coding cost is input, so cutting input 94 percent saves about 61 percent total while a 75 percent output cut saves about 8.

The fix is a local search layer between codebase and model, in five steps. Code is chunked into meaningful units, functions, classes, and methods rather than arbitrary windows. Two searches run in parallel, one semantic and one exact-keyword, and their results merge; each alone misses about one in four results, together about one in ten, because embeddings miss exact names like a specific auth function while keyword search misses that "login flow" and "sign in" are the same idea. Results are shrunk further, a 50-line function down to a five-line name-plus-description. A call graph tracks which function calls which, so one hit pulls in its connected code. And every result gets a relevance score with a floor below which nothing is sent, since confident answers built on bad context are worse than no answer. Everything runs on the developer's machine.

The scoring was the hard part. LLM-as-judge on retrieved results added 2 to 3 seconds per query; a fixed score threshold failed because short queries score low even on perfect matches. The shipped formula weights 50 percent semantic score, 30 percent keyword score, and 20 percent code recency, with an adaptive threshold, and runs in 0.4 milliseconds with no extra model calls. His stated lesson is that a simple formula beats a complex model most of the time.

The numbers come from a public test on FastAPI, 53 files and 20 realistic developer questions: 83,000 tokens per question without the tool, 4,900 with it, a 94 percent cut, and 523 with extra compression, at 90 percent retrieval accuracy. Sakthivel is candid about limits. The 94 percent baseline assumes worst-case full-file reading, and tools like Claude Code are already smarter than that, so real savings run lower. On a 396-file project with mixed-responsibility files, recall dropped to almost zero. The team also chose a small fast model for search, giving sub-second re-indexing at some recall cost. A shared index plus persistent memory lets Claude Code, Cursor, and Copilot draw on the same understanding instead of each relearning the project. On one real project the tool's tracker logged 247 queries, 12.4 million tokens saved, and about 186 dollars not spent, 84 percent of it from the search layer. The tool, invoked as cce, is free and open source, and he closes by arguing the Opus-versus-Sonnet debate misses the point when roughly 70 percent of cost is what you feed the model.

## Notable moments

- [0:01:02](https://www.youtube.com/watch?v=dRmWYHuIJxM&t=62s) The measurement that started it: 45,000 context tokens sent per query, about 5,000 of them useful.
- [0:02:02](https://www.youtube.com/watch?v=dRmWYHuIJxM&t=122s) The cost arithmetic: 90 percent of spend is input, so a 94 percent input cut saves about 61 percent total.
- [0:06:07](https://www.youtube.com/watch?v=dRmWYHuIJxM&t=367s) The 50/30/20 scoring formula running in 0.4 milliseconds, and the FastAPI benchmark of 83K down to 4.9K tokens per question.
- [0:07:10](https://www.youtube.com/watch?v=dRmWYHuIJxM&t=430s) The honest limits: 94 percent is the worst-case baseline, and recall collapsed on a 396-file mixed codebase.

## Connections

- [Unblocked](../../companies/swe-infrastructure/unblocked.md), a commercial context engine attacking the same problem of feeding agents less but better context.
- [Sourcegraph](../../companies/coding-agents/sourcegraph.md), the established player in code indexing and search that this local, cost-focused approach sits beside.
