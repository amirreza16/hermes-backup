# Hermes Phase -2 Capability Matrix
Revision: 1 | Updated: 2026-08-29 | Stage: -2.6

Schema: Master Plan Section 8/A.4. Maps every active Hermes research need
(the domain registry in `research-domains.md`) to its best-evidenced
candidate(s) from `pattern-catalog.md` (primary source this stage), plus
`skill-catalog.md`/`repo-catalog.md` records where a pattern doesn't fully
capture the candidate. Built directly from the finished Stage -2.5 catalog —
every row cites the PAT-### record(s) it's drawn from, so full reasoning,
adversarial review, and role notes live there, not duplicated here.

**Reuse Class rules (Section 8, enforced below):** REUSE only when a
mechanism is already present and satisfactory in REPO-001 (Hermes' fixed
base architecture) as shipped, with assumptions demonstrably compatible with
Hermes at current knowledge — not merely "exists in code somewhere." ADAPT
where a real mechanism (in REPO-001, a comparison repo, or a skill) needs
non-trivial rework before it satisfies the need. REFERENCE where a
mechanism is comparison-baseline/pattern-only value, not itself an adoption
candidate (e.g., REPO-001's base architecture is already fixed, so
comparison SDKs cannot be "adopted," only referenced). REJECT for a named
anti-pattern the research found and recommends against. UNKNOWN where
evidence is insufficient to classify at all (the documented gaps).
**Adaptation Level** (NONE/LIGHT/MEDIUM/HEAVY/PATTERN_ONLY) is assigned
independently of Reuse Class — a REUSE row can still carry a LIGHT
adaptation level if enabling a shipped-but-off-by-default mechanism counts
as "using it," which this matrix treats as LIGHT ADAPT, not pure REUSE, per
the recurring "ships mechanism, defaults off" finding (see PAT-020, PAT-021,
PAT-046-048, PAT-051) — a config flip is not zero-adaptation reuse when the
Owner's principles require it to actually be turned on and verified.

---

## Matrix

