---
title: "Agents Should Prepare Decisions, Not Make Them"
date: 2026-07-02
description: "The approval gate is an engineering primitive with a real stack behind it: durable workflow engines hold pending state, a contact layer routes the decision, and the agent's job is to make approving easy. A practitioner synthesis of what the workflow vendors and the agent-security papers are converging on."
tags: [agents, human-in-the-loop, durable-execution, approval-gates, agent-security, back-office-ai]
draft: true
sources:
  - briefs/2026-07-02-aiewf-batch-01.md (brief #3)
  - companies/agent-orchestration/humanlayer.md
  - companies/agent-orchestration/temporal.md
  - companies/agent-orchestration/inngest.md
  - companies/agent-orchestration/orkes.md
  - companies/security-identity/workos.md
  - companies/security-identity/scalekit.md
  - papers/tool-use-governance/governance-by-construction-for-generalist-agents.md
  - papers/tool-use-governance/camels-can-use-computers-too-system-level-security-for-comp.md
  - papers/tool-use-governance/clawless-a-security-model-of-ai-agents.md
  - notes/conference-notes-raw.md
---

Here's a number from a paper that should change how you build agents: in IBM's Governance by Construction benchmarks, adding five structural policy checkpoints to an agent loop took GPT-OSS-120B from 75% to 100% task success on insurance workflows, and from 49.2% to 82.3% on business-operations tasks — a 33-point jump with no fine-tuning. The pattern underneath the whole ablation: the weakest, cheapest model *with* structural constraints beat the strongest model without them.

One of those five checkpoints is a human approval gate. Not a disclaimer. Not a "human oversight" slide in the compliance deck. A pause in the execution graph, after the agent has generated its action but before the action runs, where a person looks at prepared evidence and says yes or no.

I spent three days at the AI Engineer World's Fair in Moscone West this week, and my raw notes have a line that just says "approval loops — HumanLayer, metareflection/guardians." Walking the expo floor, it clicked that the approval gate isn't one product — it's three infrastructure layers that already exist, built by vendors who mostly arrived at the problem from different directions. Nobody at the conference said this as one sentence, so here it is: **the agent's job is to prepare the decision — assemble the evidence, draft the action, quantify the stakes — and the infrastructure's job is to hold that prepared decision durably, route it to the right human, and record what happened.** The agent should not make the decision. Not because models are dumb, but because the system that separates preparation from authority is more reliable, more auditable, and — per the numbers above — measurably better at the task.

## "Human in the loop" is usually vaporware

Ask a team demoing an agent product how humans stay in control and you'll usually get one of three answers, all of which are checkboxes rather than systems:

1. **The confirm dialog.** The agent prints "I'm about to send this email, OK?" in a chat window. If the user has tabbed away, the agent waits forever or times out and gives up. There is no state — close the tab and the pending action evaporates.
2. **The dry-run mode.** The agent produces a plan a human is supposed to read before flipping the real switch. In practice the plan is 400 lines and nobody reads past line 20.
3. **The audit-after.** Everything the agent did is logged somewhere, and if something goes wrong you can reconstruct it. This is a flight recorder, not a control surface.

What all three lack is the same thing: **a pending decision as a first-class piece of state.** A real approval gate needs the agent's proposed action to survive a process crash, wait hours or days without burning compute, escalate if ignored, reach the approver where they actually work (Slack, email, SMS — not a tab they closed), and leave a signed record of who decided what. That's not a prompt-engineering problem. It's a distributed-systems problem, and it's already been solved — by accident, for other reasons.

## The accidental substrate: durability built for machines fits humans better

Durable workflow engines — Temporal, Inngest, Orkes/Conductor — were built to survive *machine* failures: a worker dies mid-payment, a third-party API flakes, a deploy interrupts a batch job. The core mechanism in each is that workflow state persists outside the running process, so execution can pause indefinitely and resume exactly where it stopped.

Here's the non-obvious part: infrastructure built for millisecond-scale machine failures is *accidentally the right substrate for hour-scale human latency*. A human who takes six hours to approve a change order is, from the engine's perspective, indistinguishable from a rate-limited API that will succeed on retry tomorrow. The engines don't care why the workflow is waiting. Waiting is the thing they're good at.

The three vendors solve "where does the pending-human-decision state live" differently, and the difference matters if you're picking one:

**Temporal** event-sources the entire workflow execution: every side effect (an "activity" — API call, DB write, LLM call) is intercepted and appended to a history. A workflow can `sleep` for a month; a human decision arrives as a **signal** that wakes it. If the worker died in the meantime, another worker deterministically replays the history and resumes at the wait point — critically, *without re-executing the LLM calls that produced the pending action*, because their results are in the history. You don't re-burn tokens to recover a paused decision. This is the heavyweight option: OpenAI reportedly runs Codex on Temporal in production, and the company raised a $300M Series D at a $5B valuation in February 2026 explicitly positioning as the reliability substrate under agents. The cost is the programming model — workflow code must be deterministic, and versioning in-flight workflows is a known pain.

**Inngest** checkpoints at the step level: you write functions composed of `step.run()` calls, each step's result is persisted, and — this is the directly relevant primitive — `waitForEvent()` pauses a workflow for hours or days until a matching event arrives. The human's approval *is* an event. Because Inngest invokes your functions over plain HTTP, the same gate code runs on serverless or a long-lived server, and the local dev server gives you full run traces while you're building. It's the option sized for a small team: a real product (raised a $21M Series A led by Altimeter in September 2025), but you can wire a gate in an afternoon.

**Orkes/Conductor** (from the Netflix Conductor creators; $60M Series B in April 2026) represents workflows as declarative JSON DAGs rather than code, and ships **human-in-the-loop approval tasks as a native task type**, alongside RBAC with fine-grained policies and audit logs at the enterprise tier. The pending decision lives as data in the DAG's state. The pitch writes the governance story for you — the counterargument is that JSON-DSL workflows get unwieldy compared to code, which is exactly Temporal's counter-pitch.

The shared insight across all three: **a pending human decision is just a paused workflow step.** Timeout semantics, escalation (a timer branch that fires if nobody responds), retries on the notification, resumption after approval — all of it falls out of machinery these vendors built before agents were the customer.

## The second layer: routing the decision to a human

Durable state solves *where the pending decision waits*. It doesn't solve *how a human finds out about it*. That's a contact-layer problem: reach the approver in Slack, email, or SMS; render the prepared decision legibly; capture an authenticated yes/no; deliver it back as the signal/event that resumes the workflow.

The company whose name is on this layer is HumanLayer, and its trajectory is itself a data point worth being honest about. HumanLayer v1 was exactly this: a framework-agnostic API + SDK that let any agent pause and contact a human over Slack, email, or SMS before executing high-stakes tool calls. Founder Dex Horthy built it after his own SQL-warehouse-cleanup agent needed sign-off before dropping tables — the canonical origin story for this whole pattern. That SDK sits at ~11k GitHub stars. It is also **explicitly marked deprecated by the maintainers.** The company pivoted to CodeLayer, an IDE for orchestrating fleets of coding agents — which is still approval gates all the way down (humans reviewing research, plans, and diffs at every phase), but narrowed to software engineering, where the willingness to pay showed up first.

Two readings of that pivot. The bearish one: a standalone approval-routing API wasn't a big enough product. The bullish one — which I think is correct — is that approval routing is a *thin* layer, and thin layers get absorbed: into the workflow engines (Orkes ships human tasks natively; Inngest's `waitForEvent` plus a Slack webhook is 80% of the v1 SDK), or into the vertical product like CodeLayer. Either way, the pattern won even though the standalone product moved on. The 12-factor-agents guide Horthy wrote — with "contact humans as a tool call" as one of its factors — has near 10k stars and shaped how a lot of the floor talks about this.

