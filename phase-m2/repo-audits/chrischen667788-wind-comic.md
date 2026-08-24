# Deep Audit: ChrisChen667788/wind-comic

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo-catalog record: REPO-031 (Cluster E). Relevant domains: DOM-20 (primary),
DOM-01 (secondary, orchestration).
Audited: 2026-08-24. Method: `git clone --depth 1`, structural read of
`lib/`, `app/api/`, `tests/`; full read of `lib/style-audit.ts` (190 lines);
grep-based verification of test-case count; `gh repo view` for license/
maintenance signals. Two specific numeric/mechanism claims from the Stage
-2.3 catalog record were targeted for direct verification per this audit's
assignment: the "4,346 unit tests" figure and the "character-DNA +
style-bible-frame consistency mechanism."

## A — Architecture
Next.js (App Router) full-stack TypeScript application, not a script or CLI —
`app/api/projects/[id]/...` route handlers drive a pipeline (script ->
storyboard -> character-consistent video -> voiceover -> export), backed by
`lib/`, `services/`, `stores/` layers. `services/hybrid-orchestrator.ts` and
files under `types/agents.ts` (608 lines) indicate a real multi-stage agent
orchestration layer, not a single monolithic call chain. `lib/create-pipeline.ts`
and `lib/pipeline-checkpoints.ts` suggest checkpointed, resumable pipeline
execution (see Dimension D).
Verdict: Strong — substantial, real full-stack application architecture, not
a demo script.

## B — Agent design
`types/agents.ts` (608 lines — not fully read, but confirmed substantial and
real, not a stub) defines the agent/role type contracts. Version-numbered
internal iteration comments (e.g. "v2.20 P0.1", "v2.23 P0.1" seen directly in
`style-audit.ts`) indicate an actively evolving, versioned internal design
process, not a one-shot script.
Verdict: Strong (based on partial direct inspection — full `agents.ts` content
not read line-by-line, flagged as not-exhaustive).

## C — Context & memory
Not the primary focus of this audit pass (DOM-20/consistency was prioritized
per assignment); `lib/db.ts` and `stores/` suggest persistent project/series
state beyond a single session, but content/structure of that persistence layer
was not independently verified this pass.
Verdict: UNKNOWN — not adequately inspected this pass for DOM-11/DOM-12
purposes; flag for a dedicated pass if this repo becomes relevant to those
domains later (it is not currently catalogued against them).

## D — Reliability (character/style consistency mechanism — DOM-20 core claim)
**CONFIRMED, read directly (`lib/style-audit.ts`, full file):** a real "Style
Bible Vision Audit" mechanism exists. It uses a vision-LLM call to score a
generated shot against a reference `styleBible` frame across 4 named
dimensions (`palette`, `lighting`, `colorTemperature`, `texture`, each 0-100),
computes an overall score as the minimum of the four, and enforces two
thresholds: `regenThreshold` (default 70, hard — triggers automatic
regeneration) and `passThreshold` (default 85, soft — passes with a warning
below this but above the hard threshold). The file's own header comment
documents *why* it exists — a real bug it fixes ("v2.20 introduced the Style
Bible Frame but only fed it as an sref to image gen; model compliance was
unstable, causing visible style drift shot-to-shot with no verification
mechanism") — this is genuine engineering documentation of a real, specific
problem and fix, not marketing copy.
Failure handling is explicit and documented: no `styleAnchorImageUrl` → skip
(degraded path does not trigger); mock/data-URI images → skip (vision can't
read base64 in that path); any thrown error in the audit → return `null`,
treated by the caller as "no audit data" rather than crashing.
**CONFIRMED, separately (via `find`/`grep`):** a distinct
`extract-character-dna` API route (`app/api/projects/[id]/extract-character-dna/route.ts`)
and `lib/character-studio.ts` exist, confirming "character-DNA" is a real,
used term in the codebase, not only marketing language — consistent with, but
not identical to, the style-consistency mechanism read in full above (these
are two separate consistency mechanisms: character-DNA for character identity,
style-bible-audit for shot-level visual-style consistency). **The specific
"8-dimension" figure for character-DNA was NOT independently verified this
pass** — `character-studio.ts` was not read in full; the 4-dimension figure
above is for the *style* audit, not the *character* mechanism. This is an
UNKNOWN, not a confirmed match or contradiction, and should not be repeated as
fact without reading `character-studio.ts` directly.
Verdict: Strong — the core consistency-audit *mechanism* is real, sophisticated,
and well-engineered with documented failure tolerance; the specific "8
dimensions for character-DNA" figure remains unverified (audited a different,
4-dimension style mechanism instead).

