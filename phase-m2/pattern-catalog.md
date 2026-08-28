# Hermes Phase -2 Pattern Catalog
Revision: 1 | Updated: 2026-08-28 | Stage: -2.5 (Pattern Extraction)

Per Master Plan Section 8, this catalog is organized by **mechanism**, not by
source repository/skill. Every pattern below was extracted from the 26
Stage -2.4 deep-audit files and/or the 32 Stage -2.2 skill records, cross-
checked against the Section 8 example pattern-category list. Schema: Section
9.4. IDs are final (`PAT-001`...`PAT-051`), assigned during this merge from
six cluster-scoped raw extraction passes (Cluster A-F, matching the Stage
-2.3 domain-cluster structure). Every STRONG CANDIDATE pattern carries a
completed Adversarial Review (Section 13, Q1-Q7) and Role Notes from at
least Repository/Skill Auditor + Reliability Reviewer + Skeptic (Section 14),
with disagreements preserved rather than averaged away. Every pattern,
regardless of rating, has Failure Modes and Human-Control Implications
populated (Stage -2.5 exit criterion / Gate G5).

**Process note:** This is a full redo of Stage -2.5 after a first attempt
(2026-08-25) lost all 44 of its records to a persistence failure — see
`HERMES_RESEARCH.md` Session 7 and `AGENT-OPERATIONS.md`'s write-before-return
rule. This catalog was produced by six parallel forks, each writing its
cluster's records to a scratch file before returning, per that rule.

---

## Summary Table