Practically, in mid-2026, you should expect to hand-roll this layer: a Slack Block Kit message with approve/reject buttons, an endpoint that verifies the click and emits the resume event. It's a day of work, and you own the UX of the most important screen in your system.

## The third layer: the paper trail, and who the agent even is

An approval gate without an audit trail is a rubber stamp with extra steps. Two identity-layer vendors from the expo floor cover this:

**WorkOS** (platinum sponsor; $100M Series C at a $2B valuation in March 2026, raised explicitly for "securing agentic software") sells the audit-log and identity plumbing as APIs — and its newer agent-facing work matters here: AuthKit as an OAuth 2.1 authorization server for MCP servers, and session-scoped, time-bounded access grants for agent data connections instead of standing OAuth tokens. Translation: the agent that prepared your decision was operating under a scoped, expiring credential, and the human who approved it authenticated through real SSO. The approval event is attributable.

**Scalekit** (seed stage, $5.5M) is the sharper articulation of the delegation problem: agents act as *the specific user who triggered them* — delegated identity inheriting that user's SSO permissions — not as an org-wide service account, with every action logged as a delegation chain: which user authorized, which agent acted, which tool, what scope, what result, exportable to SIEM. Whether or not you buy the product, "delegation chain" is the right schema for your audit table. When the change order goes wrong, "the agent did it" is not an answer; "Sarah's session authorized agent run 4821, which proposed action X, approved by Mike at 2:14 PM" is.

