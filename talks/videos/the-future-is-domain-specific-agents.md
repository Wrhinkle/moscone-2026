# The Future Is Domain-Specific Agents

> Justin Schroeder argues that fleets of small, narrowly scoped agents composed under a coordinator will beat large general-purpose agents inflated with MCP servers and skills.

- **Speaker:** Justin Schroeder, StandardAgents
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=spNAUEgq_A8) (AI Engineer channel; ~31m, released 2026-06-29)
- **Program:** Online Track 2026

## Summary

Schroeder frames the current moment as an accelerated Industrial Revolution: where machines harnessed energy, agents harness intelligence. He offers a working definition, agents are deterministic software that harness the non-deterministic outputs of models in pursuit of an objective, and dismisses the agent-versus-harness distinction as pedantic.

His starting observation is that everyone is building custom agents, from a real estate agency down the street to Fortune 500 companies, because businesses want their data integrated into AI. But building agents is hard: the agentic loop, provider abstractions, durable execution, telemetry, and portability all bite. Agents that work as demos rarely survive handoff, since environment variables and runtime differences break them on the next machine. Teams then retreat to MCP, which Schroeder says has become a de facto tool distribution mechanism; on the official client support matrix, only the tools column is filled in all the way down. Skills fare no better in his telling. They are documentation in markdown, and research shows installing many of them degrades the agent. His joke: we did not land a man on the moon by giving one guy a ton of tools.

The structural diagnosis is that MCP and skills are inheritance, piling more attributes onto one object, and the old rule of composition over inheritance applies. His alternative is the domain-specific agent: a full agent with its own system prompt written for one domain (Figma, Gmail, travel), only the tools that domain needs, and its own short message history. A coordinator agent above them communicates in plain English, asking the Gmail agent for the last email from Debbie without shipping the whole conversation context down.

Schroeder reports numbers from StandardAgents' still-unannounced platform. Domain-specific agents regularly hit over 80 percent token efficiency per task, because each call carries only a system message, a small toolset, and one request. They also make small models practical: he cites DeepSeek V4 Flash at 137 times cheaper per task than Fable 5, viable when the task list is pre-scoped so the small model does not flail. He adds two more advantages: strict capability limits that calm IT departments used to seeing everyone bypass permission prompts, and scaling characteristics that let thousands of isolated agent instances run in parallel across regions.

The economic argument leans on a trend reversal he tracks: token costs stopped falling in 2026 and are up 29 percent adjusted for IQ, 76 percent unadjusted, by mid-year. That makes it untenable to put a frontier model in front of customers unless their lifetime value is massive. His public prediction: the back half of 2026 sees a rapid uptick in domain-specific agent frameworks, and 2027 becomes the year of multi-agent orchestration. He points to Vercel's just-released Eve framework, which markets itself for building a "domain-specific agent," as the first echo of the term coming back to him.

The closing sketch describes his ideal agent primitive: model, system prompt, a tool layer split into functions, prompts, and full sub-agents, plus hooks (for example injecting the current time as an artificial message), agent rules like turn limits, and a sandboxed file system and code execution environment baked in. Sub-agents recurse: a coordinator delegates to a Salesforce agent, which calls an asset-generation agent, while a legal-team agent keeps a separate GDPR sub-agent so the main context never carries 45 megabytes of compliance text.

## Notable moments

- [0:12:10](https://www.youtube.com/watch?v=spNAUEgq_A8&t=730s) Schroeder names the pattern: MCP servers and skills are inheritance, and composition should win instead.
- [0:16:17](https://www.youtube.com/watch?v=spNAUEgq_A8&t=977s) Apollo 11 launch control as biomimicry for multi-agent systems, one flight controller as an agent with only his own tools.
- [0:22:20](https://www.youtube.com/watch?v=spNAUEgq_A8&t=1340s) The token cost reversal: up 29 percent IQ-adjusted and 76 percent raw in the first half of 2026.
- [0:27:23](https://www.youtube.com/watch?v=spNAUEgq_A8&t=1643s) The ideal agent primitive, ending in recursive sub-agents down to a GDPR compliance agent.

## Connections

- [Vercel](../../companies/cloud-compute/vercel.md), whose Eve framework and AI SDK Schroeder cites as the closest existing thing to his domain-specific agent vision.
- [Session recaps](../../notes/session-recaps.md), where the in-person Vercel session on Eve covers the same framework he points to as validation.
- [LangChain](../../companies/agent-orchestration/langchain.md), an incumbent in the multi-agent orchestration space Schroeder predicts will define 2027.
