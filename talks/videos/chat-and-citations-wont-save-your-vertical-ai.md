# Chat and citations won't save your vertical AI

> Filed's CTO argues vertical AI products must be designed for delegation rather than participation, with skills, traces, and takeback controls replacing chat as the core interface.

- **Speaker:** Atul Ramachandran, Filed Inc
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=RGiXcVxSD3s) (AI Engineer channel; ~15m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Ramachandran is CTO and co-founder of Filed, which builds AI products for US tax professionals, has raised more than $17 million, and in the month before the talk closed more revenue than in the entire prior year. His thesis is that chat and citations, the default interfaces of vertical AI in healthcare, legal, and taxes, cannot keep the promise those products sell. Chat is synchronous, so the customer sits waiting for the agent instead of leaving to do other work. Citations ground answers and reduce hallucinations, but they push the verification burden onto the customer, who now reviews the agent's work item by item. Both undercut the pitch that agents do the work while you sleep.

He frames the moment as a third abstraction level, using banking as the example. First, physical branches, where value was bottlenecked by employee count. Then digital self-service, where the bottleneck moved to user count. Now agentic delegation, where users come to hand work off rather than to use the product, and value stops scaling with visits because agents keep working after the user leaves. His product metaphor is a conveyor belt: agents are the workers, the product is the belt and its surrounding infrastructure, and the user is the supervisor.

Building the belt takes four components. Delegation: find tasks users do themselves that take more than an hour or two; Filed identified three such tasks in the tax workflow, and these become long-running background agents. Teaching: a background agent gets 80 to 90 percent of the way, but every professional has their own conventions, so the product needs skills that capture how each user works. Filed captures these automatically from product usage rather than asking users to author them in a separate interface, which Ramachandran says would not work. Monitoring: task lists show where each long-running job stands, and traces let users follow back every value the agent produced, which he calls where trust is built and where most complaints get addressed. Control: when the agent hits a judgment call, Filed pauses the belt and users tag the agent in a chat thread to resolve the conflict; for dangerous irreversible actions, such as data entry that can erase existing records in tax software, the product presents a plan for approval first. He adds that level-two self-service features must remain, because users only delegate when they believe they can take back the wheel.

The measurement claim closes the talk. Weekly active users, the standard metric, belongs to the era when people did the work in the platform. The right metric for delegation products is weekly active sessions, counting tasks completed whether or not a human was present. Success looks like weekly active users going down while weekly active sessions go up.

## Notable moments

- [0:01:01](https://www.youtube.com/watch?v=RGiXcVxSD3s&t=61s) Filed's traction: $17M raised, and one recent month out-earning the whole prior year.
- [0:02:03](https://www.youtube.com/watch?v=RGiXcVxSD3s&t=123s) Why chat and citations fail: synchrony and the verification burden.
- [0:04:05](https://www.youtube.com/watch?v=RGiXcVxSD3s&t=245s) The three abstraction levels and the bottleneck shifting from employees to users to neither.
- [0:09:09](https://www.youtube.com/watch?v=RGiXcVxSD3s&t=549s) Skills captured automatically from product usage instead of a separate authoring interface.
- [0:13:11](https://www.youtube.com/watch?v=RGiXcVxSD3s&t=791s) The metric swap: weekly active sessions up, weekly active users down.

## Connections

- [Session recaps](../../notes/session-recaps.md) discuss the skills-and-agent-definitions pattern in agent harnesses, the same mechanism Filed uses to capture each professional's working conventions.
- [Reducto](../../companies/back-office-automation/reducto.md) works the adjacent document-heavy back-office layer that vertical agents like Filed's depend on for accurate extraction.
