---
title: "Stop Building Chatbots for the Back Office — Build Evaluators"
date: 2026-07-02
description: "The useful shape of back-office AI is not a conversation. It's an evaluator: messy operational text in, structured state, gap detection, and human-approvable next actions out — with the checklist hardcoded and the model kept away from the verdict."
tags:
  - agents
  - back-office-automation
  - document-extraction
  - evaluators
  - approval-gates
  - construction
  - aiewf-2026
draft: true
sources:
  - briefs/2026-07-02-aiewf-batch-01.md
  - companies/back-office-automation/reducto.md
  - companies/back-office-automation/extend.md
  - companies/back-office-automation/bem.md
  - companies/back-office-automation/wisedocs.md
  - companies/agent-orchestration/humanlayer.md
  - papers/planning-architecture/reagent-requirement-driven-llm-agents-for-software-issue-re.md
  - papers/planning-architecture/from-plan-to-action-how-well-do-agents-follow-the-plan.md
  - papers/tool-use-governance/governance-by-construction-for-generalist-agents.md
  - notes/conference-notes-raw.md
  - notes/source-map-aiewf-2026.md
---

Here's a job packet that's about to go wrong. A residential re-roof in Pasco County, Florida: signed contract, approved estimate, EagleView measurement report, material and labor orders, a county permit issued and on file. Twenty-seven documents, sixty-one logged communications, job value $16,240. The CRM milestone says "Approved," and the coordinator is about to move it to Production.

Two things are broken, and both are visible in the packet if you know to look. The Notice of Commencement, which Florida requires to be recorded before the first inspection (the warning is printed on the permit itself), was never recorded. And the shingle color is "TBD" in three separate places: the contract filename, the quote, and the crew's labor ticket, which literally says "confirm before dispatch." Nobody catches either one, because everything *looks* done. The gaps get caught late: at the permit desk, on the roof, when the supplier calls asking what color to load. Every late catch is a callback, a delay, or a re-trip.

(That packet is a synthetic test fixture, with fabricated names and addresses, structured one-to-one with real AccuLynx job-packet exports. The failure mode is not synthetic.)

I spent June 30 through July 2 at the AI Engineer World's Fair in Moscone West, walking the expo floor with exactly this problem in my pocket, because I work with a roofing and insurance-restoration contractor whose back office lives in these packets. The question I kept testing against every booth: does anything here catch the missing NOC *before* the crew rolls?

By the last day I had a strong opinion: the useful form of back-office AI is not conversational. It's an evaluator. Messy operational context in; structured state, missing-item detection, and human-approvable next actions out. Chat is an interface mismatch for work that has a checklist.

## Why a chatbot doesn't fix this

The default move (still, from what I can see, the default shape of most small-business "AI adoption") is a chatbot bolted onto the CRM. Ask your data questions in natural language. It demos well. It fails at this job for reasons that are structural, and a better model doesn't fix them.

Chat is pull-based, and the failure mode here is that nobody pulled. A chatbot answers questions someone thinks to ask. The Foster packet goes to production precisely because no one thought to ask "is the NOC recorded?"; the coordinator believed the packet was complete. A chatbot's value depends on the operator already suspecting the gap, so it misses the gaps nobody suspects. The audit has to run unprompted, over everything, the same way every time.

Chat output is prose, and operational state needs to be diffable. Ask a chatbot "is the Foster job ready?" and you get paragraphs. Paragraphs can't be compared across the forty other jobs in the pipeline or regression-tested when you change the prompt, and they can't drive a downstream tool call. A checklist evaluation is a data structure: every required item resolved to `present | missing | unclear`, with an evidence snippet. You can sort the pipeline on it and alert on it. You can also hold it to a standard.

Conversation has no completion semantics. A chat session is done when the human stops typing. A packet audit is done when every required item has a status and every blocking gap has an owner. That property is what makes the output trustworthy: the audit is *exhaustive by construction*, and it doesn't depend on the model happening to be thorough today.

Language models still belong in this loop, doing the extraction and the drafting. They stay away from the interface and the verdict.

## The evaluator pattern

The pattern, mechanically. Five stages. Data flows one direction and stops at a human.

