# Replicated

> Tooling that lets a software vendor ship its SaaS product as a self-hosted/on-prem/air-gapped install into an enterprise customer's own environment — without building an on-prem delivery team.

- **Category:** cloud-compute
- **AIEWF 2026 tier:** gold
- **Founded:** 2015, Los Angeles (Verified — TechCrunch, company site)
- **Website / GitHub:** https://www.replicated.com · https://github.com/replicatedhq · https://docs.replicated.com

## What they do
Replicated solves the "your biggest prospect won't send data to your cloud" problem. A vendor packages their app (Helm chart / Kubernetes manifests) once, and Replicated handles the machinery of distributing and operating it inside customer-controlled environments: on-prem data centers, customer VPCs, air-gapped networks. The platform's main pieces:

- **KOTS** (Kubernetes Off-The-Shelf, open source, Apache 2.0): admin console + framework for installing, configuring, and updating third-party Kubernetes apps in someone else's cluster, including fully air-gapped update flows.
- **Embedded Cluster** (successor to their **kURL** installer): a single-binary install that brings its own Kubernetes, so end customers with no K8s expertise can stand the app up on a VM/bare metal; multi-node support went GA June 2025.
- **Troubleshoot** (open source): preflight checks ("does this environment meet requirements?") and support bundles (redacted diagnostics the end customer can send back to the vendor) — the remote-debugging story for software you can't SSH into.
- **Compatibility Matrix (CMX)**: ephemeral clusters/VMs across OpenShift, EKS, GKE, AKS, kind, k3s, etc., for CI-testing releases against the distributions customers actually run; Replicated dogfoods it on every KOTS PR.
- **Vendor Portal + registry**: release channels, per-customer licensing/entitlements, install telemetry ("insights" into instances you don't host), and Advanced Registry Access Controls that gate which artifacts — including model weights — each customer license can pull.

You'd integrate it by adding the Replicated SDK/CLI to your release pipeline; end customers get a Helm install, a KOTS console, or a single-binary appliance.

## Founders & origins
**Grant Miller (CEO)** and **Marc Campbell (CTO)** founded Replicated in 2015 — their second company together after **Look.io**, a mobile live-chat startup acquired by LivePerson in 2012 (Verified — TechCrunch, Software Engineering Daily). The origin story: at LivePerson they saw large enterprises demanding on-prem versions of SaaS products and how painful each bespoke delivery was (Reported — podcast interviews). Both remain in their roles as of 2026 (Reported — company site, The Org).

## Funding
- Seed, Jun 2015: $1.5M led by boldstart ventures (Reported — Clay/Crunchbase)
- Series A, Oct 2016: $5M led by Amplify Partners (Verified — TechCrunch)
- Series B, 2020: $25M led by Two Sigma Ventures (Verified — TechCrunch, Clay)
- Series C, Jul 2021: $50M led by Owl Rock (Blue Owl Capital), with Lead Edge Capital, Headline, Two Sigma, Amplify, boldstart (Verified — company announcement, SiliconANGLE)
- **Total raised: ~$85M** (Reported — Clay). No rounds found after 2021; current valuation not found in public sources.

## Evidence of real-world use
Strong and mostly verifiable. Documented vendor customers over the years: **HashiCorp (Terraform Enterprise was delivered via Replicated), CircleCI, Snyk, Sysdig, Gradle, Wickr, Signal Sciences** (Verified — TechCrunch 2019, Replicated case-study content); the 2019 TechCrunch piece cited distribution into 1,500+ enterprises including 50 of the Fortune 100 — the company now claims 70 of the Fortune 100 run apps managed by Replicated (Reported — company site). Current customer page includes quoted case studies from **GitGuardian, Pixee, KNIME**, and logos for notably AI-heavy vendors: **Cohere, Writer, H2O.ai, Protect AI, Rasa, Vellum, Reducto, DataStax, Plotly** (Reported — logos/quotes, not audited). OSS traction is modest but real: kots ~950 GitHub stars, kURL ~800, troubleshoot ~580. Public pricing/packaging pages and active monthly release notes (Kubernetes 1.33, SELinux, VM network policies in 2025) indicate an actively developed commercial product.

## Relevance to agentic AI engineering
Replicated is the delivery rail for exactly the products this landscape tracks: AI vendors whose enterprise buyers refuse to send prompts, embeddings, or documents to a multi-tenant cloud. Cohere, Writer, and Reducto (the latter profiled in this repo under back-office-automation) shipping via Replicated is the concrete pattern — "your agent stack, inside the customer's VPC," with model weights licensed per customer via registry entitlements. That maps to the deployment/governance side of papers like *Governance by Construction for Generalist Agents* (who controls what an agent and its data can touch — here answered by keeping the whole system inside the buyer's perimeter) rather than the capability side. Compatibility Matrix is also a practical cousin of the reproducible-environment demands in *Reproducible, Explainable, and Effective Evaluations of Agentic AI for Software Engineering*: matrix-testing one release across many K8s distributions is the ops-world analog of matrix-testing an agent across environments. Not an agent framework, model host, or eval tool itself.

## Use cases & considerations
Use cases: (1) an AI startup landing its first bank/defense/healthcare customer that requires VPC or air-gapped deployment; (2) gating fine-tuned model weights per enterprise license tier; (3) debugging installs you can't access via Troubleshoot support bundles; (4) CI matrix-testing a Helm-packaged agent platform on OpenShift/EKS/GKE before customers find the breakage.

Considerations: assumes your app is containerized/Kubernetes-ready — a GPU-heavy inference stack still needs its own hardware story at each customer. Platform lock-in is moderate (Helm remains the substrate; KOTS/console layer is Replicated-specific). Pricing is sales-led beyond the entry tier. Competitors: build-it-yourself Helm + docs (the default), **Octopus Deploy (which acquired Codefresh)**, **Nuon**, **Coder's** adjacent self-hosted tooling, and newer "bring-your-own-cloud" players like **Omnistrate** and **Tessell-style BYOC** offerings. Open question: no funding since 2021 — growth trajectory and burn are not publicly visible.

## Sources
- https://www.replicated.com/ and https://www.replicated.com/ai
- https://www.replicated.com/about-us
- https://www.replicated.com/customers
- https://techcrunch.com/2016/10/31/replicated-raises-5-million-for-its-product-taking-saas-products-out-of-the-cloud/
- https://techcrunch.com/2019/11/06/as-developers-embrace-kubernetes-replicated-launches-tools-to-manage-its-deployments/
- https://www.replicated.com/blog/series-c-announcement
- https://siliconangle.com/2021/07/27/replicated-raises-50-million-on-premises-software-delivery-tools/
- https://www.clay.com/dossier/replicated-funding
- https://github.com/replicatedhq
- https://docs.replicated.com/vendor/embedded-overview and https://docs.replicated.com/vendor/testing-about
- https://www.replicated.com/blog/how-replicated-uses-the-compatibility-matrix-to-continuously-test
- https://www.replicated.com/blog/distributing-ai-models-into-self-hosted-environments---lessons-from-replicated-and-h2o-ai
- https://softwareengineeringdaily.com/2020/01/28/replicated-software-delivery-with-grant-miller-and-marc-campbell/

*Profile compiled 2026-07-02.*
