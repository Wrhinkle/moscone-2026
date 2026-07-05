# Flox

> A Nix-powered environment manager that gives you the same reproducible, declarative dev/build environment — languages, tools, services — locally, in CI, and in production.

- **Category:** swe-infrastructure
- **AIEWF 2026 tier:** silver
- **Founded:** 2018 (public launch 2023), New York (Verified — Crunchbase, TechCrunch)
- **Website / GitHub:** https://flox.dev · https://github.com/flox/flox

## What they do
Flox wraps the Nix package manager in a friendlier CLI/config layer (`flox activate`) so a team can declare exact package, service, and env-variable sets in a manifest and get an identical, reproducible environment across macOS/Linux, x86/ARM, local machines, CI, and containers — solving "works on my machine" and letting AI coding agents spin up correctly-provisioned sandboxes without bespoke Dockerfiles.

## Founders & origins / Funding
Founded by Ron Efroni (CEO, ex-Facebook developer products, IDF Unit 8200) and Michael Brantley (CTO, built Nix tooling at D.E. Shaw). Incubated at D.E. Shaw's DESCOvery venture studio. Raised $16.5M Series A (2023, led by NEA) and $25M Series B (Sept 2025, led by Addition; NEA, D.E. Shaw group, Hetz Ventures, Illuminate Financial participating) — ~$27M+ total disclosed (Verified — TechCrunch, Flox blog).

## Evidence of real-world use
PostHog is a named customer, citing Flox for eliminating environment drift and collapsing a 16-step, 14-caveat local setup into one command (Reported — Flox blog). Open-source core on GitHub under active development.

## Relevance to agentic AI engineering
Directly relevant to SWE-agent infrastructure: reproducible environments are a prerequisite for reliable coding-agent sandboxes and CI, overlapping with this repo's coverage of Daytona, E2B, and Coder.

## Sources
- https://techcrunch.com/2023/02/07/flox-raises-27m-to-bring-nix-to-more-developers/
- https://flox.dev/blog/about-our-series-b/
- https://techstartups.com/2025/09/25/flox-raises-25m-series-b-to-tackle-software-supply-chain-chaos-with-unified-dev-infrastructure/
- https://flox.dev/blog/works-on-my-machine-a-platform-problem/
- https://github.com/flox/flox
