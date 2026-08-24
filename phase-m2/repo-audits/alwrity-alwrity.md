# Deep Repository Audit — ALwrity/ALwrity (REPO-034)

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Date: 2026-08-24. Triage record: `repo-catalog.md` Cluster E, DEEP AUDIT for
DOM-19 (secondary/comparison to digital-marketing-pro, audited separately),
DOM-20/21/22.

**Method:** `git clone --depth 1`; direct reading of
`backend/services/product_marketing/brand_dna_sync.py` (the "brand brain"
mechanism this audit was specifically asked to verify as real vs.
aspirational), plus `gh repo view` for maintenance/license signals.

## A — Architecture
Full-stack app: FastAPI/SQLAlchemy backend (`backend/`), React/TypeScript
frontend (`frontend/`), plus a separate `docs-site/`. Real separation between
onboarding data collection, a normalization/integration layer, and downstream
content-generation consumers.
**Verdict: Moderate — coherent full-stack structure, not deep-audited beyond the brand-DNA pipeline this pass focused on.**

## B — Agent design
Not a multi-agent system in the DOM-01/02 sense — a content-generation
platform with service classes, not agent roles/contracts.
**Verdict: Absent — not comparable to DOM-01/02.**

## C — Context & memory
Not applicable — relational app state (SQLAlchemy), not agent memory.
**Verdict: Absent.**

## D — Reliability
Not the focus of this pass; not inspected.
**Verdict: Unknown — not inspected this pass.**

## E — Human control
Not inspected this pass (out of assigned scope for this fork).
**Verdict: Unknown.**

## F — Evaluation
Not inspected this pass.
**Verdict: Unknown.**

## G — Operations
Stage -2.3 catalog noted "production-security features present (JWT/OAuth2,
rate limiting)" — not independently re-verified this pass; treat as
UNCONFIRMED pending a follow-up read, not silently accepted.
**Verdict: Unknown — claim not independently re-verified.**

## H — Reusability
The brand-DNA-token pipeline pattern (ingest -> canonical profile ->
layered/prioritized token extraction -> prompt-injection-ready output) is
cleanly separable as a design pattern; the code itself is tightly coupled to
this app's specific `OnboardingDataIntegrationService` and database schema.
**Verdict: Moderate.**

## I — Evidence — the priority finding for this repo
**This audit's primary task was verifying whether the "brand brain" and
multi-modal generation claims are real or aspirational, given the repo was
flagged as "active but WIP" (77 open issues/30 PRs).** FACT (verified by
reading `backend/services/product_marketing/brand_dna_sync.py` in full,
211 lines): the `BrandDNASyncService.get_brand_dna_tokens()` method is a real,
non-stubbed implementation — no `TODO`/`FIXME`/`NotImplementedError`/mock
markers found anywhere in the file. It genuinely queries a database session,
calls a real `OnboardingDataIntegrationService.get_integrated_data_sync()`
method, and normalizes THREE distinct real inputs (`website_analysis`,
`persona_data`, `competitor_analysis`) plus a `canonical_profile` into a
layered `brand_tokens` dict (writing_style, target_audience, visual_identity,
persona, competitive_positioning) explicitly documented as "ready for prompt
injection." A corresponding real frontend component
(`frontend/src/components/StrategySetupWizard/BrandBrainView.tsx`) and
onboarding-flow components (`WebsiteStep/BrandAnalysisSection.tsx`,
`PersonalizationStep/BrandAvatarStudio.tsx`) exist, confirming the feature has
both a backend implementation and a wired-up UI, not just one or the other.
FACT: 52 test files found. **Verdict on the priority question: the "brand
brain" mechanism is REAL, not aspirational** — the "active but WIP" signal
from Stage -2.3 (77 open issues/30 PRs) reflects genuine ongoing development
activity on a working core, not a facade over an unimplemented feature.
**Verdict: Strong — the specific claim this audit was tasked to verify is confirmed by direct code reading, not just presence of a matching filename.**

## J — License
**CORRECTION TO THE STAGE -2.3 CATALOG RECORD.** FACT (verified two ways):
no `LICENSE` file exists anywhere in the cloned repository (checked at
top level and depth 2), and `gh repo view ALwrity/ALwrity --json licenseInfo`
returns `licenseInfo: null` — GitHub's own license detector finds none. This
DIRECTLY CONTRADICTS the Stage -2.3 `repo-catalog.md` record for REPO-034,
which states "License: MIT." That record's MIT claim was evidently taken from
a secondary source or assumption during the discovery pass, not verified
against the repo itself — this audit is the first direct check.
**Verdict: Weak — no license file exists; the repo is effectively "all rights reserved" by default under copyright law until the maintainers add one. `repo-catalog.md` REPO-034 needs its License field corrected from "MIT" to "None found — verify before any reuse."**

---

## Evidence Section — Docs vs. Code Disagreements

1. **License (significant):** `repo-catalog.md`'s Stage -2.3 record states
   "License: MIT" for this repo. Direct verification (file search + `gh repo
   view`) found no LICENSE file and `licenseInfo: null`. This is a real
   catalog error requiring correction, not a docs-vs-code gap in the repo
   itself — logged here because it was only caught during Stage -2.4's direct
   evidence discipline, exactly the kind of thing README-level Stage -2.3
   triage can miss.
2. **Brand-brain claim:** confirmed accurate, no disagreement — the feature is
   as real as the Stage -2.3 catalog record characterized it.

## FACT / INTERPRETATION Summary

- FACT: `BrandDNASyncService.get_brand_dna_tokens()` is a real, non-stubbed
  implementation with no incompleteness markers, pulling from three real data
  sources.
- FACT: no LICENSE file exists in the repo; `gh` confirms `licenseInfo: null`.
  This contradicts `repo-catalog.md`'s prior "MIT" entry — treat the prior
  entry as an unverified assumption that has now been corrected by direct
  evidence, per Section P5.
- UNKNOWN: reliability (D), human control (E), evaluation (F), and the
  specific JWT/OAuth2/rate-limiting operations claim (G) — not inspected this
  pass, out of this fork's assigned scope; do not treat as confirmed.