| Hermes Research Need | Candidate | Type | Evidence | Reuse Class | Adaptation Level | Confidence | Notes |
|---|---|---|---|---|---|---|---|
| DOM-01 Multi-agent orchestration architecture | PAT-001 Narrow-Waist Core + Plugin/Skill Edges | Pattern | REPO-001 | REUSE | LIGHT | 75 | Inherited, not chosen — REPO-001's actual shape; LIGHT because the CLI/skill/plugin boundary is a convention Hermes must actively defend, not enforce automatically. |
| DOM-01 Multi-agent orchestration architecture | PAT-002 Handoff-vs-Agents-as-Tools Composition | Pattern | REPO-003 | REFERENCE | PATTERN_ONLY | 65 | REPO-001 has no equivalent; comparison idea only, would need building from scratch on Hermes' substrate if adopted. |
| DOM-02 Agent role & contract design | PAT-003 Schema-Enforced Output With Retry-Until-Valid Loop | Pattern | REPO-003, REPO-004, REPO-005 | ADAPT | HEAVY | 85 | Confirmed gap in REPO-001 — no schema-enforced-output abstraction exists; three independent frameworks converge on the mechanism, so the design is de-risked even though the build is real work. |
| DOM-02 Agent role & contract design | PAT-007 Explicit 4-Section Agent Contract Prompt + Typed I/O + Test Checklist | Skill | SKL-021, SKL-013, SRC-001 | REFERENCE | PATTERN_ONLY | 55 | Doc-only design methodology; pairs naturally with PAT-003's runtime enforcement rather than standing alone. |
| DOM-03 Task decomposition for narrative/chained content workflows | PAT-034 Decomposed-Subgraph Content Pipeline | Repo | REPO-039 | REFERENCE | PATTERN_ONLY | 65 | Orchestration-granularity comparison baseline; not adjudicated against Hermes' actual needs this phase (see Cross-Cluster Reconciliation, pattern-catalog.md). |
| DOM-03 Task decomposition for narrative/chained content workflows | PAT-044 Fixed-Window Literal-Text Scene-Carryover Baseline | Repo | REPO-029 | REJECT | N/A | 70 | Lower-bound baseline only; no-checkpointing and silent-failure gaps make it unsuitable as a primary mechanism. |
| DOM-04 Skill design patterns | PAT-005 Progressive-Disclosure Skill Packaging (SKILL.md + Validation Gate) | Pattern | REPO-001, SKL-009, SRC-001 | REUSE | LIGHT | 70 | REPO-001's native skill tree already matches the SKILL.md shape; LIGHT adaptation to adopt SKL-009's validation-gate/shibboleths discipline on top. |
| DOM-05 Prompt/system-instruction architecture for behavioral constraints | PAT-010 Structural Pre-Execution Policy Gate (govern()/proxy interception) | Repo | REPO-010, REPO-012 | ADAPT | MEDIUM | 78 | Moves enforcement out of the prompt into code — a real, non-trivial build on Hermes' tool-call surface, not a REPO-001-native feature. |
| DOM-05 Prompt/system-instruction architecture for behavioral constraints | PAT-039 Prompt-Level-Only Behavior Rules Without Structural Enforcement | Repo | REPO-033 | REJECT | N/A | 65 | Named risk pattern — good writing style, insufficient alone for anything safety-critical; pairs with PAT-010 as the fix. |
| DOM-06 Tool-use & MCP integration patterns | PAT-006 Session-Lifecycle-Aware MCP Client Wrapper | Repo | REPO-005 | REFERENCE | PATTERN_ONLY | 70 | Comparison baseline for REPO-001's own `optional-mcps/` depth, which was not independently traced this phase. |
| DOM-06 Tool-use & MCP integration patterns | PAT-009 When-to-Use-MCP Decision Tree + Security-Hardening Sequence | Skill | SKL-024, SRC-001 | REFERENCE | PATTERN_ONLY | 45 | Doc-only design checklist; language/stack assumptions may not match REPO-001's own MCP implementation. |
| DOM-07 Human-in-the-loop approval gates for irreversible actions | PAT-020 Per-Subsystem Staged Write-Approval Gate | Pattern | REPO-001 | ADAPT | LIGHT | 75 | Real, ships in REPO-001 but off by default — LIGHT adaptation to enable + verify, not zero-cost reuse, per the matrix's stated Adaptation Level rule. |
| DOM-07 Human-in-the-loop approval gates for irreversible actions | PAT-011 Approval-Coordinator as First-Class Execution Parameter | Repo | REPO-010, REPO-011 | ADAPT | MEDIUM | 74 | Concept (action blocks structurally on an external approval object) is sound; REPO-001 lacks an equivalent pause/resume primitive, so this is real build work, not a port. |
| DOM-07 Human-in-the-loop approval gates for irreversible actions | PAT-033 Structured HITL Brief With Typed Multi-Action Response | Repo | REPO-039 | REFERENCE | PATTERN_ONLY | 85 | Best-evidenced brief/action-taxonomy design in the whole catalog, but LangGraph-interrupt-specific mechanics don't port — reusable as design, not code. |
| DOM-08 Permissions & least-privilege scoping | PAT-010 Structural Pre-Execution Policy Gate | Repo | REPO-010, REPO-012 | ADAPT | MEDIUM | 78 | Same mechanism as DOM-05's row; primary DOM-08 relevance (least-privilege enforcement) is the leading use case. |
| DOM-08 Permissions & least-privilege scoping | PAT-047 Automatic Per-Context Memory Scoping (`context_id` routing) | Repo | REPO-040, REPO-001 (PR #47552) | ADAPT | MEDIUM | 80 | Real, tested fix; not yet merged upstream — adopting today means depending on the `cyborg-garden` fork or reimplementing independently. |
| DOM-09 Ambiguity detection & clarification-seeking behavior | PAT-016 Multi-Factor Risk/Ambiguity Gate, Assess-Before-Generate | Skill | SKL-012, SKL-027, SKL-028, SRC-001 | ADAPT | MEDIUM | 68 | Best-evidenced DOM-09 finding (3 independently-original sources converge); the ambiguity-signal detection itself is Hermes-specific work this pattern doesn't solve. |
| DOM-10 Progressive autonomy / trust calibration over time | PAT-015 Confidence-Threshold-to-Handler Escalation Pipeline | Repo | REPO-013 | REFERENCE | PATTERN_ONLY | 55 | Single-source, zero external adoption signal; measures model-confidence, not task-ambiguity — a different DOM-09-adjacent concern. |
| DOM-10 Progressive autonomy / trust calibration over time | PAT-018 Urgency-Tiered Owner-Notification Escalation | Skill | SKL-019, SRC-001 | REFERENCE | PATTERN_ONLY | 50 | Real tiering scheme; needs full retargeting from software-dev to content/social-ops context. |
| DOM-11 Append-only memory & audit-log architecture | (none — documented gap) | — | PAT-019, PAT-021, PAT-022 | UNKNOWN | — | — | No off-the-shelf solution found across all of Phase -2. PAT-021 (AVOID) names the failure mode to guard against; PAT-019/PAT-022 are partial, adjacent mechanisms informing a Hermes-specific design, not a candidate to adopt. |
| DOM-12 Context engineering for long-running, narratively-continuous agents | PAT-022 Bi-Temporal Fact Invalidation over Destructive Update | Repo | REPO-017 | REFERENCE | PATTERN_ONLY | 72 | Graph-database dependency is real infrastructure; the bi-temporal schema idea is the transferable part, not the library. |
| DOM-13 Long-running agent reliability & failure recovery | PAT-024 WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed Agent State | Pattern | REPO-001 | REUSE | NONE | 80 | Already present in REPO-001's `hermes_state.py`, grounded in a named real production incident — genuinely inherited for free if the state layer is retained as-is. |
| DOM-13 Long-running agent reliability & failure recovery | PAT-023 DAG-Scheduled Task Execution with Wired Hard Budget-Abort | Repo | REPO-016, REPO-001 | REFERENCE | PATTERN_ONLY | 65 | Comparison baseline for REPO-001's own cron subsystem, whose full crash-recovery contract (`docs/chronos-managed-cron-contract.md`) was not read this phase. |
| DOM-14 Observability for autonomous-agent trust | PAT-025 Urgency-Tiered Human-Facing Status Digest | Skill | SKL-019, SKL-023, SRC-001 | REFERENCE | PATTERN_ONLY | 55 | Concrete shape (urgency tiers, weighted quality index) but neither source is deep-audited code; real retargeting work either way. |
| DOM-15 Agent evaluation & pre-publish quality gating | PAT-017 Gate Format Calibrated to Task Novelty (DO-CONFIRM/READ-DO) | Skill | SKL-030, SKL-012, SRC-001 | ADAPT | LIGHT | 72 | Strongest-evidenced skill-catalog source in the whole project (externally-documented real-world outcomes); team-coordination details need solo-owner reinterpretation. |
| DOM-15 Agent evaluation & pre-publish quality gating | PAT-031 Advisory Critique-Before-Decision (Non-Blocking Structured Review) | Repo | REPO-026 | REFERENCE | PATTERN_ONLY | 75 | Explicitly not an enforcement mechanism — the review-step half of a DOM-07/DOM-15 pipeline, must pair with a real gate (PAT-011/PAT-016/PAT-017). |
| DOM-16 Cost control & model-routing governance | PAT-026 Pre-Call Blocking Budget Enforcement | Repo | REPO-022, SKL-015, SKL-025, SRC-001 | ADAPT | HEAVY | 85 | Strongest DOM-16 mechanism found; REPO-001's own billing subsystem enforcement status is UNKNOWN (PAT-028), so this is likely necessary new build, not a REPO-001 upgrade. |
| DOM-16 Cost control & model-routing governance | PAT-027 Task-Classified Multi-Strategy Cost-Aware Model Routing | Repo | REPO-022, SKL-016, SRC-001 | ADAPT | MEDIUM | 75 | No equivalent task-difficulty-based routing confirmed in REPO-001; CLI commands found are manual presets, not automatic tiering. |
| DOM-16 Cost control & model-routing governance | PAT-028 Reported-Only Cost Tracking (gap) | Pattern | REPO-001 | UNKNOWN | — | 40 | Central open question: does REPO-001's billing subsystem actually cap spend or only report it? `docs/billing-lifecycle.md` unread; independently corroborated as the same open question by PAT-051 (REPO-041). |
| DOM-17 Security & governance patterns for multi-account social automation | PAT-030 Dependency-Aggregation Guardrail Architecture | Repo | REPO-024 | REFERENCE | PATTERN_ONLY | 70 | Real, well-engineered, but 28+ third-party integration surface is likely disproportionate for Hermes' current solo-owner scale (Skeptic objection preserved in pattern-catalog.md). |
| DOM-17 Security & governance patterns for multi-account social automation | PAT-032 Entropy-Threshold Secret Detection | Skill | SKL-017, SRC-001 | ADAPT | LIGHT | 55 | Concrete, cheap technique for the credential half of DOM-17; single-source, not independently corroborated. Cluster B's flagged agentward dependency-scanner remains unresolved (see pattern-catalog.md Cross-Cluster Reconciliation item 1). |
| DOM-18 Competitive & audience research automation | PAT-036 Fetch-Then-Tag Competitive/Audience Research Synthesis | Repo | REPO-033 | ADAPT | MEDIUM | 82 | Best-evidenced DOM-18 finding this phase — real scraping infra + tiered agent contract; social-platform scraping targets would need substantial rework from this repo's general-marketing-page scraping. |
| DOM-19 Content strategy, planning & brand consistency | PAT-036 Fetch-Then-Tag Competitive/Audience Research Synthesis | Repo | REPO-033 | ADAPT | MEDIUM | 82 | Same source as DOM-18; secondary relevance here is the snapshot/monitoring dual-mode design (PAT-038). |
| DOM-19 Content strategy, planning & brand consistency | PAT-037 Brand-Isolated Storage Path Convention | Repo | REPO-033 | ADAPT | LIGHT | 60 | Simple, structural, low-effort; weaker-enforced than REPO-001's own profile-routing (PAT-046) — a real lightweight-vs-heavyweight tradeoff for Stage -2.7 to note, not resolve. |
| DOM-20 Multi-modal content generation (text/image/video, narrative continuity) | PAT-041 Static/Dynamic Character-Feature Separation | Repo | REPO-030 | ADAPT | MEDIUM | 78 | Conditional on Hermes actually needing visual generation (raw idea says "probably video," not confirmed) — schema/parser plumbing is framework-specific, the prompt-design idea is not. |
| DOM-20 Multi-modal content generation (text/image/video, narrative continuity) | PAT-043 Dual-Threshold Vision-LLM Consistency Audit | Repo | REPO-031 | ADAPT | MEDIUM | 80 | Complementary to PAT-041 (verifies after generation vs. consistency-by-construction); threshold values need Hermes-specific calibration. |
| DOM-21 Publishing workflow operations | PAT-035 Reversibility-Differentiated Retry/No-Retry Publish Policy | Repo | REPO-036, REPO-037 | ADAPT | MEDIUM | 88 | Strongest convergent-evidence finding in the entire social-media-operations domain — two unrelated implementations independently reach the same design. Both source repos are AGPL-3.0: pattern is freely reusable, code is not. |
| DOM-22 Analytics & experimentation feedback loops | (none — documented gap) | — | PAT-045 | UNKNOWN | — | — | Zero inspectable implementation anywhere in this research's 26 deep-audited repos or 32 skill records. PAT-045 is the closest comparison (skill-usage analytics, not content-performance analytics) — a retargeting exercise, not adaptation. |
| DOM-23 Community management / audience engagement automation | BLOCKED — not researched | — | OQ-01 | — | — | — | Left BLOCKED per Owner instruction at the Stage -2.1 checkpoint; OQ-01 remains open in `open-questions.md`. No candidates sought this phase. |
| DOM-24 Multi-tenant / multi-instance onboarding patterns | PAT-046 Profile-Based Tenant Isolation | Pattern | REPO-001 | ADAPT | LIGHT | 85 | REPO-001-native, mainline, but off by default and heavyweight per-boundary — satisfies whole-page isolation, not fine-grained (thread/DM) isolation. |
| DOM-24 Multi-tenant / multi-instance onboarding patterns | PAT-047 Automatic Per-Context Memory Scoping | Repo | REPO-040, REPO-001 (PR #47552) | ADAPT | MEDIUM | 80 | Closer structural analog to the raw idea's "add a page without a from-scratch project" goal; real dependency on an unmerged upstream PR or an external fork. |
| DOM-24 Multi-tenant / multi-instance onboarding patterns | PAT-048 Three-Layer Deployment Separation (Image/Scaffolding/Artefact) | Repo | REPO-041 | REFERENCE | PATTERN_ONLY | 75 | Sound structural answer to "ships mechanism, defaults off," but commits to container-per-agent deployment — real architectural weight for a private single-operator system (OD-001); Skeptic recommends architecture-reference only at current scale. |
| DOM-25 Self-updating ecosystem-intelligence agent design | (none — documented gap) | — | — | UNKNOWN | — | — | Zero mechanism found anywhere in this research resembling autonomous external-technology-scouting with recommendation synthesis. `hermes curator`/`hermes journey` CLI commands are surface-level analogs, not inspected beyond a reference-table entry. Notable: this phase's own research process may be the closest existing model. |

---

## Gate G6 Self-Check (Stage -2.6 Exit Criteria, Master Plan Section 17)

- [x] **Every domain from Section 7 has >=1 row OR a documented no-candidate
  finding.** 24 active domains (excluding DOM-23, BLOCKED) all have >=1 row;
  DOM-11, DOM-22, and DOM-25 have explicit UNKNOWN/no-candidate rows rather
  than a forced weak REUSE/ADAPT entry. DOM-23 has its own BLOCKED row
  pointing to OQ-01 rather than being silently omitted from the table.
- [x] **No REUSE without demonstrably compatible assumptions.** Only 3 rows
  use REUSE (PAT-001, PAT-005, PAT-024) — all three are mechanisms
  confirmed present and functioning in REPO-001 as shipped, with no
  off-by-default caveat attached (contrast PAT-020/PAT-046/PAT-047, which
  are real REPO-001/fork mechanisms but marked ADAPT specifically because
  they ship disabled or externally-dependent, per this file's stated
  Adaptation Level rule).
- [x] **Every row cites record IDs.** All rows cite at least one PAT-/REPO-/
  SKL- ID; SRC-001 is additionally cited wherever the underlying source
  traces to the SomeClaudeSkills gallery (Stage -2.2's registered research
  input).
- [x] **Adaptation levels assigned explicitly, not left blank.** All non-gap
  rows specify NONE/LIGHT/MEDIUM/HEAVY/PATTERN_ONLY per the Reuse Class
  each row carries.

**Stage -2.6 exit criteria met.**

---

## What This Matrix Deliberately Does Not Do

Per Section 5.1 (no premature architecture) and P7 (no premature
architecture), this matrix does not select a final Hermes design — it maps
research needs to evidenced candidates for Phase -1 to weigh. Where two
candidates address the same need at different weights (e.g. DOM-24's PAT-046
vs. PAT-047; DOM-19's PAT-037 vs. Cluster F's heavier profile-routing), both
are listed with their tradeoffs stated, not collapsed into one recommended
choice. That collapsing, if it happens at all, belongs to Phase -1's
Hermes-specific fit/adaptation analysis, not to this phase's ecosystem
intelligence.
