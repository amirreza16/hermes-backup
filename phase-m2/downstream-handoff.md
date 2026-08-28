# Phase -2 Downstream Handoff
Exit Status: M2-CONDITIONALLY-COMPLETE
Date: 2026-08-29 (updated 2026-08-29 — OQ-01 resolved post-phase-end; see
`HERMES_RESEARCH.md` 2026-08-29 entry for the dated correction record)

## Exit Gate Determination (Master Plan Section 18)

All of X1-X7 hold (verified below); X8-X10 also hold cleanly. Status
remains CONDITIONALLY-COMPLETE rather than COMPLETE, but the reason has
narrowed since this file was first written: OQ-01 (DOM-23's scope) is now
**resolved** — the Owner confirmed DOM-23 is explicitly out of scope, not
merely left undecided — so it no longer contributes to the
CONDITIONALLY-COMPLETE determination. The remaining reason is unchanged:
DOM-11, DOM-22, and DOM-25 have no positive candidate, only documented
gaps, which are real material unknowns that do not block Phase -1's
fit/adaptation analysis from starting on everything else. Per Section
18.2's decision rule, X1-X7 holding with real-but-non-blocking unknowns
remaining is exactly what CONDITIONALLY-COMPLETE is for — it is simply a
narrower set of unknowns now than at initial phase-end.

| # | Condition | Status | Verification |
|---|---|---|---|
| X1 | Coverage | HOLDS | 24/24 active domains have >=1 candidate or a documented reason none was found (`capability-matrix.md`); DOM-23 is a 25th, deliberately excluded domain, not counted against this condition |
| X2 | Evidence | HOLDS | Every strong recommendation cites record IDs; 21/21 STRONG CANDIDATE patterns traceable to source (`pattern-catalog.md`) |
| X3 | Deep review | HOLDS | 25 repos deep-audited via actual clone-and-read across dimensions A-J (`repo-audits/`) |
| X4 | Deduplication | HOLDS | 9 clusters (5 skill-level, 4 repo-level) map major overlap (`deduplication-map.md`) |
| X5 | Pattern extraction | HOLDS | 51 pattern records, not a source list (`pattern-catalog.md`) |
| X6 | Negative review | HOLDS | Section 13/14 completed per STRONG CANDIDATE + a synthesis-level Skeptic pass across the whole reuse stack (`HERMES-REUSE-STACK.md`) |
| X7 | Gaps documented | HOLDS | DOM-11/22/25 explicit no-candidate findings, still open; OQ-01/DOM-23 now RESOLVED as an explicit scope exclusion, not merely preserved-as-open (`open-questions.md`) |
| X8 | No premature architecture | HOLDS | Self-audit against Section 2.3: no architecture/framework/version chosen by this phase; REPO-001 was Owner-disclosed, not phase-selected |
| X9 | No implementation | HOLDS | Zero Hermes source code exists (confirmed, `AGENT-OPERATIONS.md` Active Rule 4 status note) |
| X10 | Execution boundary respected | HOLDS | No Owner-Claude operational rule (e.g. write-before-return) was promoted to an Owner-Hermes requirement |

---

## 1. Evidence Summary

32 Claude Skills, 50 repositories (25 deep-audited), 31 non-repository
sources, across 24 active research domains (DOM-23 BLOCKED). Full detail:
`skill-catalog.md`, `repo-catalog.md`, `repo-audits/`, `source-register.md`.
Capstone narrative: `HERMES-CAPABILITY-INTELLIGENCE-M2.md`.

## 2. Extracted Patterns

51 records in `pattern-catalog.md` (PAT-001 through PAT-051): 21 STRONG
CANDIDATE, 21 CANDIDATE, 5 CONTEXT-DEPENDENT, 1 AVOID, 3 INSUFFICIENT
EVIDENCE. Every record separates the reusable mechanism from its original
project/domain assumptions per Section P2. Gate G5 self-check included in
the file.

## 3. Candidate Knowledge

Full need-by-need mapping in `capability-matrix.md` (24 domains x
candidates); concise decision-oriented rollup in `HERMES-REUSE-STACK.md`
(REUSE/ADAPT/REFERENCE/REJECT/UNKNOWN buckets). Every entry cites record
IDs per Section 16.3's rules.

## 4. Candidate Assumptions Register

**[Corrected 2026-08-29 — see `HERMES_RESEARCH.md`; the prior version of
this entry treated PAT-021 as a mechanism needing to be "enabled and
verified" alongside PAT-020/PAT-046/PAT-047, which is backwards — PAT-021
is destructive, and its default-off state is the one currently protecting
Hermes' never-delete principle. A same-day second correction split
PAT-047 out of the PAT-020/PAT-046 bullet below: PAT-047 is not shipped
in REPO-001 at all, so "will actually enable and verify them" does not
describe what it needs.]**

The recurring, load-bearing assumption across the majority of ADAPT
entries touching REPO-001 splits into four distinct cases, not one
uniform posture:
- **PAT-020 (write-approval), PAT-046 (profile-based tenant isolation):**
  real protective mechanisms, native to REPO-001 mainline, that ship off
  by default and protect nothing on a stock, unconfigured deployment —
  the assumption here is that whoever configures Hermes will actually
  enable and verify them.
- **PAT-021 (REJECT — auto-prune guard):** the inverse assumption applies —
  this is a real, permanent-deletion mechanism whose off-by-default state
  is what currently keeps a stock deployment compliant with the never-delete
  principle. The load-bearing assumption to guard against is the opposite
  one: that this stays off, structurally, not that it gets turned on.
- **PAT-047 (context-scoped tenant isolation):** not the same assumption
  as PAT-046 despite covering the same DOM-24 need — this mechanism is
  not merged into REPO-001 mainline at all, only into an external fork,
  behind an open upstream PR. The assumption to avoid here is treating it
  as an existing-but-disabled REPO-001 feature; the real open question is
  whether Phase -1 waits for the PR, depends on the fork, or reimplements
  the fix.
- **PAT-028/PAT-051 (cost enforcement):** neither "off" nor "on" is
  confirmed — no enforcement call site was found in either REPO-001's
  billing subsystem or REPO-041's budget-check within this phase's search
  depth. The assumption to avoid here is treating the presence of
  cost-tracking code as evidence that spend is actually capped.

Secondary assumptions are recorded per-pattern in `pattern-catalog.md`'s
Required Conditions and Adversarial Review Q1 fields.

## 5. Conflicts & Overlap

`deduplication-map.md`: 5 skill-level clusters (Stage -2.2) + 4 repo-level
clusters (Clusters 6-9, run this stage to close a previously-unaddressed
Section 11.1 trigger-(b) gap). No candidate appears as both canonical and
rejected without an explanatory entry. Real, preserved-not-resolved
conflicts: PAT-046 (heavyweight, native) vs. PAT-047 (lightweight, external
fork dependency) as competing DOM-24 answers; PAT-035's postiz-app
(architecturally richer, zero test coverage) vs. brightbean-studio
(simpler, test-covered) as offsetting-strength co-primary sources.

## 6. Rejected Alternatives

8 formal skill/repo-level rejections (`rejected-candidates.md`, each with
reversal conditions) + 3 pattern-level REJECT entries
(`HERMES-REUSE-STACK.md`): PAT-021 (auto-deletion, direct never-delete
conflict), PAT-039 (prompt-only enforcement as sole safeguard), PAT-044
(naive scene-carryover baseline).

## 7. Confidence Assessment

See `HERMES-CAPABILITY-INTELLIGENCE-M2.md` Section 23. Highest confidence
(80-90) where multiple independent code-verified sources converge on a
Hermes-specific research question; lowest (30-45) for deliberate
gap-documentation records and single-source doc-only skill patterns.

## 8. Open Questions

**Blocking:** none remain. OQ-01 / DOM-23 (is community/audience-engagement
automation in Hermes' remit at all?) — raised Stage -2.1, was the only
blocking item — is now **resolved** (2026-08-29): the Owner confirmed
DOM-23 is explicitly out of scope, no comment-or-DM-reply functionality
exists in the current system design, and this was never part of the
intended scope. This is a closed, deliberate scope boundary for Phase -1,
not an open question — see `open-questions.md` and
`research-domains.md`'s Revision 3 for the full resolution record.

**Non-blocking (Phase -1 can proceed on everything else while these
remain open):**
- DOM-11 (append-only memory/audit-log): no candidate found, genuine
  Hermes-specific design gap.
- DOM-22 (analytics feedback loops): no candidate found, not exhaustively
  re-searched this phase beyond the standard discovery passes.
- DOM-25 (self-updating ecosystem-intelligence agent): no external
  candidate found; REPO-001's `hermes curator`/`hermes journey` CLI
  commands were noted but never inspected beyond a reference-table entry —
  worth a dedicated read before concluding this is a true external gap.
- 6 unresolved cross-cluster flags from Stage -2.5 (full list:
  `pattern-catalog.md` Cross-Cluster Reconciliation section) — e.g.
  agentward's pre-deployment dependency scanner never independently
  verified against DOM-17; a three-way orchestration-granularity
  comparison (PAT-001 vs. PAT-034 vs. PAT-042) no cluster's evidence
  adjudicates.
- DOM-16 enforcement: whether REPO-001's own billing subsystem
  (`docs/billing-lifecycle.md`, unread) actually caps spend or only
  reports it (PAT-028/PAT-051).

## 9. Hermes Implications (Not Decisions)

**[Corrected 2026-08-29 — see `HERMES_RESEARCH.md`; the prior version of
this sentence applied one uniform "not safe to trust as a default"
framing across all three behavioral principles, which misstated the
never-delete case the same way the reuse-stack/capstone/Section-4
passages did before their correction.]**

The dominant implication, not a decision: Hermes' fixed base architecture
ships real mechanisms touching all three of its named behavioral
principles, but the trustworthiness of each one's *default* state differs
by case, not uniformly untrustworthy. For irreversible-action confirmation
and cost control, the shipped mechanisms are off by default and genuinely
not safe to trust as-is — Phase -1's specification work should treat
"verify and enable the safety configuration profile" as an early, explicit
step for these two, not an assumed-inherited property. For never-delete,
the opposite is true: the shipped mechanism (the auto-prune guard) being
off *is* currently the trustworthy, protective default for that
principle specifically — the early step there is confirming it stays
locked off, not enabling it. Treating all three principles' defaults as
equally untrustworthy would risk exactly the wrong action (enabling
auto-prune) for the one case where the default is already correct. A
second implication: the strongest available fix for fine-grained multi-tenant
memory isolation (PAT-047) currently depends on an external, unmerged
upstream PR and an external org's fork — Phase -1 should weigh whether to
wait, depend on the fork, or reimplement independently, as a real,
non-deferrable early decision if DOM-24 is prioritized.

## 10. Adaptation Candidates for Phase -1

Every entry in `HERMES-REUSE-STACK.md`'s ADAPT section is a candidate for
deeper Phase -1 fit analysis; the 3 REUSE entries (PAT-001, PAT-005,
PAT-024) are the lowest-friction starting points since they require no
adaptation beyond active defense of an existing convention. The single
highest-leverage early adaptation candidate, per the cross-cutting risk
named in Section 22 of the capstone report: a unified, audited
configuration profile that enables and verifies every off-by-default
REPO-001 safety mechanism at once (PAT-020, PAT-046), paired with a
separate, deliberate dependency decision for PAT-047 — wait for the
upstream PR to merge, depend on the fork, or reimplement independently —
since it has no REPO-001 switch to flip and a configuration pass cannot
resolve it, before other adaptation work begins.

---

## Files Transferred (Section 19.1)

```
phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md
HERMES-REUSE-STACK.md
phase-m2/pattern-catalog.md
phase-m2/capability-matrix.md
phase-m2/deduplication-map.md
phase-m2/source-register.md
phase-m2/rejected-candidates.md
phase-m2/open-questions.md
phase-m2/downstream-handoff.md
```

## Receiver Rules for Phase -1 (Section 19.3)

Phase -1 MUST NOT assume any Phase -2 recommendation is automatically
appropriate. Phase -1 owns: which knowledge fits; what adapts/rejects;
remaining gaps; and the best evidence-based specification path (possibly
V1/V2 maturity stages, multi-document structures, or alternatives). Phase
-2 does not constrain that choice beyond the Build Readiness North Star
(Section 2.4).
