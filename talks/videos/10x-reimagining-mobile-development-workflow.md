# 10x: Reimagining Mobile Development Workflow

> A mobile engineer argues the promised 10x from AI has not arrived because teams changed the engine without changing the workflow, and pitches cloud sandboxes for mobile as the fix.

- **Speaker:** Orel Zion, stag.build
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=rCVVsxHWai8) (AI Engineer channel; ~8m, released 2026-06-22)
- **Program:** Online Track 2026

## Summary

Zion, a mobile software engineer of 14 years, opens by asking whether anyone actually feels 10x more productive now that engineering has shifted to chat-style work with Claude Code, Codex, or Cursor. His answer is no, not as individual engineers, not as teams, and not as whole companies. His explanation borrows the history of factory electrification. When factories swapped steam engines for electric ones, the gains were modest, because machines stayed arranged around proximity to one central engine. The 10x to 30x gains came years later, when smaller electric motors went inside each machine and factories rearranged themselves around the actual workflow.

The software equivalent, in Zion's telling, is the iteration loop. PMs iterate with designers, designers with users, users with devs, devs back with designers, then QA, then devs again, and maybe something ships. Each iteration creates context switches, wasted time, and synchronization overhead. AI sped up the code inside that loop but did not remove the friction between the roles.

His reimagined workflow puts everyone on one tool and one codebase. Designers design on code and send the developer a PR instead of a Figma document. QA iterates with the agent directly, getting a link to a simulator and telling the agent what to test and what to fix. He dismisses the two obvious ways to get there. Asking designers and PMs to install Xcode and Android Studio and give up 200 GB of storage would be rejected, and routing agent iteration through CI fails because mobile CI builds take 20 to 40 minutes, too long for an agent to wait just to learn that its iOS code failed to build.

The answer he proposes is cloud sandboxes, a concept he notes has existed for years but not yet for mobile development. The agent talks to a CLI that spins up a small single-iteration VM booting in 30 seconds or less, builds the app, and shows a simulator in the browser inside Claude Code, Codex, or Cursor. A designer iterates against the live simulator, sees changes immediately, and tells the agent to open a PR when done. Developers run multiple VMs in parallel, QA drives its own agent session, and from there the build goes to store review. The demo walkthrough shows the chat interface on the left and the running app on the right. Zion's closing point mirrors the electrification story: the productivity comes from using AI to remove the iteration friction the industry took for granted, and the tooling change alone was never going to deliver it.

## Notable moments

- [0:01:01](https://www.youtube.com/watch?v=rCVVsxHWai8&t=61s) The factory electrification analogy: swapping engines gave little until the workflow was rearranged.
- [0:03:02](https://www.youtube.com/watch?v=rCVVsxHWai8&t=182s) The iteration map across PM, design, dev, and QA, and why iteration is the friction AI has not removed.
- [0:05:03](https://www.youtube.com/watch?v=rCVVsxHWai8&t=303s) Why CI cannot host the agent loop: 20 to 40 minute mobile builds.
- [0:06:03](https://www.youtube.com/watch?v=rCVVsxHWai8&t=363s) Cloud sandboxes for mobile: per-iteration VMs booting in under 30 seconds with a browser simulator.

## Connections

- [Daytona](../../companies/swe-infrastructure/daytona.md) sells the sandboxed execution environments for agents that this talk extends to mobile builds and simulators.
- [Coder](../../companies/swe-infrastructure/coder.md) runs cloud development environments, the adjacent infrastructure pattern for moving heavyweight toolchains off laptops.
