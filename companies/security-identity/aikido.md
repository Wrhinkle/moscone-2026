# Aikido

> Developer-first "all-in-one" application security platform (SAST, SCA, secrets, IaC, cloud, runtime) that aggressively filters false positives and auto-fixes issues — a Ghent, Belgium unicorn positioning itself as the AppSec layer for AI-generated code.

- **Category:** security-identity
- **AIEWF 2026 tier:** silver
- **Founded:** Incorporated October 2022, Ghent, Belgium (Verified — Wikipedia, TechCrunch, company site)
- **Website / GitHub:** https://www.aikido.dev · https://github.com/AikidoSec · https://github.com/opengrep/opengrep

## What they do

Aikido bundles ~10 scanner categories that mid-size teams would otherwise assemble from separate vendors into one platform: SAST, SCA/dependency scanning, secrets detection, IaC scanning, container scanning, DAST, CSPM, license scanning, and malware detection in open-source dependencies (their "Aikido Intel" threat feed). It plugs into git providers (GitHub/GitLab/Bitbucket/Azure DevOps), CI, IDEs, and cloud accounts; findings are deduplicated and triaged with reachability/exploitability filtering — the core pitch is "no BS": they claim ~75% noise reduction versus running the underlying scanners raw. An **AI Autofix** feature opens PRs that remediate SAST/IaC/dependency findings.

Two pieces matter for supply-chain defense: **Safe Chain**, a free npm-install wrapper/proxy that blocks known-malicious packages at install time, and **Aikido Intel**, which does automated (LLM-assisted) analysis of newly published package versions to catch malware before advisories exist. On the runtime side, **Zen** is an open-source in-app firewall (embedded agent for Node.js, Python, PHP, Java, Ruby...) that blocks injection attacks, SSRF, and bot traffic inside the application process.

They also co-launched **Opengrep** (January 2025), a consortium fork of Semgrep's SAST engine created with ~10 otherwise-competing AppSec vendors (Endor Labs, Orca, Kodem, Amplify, etc.) after Semgrep moved key open-source capabilities behind its paid platform. Opengrep restores cross-file taint analysis and fingerprinting under LGPL and underpins Aikido's own SAST.

## Founders & origins

- **Willem Delbare** — CEO; previously co-founder/CTO of Teamleader and Officient (Verified — TechCrunch, company About page).
- **Roeland Delrue** — co-founder; ex-Showpad, Officient (Verified).
- **Felix Garriau** — co-founder; ex-nexxworks (Verified).
- Amber Rucker (ex-Veriff, CloudBees) is listed in some profiles as part of the founding team (Reported — Tracxn/press summaries).

Origin story: Delbare's experience as a scale-up CTO drowning in security-tool noise and vendor sprawl; Aikido was built as the tool he wished he'd had — SMB-friendly, self-serve, with a free tier.

## Funding

- Pre-seed: €2M, January 2023 (Verified — company blog, press).
- Seed: €5M, November 2023, co-led by Notion Capital and Connect Ventures (Verified).
- Series A: $17M, May 2024, led by Singular (Verified — TechCrunch).
- Series B: $60M at a **$1B valuation**, announced January 14, 2026, led by DST Global with PSG Equity, Notion Capital, and Singular participating — reported as the fastest European cybersecurity company to reach unicorn status (Verified — GlobeNewswire, SecurityWeek, SiliconANGLE).
- Total raised: ~$85M from verified rounds; Tracxn lists $94.7M (Reported).

## Evidence of real-world use

- Named customers: Revolut, Deel, the Premier League, SoundCloud, Niantic, Tines, n8n; a documented Supermetrics case study (workflow/noise-reduction claims). Series B PR claims 100k+ teams and 5x revenue growth in 2025 (company-sourced; treat growth numbers as Reported).
- Strongest independent signal: Aikido's research team repeatedly *broke* major npm supply-chain incidents before official advisories — they were among the first to flag the September 2025 compromise of `chalk`/`debug` (the qix phishing incident, ~2.6B weekly downloads affected), tracked the self-propagating **Shai-Hulud** worm and its November 2025 v2 wave (Zapier, ENS packages), and spotted new strains in December 2025 (Verified — The Hacker News, DevOps.com, Wiz cross-references).
- Public self-serve pricing with a genuinely free tier; listed on AWS Marketplace.
- OSS footprint: Opengrep is an active multi-vendor project; Zen and Safe Chain are open source under AikidoSec.

## Relevance to agentic AI engineering

Aikido's explicit thesis for 2026 is securing AI-generated code and moving toward "autonomous self-securing software" — i.e., scanners plus agents that fix what they find. For anyone running coding agents (the agentic-SWE-benchmark thread in this repo — SWE-bench-style automated patching), Aikido sits on both sides: AI Autofix is itself an agentic SWE workflow with a guardrail-shaped harness (scan → propose patch → PR → human merge), and the platform is the review layer that catches vulnerable agent-written code in CI. Safe Chain/Aikido Intel is directly relevant to tool-use governance: agents that `npm install` on their own are a prime target for the Shai-Hulud-class attacks Aikido documents, so install-time malware blocking is a concrete control for sandboxed agent environments. Adjacent repo profiles: Snyk (same category), Sonar and Qodo (code-quality/review for AI code).

## Use cases & considerations

Use cases: (1) single AppSec pane for a small platform team instead of 5+ tools; (2) install-time supply-chain protection for CI and agent sandboxes via Safe Chain; (3) auto-remediation PRs for dependency/IaC findings; (4) runtime protection via Zen where a WAF is too coarse.

Considerations: breadth-over-depth tradeoff — each individual scanner is likely shallower than a best-of-breed specialist (Semgrep/Snyk for SAST, Wiz for cloud); noise-reduction claims are vendor-stated; the platform is closed-source even though components (Opengrep, Zen) are open. Main competitors: Snyk, Semgrep, GitHub Advanced Security, Socket (supply chain), Arnica/Ox (ASPM), Wiz (cloud side). Open questions: how "autonomous self-securing" plays out beyond marketing, and whether SMB-friendly pricing holds as they push upmarket post-Series B.

## Sources

- https://techcrunch.com/2024/05/01/belgiums-aikido-lands-17m-series-a-for-its-no-bs-security-platform-aimed-at-developers/
- https://www.globenewswire.com/news-release/2026/01/14/3218567/0/en/aikido-security-raises-60-million-series-b-at-1-billion-valuation-to-lead-software-security.html
- https://www.securityweek.com/aikido-security-raises-60-million-at-1-billion-valuation/
- https://siliconangle.com/2026/01/14/aikido-security-raises-60m-series-b-1b-valuation-unify-application-security/
- https://www.aikido.dev/ and https://www.aikido.dev/about
- https://www.aikido.dev/blog/aikido-funding-series-b
- https://www.aikido.dev/blog/launching-opengrep-why-we-forked-semgrep
- https://github.com/opengrep/opengrep
- https://www.aikido.dev/blog/shai-hulud-strikes-again-hitting-zapier-ensdomains
- https://thehackernews.com/2025/12/researchers-spot-modified-shai-hulud.html
- https://devops.com/attackers-testing-new-strain-of-shai-hulud-on-npm-aikido/
- https://www.wiz.io/blog/shai-hulud-2-0-ongoing-supply-chain-attack
- https://en.wikipedia.org/wiki/Aikido_Security
- https://tracxn.com/d/companies/aikido/__xQ2U4WYMnhUY7OwCBzy1vKkt86W3WYGS5C0LXCvrWsw
- https://aws.amazon.com/marketplace/pp/prodview-cogk44gx2w4ge