1. State reconstruction. Take the messy input (pasted CRM notes, email threads, a document folder's filename list) and extract typed facts against a fixed schema: permit number, NOC status, color selection, HOA approval, order status. This is the only stage where the model does open-ended reading.
2. Gap detection. Diff the extracted state against a hardcoded required-item checklist. Every item resolves to a tri-state: `present`, `missing`, or `unclear`. The design rule that matters most: prefer `unclear` over a false `present`. Weak evidence becomes a follow-up question. It never becomes a silent pass.
3. Risk classification. Each checklist item carries a `blocking` flag, set in code by a human who knows the domain; the model never infers it per run. Verdict semantics are then trivial and deterministic: `NOT READY` if any blocking item is missing *or unclear*; `READY WITH RISKS` if blocking items are all present but non-blocking ones aren't; `READY` only if everything required is present.
4. Next actions, routed by owner. Every gap becomes a task in one of two lanes: office follow-up (record the NOC, chase the HOA letter, lock the color) or production concerns (crew scope, materials, access). A gap with no owner survives.
5. Structured output, terminating at a human. A verdict badge, the checklist table with evidence quotes, the two task lanes, two copy-ready notes (one customer-facing, one internal for the CRM), and the whole thing as JSON. The tool advises; a person releases the job.

The architectural decision hiding in there is the split between judgment and reading. The checklist (what's required, what blocks, what the verdict rules are) is configuration, authored by the operator and executed deterministically. The model handles the parts that genuinely need language understanding: pulling "NOC still needs to be recorded before first inspection — homeowner has not returned the signed NOC yet" out of a communications log and mapping it to `noc: missing`, and drafting the follow-up prose. If the extraction pass and a blocking rule ever disagree, the rule wins. You get the model's tolerance for mess without giving it authority over the outcome.

## The walkthrough: a job packet readiness auditor in an evening

I built this as the Job Packet Readiness Auditor, a deliberately small tool stood up in about two hours around the conference. One page, vanilla HTML/JS/CSS, no build step, no database, no auth, no CRM integration. Paste the job's notes and document list, click Audit.

Concrete details that carry the pattern:

- The checklist is a config array with no logic in it. Each entry: an id, a label, detection patterns, and a `blocking` flag. For a Florida retail re-roof, blocking items include the signed contract, an address-matched measurement report, the approved estimate, material and labor orders, the county permit, the recorded Notice of Commencement, and a confirmed shingle color. Conditional items activate on toggles: HOA approval only if the property has an HOA, insurance scope docs only for insurance jobs, financing docs only if financing is involved. A *satisfied* conditional must not block; an unmet one must.
- `unclear` blocks. A permit is `present` if there's a permit-number pattern (`RESRRF-2025-######`), the word "permit" with an issue date, or a permit PDF in the folder. Anything weaker is `unclear`, and `unclear` on a blocking item yields `NOT READY`. That single rule is most of the tool's integrity: it converts extraction uncertainty into a human question before it can become a false green light.
- Evidence must be attributed to the right job. The NOT-READY test fixture deliberately includes a stray mis-filed document from a different customer in the email folder. A naive keyword scan counts it as evidence; the auditor must not. Attribution is what makes the checklist table auditable: this snippet, from this job's log, supports this status.
- The human can overrule the reading. The rules stay fixed. Each checklist row has a status override, so the coordinator corrects a bad extraction and the verdict, lanes, and notes recompute. What they can't do is mark a job READY while a blocking item stays missing.
- The output is already the follow-up. The customer note ("we need your final shingle color and the signed NOC before we can schedule") and the internal CRM note (verdict, blocking gaps, owners, next actions) are generated, copy-ready. The audit doesn't just find the gap; it hands you the message that closes it.

Honest status: the version that exists today is a local prototype whose extraction layer is keyword and pattern matching with the manual override as backstop. The LLM extraction pass, which would read free-text communication logs the way a person does and feed the same deterministic checklist, is the specified next slot in the design, along with a public repo and an obfuscated real packet as the demo fixture. The checklist authority, verdict semantics, tri-state statuses, lanes, and copy-ready notes are all running. Nothing about the pattern waits on the model getting smarter.

## The parsing layer is a commodity; the checklist is not

Walking the expo floor settled one question for me: turning ugly documents into structured JSON is now a product category with real capital and real customers, at every altitude of the stack.

- Reducto (parsing API): $108M raised, the last $75M led by Andreessen Horowitz in October 2025. Multi-pass "Agentic OCR" (CV/layout models segment the page, then vision-language models review and correct the output on handwriting, checkboxes, and rotated scans) with bounding-box citations for auditability. On their open RD-TableBench (1,000 hand-labeled complex tables) they report roughly 0.90 similarity, about 10–20 points above the AWS/Google/Azure document APIs; their benchmark, but the dataset and scoring code are public. Harvey put them in production in six weeks. 3B+ pages processed. Self-serve, $0.015 a credit.
- Extend (developer workflow product): $17M from Innovation Endeavors and others, with Brex, Square, and Checkr as named customers. The interesting parts sit *above* parsing: per-field confidence scores so low-certainty extractions route to human review, an eval harness for schema regression testing, and a "Composer" agent that iterates on your extraction schema against eval sets.
- Bem (workflow and governance): a $3.7M seed led by Uncork, and a contrarian self-description, "we don't sell software, we sell trust." Seven composable typed functions (Extract, Classify, Parse, Split, Join, Enrich, Payload Shaping) chained into versioned workflows with fallback states, plus golden datasets, drift detection, and a built-in human-review inbox.
- Wisedocs (vertical solution): since 2018, ingesting thousand-page medical claim files for insurers (dedup, chronology, summaries), with expert clinician QA on outputs as a product feature, because the summaries feed legally defensible reports.

Those four form a gradient. Each step up the stack absorbs more of the loop (parsing, then confidence-and-review plumbing, then the whole vertical workflow) and knows less about *your* domain. Every one of them ships some flavor of confidence scoring and human review, which tells you where the industry thinks the hard boundary is. But none of them know that a Pasco County retail re-roof needs a recorded Notice of Commencement before first inspection, that "COLOR TBD" in a labor ticket is a blocking gap, or that HOA approval is required for this subdivision but not the next one. That knowledge is a config array a working coordinator can dictate in twenty minutes, and it is worth more than the parsing layer it sits on. The parsing layer is for sale to your competitors at $0.015 a credit; the checklist isn't for sale at all. The place to differentiate moved from reading the documents to judging readiness.

## This is plan compliance for operations

The part I didn't expect: the strongest justification for this architecture comes from coding-agent research that never mentions a back office.

REAgent (Tianjin University and Huawei, April 2026) attacks software issue resolution by inserting a requirements-engineering stage before any patching: an agent rewrites the messy GitHub issue into a structured requirement with 9 fixed attributes, scores requirement quality mechanically, and routes low-scoring specs back for clarification before anything executes. Their ablations are the punchline. Removing the requirement-modeling stage costs 9.5 points of resolve rate, the largest single component, more than any tooling change. Restructuring the *spec* carried the gain. A job packet is a messy issue: the auditor's state-reconstruction stage is the same move, with `unclear` playing the role of the low-quality spec that goes back to a human for clarification.

From Plan to Action (April 2026) analyzed 16,991 SWE-agent trajectories and found that plans handed to agents in prompts are advisory: as the trajectory grows, the plan competes with tool-call history and drifts. Good plans help, incomplete plans are *worse than no plan*, and periodic re-injection of the plan measurably reduces violations. The operational translation: don't put your checklist in a prompt and hope. The auditor enforces the plan structurally. The checklist is code, evaluated in full on every run, so phase-skipping can't happen.

Governance by Construction (IBM Research, May 2026) makes that idea general: five typed enforcement checkpoints in an agent loop (intent guard, playbook injection, tool guidance, human approval on sensitive tools, and forced output schemas) lifted task success on their business-operations benchmark by 18–38 percentage points with no fine-tuning. Two details transfer directly. Their weakest, cheapest model *with* policies beat their strongest model without them; structure substitutes for capability, which is exactly the economics a small operator wants. And their own red-team scenario shows an intent guard bypassed by rephrasing, caught only by the human approval gate. Defense-in-depth is load-bearing, which is why the evaluator always terminates at a person. (The overhead is real too: they paid roughly 1.5–3.3x tokens for governance. For a back-office audit that replaces a re-trip to a roof, that trade is not close.)

Three papers, one finding. The reliability gains came from the structure around the model (spec construction, enforced plans, typed checkpoints), and the model itself was never the variable that moved. The evaluator pattern is that finding, applied to operations.

## Where the JSON goes next

Right now the auditor's JSON is terminal: a human reads the report, copies the notes, does the work. That's the correct v1 boundary. But the output was shaped for what comes after. Each next-action is one small step from a proposed tool call: `record_crm_note(job_id, note)`, `draft_email(recipient, body)`, `create_task(owner, description, due)`.

The move that keeps the pattern honest is that these stay *proposed*. The agent's job is to make the decision easy, with the evidence attached, an owner assigned, and the prose already drafted; a human's click executes it. This is the approval-gate primitive HumanLayer built its original API around: agent pauses, contacts a human over Slack or email, proceeds only on sign-off. (Worth knowing: that SDK is now explicitly deprecated. The company pivoted to CodeLayer, an orchestration IDE for coding agents. But the pattern outlived the product, and IBM's Tool Approval checkpoint is the same primitive shipping inside CUGA today.) Add durable pending state so an approval can wait hours without losing the agent's work, and the evaluator stops being a report generator and becomes the front half of an operations loop: observe, condense, propose, gate, act, improve.

My raw conference notes reduce to that one line, honestly: every thread I chased at Moscone, from software factories to voice agents, was some version of *loop with a human checkpoint in it*.

What I don't have yet is proof of quality at the standard I'm arguing for. Without that proof, the evaluator is a chatbot with better formatting. The next build is the eval harness: twenty obfuscated packets with known verdicts, a scoring script, a regression run on every checklist or prompt change. That's the golden-set discipline the extraction vendors sell at enterprise scale, sized down to one operator and an afternoon. The open question I keep turning over is where the ceiling is. Gap detection is clearly the evaluator's job, and releasing the job to production is clearly the human's. Risk *scoring*, the middle layer that says this missing item matters more than that one, sits uncomfortably between them. I know how I'd test it. Twenty packets at a time.