## The worked example: a change-order explainer with a real gate

Theory earns nothing until it's wired. Here's the build I'm doing next — small enough for a weekend, real enough to screenshot. Context: I work with a roofing/insurance-restoration company, and change orders are the highest-stakes routine communication in the business. A change order tells a homeowner mid-project that scope and price changed. Get the explanation wrong — or worse, let it go out with an error — and you've burned trust with someone who already has a hole in their roof.

The agent's job is *preparation*, defined precisely:

1. **Assemble evidence.** From the pasted job file (notes, original scope, supplement docs — same paste-text-in pattern as the job-packet auditor I built during the conference): what changed, why (rot discovered under decking, code-required upgrade, supplement approved by the insurance carrier), and the cost delta.
2. **Draft the action.** A plain-language customer-facing explanation of the change order, plus an internal CRM note, plus a line-item evidence list — each claim in the draft linked to the source line in the job file that supports it.
3. **Quantify the stakes.** Dollar delta, whether the change is carrier-approved or homeowner-pay, and a flag if any claim in the draft has *no* supporting line (the agent must say "I couldn't verify X" rather than smooth it over).

Then the gate, wired concretely on Inngest as the pending-state layer (right-sized for one person; the same shape ports to Temporal signals or an Orkes human task):

```
inngest.createFunction("change-order-explainer", async ({ step }) => {
  const evidence = await step.run("assemble", () => auditJobFile(input));
  const draft    = await step.run("draft", () => draftExplanation(evidence));

  await step.run("notify", () => postSlackApproval(draft, evidence));

  const decision = await step.waitForEvent("approval.decided", {
    match: "data.changeOrderId",
    timeout: "24h",          // the load-bearing line
  });

  if (!decision) return escalate(draft);          // timeout ≠ yes
  if (decision.data.approved) {
    await step.run("send", () => sendToCustomer(draft));
  }
  await step.run("audit", () => logDelegationChain(decision));
});
```

The Slack message is the product: the drafted customer message on top, the evidence list with source links below, the dollar delta in the header, two buttons. The approver should be able to decide in under a minute *because the agent did the preparation* — that's the whole thesis in one screen. The timeout resolves to escalation (notify the office manager), never to auto-send. The audit step writes the delegation chain: run ID, evidence hash, approver identity, timestamp.

Every step result is checkpointed, so if the process dies while the approval sits in Slack overnight, nothing is lost and no LLM call re-runs. Total new infrastructure: zero servers I didn't already have.

## What the security papers add: the gate is one checkpoint, not the whole defense

Three 2026 papers, read together, upgrade the approval gate from "good practice" to "component of a defense-in-depth architecture" — and each contributes one specific idea.