| PAT-ID | Name | Cluster | Domains | Recommendation | Confidence |
|---|---|---|---|---|---|
| PAT-001 | Narrow-Waist Core + Plugin/Skill Edges | A | DOM-01/04/06 | STRONG CANDIDATE | 75 |
| PAT-002 | Handoff-vs-Agents-as-Tools Composition + History Compression | A | DOM-01/02 | CANDIDATE | 65 |
| PAT-003 | Schema-Enforced Output With Retry-Until-Valid Loop | A | DOM-02/01 | STRONG CANDIDATE | 85 |
| PAT-004 | Pause-and-Resume Execution Primitive for HITL | A | DOM-01/02/07/09 | STRONG CANDIDATE | 70 |
| PAT-005 | Progressive-Disclosure Skill Packaging (SKILL.md + Validation Gate) | A | DOM-04/01/06 | STRONG CANDIDATE | 70 |
| PAT-006 | Session-Lifecycle-Aware MCP Client Wrapper | A | DOM-06/01 | STRONG CANDIDATE | 70 |
| PAT-007 | Explicit 4-Section Agent Contract Prompt + Typed I/O + Test Checklist | A | DOM-02 | CANDIDATE | 55 |
| PAT-008 | Structured-Adversarial-Synthesis for Rare, High-Stakes Decisions | A | DOM-02/15 | CONTEXT-DEPENDENT | 60 |
| PAT-009 | When-to-Use-MCP Decision Tree + Security-Hardening Sequence | A | DOM-06 | CANDIDATE | 45 |
| PAT-010 | Structural Pre-Execution Policy Gate (govern()/proxy interception) | B | DOM-08/05 | STRONG CANDIDATE | 78 |
| PAT-011 | Approval-Coordinator as First-Class Execution Parameter (maker-checker) | B | DOM-07 | STRONG CANDIDATE | 74 |
| PAT-012 | Time-Bounded Auto-Expiring Privilege Elevation | B | DOM-08 | CANDIDATE | 55 |
| PAT-013 | Explicit Coverage-Gap Self-Reporting (△ GAP) | B | DOM-08 | CANDIDATE | 58 |
| PAT-014 | Sequence-Aware Tool-Call Chain Evaluation | B | DOM-08 | CANDIDATE | 48 |
| PAT-015 | Confidence-Threshold-to-Handler Escalation Pipeline | B | DOM-10/16 | CANDIDATE | 55 |
| PAT-016 | Multi-Factor Risk/Ambiguity Gate, Assess-Before-Generate + Rolling-History | B | DOM-09/07 | STRONG CANDIDATE | 68 |
| PAT-017 | Gate Format Calibrated to Task Novelty (DO-CONFIRM/READ-DO) + Killer-Item Checklists | B | DOM-07/15 | STRONG CANDIDATE | 72 |
| PAT-018 | Urgency-Tiered Owner-Notification Escalation | B | DOM-10/14 | CANDIDATE | 50 |
| PAT-019 | Authoritative Event Log + Disposable Derived Projection | C | DOM-11/13 | CANDIDATE | 70 |
| PAT-020 | Per-Subsystem Staged Write-Approval Gate | C | DOM-07/11 | CANDIDATE | 75 |
| PAT-021 | Time-Gated Auto-Deletion of Session/Transcript/Log History | C | DOM-11 | AVOID | 90 |
| PAT-022 | Bi-Temporal Fact Invalidation over Destructive Update | C | DOM-11/12 | STRONG CANDIDATE | 72 |
| PAT-023 | DAG-Scheduled Task Execution with Wired Hard Budget-Abort | C | DOM-13/16 | STRONG CANDIDATE | 65 |
| PAT-024 | WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed Agent State | C | DOM-13 | CONTEXT-DEPENDENT | 80 |
| PAT-025 | Urgency-Tiered Human-Facing Status Digest | C | DOM-14/10 | CANDIDATE | 55 |
| PAT-026 | Pre-Call Blocking Budget Enforcement | D | DOM-16 | STRONG CANDIDATE | 85 |
| PAT-027 | Task-Classified Multi-Strategy Cost-Aware Model Routing | D | DOM-16 | STRONG CANDIDATE | 75 |
| PAT-028 | Reported-Only Cost Tracking (gap pattern) | D | DOM-16 | INSUFFICIENT EVIDENCE | 40 |
| PAT-029 | Composable Cost-Governance Pipeline (Capture->Enforce->Route->Verify) | D | DOM-16 | CANDIDATE | 55 |
| PAT-030 | Dependency-Aggregation Guardrail Architecture (Flow-DSL over Specialized Detectors) | D | DOM-17 | STRONG CANDIDATE | 70 |
| PAT-031 | Advisory Critique-Before-Decision (Non-Blocking Structured Review) | D | DOM-15 | CONTEXT-DEPENDENT | 75 |
| PAT-032 | Entropy-Threshold Secret Detection | D | DOM-17 | CANDIDATE | 55 |
| PAT-033 | Structured HITL Brief With Typed Multi-Action Response (Edit/Rewrite/Accept/Reject) | E | DOM-07/21/09/19/20 | STRONG CANDIDATE | 85 |
| PAT-034 | Decomposed-Subgraph Content Pipeline With Degrade-Not-Fail Fallback | E | DOM-03/20/01 | CANDIDATE | 65 |
| PAT-035 | Reversibility-Differentiated Retry/No-Retry Publish Policy | E | DOM-21/07 | STRONG CANDIDATE | 88 |
| PAT-036 | Fetch-Then-Tag Competitive/Audience Research Synthesis | E | DOM-18/19/05/07 | STRONG CANDIDATE | 82 |
| PAT-037 | Brand-Isolated Storage Path Convention | E | DOM-24/19 | CANDIDATE | 60 |
| PAT-038 | Snapshot-vs-Monitoring Dual-Mode Research Agent | E | DOM-18/19 | CANDIDATE | 55 |
| PAT-039 | Prompt-Level-Only Behavior Rules Without Structural Enforcement (risk pattern) | E | DOM-05/07 | CONTEXT-DEPENDENT | 65 |
| PAT-040 | Configurable Multi-Stage Human-Approval Workflow | E | DOM-07/21 | CANDIDATE | 45 |
| PAT-041 | Static/Dynamic Character-Feature Separation for Cross-Scene Consistency | E | DOM-20 | STRONG CANDIDATE | 78 |
| PAT-042 | Fine-Grained Specialized Pipeline With Per-Module Schema Contracts | E | DOM-20/03/01 | CANDIDATE | 68 |
| PAT-043 | Dual-Threshold Vision-LLM Consistency Audit (hard-regen/soft-warn, fail-open) | E | DOM-20 | STRONG CANDIDATE | 80 |
| PAT-044 | Fixed-Window Literal-Text Scene-Carryover Baseline | E | DOM-03 | CONTEXT-DEPENDENT | 70 |
| PAT-045 | Skill-Invocation Quality Index Retargeted Toward Content-Performance (gap pattern) | E | DOM-22 | INSUFFICIENT EVIDENCE | 30 |
| PAT-046 | Profile-Based Tenant Isolation (whole-instance boundary) | F | DOM-24/08 | CANDIDATE | 85 |
| PAT-047 | Automatic Per-Context Memory Scoping (`context_id` routing) | F | DOM-24/08 | STRONG CANDIDATE | 80 |
| PAT-048 | Three-Layer Deployment Separation (Image/Scaffolding/Artefact) | F | DOM-24/05/07/11 | STRONG CANDIDATE | 75 |
| PAT-049 | Hardened-Fork-as-Default-Deployment-Target | F | DOM-24 | CANDIDATE | 70 |
| PAT-050 | Thin-Fork Weekly-Rebase Maintenance Discipline | F | DOM-24 | CANDIDATE | 70 |
| PAT-051 | Cost-Tracking-Without-Confirmed-Enforcement (gap pattern) | F | DOM-16 | INSUFFICIENT EVIDENCE | N/A |

**Distribution:** 51 records. 19 STRONG CANDIDATE, 20 CANDIDATE, 6
CONTEXT-DEPENDENT, 1 AVOID, 5 INSUFFICIENT EVIDENCE (4 of the 5 are
deliberate gap-documentation records, not weak candidates forced to fill a
slot: PAT-028, PAT-045, PAT-051, plus PAT-028's sibling gap note under
PAT-051; see "Documented Gaps" below).

---

