# Research to Reality: Bringing Frontier ML Research to Production

> Higharc's process for handing ML research prototypes to software engineers: a taxonomy document, a microservices mono repo, and a stacked-diff decomposition plan.

- **Speaker:** Vaidas Razgaitis, Higharc
- **Video:** [Watch on YouTube](https://www.youtube.com/watch?v=OXMMN-XbxwA) (AI Engineer channel; ~15m, released 2026-06-28)
- **Program:** Online Track 2026

## Summary

Razgaitis is a senior research engineer on the labs team at Higharc, whose home-building product pulls in most of the applied ML toolbox: computer vision to parse hand-sketched floor plans into an internal data model, reasoning agents, custom transformers, and diffusion models for image generation. The talk's problem is the baton pass between two groups. Platform and backend engineers know how to build production-grade code but not computer vision methodology or LLM training; ML researchers read the latest papers and combine concepts creatively but have rarely owned production APIs. Razgaitis treats the handoff as a systems and process problem with three levers.

The first lever is research legibility. Citing the Pragmatic Engineer's argument that scaling teams need written design documents, Higharc requires a research prototype taxonomy document (they write it in Notion) for every prototype. It opens with domain context, the representations a new hire from, say, JP Morgan would need before touching the project, such as parti diagrams, circulation graphs through a home, or latent space representations, followed by the business goal. The rest is conventional design-doc material with ML twists: the type contract between the core product repo and the ML repo and how types stay in sync, the persistence layer (deliberately left thin by researchers, since it is the natural first entry point for incoming software engineers), the system architecture including external LLM calls, and the plan for merging and decomposing the work.

The second lever is code structure. Higharc keeps a Python mono repo separate from the core product repo, organized as cleanly isolated, fully decoupled microservices at roughly a one-to-one researcher-to-microservice ratio. A gateway guards requests on a single Docker bridge network and routes calls from web application clients to the right service. Each microservice follows the same layered anatomy (API routers wrapping controllers wrapping business logic, exposed as a standalone FastAPI application) with a Dockerfile, dependencies, and lock files in its root, plus clearly documented specs so coding agents can navigate the repo and accelerate the researchers. GitHub Actions handles builds, tests, linting, and type checks, and Jupyter notebooks run on Modal for GPU compute.

The third lever is decomposition and review. A proven monolithic prototype gets sliced along its dependency graph, and Higharc uses Graphite stacked diffs so review is asynchronous: one engineer works at the top of the stack while a domain specialist reviews a lower PR, and tightly scoped slices go to the right subject matter experts. He closes with diagnostics for each lever: if newly staffed engineers cannot tell where to concentrate, revisit the taxonomy document; if new research keeps fighting old abstractions, the repo has been outgrown; if delivery timelines for productionizing research are consistently unpredictable, the problem is upstream in the handoff or the host codebase.

## Notable moments

- [0:04:02](https://www.youtube.com/watch?v=OXMMN-XbxwA&t=242s) The research prototype taxonomy document: a design doc that starts with domain context and type contracts rather than implementation.
- [0:07:03](https://www.youtube.com/watch?v=OXMMN-XbxwA&t=423s) The ML mono repo: decoupled microservices, one per researcher, behind a gateway on a Docker bridge network.
- [0:11:06](https://www.youtube.com/watch?v=OXMMN-XbxwA&t=666s) Decomposing a platform-wide agent feature with Graphite stacked diffs and per-slice expert review.

## Connections

- [Modal](../../companies/cloud-compute/modal.md) is where Higharc runs its GPU-backed Jupyter notebooks and ML studies in this workflow.
