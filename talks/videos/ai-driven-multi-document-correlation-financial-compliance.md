# AI-Driven Multi-Document Correlation for Financial Compliance
> A three-part framework (graph entity correlation, probabilistic risk scoring, cross-jurisdictional normalization) for catching fraud that only shows up between documents, evaluated on 3 million financial records.

- **Speaker:** Varsha Shah, Independent
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=Iwe_RY-fYgI) (AI Engineer channel; ~19m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary
Varsha Shah, who describes herself as an enterprise technical architect at Tata Consultancy Services working for Microsoft, presents research on fraud detection in enterprise financial compliance. Her starting claim: most compliance systems validate documents independently. A payroll register gets checked against payroll rules, a vendor invoice against procurement policy, a tax filing against tax regulations, and if each passes on its own, the transaction is treated as compliant. Shah argues modern fraud rarely appears as an error inside a single document. It exploits inconsistencies across systems, so each record looks legitimate in isolation and the risk only becomes visible when records are connected. The information already exists; what is missing is the ability to model the relationships.

The framework has three components. A graph-based entity correlation engine links employees, vendors, accounts, transactions, and regulatory filings across payroll, tax, procurement, and financial systems into one network, answering the question of what is connected. An adaptive probabilistic risk model then scores the connected patterns, combining signals like anomaly strength, source reliability, and historical patterns into a confidence-based risk score rather than firing alerts off single rules, and it learns from audit outcomes over time. A cross-jurisdictional normalization layer standardizes currencies, tax structures, reporting periods, and classification schemes so the same transaction is interpreted consistently regardless of where it originated.

Shah evaluated the framework on approximately 3 million financial records collected over five years across four regulatory jurisdictions. She reports 91 percent precision, 87 percent recall, and an F1 score of 0.89, and says these results held consistently across jurisdictions. The operational numbers matter more to compliance teams: a 76 percent reduction in false positives, meaning investigators spend far less time clearing legitimate cases, and roughly a 40 percent reduction in manual audit effort. She frames the comparison against rule-based baselines simply: connecting data across documents produces better detection and fewer false positives than analyzing documents in isolation.

The closing sections cover the learning loop and deployment. Confirmed fraud cases strengthen future detection patterns while false positives refine the risk scoring, so the system adapts as fraud evolves instead of waiting on manual rule updates. Shah positions this as a shift from reactive compliance, where issues surface after audits and regulatory reviews, to predictive governance, where teams ask what is likely to go wrong next. For enterprise deployment she lists four considerations: integration with existing ERP, payroll, procurement, and tax platforms; jurisdiction-specific configuration; alignment with audit workflows so investigators work from prioritized risk-scored cases; and scalability to millions of records. The talk stays at the architecture level throughout, with no detail on specific models, graph algorithms, or the provenance of the evaluation data.

## Notable moments
- [0:05:08](https://www.youtube.com/watch?v=Iwe_RY-fYgI&t=308s) The three framework components introduced: correlation engine, risk model, normalization layer.
- [0:10:10](https://www.youtube.com/watch?v=Iwe_RY-fYgI&t=610s) Detection results: 91 percent precision, 87 percent recall, F1 of 0.89.
- [0:11:10](https://www.youtube.com/watch?v=Iwe_RY-fYgI&t=670s) Operational results: 76 percent fewer false positives, about 40 percent less manual audit effort.
- [0:14:12](https://www.youtube.com/watch?v=Iwe_RY-fYgI&t=852s) The continuous learning cycle from completed audits and investigator feedback.

## Connections
- [Neo4j](../../companies/memory-rag-search/neo4j.md) sells the graph database category that the entity correlation engine depends on.
- [Session recaps](../../notes/session-recaps.md) covers Stephen Chin's in-person GraphRAG session, which made the same case that auditable graph traversal beats isolated similarity lookups.