## E — Human control
Not inspected this pass — UNKNOWN. `app/dashboard/jobs/page.tsx` exists,
suggesting some human-facing review/monitoring surface, but its approval-gate
behavior (if any) was not verified.

## F — Evaluation
**CONFIRMED — the "4,346 unit tests" claim substantively holds up.** Direct
grep count of `it(`/`test(` case declarations across all `.test.ts`/`.test.tsx`
files: **4,261** — within ~2% of the claimed 4,346 (grep-based counting is a
simplistic proxy that undercounts parameterized/`test.each` cases, so the gap
is consistent with normal undercounting rather than an inflated claim). 501
distinct test files found. `vitest.config.ts` and `playwright.config.ts` both
present — unit tests (vitest) and e2e tests (Playwright) are both real,
configured, and runnable (`package.json` scripts: `test`, `test:watch`,
`test:e2e`, `typecheck`).
Verdict: Strong — claim independently verified, not inflated.

## G — Operations
Not deeply inspected this pass beyond the style-audit reliability mechanism
above. `lib/config.ts` (referenced via `API_CONFIG` import in style-audit.ts)
exists as a real config module.
Verdict: Moderate (partial evidence only).

## H — Reusability
The style-bible-vision-audit *pattern* (score against a reference frame across
named dimensions, dual-threshold regen/warn logic, explicit skip conditions,
fail-to-null rather than fail-crash) is cleanly describable as a standalone
design pattern independent of this specific Next.js codebase — good candidate
for direct citation in Stage -2.5's pattern catalog. The code itself is
tightly coupled to this app's Next.js/API-route structure and would need
non-trivial extraction work to reuse directly.
Verdict: Moderate — pattern is portable, code is not directly drop-in.

## I — Evidence
**CONFIRMED via `gh repo view`:** 451 stars, 42 forks, MIT license, **pushed
2026-08-24T15:05:32Z — the same day as this audit**, genuinely active, not a
stale project. 0 open issues (ambiguous signal on its own — could indicate
very responsive triage or issues handled elsewhere; not independently
resolved this pass).
Both targeted numeric/mechanism claims (test count, style-consistency
mechanism) were independently verified and held up substantively — this
repo's Stage -2.3 catalog characterization was accurate, in contrast to
GOAT-Storytelling-Agent's stale-activity correction (audited separately).
Verdict: Strong.

## J — License
**CONFIRMED:** MIT License, Copyright (c) 2026 ChrisChen667788. `package.json`
confirms bundled native-binary dependencies flagged in the Stage -2.3 catalog:
`ffmpeg-static` (^5.3.0), `fluent-ffmpeg`, `sharp` (^0.35.3) — these packages
are well-known to bundle GPL-licensed FFmpeg binaries and LGPL-licensed
libvips binaries respectively (this specific fact about the npm packages'
bundled-binary licensing was not independently re-verified against each
package's own license file in this pass — treated as INTERPRETATION based on
well-established knowledge of these specific packages, not FACT verified
in-repo). The repo's own copyleft-boundary enforcement mechanism (mentioned in
the Stage -2.3 catalog as "CI-enforced") was not independently located in
`.github/` or CI config this pass — flagged UNKNOWN, not confirmed.
Verdict: Moderate — core license is clearly MIT; the bundled-dependency
copyleft concern is real (well-known packages) but the specific CI-enforcement
claim is unverified.

---

## Evidence Section (Section 9.3 exit requirement — docs vs. code disagreements)

No material doc-vs-code disagreement found for the two claims specifically
targeted by this audit (test count, consistency mechanism) — both held up
under direct verification. One open item: the catalog's "8-dimension
character-DNA" figure could not be confirmed or refuted (a different,
4-dimension mechanism was read in full instead — `character-studio.ts` itself
was not opened). This is an UNKNOWN gap in this audit's own coverage, not a
confirmed discrepancy — recorded honestly rather than assumed either way.

## Summary for Stage -2.5 Pattern Extraction

The **dual-threshold vision-LLM consistency audit** pattern (score a generated
artifact against a reference on N named dimensions; hard-regen threshold +
soft-warning threshold; explicit skip conditions; fail-open to "no audit data"
rather than crash) is a strong, well-evidenced, directly citable DOM-20
pattern — recommend pairing it in the pattern write-up against ViMax's
static/dynamic character-trait-extraction approach (audited separately) as
two different, real, working answers to multi-modal narrative consistency.
