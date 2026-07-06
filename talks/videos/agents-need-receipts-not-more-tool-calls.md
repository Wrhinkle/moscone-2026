# Agents Need Receipts, Not More Tool Calls

> Alithea Bio introduces Froglet, a protocol that lets agents discover, pay for, and get cryptographically verifiable receipts for work done across organizational boundaries.

- **Speaker:** Armanas Povilionis, Alithea Bio
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Q9ycQHbDdJs) (AI Engineer channel; ~10m, released 2026-06-26)
- **Program:** Online Track 2026

## Summary

Povilionis, drawing on a decade of life-sciences collaboration projects, argues that scientific research is among the most valuable targets for agentic automation and that more tools alone will not get there, because science runs on collaboration across organizations. His kitchen analogy carries the argument. Giving agents better knives and more ovens improves local work, but science is less like cooking alone and more like running a Michelin-star restaurant, where outcomes depend on suppliers, service, and consistent delivery. The challenge is aligning a supply chain, while today's data and specialized analytics algorithms sit in silos across organizations.

The thesis that follows: as agentic automation matures, organizations will stop just giving agents more tools and start allocating them budgets. Token budgets per task are the primitive version. The next step is agents managing their own budget for discovering services, requesting data, negotiating execution, and paying for work across organizational boundaries. At that point the agent stops being a cook with a better knife and starts acting like an executive chef.

Froglet is Alithea's protocol for that. It lets agents discover external services, transact with providers, and receive verifiable receipts. Povilionis stresses that it replaces nothing: it integrates with existing payment rails, agent harnesses, execution environments, and network transports, requiring only a shared interface rather than a shared software stack. His cost comparison is the sharpest claim in the talk. A bespoke enterprise collaboration project can take years and cost millions before the first reusable workflow exists; with Froglet, once an organization deems a resource shareable, an agent can discover it, understand its terms, request work, and receive a verifiable receipt in minutes for a few thousand tokens.

The walkthrough covers the mechanics. The network consists of homogeneous nodes playing different roles: requesters, providers, and a marketplace that is itself just a Froglet node running a specialized indexing service. Each node generates a key pair for identity and signing, and every step of a transaction is signed onto a chain running descriptor, offer, quote, deal, invoice, receipt. Tampering with any link breaks the chain. Discovery goes through the marketplace, but once a requester has an index of services, it communicates with the provider directly with no middleman: request, signing, execution, and receipt happen in one interaction. Payments have two parts by design. A base payment protects providers from being flooded with speculative requests, and a success fee protects requesters from malicious providers. Povilionis is explicit that Froglet is an interface for agents rather than an agent itself, and points to froglet.dev, where it runs locally with one command or remotely with one prompt.

## Notable moments

- [0:02:02](https://www.youtube.com/watch?v=Q9ycQHbDdJs&t=122s) The core prediction: organizations will move from giving agents more tools to allocating them budgets they manage themselves.
- [0:05:05](https://www.youtube.com/watch?v=Q9ycQHbDdJs&t=305s) Years and millions for a bespoke collaboration project versus minutes and a few thousand tokens through the protocol.
- [0:07:07](https://www.youtube.com/watch?v=Q9ycQHbDdJs&t=427s) The signed transaction chain from descriptor to receipt that cannot be tampered with without breaking.
- [0:08:08](https://www.youtube.com/watch?v=Q9ycQHbDdJs&t=488s) Direct requester-provider settlement and the two-part payment design of base fee plus success fee.

## Connections

- [PayPal](../../companies/fintech-payments/paypal.md) is building agentic commerce and payment rails at consumer scale, the incumbent version of the settlement layer Froglet wants to interface with.
- [The Evolution of Tool Use in LLM Agents](../../papers/tool-use-governance/the-evolution-of-tool-use-in-llm-agents-from-single-tool-ca.md) traces the tool-calling progression this talk argues has hit its limit for cross-organizational work.
