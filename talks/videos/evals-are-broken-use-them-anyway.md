# Evals Are Broken, Use Them Anyway

> A Cline engineer critiques how the industry reads eval numbers, then shows how Cline hill-climbs Terminal Bench with parallel sandboxed runs and failure-trace triage.

- **Speaker:** Ara Khan, Cline
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=QuuIywMG4s8) (AI Engineer channel; ~19m, released 2026-06-06)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Khan opens with the claim that most people are wrong about evals, and sorts them into two camps. The objective-metrics camp reads leaderboard dashboards as if similar scores mean similar models, which Khan calls a hoax, citing a same-morning tweet accusing Meta of classic benchmark maxing. The taste camp goes the other way, treating everything as vibes and anthropomorphizing models. The truth sits in the middle, and Khan offers heuristics for finding it: never believe a model lab's own eval numbers, since researchers routinely dismiss them internally; stay current but skip being the earliest adopter, because Epoch's index shows the frontier model changing every couple of months, so let a release settle for a few weeks first; and seek out very new, very precise evals, since standardized ones age out. He quotes OpenAI's own blog admitting SWE-bench Verified no longer measures frontier coding capabilities.

The second half is Cline's own story. A year ago Khan says Cline, like the Codex team and others, mostly ignored evals as unnecessary. The team then built their own from scratch, paying users who opted in to share coding data, then doing hard manual labor to clean that corpus into problems that represent real work. The difficulty is that single-turn evals have binary answers and a small search space, while an agent asked to fix a broken MCP server reads files, searches docs, installs an environment, runs scripts, and might fix the target while breaking something else, and all of that has to be graded.

Cline's current setup uses Terminal Bench, 89 coding problems from a Stanford group that Khan considers a decent approximation of real programming work, with tasks running 30 to 40 minutes. Harbor, from the Laude Institute, defines the infrastructure per task, machine spec, RAM, CPU, so all 89 run in parallel in isolated VMs, making the slowest task the wall-clock limit. Cline runs this on Modal. The loop: run the suite, take the failures, and have another agent read each failure trace to allocate causes, this task failed on a broken retry tool, that one on a timeout. A run tests three things at once, the model, the harness, and the problems themselves, and Khan notes a model can feel much better in one harness than another, as Anthropic models do in Claude Code. Cline's score climbed from an original 43 percent through changes to container CPU and memory, raised timeouts, and tuned thinking behavior, since asking a model to think more sometimes sends it in circles.

Khan closes with three zones of improvement: zone one is obvious flaws like harness crashes and rate limits; zone two, the essence of the craft, is nuanced tuning, since prompt techniques that work on Anthropic model families do not transfer to Codex or Gemini families; zone three is overfitting, cheating for a score you can tweet. Hill climbing taught Cline it was strong on Anthropic models and weak on Gemini and Kimi families, and fixing that opened whole user populations. His advice: pass the vibe check and hold a decent score, and do both.

## Notable moments

- [0:05:18](https://www.youtube.com/watch?v=QuuIywMG4s8&t=318s) OpenAI's blog concedes SWE-bench Verified no longer measures frontier coding, Khan's case for very new, very precise evals.
- [0:08:20](https://www.youtube.com/watch?v=QuuIywMG4s8&t=500s) Cline builds evals from scratch by paying opted-in users for real coding data and manually cleaning it into problems.
- [0:11:23](https://www.youtube.com/watch?v=QuuIywMG4s8&t=683s) Terminal Bench's 89 tasks run in parallel isolated VMs via Harbor, with the slowest task as the limiting factor.
- [0:15:25](https://www.youtube.com/watch?v=QuuIywMG4s8&t=925s) The three zones: fix obvious flaws, do the nuanced per-model-family tuning, and stay out of the overfitting danger zone.

## Connections

- [Cline](../../companies/coding-agents/cline.md) is the speaker's company, the open-source coding agent whose harness this eval loop tunes.
- [Modal](../../companies/cloud-compute/modal.md) provides the sandboxed parallel compute Cline runs its Terminal Bench suite on, credited by name in the talk.
- [Position: coding benchmarks are misaligned with agentic software engineering](../../papers/swe-agents/position-coding-benchmarks-are-misaligned-with-agentic-soft.md) makes the academic version of Khan's argument that standardized coding evals stopped measuring real work.