**Governance by Construction** (IBM Research) supplies the empirical case and a warning. The five checkpoints — intent guard, playbook injection, tool-boundary guidance, **tool approval**, output formatting — bought +18 to +38 points of task success across models. But the detail that matters most: in their own red-team scenario, the intent guard was *bypassed by rewording the malicious request*, and the tool-approval gate was what caught it. The probabilistic defenses (prompts, classifiers) leak; the structural pause before the sensitive action is the backstop. Defense-in-depth isn't a platitude here — it's load-bearing, and the human gate is the deepest layer. Budget note: the policy machinery cost 1.5–3.3x tokens. Reliability isn't free; it's just cheaper than the failure.

**CaMeLs Can Use Computers Too** contributes the *separation principle*. Its architecture splits a privileged planner (which compiles the full execution plan before ever seeing untrusted content) from a quarantined perception model (which can fill in values but cannot alter control flow). Result: injected content — like the cookie-banner injection that hijacked 100% of undefended computer-use agents in their tests — cannot execute anything outside the pre-approved plan. The approval-gate translation: **what the human approves should be a complete, bounded plan, not a running conversation.** If the approved artifact is "send exactly this message to exactly this customer," then nothing the agent ingested — a malicious line pasted into the job notes, say — can widen the blast radius after approval. Approve plans, not vibes.

**ClawLess** contributes the *enforcement floor* — with the honest caveat that it's a design paper with no empirical evaluation yet. Its model assumes the agent itself may be compromised and enforces dynamic, taint-aware policies at the syscall layer (gVisor + BPF), entirely outside the model: "if the agent reads sensitive files, permanently revoke its network access." Its most stealable idea is the **Visible** permission — an agent can *reference* a credential without ever reading its contents. For the change-order build: the agent drafts the send; the workflow engine, holding the actual API credential, executes it after approval. The agent never touches the thing that makes the action irreversible. Preparation and authority stay in different trust scopes — which is the security formalization of this post's title.

## The failure modes are human, and you should design for them on day one

The gate's weakest component is the approver, and the literature on alert fatigue applies verbatim:

- **Approval fatigue.** If every low-stakes action hits the gate, approvals become noise and the one that matters gets rubber-stamped at 4:55 PM on a Friday. The fix is risk-tiering: the Governance-by-Construction approach gates *sensitive* tools (DB writes, third-party sends), not everything. For change orders: auto-proceed under a dollar threshold with post-hoc review, gate above it.
- **Rubber-stamping.** If approvers always click yes, measure it — approval rate, median time-to-decision, and whether *any* request has ever been rejected. A gate with a 100% approval rate over months is either perfectly tuned or decorative, and you should find out which. This is an eval problem, and your golden set should include cases the human *must* reject.
- **Timeout defaults.** The single most consequential line in the workflow is what happens when nobody answers. Timeout-to-proceed silently converts your approval gate into a notification system. Timeout-to-escalate is the only defensible default for customer-facing or destructive actions, even though it costs throughput.
- **Evidence quality decay.** If the agent's evidence lists get sloppy, approvers stop reading them, and you're back to vaporware with better logging. The evidence artifact needs its own eval — does every claim in the draft trace to a source line? — separate from whether the draft "sounds good."

## Where this goes

The pieces are conspicuously ready to be one thing. The workflow engines hold pending decisions durably; the identity layer signs and scopes them; the security papers say what the approved artifact should be (a complete plan, executed under credentials the agent never holds). What doesn't exist yet is the connective standard: a common schema for a *prepared decision* — evidence, proposed action, stakes, expiry, escalation path — that any engine can hold and any chat surface can render. HumanLayer's deprecated SDK was the closest thing to it, and the shape of its pivot suggests the schema may end up living in the engines rather than as a standalone product.

My next experiment is the unglamorous version of that question: build the change-order explainer above, run it on real (obfuscated) job files for two weeks, and track exactly two numbers — median time-to-approval, and how many drafts the human edited before approving. If the second number doesn't drop week over week, the agent isn't actually preparing decisions; it's generating homework. That's the metric I'd want every "human in the loop" vendor at next year's World's Fair to put on the slide.
