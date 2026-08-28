# Hermes Capability Intelligence — Phase -2 Capstone Report
Revision: 1 | Date: 2026-08-29 | Phase: HERMES -2 / Ecosystem Intelligence & Reuse Discovery

---

## 1. Executive Summary

This phase set out to answer one question: for every major capability
Hermes may require, what proven approaches already exist, what evidence
supports them, what assumptions they carry, how much they overlap, and
where genuinely new Hermes-specific design will be required. Across seven
stages — scope formation, skill discovery, repository discovery, deep
audit, pattern extraction, capability mapping, and synthesis — this phase
inspected 32 Claude Skills, 50 repositories (25 of them deep-audited via
actual cloned source/test/doc reading, never README alone), and 31
independent non-repository sources, and extracted 51 reusable patterns
covering 23 of 25 research domains with direct evidence (the 24th, DOM-23,
remains an Owner-instructed BLOCKED exclusion; the 25th's status is
detailed below).

The single most consequential finding is not any one pattern but a
recurring structural theme confirmed independently across five separate
mechanisms in REPO-001 (`NousResearch/hermes-agent`, Hermes' Owner-disclosed
fixed base architecture) and its derivatives — though, corrected here
2026-08-29 (see `HERMES_RESEARCH.md`), these five split into three
genuinely distinct cases, not one uniform "off by default" bucket. Three
are real, working protective mechanisms that sit inert until an operator
explicitly enables and verifies them: write-approval gating (irreversible-
action confirmation) and two tenant/profile-isolation mechanisms. A fourth,
the session/transcript auto-prune guard, is the opposite case — it is a
real, permanent-deletion mechanism, and its being off by default is the
*correct, currently-protective* state for the never-delete principle; it
must be structurally locked off, never enabled alongside the other three.
A fifth, cost-enforcement (spanning REPO-001's billing subsystem and
REPO-041's budget-check), is not confirmed to be off at all — no
enforcement call site was found in either direction within this phase's
search depth, and two specific sources needed to resolve it were never
read. This means Hermes cannot inherit safety from REPO-001's defaults
uncritically for any of its three named behavioral principles
(irreversible-action confirmation, cost control, never-delete) — but the
corrective action differs by case: deliberately enable-and-verify the
protective three, structurally lock the destructive one off, and
investigate the unconfirmed one before making any enable/disable claim
about it. Full three-way breakdown: `HERMES-REUSE-STACK.md`'s
Synthesis-Level Skeptic Pass, item 1.

Three genuine, exhaustively-searched-and-not-found gaps remain: DOM-11
(append-only memory/audit-log architecture), DOM-22 (analytics/
experimentation feedback loops), and DOM-25 (self-updating ecosystem-
intelligence agent design). None of these were papered over with a forced
weak candidate — each is documented as an open Hermes-specific design
question for Phase -1, consistent with Section P2/P5 discipline throughout
this phase.

No architecture, framework, or version structure has been locked. This
report and its companion decision file (`HERMES-REUSE-STACK.md`) hand Phase
-1 evidence, not a specification.

---

## 2. Research Scope

Phase -2 operated under a fixed, Owner-disclosed constraint not present in
a typical greenfield ecosystem scan: Hermes will be built on
`NousResearch/hermes-agent` (REPO-001), disclosed at the Stage -2.1 Owner
Checkpoint. Per Master Plan Section 2.3, this does not permit Phase -2 to
select or lock any *further* architecture — it means seven of the 25
research domains (DOM-01, 02, 04, 06, 11, 13, 16, 24) were explicitly
reframed from "what's the best pattern in the world" to "how does
hermes-agent implement this, does it satisfy Hermes' needs, what's the
gap" — outside evidence became a comparison baseline for those domains, not
a green-field search. The remaining domains retained the original
open-discovery framing. Full domain definitions, the Stage -2.1 seed
reconciliation log, and the Known Base Architecture disclosure live in
`research-domains.md`.

One domain, DOM-23 (community/audience-engagement automation), was left
BLOCKED at the Owner's explicit instruction at the Stage -2.1 checkpoint
(OQ-01, `open-questions.md`) and was not researched this phase.

---

## 3. Methodology

Seven stages per Master Plan Section 8: Scope Formation (-2.1, with a
mandatory blocking Owner Checkpoint) → Skill Discovery (-2.2) → Repository
Discovery (-2.3) → Deep Repository Audit (-2.4) → Pattern Extraction (-2.5)
→ Capability Matrix (-2.6) → Synthesis (-2.7, this report). Deep audits read
actual source/test/doc/config, not README summaries; every claim traceable
to a repo or skill carries FACT/INTERPRETATION/UNKNOWN labeling at the
record level. Every candidate proposed as a STRONG recommendation underwent
Section 13's seven-question adversarial review and Section 14's minimum
three-role independent review (Repository/Skill Auditor, Reliability
Reviewer, Skeptic), with disagreements preserved rather than averaged away
— visible throughout `pattern-catalog.md`.

**A methodology note that is itself part of this phase's record:** the
first attempt at Stage -2.5 (2026-08-24/25) lost all 44 of its pattern
records to a persistence failure — six parallel sub-agents returned their
findings only as chat summaries and never wrote them to disk, and ~1.95M
tokens were spent producing output that was never recovered. This produced
a new standing rule (`AGENT-OPERATIONS.md`, write-before-return, mandatory
for all sub-agents phase-independent) under which Stage -2.5 was redone in
full on 2026-08-28, successfully, with every fork's output verified on
disk before being trusted. Full incident record: `HERMES_RESEARCH.md`
Session 7; fix: `AGENT-OPERATIONS.md`.

---

## 4. Sources Investigated

- **32 Claude Skills** from the SomeClaudeSkills gallery (181-skill gallery
  triaged to 32 inspected beyond title/description), `skill-catalog.md`.
- **50 repositories** considered (REPO-001 known + REPO-002 through
  REPO-050 discovered), 25 deep-audited via actual clone-and-read,
  `repo-catalog.md` and `repo-audits/`.
- **31 non-repository sources** (official docs, GitHub issues/PRs,
  discussions) registered where claims materially informed a decision or
  were cited across multiple records, `source-register.md`.
- **8 formally rejected candidates** with reversal conditions preserved,
  `rejected-candidates.md`.
- **6 Owner decisions** (OD-001 through OD-006) governing scope boundaries
  this research operated inside (private single-user system, memory
  architecture, agent-to-agent access deferral, control-review cadence,
  suggest-only posture, update/rollback discipline), `decisions/`.

---

## 5. Research Domains

25 domains across 6 clusters (Core Agent Architecture; Human Control,
Safety & Trust; State, Memory & Reliability; Security & Governance;
Social-Media Operations; Scaling & Self-Maintenance) — see
`research-domains.md` for full per-domain definitions, search strategy, and
the Revision 2 reframing log. 24 active; DOM-23 BLOCKED per Owner
instruction (OQ-01).

---

## 6. Skill Landscape

32 skills inspected beyond title/description: 24 ADAPT, 6 REFERENCE, 2
REJECT, 0 REUSE (expected at Stage -2.2 — all evidence was single-source
documentation, not code-verified, so nothing cleared the direct-adoption
bar at that stage). 5 skills reached Strong-Candidate status with
completed adversarial review: SKL-012 (Human Gate Designer), SKL-021
(Skillful Subagent Creator), SKL-027/SKL-028 (Crisis Detection/Response,
reviewed jointly), SKL-030 (Checklist Discipline — the best-evidenced
single source in the entire skill pass, grounded in independently-
verifiable real-world outcomes rather than vendor claims). Full records:
`skill-catalog.md`.

---

## 7. Repository Landscape

49 discovered candidates (REPO-002 through REPO-050) plus the disclosed
base architecture (REPO-001): 24 DEEP AUDIT, 19 REFERENCE ONLY, 6 REJECT
from the discovery triage; all 25 DEEP AUDIT repos (24 discovered +
REPO-001) received full A-J dimension audits. Four factual corrections
were made during deep audit that the initial triage got wrong (ALwrity's
license, LiteLLM's dual-license structure, an org rename with a GHCR
staleness deployment trap on REPO-040, and DOM-18's coverage-gap status
changing from open to resolved) — see `repo-catalog.md`'s in-place
corrections and `repo-audits/` for full A-J records.

**The REPO-001/040/041 story**, fully verified end-to-end via direct
`git clone` + `gh api`, not taken on any discovering fork's summary alone:
REPO-001 (upstream) has tenant isolation, but it is config-heavy and the
lighter automatic fix is an open, unmerged PR (#47552). REPO-040
(`cyborg-garden/hermes-agent-mt`, an org renamed from NimbleCoAI — the old
GHCR images are frozen/stale, a real deployment trap) is that exact fix,
tested and running in production. REPO-041 (`hermes-swarm-map`) is a
fleet-orchestration control plane that deploys REPO-040, not plain
REPO-001, **by default** — verified directly in Docker config and test
assertions, not assumed from a README.

---

## 8. High-Value Patterns

51 pattern records, `pattern-catalog.md`: 21 STRONG CANDIDATE, 21
CANDIDATE, 5 CONTEXT-DEPENDENT, 1 AVOID, 3 INSUFFICIENT EVIDENCE (the
latter 3 are deliberate gap-documentation, not weak candidates forced to
fill a slot). Every STRONG CANDIDATE carries completed Section 13
adversarial review and Section 14 three-role review with disagreements
preserved. The single clearest actionable finding: DOM-02's exact research
question ("does hermes-agent enforce or merely suggest a structured-output
contract?") now has a direct, confirmed answer — no, REPO-001 has no such
mechanism — while three independently-built comparison frameworks
(pydantic-ai, adk-python, openai-agents-python) converge on the same
well-evidenced solution (PAT-003).

---

## 9. Architecture Pattern Comparison

REPO-001's actual shape is a narrow-waist core with three sanctioned
extension surfaces — CLI+skill, service-gated tool, or plugin (PAT-001) —
a real, code-verified philosophy, not just an `AGENTS.md` claim, though
enforced by convention, not tooling. Four independently-built general-
purpose orchestration SDKs (langgraph, openai-agents-python, pydantic-ai,
adk-python) were deep-audited purely as comparison baselines against this
fixed shape, per the DOM-01/02/06 reframing — none is an adoption
candidate in its own right (`deduplication-map.md` Cluster 6). Three
distinct orchestration-granularity philosophies were found in the content-
generation domain (PAT-001's narrow-waist minimalism, PAT-034's 7-subgraph
decomposition, PAT-042's 13-module fine-grained decomposition) with no
single cluster's evidence positioned to rank them against Hermes' actual
needs — flagged explicitly for Phase -1 triangulation, not resolved here.

---

## 10. Agent Design Pattern Comparison

The clearest, best-evidenced finding in this whole research effort:
schema-enforced output with a retry-until-valid loop (PAT-003), converged
on independently by three separately-built frameworks, directly answering
DOM-02's research question with a confirmed gap in REPO-001. Complementary
composition and contract patterns (PAT-002 handoff-vs-agent-as-tool,
PAT-007 design-time contract authoring) remain REFERENCE-level — real,
well-specified, but single-sourced or without a REPO-001 equivalent.

---

## 11. Memory Pattern Comparison

REPO-001's own memory-safety posture is the recurring cross-cutting
finding of this entire phase: `write_approval.py` (staged write gating,
PAT-020) and `maybe_auto_prune_and_vacuum` (hard deletion, PAT-021) both
ship real and both ship off by default. Two independent code-verified
instances of the exact deletion failure mode DOM-11 exists to guard
against (REPO-001's own auto-prune, cronicle's independently-built log
rotation) were found — DOM-11 itself remains a genuine, exhaustively-
searched-and-unfilled gap; no off-the-shelf append-only/audit-log solution
exists anywhere in this research's discovery set. Graphiti's bi-temporal
fact-invalidation (PAT-022) is the best available adjacent mechanism —
non-destructive by design intent, but the same library ships a
first-class public `remove_episode()` delete API, so it is REFERENCE, not
a compliance guarantee, without an integration-side fence.

---

## 12. Human-Control Pattern Comparison

The best-evidenced convergent finding for DOM-09 (ambiguity handling):
three independently-original source domains — a generic DAG-workflow
gate-design skill, a mental-health crisis-intervention skill pair, and (a
third corroboration found during Cluster E's social-media-agent audit) a
real code implementation — all independently arrive at "assess with more
than the single triggering input, before acting, non-binary response"
(PAT-016). For DOM-07 (approval gates), the maker-checker approval-
coordinator pattern (PAT-011) is the most concretely-tested mechanism
found, though its clearest verified implementation (humanlayer) is itself
a deprecated project — the mechanism is sound, the codebase is not
adoptable as-is. Three independently-built governance-policy frameworks
(agent-governance-toolkit, humanlayer, agentward) converge on structural
pre-execution policy interception (PAT-010) as the answer to "prompt rules
alone aren't reliable enough" — corroborated a second time by an
independent, unrelated finding in the social-media-operations domain
(PAT-039, digital-marketing-pro's prompt-only Behavior Rules, a named risk
pattern for exactly this gap).

---

## 13. Evaluation Pattern Comparison

DOM-15's clearest finding is a *distinction*, not a mechanism: pr-agent's
review step was initially triaged as an enforcement gate but direct code
reading found the gate exists in source and is dead code on the live
path — it posts advisory comments, it does not block (PAT-031). This
"surface critique" half must be explicitly paired with a real gate
(PAT-011/PAT-016/PAT-017) to satisfy Hermes' stated irreversible-action
principle; conflating the two would be a real, load-bearing error. SKL-030
(Checklist Discipline, PAT-017) remains the single best-evidenced source in
the entire skill-catalog pass — grounded in independently-verifiable
real-world outcomes (WHO Safe Surgery Checklist, Boeing 299, Pronovost's
central-line protocol), not vendor claims.

---

## 14. Reliability Pattern Comparison

REPO-001's SQLite crash-safety discipline (PAT-024, `PRAGMA
wal_checkpoint(PASSIVE)`, replacing a `TRUNCATE` strategy that caused real
production B-tree corruption) is a genuine, inherited-for-free REUSE
finding — the one clean example in this research of a reliability
mechanism that is neither off-by-default nor comparison-only. Its cron
subsystem's budget-abort path (PAT-023, cross-checked against cronicle's
independently-verified `BudgetUSD` enforcement) is well-evidenced but its
full crash-recovery *contract* remains unread. Cost-tracking-without-
confirmed-enforcement (PAT-028, PAT-051) was independently found twice, in
two structurally unrelated repos (REPO-001, REPO-041) — the strongest
single reason Phase -1 should not assume REPO-001's billing subsystem
already caps spend.

---

## 15. Social-Media-Specific Findings

The single strongest convergent-evidence finding in the entire social-
media-operations domain: reversibility-differentiated retry/no-retry
publish policy (PAT-035) — two structurally unrelated implementations
(postiz-app's Temporal-based workflow engine, brightbean-studio's simpler
Django/DB-flag design) independently arrive at the identical design
(irreversible publish mutations get effectively zero retries, treated as
"outcome unknown" on timeout). Both source repos are AGPL-3.0 — the
pattern is freely reusable, direct code is not. digital-marketing-pro's
fetch-then-tag competitive-research pipeline (PAT-036) resolved what had
been an open Stage -2.3 coverage gap on DOM-18 with real, code-verified,
non-trivial synthesis (its own test suite exceeded its catalog claim, a
rare positive-direction evidence correction). DOM-22 (analytics/
experimentation feedback loops) remains a fully open gap — zero
inspectable implementation found anywhere in this research's 26
deep-audited repos or 32 skill records.

---

## 16. Capability Matrix (Summary View)

24 active domains (excluding BLOCKED DOM-23) each map to >=1 candidate row
or an explicit documented no-candidate finding — full need-by-need table in
`capability-matrix.md`. 3 rows use REUSE (all confirmed present and
functioning in REPO-001 as shipped, no off-by-default caveat); the majority
use ADAPT or REFERENCE; DOM-11/DOM-22/DOM-25 use UNKNOWN with named
required follow-up evidence rather than a forced weak entry.

---

## 17. Deduplication Findings

Skill-level (Stage -2.2, `deduplication-map.md` Clusters 1-5): one genuine
redundancy resolved (4 near-identical skill-authoring-methodology skills,
canonical SKL-009). Two clusters explicitly NOT collapsed to one canonical
because members are complementary pipeline stages, not competing
implementations (cost-governance; crisis detect+respond).

Repo-level (Clusters 6-9, run this stage to close a Section 11.1
trigger-(b) gap that had gone unaddressed since Stage -2.4 completed):
general-purpose orchestration SDKs (4 repos, all kept independent as
comparison baselines — no canonical needed since none is an adoption
candidate against the already-fixed REPO-001 base); narrative/multi-modal
content-generation pipelines (ViMax canonical on evidence depth, wind-comic
and GOAT-Storytelling-Agent as secondary references at different points on
a maturity spectrum); social-media publish-mechanics platforms (postiz-app
and brightbean-studio kept co-primary — offsetting evidence strengths, not
forced to one pick); human-control governance frameworks (3 repos, again no
canonical since none is adoptable as-is). One considered-but-rejected
cluster (digital-marketing-pro vs. ALwrity) logged for transparency.

---

## 18. Strong Candidates

21 patterns rated STRONG CANDIDATE, full list with adversarial review and
role notes in `pattern-catalog.md`. Highlights: PAT-003 (schema-enforced
output, 3-source convergence, confirmed REPO-001 gap), PAT-016 (multi-
factor ambiguity gate, 3-source convergence including a third independent
corroboration), PAT-035 (reversibility-differentiated publish retry,
2-source convergence, this phase's strongest social-media-operations
finding), PAT-017 (checklist discipline, externally-verifiable real-world
grounding — the single best-evidenced skill-catalog source in the project).

---

## 19. Pattern-Only Candidates

14 patterns rated REFERENCE / PATTERN_ONLY in the capability matrix — real,
well-evidenced mechanisms not directly portable as adoption candidates,
either because REPO-001's own comparable depth was not independently
traced (PAT-006), because the source project itself is non-viable
(PAT-011's humanlayer half), or because adopting the pattern's full weight
would commit Hermes to an architectural posture disproportionate to its
current private, single-operator scale (PAT-030's 28-integration guardrail
breadth, PAT-048's container-per-agent deployment commitment). Full list in
`HERMES-REUSE-STACK.md`'s REFERENCE section.

---

## 20. Rejected Candidates

8 formally rejected candidates at the skill/repo level (`rejected-
candidates.md`), plus 3 pattern-level REJECT entries in the reuse stack:
PAT-021 (time-gated auto-deletion — the clearest direct conflict with
Hermes' never-delete principle found anywhere in this research), PAT-039
(prompt-level-only behavior rules as a sole safeguard — a named risk
pattern, not a blanket rejection of the writing style), PAT-044 (naive
scene-carryover — useful only as a documented lower bound).

---

## 21. Knowledge Gaps

Three genuine, exhaustively-searched gaps, none papered over:

- **DOM-11** (append-only memory/audit-log architecture): no off-the-shelf
  solution anywhere in this research; two independent negative examples
  (REPO-001, cronicle) sharpen the failure mode to avoid without
  constituting a solution.
- **DOM-22** (analytics & experimentation feedback loops): zero
  inspectable implementation found across 26 deep-audited repos and 32
  skill records.
- **DOM-25** (self-updating ecosystem-intelligence agent design): zero
  mechanism found; this phase's own research process may be the closest
  existing model, since no external precedent exists. REPO-001's `hermes
  curator`/`hermes journey` CLI commands were noted but never inspected
  beyond a reference-table entry — a real remaining follow-up before
  concluding this is a true external gap.

Additionally, 6 cross-cluster flags raised during Stage -2.5 pattern
extraction were never independently resolved by the cluster they were
routed to (full list: `pattern-catalog.md`'s Cross-Cluster Reconciliation
section) — genuine open items, not oversights papered over.

---

## 22. Risks

**[Corrected 2026-08-29 — see `HERMES_RESEARCH.md`; the prior version of
this section applied one uniform "turn it on" framing across all five
findings below, which incorrectly included the auto-prune guard.]**

The dominant cross-cutting risk, confirmed independently across five
findings that split into three distinct cases: REPO-001 and its
derivatives repeatedly ship the *mechanism* for a safety/isolation property
Hermes needs, but the correct response differs by case. (1) Write-approval
gating and profile/context-scoped tenant isolation are real, working
mechanisms that default off and need to be deliberately enabled and
verified — Hermes cannot assume these protect anything on a stock
deployment. (2) The session/transcript auto-prune guard is the opposite:
it is a real, permanent-deletion mechanism whose default-off state is
*correct and currently protective* for the never-delete principle — it
must be structurally locked off (config lock, patched out, or replaced
with a non-destructive alternative), never enabled alongside case (1). (3)
Cost enforcement (REPO-001's billing subsystem, REPO-041's budget-check)
has an unconfirmed status in either direction — no enforcement call site
was found, but two specific sources that could resolve this
(`docs/billing-lifecycle.md`, REPO-041's dashboard code) were never fully
read this phase. Hermes cannot rely on REPO-001's defaults uncritically —
it needs one deliberate, audited configuration pass at Phase -1's outset
that enables-and-verifies case (1), confirms case (2) stays locked off, and
resolves case (3) before assuming either direction, rather than treating
all five as one uniform "turn it on" action. Full breakdown:
`HERMES-REUSE-STACK.md`'s Synthesis-Level Skeptic Pass, item 1.
Secondary risks: AGPL-3.0 exposure clusters around the two social-media
publish-mechanics repos if code-level (not pattern-level) reuse is ever
considered; an unmerged upstream PR (#47552) and an external fork
(`cyborg-garden`) that Hermes does not control are the practical
availability path for the strongest DOM-24 mechanism found.

---

## 23. Confidence Assessment

Confidence is highest (80-90) where multiple independent, code-verified
sources converge on the same mechanism against a Hermes-specific research
question (PAT-003, PAT-021, PAT-035) or where a single deep-audited source
provides unusually rich, multi-file, tested evidence (PAT-024, PAT-047).
Confidence is lowest (30-45) for the three deliberate gap-documentation
records and for single-source, doc-only skill patterns with no code
verification (PAT-009, PAT-045). No STRONG CANDIDATE rests on a single
low-confidence source without an explicit, preserved Skeptic objection on
record.

---

## 24. Phase -1 Inputs

Per Master Plan Section 19.3, Phase -1 owns which of the above fits,
what adapts or is rejected, and the best evidence-based specification
path — nothing in this report constrains that choice beyond the Build
Readiness North Star. The single most actionable early input: resolve the
"ships mechanism, defaults off" cross-cutting risk (Section 22 above) with
one deliberate configuration decision before any other adaptation work
begins, since every REUSE/ADAPT entry touching REPO-001 depends on it.
Full structured handoff contract: `downstream-handoff.md`.
