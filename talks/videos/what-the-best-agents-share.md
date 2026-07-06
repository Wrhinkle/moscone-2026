# What the Best Agents Share

> Mardu Swanepoel dissects four UX patterns common to leading agent products: focus modes, transparent execution, personalization, and reversibility.

- **Speaker:** Mardu Swanepoel, Flinn AI
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=7CrPrHgoEYk) (AI Engineer channel; ~10m, released 2026-05-26)
- **Program:** AI Engineer 2026 release, program placement unconfirmed

## Summary

Swanepoel frames the talk with Picasso's "great artists steal," in the sense of studying something deeply enough to build something better. He picks four agent products he considers among the best available, Cursor, Claude cowork, Harvey, and Manifold, and extracts four patterns, giving each the same treatment: what it is, what value it adds, and how it looks in the product.

The first pattern is focus modes: putting the agent in a named mode that constrains both the action space and the input space. For engineers, a smaller constrained space means you can drop tools, sharpen the system prompt, and tune evals to perform well on that slice before generalizing. For users, an ask-me-anything interface gives no guidance on how to get good results, while a mode aligns expectations and shapes inputs. His exhibit is Cursor's mode drop-down: planning mode writes no code, just a plan and questions, and debug mode runs a hypothesis-driven process that spins up a dedicated debug server and pushes logs to it.

The second is transparent execution: making what the agent is doing, using, and thinking clear enough to shift the relationship from delegation to collaboration. Swanepoel's argument is about trust and waste. A bare result earns less trust than a result accompanied by process, assumptions, and uncertainties, and visible steps let the user intervene early, stopping the agent at step two when it reads the wrong Notion docs instead of after it finishes. Claude cowork does this well for him, with a progress list, visible context and skills, and full tool-call inputs and outputs; Manifold shows similar task progress and what it made of each source.

The third is personalization, which he defines as giving the agent the knowledge, principles, and patterns you would have used yourself. The distinction he draws is optimizing for speed to understanding over speed to outcome: generating an output fast is easy, but output misaligned with how the user wanted the task done is useless, so the agent must do the right thing and not just something. Examples: Harvey's playbooks encode a legal firm's contract-review methods so the agent reviews the way that firm does; Harvey also builds memory across interactions; Claude adds skills and connectors.

The fourth is reversibility: the user's ability to undo agent actions, which bounds the cost of mistakes. Once the worst case is known, the ROI calculation gets easier and users become bolder, delegating higher-value tasks. Cursor offers undo at line, file, and conversation-state granularity, plus parallel outputs from different models on the same input where the user knowingly keeps one and discards the rest. Harvey achieves reversibility inside Microsoft Word by integrating with the native Word change-tracking API, so edits are reviewed the way an editor reviews a colleague's redlines.

## Notable moments

- [0:02:08](https://www.youtube.com/watch?v=7CrPrHgoEYk&t=128s) Cursor's focus modes: planning mode that refuses to write code, debug mode with its own log server.
- [0:04:11](https://www.youtube.com/watch?v=7CrPrHgoEYk&t=251s) Transparent execution in Claude cowork: progress list, visible skills, and full tool-call I/O.
- [0:06:13](https://www.youtube.com/watch?v=7CrPrHgoEYk&t=373s) Speed to understanding versus speed to outcome, with Harvey playbooks as the fix.
- [0:07:14](https://www.youtube.com/watch?v=7CrPrHgoEYk&t=434s) Reversibility as binding the cost of mistakes, making users bolder about delegating high-value work.

## Connections

- [Session recaps](../../notes/session-recaps.md): the in-person Anthropic conversation covered cowork's product direction, including the skills model Swanepoel cites under personalization.
- [Cline](../../companies/coding-agents/cline.md): an adjacent coding agent built around plan/act modes and transparent diffs, the first two patterns in open-source form.
