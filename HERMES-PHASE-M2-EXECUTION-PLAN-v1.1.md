# HERMES — PHASE -2 EXECUTION MASTER PLAN
## Ecosystem Intelligence & Reuse Discovery — Complete Operational Plan

**Document ID:** HERMES-M2-PLAN
**Based on:** HERMES-PHASE-M2-SPEC-R1.3 plus final Owner review corrections
**Plan Revision:** FINAL-1.0 — Evidence-Driven Research Seeds
**Status:** Execution Plan — Ready for Deployment
**Execution Environment:** Claude Code on Owner VPS
**Implementation Status:** PROHIBITED during entire phase
**Downstream Consumer:** Phase -1 (Fit, Adaptation & Specification-Path Determination)

---

## Table of Contents

1. Mission Statement
2. Program Context & Pipeline
3. Objectives & Non-Objectives
4. Governing Principles
5. Governance & Execution Boundary
6. Environment Setup & Workspace Bootstrap
7. Research Domain Map
8. Master Workflow — Stage-by-Stage Execution
9. Record Schemas & Templates
10. Scoring Framework — Calibrated Rubric
11. Deduplication Protocol
12. Source Quality & Evidence Hierarchy
13. Negative Research Protocol
14. Role Simulation Protocol
15. Named Source Campaigns
16. Deliverables Specification
17. Quality Assurance Gates
18. Exit Gate & Decision Logic
19. Handoff Package to Phase -1
20. Work Breakdown, Sequencing & Effort Model
21. Metrics & Progress Tracking
22. Risk Register & Mitigations
23. Failure & Contingency Playbook
24. Reporting Cadence
25. CLAUDE.md Guardrail File Content
26. Definition of Success
27. Appendix A — Copy-Paste Templates
28. Appendix B — Checklists
29. Appendix C — Traceability Matrix (Plan ↔ Spec)

---

# 1. Mission Statement

> **Before designing Hermes, build — with evidence and provenance — a sufficiently broad, high-quality research base across the areas that may matter to Hermes, then convert the strongest findings into a small, deduplicated, high-signal reuse map that makes Phase -1 possible. Continue discovery while it produces meaningful new signal; do not pursue artificial completeness.**

Phase -2 is **not** product design. Phase -2 is **not** implementation. Claude Code operates strictly as a **research, comparative-analysis, and architecture-intelligence system**.

Success is measured by signal density and evidential integrity — never by volume of findings.

---

# 2. Program Context & Pipeline

## 2.1 Where This Phase Sits

```text
Raw Hermes Idea
      |
      v
>> PHASE -2 <<   (THIS PHASE — Ecosystem Intelligence & Reuse Discovery)
      |
      v
Phase -1 — Fit, Adaptation & Specification-Path Determination
      |
      v
Specification Maturation (structure determined from evidence)
      |
      v
Implementation-Ready Hermes Master Specification
      |
      v
Independent Build-Readiness Review (fresh coding-agent context)
      |
      v
STOP
```

## 2.2 What Hermes Is (Current Knowledge)

An **unresolved agentic product/system concept**, expected to eventually manage a social-media page with high autonomy. Nothing more is fixed at this point.

## 2.3 What Is Deliberately Undecided (Do NOT Decide Now)

| Forbidden Premature Decisions |
|---|
| Which exact skills / agents to use |
| Single-agent vs multi-agent |
| Orchestration pattern |
| Memory architecture |
| Framework selection |
| Model provider selection |
| Social-platform API selection |
| Automation topology |
| Base architecture repo |
| Final document hierarchy or version boundaries (V1/V2 semantics) |

## 2.4 The North Star — Build Readiness

The final Hermes master specification must let a competent coding agent in a fresh context, reading only the spec plus referenced artifacts, determine: intent, rationale, required behavior, prohibited behavior, boundaries, interactions, fixed vs configurable decisions, constraints, failure handling, human-authority requirements, and verification methods — minimizing unresolved intent, hidden assumptions, contradictions, guesswork, ambiguity, and rework-from-misunderstanding.

Phase -2 must preserve knowledge in a form that makes this downstream fresh-context build-readiness test possible.

---

# 3. Objectives & Non-Objectives

## 3.1 Primary Objectives

| # | Objective | Measured By |
|---|---|---|
| O1 | Map the ecosystem of reusable intelligence relevant to Hermes' candidate needs | Coverage of the current approved research-domain registry, with documented saturation or gaps |
| O2 | Extract generalizable patterns separated from original domains | `pattern-catalog.md` entries with provenance |
| O3 | Produce calibrated candidate classifications | Skill/repo catalogs + capability matrix with scores & confidence |
| O4 | Surface conflicts, overlaps, and redundancy | `deduplication-map.md` |
| O5 | Preserve negative results and rejection reasoning | `rejected-candidates.md` |
| O6 | Maintain full source provenance | `source-register.md`, per-record URLs/dates |
| O7 | Document gaps, unknowns, risks honestly | `open-questions.md`, final report |
| O8 | Enable evidence-based Phase -1 fit analysis without constraining architecture choice | `HERMES-REUSE-STACK.md` + handoff contract |

## 3.2 Explicit Non-Objectives

- Building the largest possible list of repositories or skills.
- Selecting any Hermes architecture, framework, agent model, or versioning scheme.
- Implementing anything.
- Converting any finding into a Hermes requirement.
- Designing future Owner–Hermes governance.

---

# 4. Governing Principles

## P1 — Need Before Solution

Reasoning direction is always:

```text
Hermes Need -> Required Capability -> Evidence -> Candidate Pattern/Knowledge -> Validated Hermes Decision
```

Never: "Interesting Existing Tool" -> "Force Hermes To Use It".

## P2 — Extract Patterns, Not Products

Transformation chain for ALL research:

```text
Sources -> Skills/Repos/Templates/Frameworks -> Internal Mechanisms
        -> Generalizable Patterns -> Hermes Relevance -> REUSE / ADAPT / REFERENCE / REJECT
```

Hermes must not become a collage of unrelated repositories. Output = **pattern library with provenance**.

## P3 — Traceability

Every important downstream decision must eventually be traceable:

```text
Need -> Evidence/Reasoning -> Selected Pattern -> Specification Decision -> Verification Method
```

If a major decision cannot be traced to a real need, an explicit constraint, strong evidence, or a justified design decision — challenge it.

## P4 — Handoff Boundary

A Phase -2 recommendation is NOT a Hermes requirement. A discovered pattern is NOT a Hermes architecture decision. A popular framework is NOT the implementation framework. All findings are **inputs to Phase -1 only**.

## P5 — Epistemic Honesty

Every recommendation distinguishes:

- **FACT** — directly supported by source material;
- **INTERPRETATION** — Claude's analysis of the evidence;
- **HYPOTHESIS** — may apply to Hermes, unvalidated;
- **UNKNOWN** — Phase -2 cannot resolve.

## P6 — Separation of Builder and Product

`Owner <-> Claude Code` (research executor) is NOT the same relationship as `Owner <-> Hermes` (future product). No Phase -2 Owner–Claude rule may silently become an Owner–Hermes requirement.

## P7 — No Premature Architecture

Research stays architecture-neutral end-to-end.

## P8 — Research Seeds Are Not Requirements

Owner-provided topics, examples, candidate skills, categories, search terms, and known sources are **starting leads only**.

Claude MUST be free to:

- challenge them;
- merge overlapping areas;
- remove weak or irrelevant areas;
- add newly discovered areas;
- replace weak sources with stronger ones;
- stop following a seed when evidence shows low value.

Research must optimize for **new evidence and useful signal**, not checklist completion.

A seed becomes part of the active research scope only when Claude can justify its relevance.

---

# 5. Governance & Execution Boundary

## 5.1 Hard Guardrail — NO IMPLEMENTATION

During Phase -2 Claude Code MUST NOT:

- Write production code; scaffold Hermes; create Hermes agents or skills
- Create application services; select a production framework
- Lock an architecture; generate implementation tickets
- Create deployment infrastructure; optimize for shipping
- Infer missing requirements as facts

Allowed activities: research, browsing, repo/skill inspection, architecture comparison, pattern extraction, evidence collection, classification, scoring, gap identification, recommendation-with-uncertainty, documentation. Implementation code found in sources may be **studied as evidence**, never copied into Hermes.

## 5.2 Autonomy Baseline (unless Owner overrides)

### Claude MAY act independently for

- Reading/searching files inside the designated research workspace
- Creating/updating Phase -2 research documents
- Inspecting authorized repos/websites
- Cloning/fetching research repos into designated locations
- Using authorized research tools (including Apify; repository-host access only when separately authorized)
- Non-destructive analysis; organizing outputs; maintaining provenance notes

### Claude MUST return to Owner before

- Destructive or irreversible filesystem actions
- Modifying unrelated apps/services/repos on the VPS
- Changing VPS security/networking/auth/system config
- Exposing/copying/transmitting/repurposing credentials or secrets
- Publishing/pushing externally unless explicitly pre-authorized
- Major research-scope changes materially altering Phase -2's objective
- Treating an unresolved high-impact assumption as a Hermes fact
- Any action with materially unclear operational risk

### Claude MUST NEVER

- Use research access as license to implement Hermes
- Modify production systems unrelated to the workspace
- Disclose secrets discovered in files/env vars
- Infer broader authorization from tool/credential access
- Treat Owner silence as approval for high-impact action

> **Principle:** Autonomy for reversible research work; escalation for material side effects, authority changes, secrets, destructive actions, or high-impact ambiguity.

## 5.3 Escalation Procedure (Operational Detail)

When an escalation trigger occurs:

1. **HALT** the triggering line of work (other independent research may continue).
2. Record in `open-questions.md` under `ESCALATIONS` with date, trigger, options considered.
3. Compose a concise escalation note to Owner: what / why / options / recommendation / cost of delay.
4. Proceed only on explicit Owner response. Silence does NOT equal approval.

## 5.4 Secret & Credential Handling

- Never echo secret contents into research artifacts, logs, or reports.
- If secrets are discovered incidentally: note existence only ("credential material present"), report to Owner.
- Research tool credentials are used only for their granted research purpose.

---

# 6. Environment Setup & Workspace Bootstrap

## 6.1 Workspace Structure (create before Stage -2.1)

**Canonical workspace root (VPS, absolute path):** `/root/m2-research-workspace`

This is the one place this path is stated explicitly. Everywhere else in this document,
the workspace is referred to relatively (as shown in the tree below, rooted at `.`) or as
"the workspace" / "repository root" — both mean `/root/m2-research-workspace`.

```text
.                                       <- /root/m2-research-workspace
|
+-- CLAUDE.md                        <- guardrail file (see Section 25)
+-- HERMES_RESEARCH.md               <- living research journal/index
|
+-- source/
|   +-- raw-hermes-idea.md           <- verbatim original concept (input, do not edit)
|
+-- phase-m2/
|   +-- research-domains.md          <- Stage -2.1 output
|   +-- skill-catalog.md             <- Stage -2.2 output
|   +-- repo-catalog.md              <- Stage -2.3 output
|   +-- source-register.md           <- continuously maintained
|   +-- pattern-catalog.md           <- Stage -2.5 output
|   +-- capability-matrix.md         <- Stage -2.6 output
|   +-- deduplication-map.md         <- continuous
|   +-- rejected-candidates.md       <- continuous
|   +-- open-questions.md            <- continuous
|   +-- downstream-handoff.md        <- final assembly
|   +-- repo-audits/
|   |   +-- <repo-name>.md           <- one per deep-audited repo
|   +-- HERMES-CAPABILITY-INTELLIGENCE-M2.md   <- capstone report
|
+-- decisions/
|   +-- ...                          <- decision records (phase-local)
|
+-- HERMES-REUSE-STACK.md            <- single decision-oriented summary
```

## 6.2 Bootstrap Procedure

1. Create the directory tree above on the VPS.
2. Place `CLAUDE.md` guardrail at repository root (full text in Section 25).
3. Import `source/raw-hermes-idea.md` verbatim.
4. Initialize `HERMES_RESEARCH.md` journal with phase start date.
5. Verify tool authorization status for Apify and any optional repository-host access. Tool availability is infrastructure context, not research evidence.
6. Confirm git initialized locally (research-only commits allowed; NO external push without explicit authorization).

## 6.3 Tool Authorization Matrix

| Tool | Authorized Use | Prohibited Use |
|---|---|---|
| Apify | Crawling, search extraction, gallery inspection, doc extraction | Any run against unauthorized targets |
| Repository-host access (if authorized) | Discover, clone/fetch, and inspect public research candidates | Pushing/modifying upstream repos or treating platform popularity as evidence |
| Filesystem | Workspace read/write, research clones | Anything outside designated locations |
| Web browsing | Source verification, docs reading | Account creation, form submission, purchases |

---
# 7. Research Seed Map & Approved Domain Registry

## 7.1 Initial Research Seeds — Non-Binding Starting Hypotheses

The following topics are **suggestions to help Claude start thinking**, not a fixed scope, quota, taxonomy, or checklist.

Claude MUST NOT optimize for preserving this list.

Claude may:

- merge topics that represent the same underlying problem;
- delete topics that prove irrelevant;
- split topics that are too broad;
- add topics discovered through evidence;
- rename topics to reflect better understanding;
- change prioritization as research progresses.

Initial seed areas:

### Product & Requirements
- Product discovery
- Product requirements

### Agent Architecture & Design
- Agent architecture
- Single-agent vs multi-agent decisioning
- Agent orchestration
- Task decomposition
- Agent role design
- Skill design
- Prompt/system-instruction architecture
- Tool-use architecture
- MCP/integration patterns
- Human-in-the-loop
- Permissions & least privilege
- Agent contracts
- Structured outputs

### State, Memory & Reliability
- Memory architecture
- Context engineering
- Knowledge management
- Long-running agents
- Failure recovery
- Observability
- Agent evaluation
- Cost control
- Model routing

### Security & Governance
- Security and governance patterns

### Social-Media Operations
- Social-media automation
- Content research
- Audience research
- Content strategy
- Content planning
- Content generation
- Content review
- Publishing workflows
- Community management
- Analytics
- Experimentation
- Brand consistency

### Process & Specification Engineering
- Decision history
- Spec-driven development
- Architecture documentation

These seeds are intentionally broad. The **Approved Domain Registry** produced by Claude after initial review is the authoritative research scope for the current point in time.

## 7.2 Approved Domain Definition Template

Every domain that Claude accepts into the active registry must have:

```text
Domain ID / Name:
Research Question:
Why Hermes May Need It:
Evidence Needed:
Likely Source Types:
Search Strategy:
Exclusion Criteria:
Priority:
Status: COVERED-CANDIDATE | COVERED-NO-CANDIDATE | IN-PROGRESS | BLOCKED | DROPPED
Rationale for Inclusion / Change:
```

There is **no required number of domains**.

## 7.3 Domain Change Control

Claude may add, merge, split, rename, reprioritize, or drop domains as evidence changes.

Every material change requires:

- short justification;
- date;
- affected record IDs;
- whether the change came from evidence, redundancy, irrelevance, or a newly discovered need.

The active registry — not the original seed list — is the source of truth.

---

# 8. Master Workflow — Stage-by-Stage Execution

Seven stages. Stages -2.1 through -2.4 are discovery-heavy; -2.5 through -2.7 are synthesis-heavy. Iteration between stages is expected and healthy; each loop must update affected downstream artifacts.

## Stage -2.1 — Research Scope Formation

**Entry criteria:** workspace bootstrapped; raw idea imported.

**Procedure:**
1. Review the Section 7 research seeds as hypotheses, not requirements.
2. Challenge each seed for relevance, overlap, and expected information value.
3. Merge, remove, split, rename, or add domains as justified.
4. Create the first **Approved Domain Registry** using Section 7.2.
5. Define practical search strategies and exclusion criteria for each approved domain.
6. Prioritize domains by expected impact on the downstream Hermes specification.

**Exit criteria:** the active domain registry is coherent, justified, and sufficient to begin discovery. No fixed domain count is required.

**Quality check:** every active domain has a distinct answerable research question and a reason for inclusion.

**Owner Checkpoint (mandatory, blocking):** Before proceeding to Stage -2.2, Claude presents the Approved Domain Registry to the Owner for explicit review: what was kept from the seed list, what was merged/dropped/added, and why. Discovery work (Stage -2.2 onward) does not begin until the Owner responds. This is the one point in Phase -2 where scope itself — not just findings — is confirmed before resource-intensive discovery starts, since a wrong scope here is expensive to correct later. Silence does not equal approval (per Section 5.3).

## Stage -2.2 — Skill Discovery

**Procedure:**
1. Use Some Claude Skills (Section 15.1) as a named starting source.
2. Treat any listed skill names as **research seeds only**; Claude may ignore, replace, or expand them.
3. Inspect promising skills beyond their short descriptions where source content is available.
4. Register inspected skills using the Skill Record schema (Section 9.1).
5. Score and classify only after inspecting the actual mechanism or method.
6. Mine unrelated-domain skills when they contain reusable patterns.
7. Add other credible sources discovered during research only after registering their provenance.

**Rules:**
- Do NOT rate a skill highly because its title sounds relevant.
- Do NOT complete a seed list for the sake of completion.
- Unrelated-domain skills remain eligible when a generalizable mechanism separates cleanly.
- Stop expanding a search direction when alternate queries produce little meaningful new signal.

**Exit criteria:** the skill landscape has enough high-signal evidence to support pattern extraction, and an alternate discovery sweep produces diminishing new value. No fixed skill count is required.

## Stage -2.3 — Open Repository / Project Discovery

**Procedure:**
1. Discover relevant public projects and repositories through authorized research channels.
2. Do **not** begin from a mandatory repo list and do not assume any named repository is relevant.
3. Use broad category ideas only as search seeds when useful, such as agent systems, orchestration, memory, evaluation, human approval, specification tooling, social-media automation, or long-running agents.
4. Triage materially relevant discovered candidates using the schema in Section 9.2.
5. Decisions remain: DEEP AUDIT / REFERENCE ONLY / REJECT.
6. Popularity is a signal, never proof.
7. Record why a candidate was investigated and what evidence justified deeper inspection.

**Exit criteria:** materially relevant discovered candidates have been triaged, major approved domains have adequate source coverage or documented gaps, and an alternate discovery pass yields diminishing new signal.

## Stage -2.4 — Deep Repository Audit

**Scope:** ONLY shortlisted (DEEP AUDIT) repositories.
**Procedure:** For each repo, work through audit dimensions A-J (Section 9.3), reading actual code/config/tests/docs — never README alone. Produce one file per repo in `phase-m2/repo-audits/<repo-name>.md`.
**Minimum inspection depth per audited repo:** repo structure; architecture docs if any; SKILL.md / CLAUDE.md / agent definitions; prompts/configs/schemas/workflows; examples; tests; license; recent commit activity; issue tone/maintenance signals.

**Exit criteria:** every DEEP AUDIT repo has a completed A-J audit file with an Evidence section that states where docs disagree with code (if anywhere).

## Stage -2.5 — Pattern Extraction (MOST IMPORTANT TRANSFORMATION)

**Procedure:**
1. Stop organizing knowledge by repository. Re-read all audits/catalogs and extract reusable mechanisms.
2. For each pattern: complete the Pattern Record schema (Section 9.4), citing multiple sources ("Observed In") wherever possible.
3. Cross-check against example pattern categories: hierarchical orchestration; router+specialists; single agent+skills; evaluator-optimizer loop; maker-checker; parallel expert review; DAG execution; structured handoff contracts; human approval gates; confidence-based escalation; persistent decision journal; working-memory scratchpad; knowledge-graph memory; file-based state; checkpointed long-running execution; schema-enforced outputs; cost-aware model routing; tool allowlisting; least-privilege permissions.
4. Rate recommendation: STRONG CANDIDATE / CANDIDATE / CONTEXT-DEPENDENT / AVOID / INSUFFICIENT EVIDENCE.
5. Publish `pattern-catalog.md`.

**Exit criteria:** every STRONG CANDIDATE pattern cites >=2 independent sources OR one deep-audited source with high confidence; every pattern has failure modes and human-control implications stated.

## Stage -2.6 — Capability Matrix

**Procedure:**
1. Build matrix rows mapping: Hermes Research Need | Candidate | Type | Evidence | Reuse Class | Adaptation Level | Confidence | Notes.
2. Enforce rules: REUSE only when assumptions are demonstrably compatible with Hermes at current knowledge; adaptation levels NONE/LIGHT/MEDIUM/HEAVY/PATTERN_ONLY assigned explicitly.
3. Every row must cite record IDs (SKL-/REPO-/PAT-) and source IDs (SRC-).
4. Publish `capability-matrix.md`.

**Exit criteria:** every domain from Section 7 has >=1 row OR a documented no-candidate finding.

## Stage -2.7 — Evidence & Decision Synthesis

**Procedure:**
1. Sweep ALL outputs; label claims FACT / INTERPRETATION / HYPOTHESIS / UNKNOWN.
2. Resolve internal contradictions between artifacts (or log as open questions).
3. Run final negative-research pass (Section 13) over all strong recommendations.
4. Assemble capstone report + reuse stack (Section 16).
5. Run Exit Gate (Section 18).

---

# 9. Record Schemas & Templates

All templates below are canonical; copy-paste versions in Appendix A.

## 9.1 Skill Record Schema (Stage -2.2)

```text
Skill ID: SKL-###
Name:
Source:                    <- e.g., SomeClaudeSkills
Repository:
URL:                       <- exact URL
License:
Last Verified:             <- ISO date

Original Purpose:
Original Domain:

Core Method:
Primary Workflow:
Inputs:
Outputs:
Dependencies:
Activation Conditions:

Generalizable Components:
Project-Specific Assumptions:
Domain-Specific Assumptions:

Hermes Research Domains Covered:   <- DOM IDs

Overlap With:              <- SKL IDs
Potential Conflicts:

Evidence Quality:          <- Low/Medium/High + basis
Maintenance Signal:
Documentation Quality:

Reuse Classification:      <- REUSE / ADAPT / REFERENCE / REJECT / UNKNOWN
Confidence:                <- 0-100
Score:                     <- 0-100 per Section 10
Reasoning Summary:
```

## 9.2 Repository Triage Schema (Stage -2.3)

```text
Repo:                     <- owner/name
URL:
Category:                 <- one of ~20 families
Stars:
Forks:
Recent Activity:
License:
Primary Language:
Maturity:                 <- experimental / active / mature / archived
Claimed Purpose:
Potential Hermes Relevance:
Triage Decision:          <- DEEP AUDIT / REFERENCE ONLY / REJECT
Decision Rationale:
Date Triaged:
```

## 9.3 Deep Audit Dimensions A–J (Stage -2.4)

| Dim | Area | Questions |
|---|---|---|
| A | Architecture | Explicit architecture? Single vs multi-agent? Orchestration model? State management? Boundaries? |
| B | Agent design | Roles defined? Mandates? Tool access? Decision authority? Contracts? Escalation? |
| C | Context & memory | Working memory? Persistent? User? Decision memory? Retrieval? Compaction? |
| D | Reliability | Retries? Fallback? Checkpointing? Structured outputs? Schema validation? Crash recovery? |
| E | Human control | Approval gates? Permission boundaries? Audit history? Reversible actions? |
| F | Evaluation | Eval framework? Acceptance criteria? Quality metrics? Regression testing? Business-level evals? |
| G | Operations | Logging? Tracing? Cost tracking? Model routing? Rate-limit handling? |
| H | Reusability | Framework coupling? Domain coupling? Modularity? Extraction difficulty? |
| I | Evidence | Docs agree with code? Examples real? Tests support claims? Recent commits indicate maintenance? |
| J | License | Can concepts be studied? Can files be reused? Restrictions? |

Each dimension ends with a verdict line: `Verdict: <Strong/Moderate/Weak/Absent> — <one-line basis>`.

## 9.4 Pattern Record Schema (Stage -2.5)

```text
Pattern ID: PAT-###
Pattern Name:
Problem Solved:
Observed In:              <- SRC/SKL/REPO IDs (aim >= 2)
Mechanism:
Required Conditions:
Strengths:
Weaknesses:
Failure Modes:
Complexity:               <- Low/Medium/High
Token/Cost Implications:
Human-Control Implications:
Hermes Relevance:         <- DOM IDs + why
Alternative Patterns:     <- PAT IDs
Recommendation:           <- STRONG CANDIDATE / CANDIDATE / CONTEXT-DEPENDENT / AVOID / INSUFFICIENT EVIDENCE
Confidence:               <- 0-100
Evidence:
```

## 9.5 Deduplication Schema

```text
Capability:
Candidates:               <- SKL/REPO/PAT IDs
Shared Coverage:
Unique Coverage:
Conflicts:
Canonical Candidate:
Secondary References:
Rejected Redundancy:
```

## 9.6 Source Register Schema

```text
Source ID: SRC-###
Title:
Type:                     <- website / repository / docs / discussion / dataset
URL:
Repository:
Author/Organization:
Date Accessed:            <- ISO date
License:
Research Domains:         <- DOM IDs
Claims Used:
Files Inspected:
Confidence:               <- 0-100
Notes:
```

## 9.7 Rejected Candidate Schema

```text
Candidate ID: REJ-###
Candidate:
Source:
Reason Rejected:
Potentially Useful Parts:
What Would Change the Decision:
Date:
```

---
# 10. Scoring Framework — Calibrated Rubric

100-point research score. Score informs ranking; it NEVER replaces qualitative analysis.

## 10.1 Weights

| # | Criterion | Max | What It Measures |
|---|---|---|---|
| 10.1.1 | Relevance | 25 | Directness of fit to a Hermes research domain |
| 10.1.2 | Generalizability | 15 | Mechanism separable from original domain? |
| 10.1.3 | Architectural Quality | 15 | Boundaries, workflows, contracts, responsibilities, state clarity |
| 10.1.4 | Evidence Quality | 15 | Claims backed by code/docs/tests/examples/multi-source |
| 10.1.5 | Reusability | 10 | Adaptation cost; assumption inheritance risk |
| 10.1.6 | Reliability Thinking | 10 | Failure, observability, validation, permissions, recovery addressed |
| 10.1.7 | Maintenance & Maturity | 5 | Activity, versioning, issue handling, community signal |
| 10.1.8 | Licensing Clarity | 5 | License clear enough to safely know reuse rights |

## 10.2 Calibrated Anchors (examples to prevent score inflation)

**Relevance (25):**
- 21–25: maps to >=1 core Hermes domain with explicit, inspectable mechanism
- 11–20: partial/indirect relevance; mechanism must be inferred
- 1–10: tangential; name-match only

**Generalizability (15):**
- 13–15: clean separation demonstrated in the source itself (docs/code separate domain logic)
- 7–12: separable with moderate effort; some domain coupling
- 1–6: deeply entangled with original project

**Evidence Quality (15):**
- 13–15: tests + real examples + docs agree + multiple independent sources corroborate
- 7–12: partial support; some README-vs-code gaps
- 1–6: claims only

**Reliability Thinking (10):**
- 9–10: explicit failure handling + observability + permissions model
- 4–8: some reliability features present
- 0–3: none addressed

## 10.3 Interpretation Bands

```text
90–100   Exceptional reference
80–89    Strong candidate
70–79    Useful candidate
60–69    Reference selectively
40–59    Weak fit
0–39     Reject
```

## 10.4 Scoring Discipline Rules

1. Score AFTER deep inspection, never from descriptions.
2. If any criterion cannot be assessed due to missing evidence, cap total at 69 and set confidence <=50.
3. Two reviewers (simulated roles) score independently for candidates intended as STRONG; divergence >15 points triggers a reconciliation note.
4. Every sub-score of >=80% of max requires a cited basis.

---

# 11. Deduplication Protocol

## 11.1 Trigger Points

Deduplication runs: (a) after Stage -2.2 completion; (b) after Stage -2.4 completion; (c) before final synthesis.

## 11.2 Procedure

1. Cluster candidates by capability surface (e.g., Agent Creator / Skill Creator / Skill Architect / Team Builder / Orchestrator all touch agent-system design).
2. For each cluster complete the dedup schema: shared coverage, unique coverage, conflicts, canonical candidate, secondary references, rejected redundancy.
3. Canonical selection criteria (ordered): evidence depth > generalizability > architectural quality > maintenance > popularity.
4. Conflicts between candidates are recorded verbatim — not silently resolved.
5. Redundant candidates are moved to `rejected-candidates.md` with cross-references preserved.

## 11.3 Output Rules

- `deduplication-map.md` must cover every capability cluster with >=2 candidates.
- No candidate may appear as both canonical and rejected without an explanatory conflict entry.

---

# 12. Source Quality & Evidence Hierarchy

## 12.1 Forbidden Inferences

Claude Code MUST NOT:

- Trust star count alone
- Trust marketing claims alone
- Trust README claims when contradicted by code
- Treat a recent repo as production-proven
- Treat an old repo as useless solely for being old
- Infer reliability from branding
- Confuse framework popularity with architectural suitability

## 12.2 Preferred Evidence Order

```text
1. Source code / schemas / tests          <- highest trust
2. Official architecture docs
3. Maintainer documentation
4. Examples
5. Issues / release history
6. Independent technical discussion
7. README marketing claims                <- lowest trust
```

## 12.3 Provenance Rule

All important claims retain their original source URL and access date. Apify is a discovery/extraction tool, NOT a source of truth by itself.

---

# 13. Negative Research Protocol

For EVERY strong candidate (skill, repo, or pattern), Claude MUST actively search for reasons NOT to use it:

```text
Q1  What assumptions does this project make?
Q2  Where could it fail for Hermes?
Q3  What complexity does it introduce?
Q4  What lock-in does it create?
Q5  What evidence is missing?
Q6  What competing approach is simpler?
Q7  What parts are marketing rather than engineering?
```

Rules:

- Answers are recorded per candidate (in its record or audit file) under `Adversarial Review`.
- A candidate CANNOT receive STRONG CANDIDATE / REUSE-leaning classification without completed adversarial review.
- If adversarial review is inconclusive, downgrade to CANDIDATE and log an open question.
- The Skeptic role (Section 14) performs a final independent pass on all strong recommendations during synthesis.

---

# 14. Role Simulation Protocol

Claude may simulate multiple independent analysis roles. For IMPORTANT decisions, roles produce independent notes BEFORE synthesis.

**Definition — IMPORTANT decision:** any classification of STRONG CANDIDATE (pattern, skill, or repo), any REUSE or ADAPT entry destined for `HERMES-REUSE-STACK.md`, and any Exit Gate (Section 18) determination. Routine CANDIDATE / CONTEXT-DEPENDENT / REFERENCE-level classifications do not require multi-role review, though any role may still flag one for escalation to IMPORTANT if warranted.

| Role | Mandate | Key Outputs |
|---|---|---|
| Research Scout | Finds candidates across sources | Candidate lists w/ discovery rationale |
| Repository Auditor | Inspects actual structure/artifacts | Audit files (A-J), triage verification |
| Agent Architect | Evaluates architecture relevance | Architecture-fit notes per candidate |
| Product Systems Analyst | Checks alignment with what Hermes may become | System-alignment notes |
| Reliability Reviewer | Hunts failure/eval/permission/observability/recovery gaps | Reliability findings |
| Skeptic | Attempts to reject every recommendation | Rejection attempts + surviving-object list |
| Synthesizer | Converts findings into patterns and final decisions | Pattern catalog entries, final reports |

## Operating Rules

1. Independent notes first: for strong-candidate decisions, at minimum Auditor + Reliability Reviewer + Skeptic produce separate notes before Synthesizer merges.
2. Role notes carry role name + date inside the artifact they influence.
3. Disagreements are preserved (not averaged away); unresolved disagreements become open questions.
4. The Skeptic's pass is MANDATORY for anything entering HERMES-REUSE-STACK.md under REUSE or ADAPT.

---

# 15. Named Source & Research-Seed Campaigns

## 15.1 Campaign SCS — Some Claude Skills (Registered Research Input)

Primary target: `https://someclaudeskills.com/skills`

This is a **named research input**, not an authority and not a mandatory checklist.

### Suggested Starting Leads — NOT Required Targets

The following are examples already identified as potentially interesting:

```text
Systems Thinking            Research Analyst           Competitive Cartographer
Product Appeal Analyzer     Task Decomposer            Orchestrator
Recursive Synthesis         Agent Creator              Skill Architect
Skill Creator               Skill Grader               Human Gate Designer
Output Contract Enforcer    Logging Observability      Cost Optimizer
LLM Router                  Security Auditor           Launch Readiness Auditor
```

Claude MUST challenge this list.

It may:

- skip weak candidates;
- discover better candidates;
- inspect unrelated skills for hidden reusable mechanisms;
- merge overlapping concepts;
- stop following the list when it no longer produces useful signal.

### Hidden Pattern Mining

Look beyond skill titles for reusable mechanisms such as:

- approval design;
- escalation logic;
- confidence handling;
- state transitions;
- review loops;
- failure recovery;
- structured outputs;
- risk gates;
- role separation;
- long-term tracking.

A domain-specific skill may contribute only one useful mechanism. Extract the mechanism, not the original product assumptions.

### Transformation Chain

```text
Source Skill -> Original Purpose/Domain -> Observed Mechanism
             -> Generalizable Pattern -> Possible Hermes Relevance
             -> Phase -1 Fit Decision
```

### Source Handling Rule

When a finding materially affects a recommendation, preserve:

- skill name;
- exact source URL when available;
- stated purpose;
- mechanism extracted;
- assumptions detected;
- affected research domain;
- reuse classification;
- confidence;
- inspection date.

## 15.2 Open Repository / Public Project Discovery

No specific repository is pre-approved, pre-required, or treated as evidence by this plan.

If repository-host access is available, Claude may use it to discover and inspect relevant public projects.

A project becomes a research source only after it is actually discovered, inspected enough to justify relevance, and registered in `source-register.md`.

README-only evaluation is insufficient for high-confidence recommendations. Deep-audited candidates should be inspected across relevant architecture docs, configuration, agent/skill definitions, schemas, workflows, examples, tests, evaluation logic, permissions, maintenance signals, and license where available.

The goal is not to cover a platform or a repo list. The goal is to find **useful evidence and reusable patterns**.

## 15.3 Campaign APIFY — Structured Extraction Support

Use Apify for authorized crawling, search-result extraction, skill-gallery inspection, documentation extraction, structured web research, and multi-source comparison.

Apify is a research tool, not the underlying source of truth. Material claims preserve the original source URL.

---
# 16. Deliverables Specification

## 16.1 Required Artifact Set

Phase -2 is NOT complete until all of the following exist:

```text
phase-m2/
|-- research-domains.md        (1) Domain map w/ per-domain definitions
|-- skill-catalog.md           (2) All skill records
|-- repo-catalog.md            (3) All triage records
|-- source-register.md         (4) Every meaningful source
|-- pattern-catalog.md         (5) Pattern library w/ provenance
|-- capability-matrix.md       (6) Need x candidate matrix
|-- deduplication-map.md       (7) Overlap/conflict resolution
|-- rejected-candidates.md     (8) Rejections w/ reversal conditions
|-- open-questions.md          (9) Unknowns + escalations
|-- downstream-handoff.md      (10) Structured handoff contract
|-- repo-audits/               (11) One A-J audit per deep-audited repo
+-- HERMES-CAPABILITY-INTELLIGENCE-M2.md   (12) Capstone report

HERMES-REUSE-STACK.md          (13) Final decision file (root)
```

## 16.2 Capstone Report Structure — HERMES-CAPABILITY-INTELLIGENCE-M2.md

```text
 1. Executive Summary
 2. Research Scope
 3. Methodology
 4. Sources Investigated
 5. Research Domains
 6. Skill Landscape
 7. Repository Landscape
 8. High-Value Patterns
 9. Architecture Pattern Comparison
10. Agent Design Pattern Comparison
11. Memory Pattern Comparison
12. Human-Control Pattern Comparison
13. Evaluation Pattern Comparison
14. Reliability Pattern Comparison
15. Social-Media-Specific Findings
16. Capability Matrix (summary view; full data in matrix file)
17. Deduplication Findings
18. Strong Candidates
19. Pattern-Only Candidates
20. Rejected Candidates
21. Knowledge Gaps
22. Risks
23. Confidence Assessment
24. Phase -1 Inputs
```

## 16.3 Decision File Structure — HERMES-REUSE-STACK.md

Concise and decision-oriented:

```text
# Hermes Reuse Stack

## REUSE
- Candidate A
  - Why: / Evidence: / Conditions:

## ADAPT
- Candidate B
  - What to preserve: / What must change: / Estimated adaptation level:

## REFERENCE
- Candidate C
  - Pattern worth studying: / Why not reuse directly:

## REJECT
- Candidate D
  - Reason:

## UNKNOWN
- Candidate E
  - Missing evidence: / Required follow-up:
```

Rules: every entry cites record IDs and SRC IDs; every REUSE entry lists compatibility conditions; every UNKNOWN lists the specific missing evidence.

---

# 17. Quality Assurance Gates

Gate checks run at stage boundaries before proceeding.

| Gate | After Stage | Mandatory Checks |
|---|---|---|
| G1 | -2.1 | Every domain in the current Approved Domain Registry is defined with question/terms/exclusions (per Section 7.2); no duplicate domains; registry size is dynamic (Section 7.2 — no fixed count) |
| G2 | -2.2 | All inspected skills recorded per Section 9.1; scores computed post-inspection only; dedup pass done; Stage -2.2 exit criteria (Section 8) met |
| G3 | -2.3 | Materially relevant discovered projects triaged; decisions have reasons; alternate discovery pass shows diminishing new signal |
| G4 | -2.4 | Each DEEP AUDIT repo has full A-J file incl. docs-vs-code evidence check |
| G5 | -2.5 | Patterns cite sources; strong patterns cite >=2 independent sources or 1 deep-audited high-confidence; failure modes present |
| G6 | -2.6 | Every domain covered by >=1 row or documented no-candidate finding; no REUSE without compatible assumptions |
| G7 | -2.7 | Fact/Interpretation/Hypothesis/Unknown labels complete; adversarial review done for all strong candidates; artifacts mutually consistent |

Additional standing QA rules:

- No record may lack a Source ID.
- No confidence value without a one-line basis.
- Any artifact edit re-runs affected downstream consistency checks.

---

# 18. Exit Gate & Decision Logic

## 18.1 Ten Exit Conditions (ALL must hold)

| # | Condition | Verification |
|---|---|---|
| X1 | Coverage: every major domain has >=1 credible candidate OR a documented reason none was found | Capability matrix vs domain list |
| X2 | Evidence: every strong recommendation traceably evidenced | Record citations |
| X3 | Deep review: important candidates inspected beyond README | Audit files exist |
| X4 | Deduplication: major overlap mapped | Dedup map complete |
| X5 | Pattern extraction: knowledge exists as reusable patterns, not just source lists | Pattern catalog |
| X6 | Negative review: strong candidates survived skeptical review | Skeptic notes |
| X7 | Gaps: unknowns and missing capabilities explicitly documented | Open questions |
| X8 | No premature architecture: no final Hermes architecture selected | Self-audit against Section 2.3 list |
| X9 | No implementation: nothing built | Workspace inspection |
| X10 | Execution boundary respected; no Owner–Claude rule promoted to Owner–Hermes requirement | Boundary review note |

## 18.2 Exit Status Determination

Exactly ONE status is issued at end of phase:

```text
M2-COMPLETE                -> ecosystem intelligence baseline sufficient to begin
                              Hermes-specific fit/adaptation analysis in Phase -1;
                              all 10 exit conditions satisfied

M2-CONDITIONALLY-COMPLETE  -> Phase -1 may begin but documented research gaps remain;
                              gaps enumerated in open-questions.md and handoff file

M2-INCOMPLETE              -> research coverage or evidence insufficient;
                              resume work per gap plan before handoff
```

Decision rule: if any of X1–X7 fails -> M2-INCOMPLETE. If X1–X7 hold but material unknowns remain that do not block fit analysis -> M2-CONDITIONALLY-COMPLETE. If all ten hold cleanly -> M2-COMPLETE. The status plus rationale goes into `downstream-handoff.md` and is reported to the Owner.

---

# 19. Handoff Package to Phase -1

## 19.1 Files Transferred

```text
HERMES-CAPABILITY-INTELLIGENCE-M2.md
HERMES-REUSE-STACK.md
pattern-catalog.md
capability-matrix.md
deduplication-map.md
source-register.md
rejected-candidates.md
open-questions.md
downstream-handoff.md
```

## 19.2 Handoff Contract Items (all ten required in downstream-handoff.md)

1. **Evidence** — what was discovered, where it came from
2. **Extracted Patterns** — reusable mechanisms separated from original domains/branding
3. **Candidate Knowledge** — skills/agents/repos/templates/methodologies/frameworks/design approaches worth considering
4. **Assumptions** — what each candidate carries from its original project
5. **Conflicts & Overlap** — duplications, competitions, contradictions
6. **Rejected Alternatives** — what was examined, why rejected, surviving sub-patterns
7. **Confidence** — how strongly each conclusion is supported
8. **Open Questions** — what Phase -2 could not determine
9. **Hermes Implications** — possible implications WITHOUT converting them into premature decisions
10. **Adaptation Candidates** — items suitable for deeper Phase -1 analysis

## 19.3 Receiver Rules for Phase -1 (stated inside handoff)

Phase -1 MUST NOT assume any Phase -2 recommendation is automatically appropriate. Phase -1 owns: which knowledge fits; what adapts/rejects; remaining gaps; and the best evidence-based specification path (possibly V1/V2 maturity stages, multi-document structures, or alternatives). Phase -2 does NOT constrain that choice beyond the Build Readiness North Star.

---

# 20. Work Breakdown, Sequencing & Effort Model

Effort units are Claude-Code working sessions on the VPS; calendar mapping depends on session cadence.

| WP | Name | Contents | Depends On | Relative Effort |
|---|---|---|---|---|
| WP0 | Bootstrap | Workspace, CLAUDE.md, tool auth, raw idea import | — | XS |
| WP1 | Research-scope formation | Review seeds; create approved domain registry | WP0 | S |
| WP2 | SCS campaign | Skill discovery + hidden-pattern mining | WP1 | M |
| WP3 | Open project discovery & triage | Stage -2.3 evidence-driven discovery | WP1 | M |
| WP4 | Deep audits | Stage -2.4 over shortlist | WP3 | L |
| WP5 | Pattern extraction | Stage -2.5 transformation | WP2+WP4 | L |
| WP6 | Capability matrix | Stage -2.6 build + rules enforcement | WP5 | M |
| WP7 | Synthesis | Stage -2.7 labeling, negative pass, dedup final | WP6 | M |
| WP8 | Capstone assembly | Report + reuse stack + handoff file | WP7 | M |
| WP9 | Exit gate & report | Gate verification; status issuance; Owner report | WP8 | S |

Critical path: WP0 -> WP1 -> WP3 -> WP4 -> WP5 -> WP6 -> WP7 -> WP8 -> WP9.
WP2 runs parallel to WP3/WP4 where sessions allow.

Iteration loops (budgeted): WP3->WP4 loop when triage uncovers new shortlist entries; WP5->WP2 loop when a pattern lacks a second confirming source.

---

# 21. Metrics & Progress Tracking

Maintained in `HERMES_RESEARCH.md` and updated per session.

Metrics measure **research quality**, not checklist volume.

| Metric | Target / Rule | Notes |
|---|---|---|
| Approved domains with clear question + status | 100% of current registry | Registry size is dynamic |
| Approved domains with credible evidence or documented gap | 100% before exit | `COVERED-NO-CANDIDATE` is valid |
| Material findings lacking source IDs | 0 | Hard rule |
| Strong candidates without adversarial review | 0 | Hard rule |
| Major overlaps left unresolved or unrecorded | 0 | Hard rule |
| High-impact unknowns hidden instead of documented | 0 | Hard rule |
| Pending Owner escalations | tracked | Blocking items clearly marked |
| New-signal rate after alternate discovery pass | diminishing | Practical saturation indicator |
| High-signal skills/projects/patterns recorded | tracked, no quota | Quality over quantity |
| Deep audits completed | as justified | Only when expected information value warrants cost |

There are **no fixed quotas** for:

- number of domains;
- number of skills;
- number of repositories/projects;
- number of deep audits;
- number of patterns.

A smaller evidence base is preferable when it is stronger, less redundant, and sufficient for Phase -1.

## 21.1 Saturation Backstop (Stopping Rule)

This backstop is **information-value-based, not session-count-based** — a fast session and a slow session are judged the same way.

For any active discovery direction (a domain, a search strategy, or a source campaign):

1. After each discovery pass, Claude records: new candidates found, new patterns surfaced, and whether any existing classification changed.
2. If **two consecutive alternate-query passes** in the same direction each produce materially the same result — no new candidate that changes a classification, no new pattern, no new open question — that direction is declared **saturated**.
3. Saturated directions stop. Claude logs the saturation call in `HERMES_RESEARCH.md` with the two passes' findings as justification.
4. If a saturated direction later needs reopening (e.g., a downstream stage exposes a gap), it may resume — saturation is a per-direction, revisable state, not a permanent close.
5. If Claude cannot tell whether a direction is saturated or simply difficult, that uncertainty itself is logged as an open question rather than used to justify continued spend.

This rule operationalizes the existing "diminishing new signal" language used throughout Sections 8 and 23 into one consistent, checkable test.

Research should continue while new searches materially change understanding. When a credible alternate search strategy produces little meaningful new signal, Claude may declare that area sufficiently saturated and move on.

---

# 22. Risk Register & Mitigations

| ID | Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| R1 | Scope creep into implementation | Med | Severe | CLAUDE.md guardrail; X9 check; workspace isolation |
| R2 | Catalog inflation / low signal | High | Medium | Soft caps; dedup gates; score discipline rules |
| R3 | README-trust bias | High | High | Beyond-README mandate; evidence hierarchy; docs-vs-code checks |
| R4 | Premature architecture lock-in | Med | Severe | Forbidden-decision list; X8 self-audit |
| R5 | Provenance loss | Med | High | Source register mandatory; URL+date per claim |
| R6 | Secret exposure during inspection | Low | Severe | Never echo secrets; incidental-discovery protocol |
| R7 | Research tool/source unavailability or access limits | Med | Medium | Use authorized fallback sources/methods; log degraded mode and evidence impact |
| R8 | Analysis paralysis / infinite discovery | Med | Medium | Stage exit criteria; saturation judgment calls logged |
| R9 | Conflicting evidence unresolved | High | Medium | Preserve conflicts verbatim; convert to open questions |
| R10 | Owner–Claude rules leaking into product requirements | Med | High | P6 separation; X10 boundary review |
| R11 | Context loss between sessions | Med | Medium | Journal updates; artifact-first working style |
| R12 | Score inflation | Med | Medium | Calibrated anchors; dual scoring for strong candidates |

---

# 23. Failure & Contingency Playbook

| Trigger | Response |
|---|---|
| Source unreachable mid-audit | Mark record INSUFFICIENT EVIDENCE; retry later; never guess contents |
| Contradiction between two trusted sources | Record both positions under conflicts; set confidence <=50; open question if decision-relevant |
| Escalation blocking critical path | Park blocked branch; continue independent workstreams; summarize parked state in journal |
| Discovery saturation suspected | Run one alternate query family; if <10% new signal -> declare domain saturated, move on |
| Session/context interruption | Resume from last committed artifact state; journal reconstructs position |
| Candidate turns out misrepresented | Move to rejected register with "what would change the decision" filled |

---

# 24. Reporting Cadence

- **Per session:** update `HERMES_RESEARCH.md` (what was inspected, key findings, next step).
- **Per stage completion:** brief status line to Owner (stage, outputs updated, blockers).
- **Escalations:** immediate, using the Section 5.3 format.
- **End of phase:** full report = capstone document + reuse stack + exit status + handoff package summary.

## 24.1 Owner-Relay Block Format (mandatory, every report to the Owner)

The Owner does not read technical detail directly — they relay Claude Code's
report to a separate assistant that translates it into plain language for
them. So every report to the Owner (stage completions, checkpoints,
escalations, the end-of-phase report) must end with one clearly-marked block,
in addition to the normal report, containing everything that assistant needs
in one place: what this task/stage was, what happened, what changed, what's
next, and the single most important risk (if any) worth the Owner's attention
— or an explicit "no significant risk" if there isn't one. Keep it short but
complete; do not omit a real risk to keep it shorter. Write it under a
clearly-marked heading, in whatever language and level of detail best
transfers the substance — it is read by an AI relay, not the Owner directly,
so optimize for complete and unambiguous transfer of meaning rather than a
fixed format or language.

---

# 25. CLAUDE.md Guardrail File Content

# 25. CLAUDE.md Guardrail File Content

The operational guardrail file is maintained as a **standalone file**, not embedded here,
to avoid two diverging copies of the same rules:

**`/root/m2-research-workspace/CLAUDE.md`**

That file is the authoritative, current version of the operational layer — it reflects
every guardrail, boundary, checkpoint, and backstop defined throughout this Master Plan
(Sections 5, 8, 14, 18, 21.1, 24). If the two ever appear to disagree, this Master Plan
governs for research methodology and scoring; the standalone CLAUDE.md governs for the
concise, always-loaded operational summary. A disagreement between them is a defect to
fix, not a precedence to rely on.

---

# 26. Definition of Success

Phase -2 succeeds when Claude Code can answer:

> For every major capability Hermes may require — what proven approaches already exist, what evidence supports them, what assumptions they carry, how much they overlap, what should be reused or only studied, and where genuinely new Hermes-specific design will likely be required?

And leaves Phase -1 with enough structured evidence to determine the best Hermes-specific specification path without being forced into any preselected architecture, framework, agent model, or version structure.

It is NOT successful merely because many repositories were found.

---
# 27. Appendix A - Copy-Paste Templates

## A.1 research-domains.md skeleton

```markdown
# Hermes Phase -2 Research Domains
Revision: <n> | Updated: <date>

## Domain Registry
| ID | Cluster | Name | Status |
|----|---------|------|--------|
| DOM-01 | A | Product discovery | IN-PROGRESS |

## Per-Domain Definitions
### DOM-01 - Product discovery
Research Question:
Why Hermes May Need It:
Evidence Wanted:
Likely Source Types:
Search Terms:
Exclusion Criteria:
Status:
```

## A.2 skill-catalog.md record wrapper

```markdown
## SKL-001 - <Skill Name>
<full schema fields per Section 9.1>
Adversarial Review: (required before any strong classification)
Role Notes: Auditor: ... | Reliability Reviewer: ... | Skeptic: ...
```

## A.3 repo-audits/<repo>.md skeleton

```markdown
# Deep Audit - <owner/repo>
Triage ref: REPO-### | Date: <date> | Audit depth: full

## A. Architecture      findings + Verdict
## B. Agent Design      findings + Verdict
## C. Context & Memory  findings + Verdict
## D. Reliability       findings + Verdict
## E. Human Control     findings + Verdict
## F. Evaluation        findings + Verdict
## G. Operations        findings + Verdict
## H. Reusability       findings + Verdict
## I. Evidence          docs-vs-code agreement; example reality; test support; maintenance
## J. License           study rights / reuse rights / restrictions

## Score Breakdown (per Section 10)
Relevance /25, Generalizability /15, ArchQuality /15, Evidence /15,
Reusability /10, Reliability /10, Maintenance /5, Licensing /5 = TOTAL/100

## Adversarial Review (Q1-Q7)
## Files Inspected
```

## A.4 capability-matrix.md table header

```markdown
| Hermes Research Need | Candidate | Type | Evidence | Reuse Class | Adaptation Level | Confidence | Notes |
|---|---|---|---|---|---|---|---|
| DOM-12 HITL escalation | PAT-007 Confidence-based escalation | Pattern | SRC-004, REPO-011 | ADAPT | LIGHT | 75 | note text |
```

## A.5 downstream-handoff.md skeleton

```markdown
# Phase -2 Downstream Handoff
Exit Status: M2-COMPLETE | M2-CONDITIONALLY-COMPLETE | M2-INCOMPLETE
Date: <date>

## 1. Evidence Summary
## 2. Extracted Patterns (index -> pattern-catalog.md)
## 3. Candidate Knowledge (index -> catalogs)
## 4. Candidate Assumptions Register
## 5. Conflicts & Overlap (-> deduplication-map.md)
## 6. Rejected Alternatives (-> rejected-candidates.md)
## 7. Confidence Assessment
## 8. Open Questions (blocking vs non-blocking)
## 9. Hermes Implications (NOT decisions)
## 10. Adaptation Candidates for Phase -1
```

---

# 28. Appendix B - Checklists

## B.1 Stage -2.2 Skill Inspection Checklist

- [ ] Actual skill content inspected (not description only)
- [ ] All Section 9.1 fields filled
- [ ] Assumptions separated: project-specific vs domain-specific
- [ ] Score computed post-inspection; high sub-scores cite basis
- [ ] Overlaps and conflicts cross-referenced
- [ ] Source URL + access date preserved
- [ ] Reuse class justified in Reasoning Summary

## B.2 Repo Triage to Deep-Audit Promotion Checklist

- [ ] DEEP AUDIT decision recorded with rationale
- [ ] License permits concept study at minimum
- [ ] Recent activity verified
- [ ] Audit dimensions A-J all answered
- [ ] Docs-vs-code disagreement explicitly stated
- [ ] Score + confidence assigned after audit

## B.3 Pre-Synthesis Consistency Checklist

- [ ] Every catalog entry has >=1 SRC reference
- [ ] Every STRONG CANDIDATE has adversarial review Q1-Q7 answers
- [ ] Dedup map covers all multi-candidate clusters
- [ ] Rejected candidates include reversal conditions
- [ ] Open questions tagged blocking/non-blocking
- [ ] No forbidden premature decision anywhere in artifacts
- [ ] Fact/Interpretation/Hypothesis/Unknown labels applied

## B.4 Exit Gate Master Checklist (X1-X10)

- [ ] X1 Coverage complete (or documented no-candidate per domain)
- [ ] X2 Evidence traceable for all strong recommendations
- [ ] X3 Beyond-README review done for important candidates
- [ ] X4 Deduplication mapped
- [ ] X5 Patterns extracted (not just source lists)
- [ ] X6 Negative review survived by strong candidates
- [ ] X7 Gaps explicitly documented
- [ ] X8 No premature architecture selected
- [ ] X9 No implementation started
- [ ] X10 Execution boundary respected; no rule promotion Owner-Claude -> Owner-Hermes

---

# 29. Appendix C - Traceability Matrix (Plan to Spec R1.3)

| Spec Section | Covered By Plan |
|---|---|
| 0 Executive Intent | Sections 1, 26 |
| 0.1 Downstream Handoff & Final Objective | Sections 2.4, 19 |
| 0.2 Build Readiness North Star | Section 2.4 |
| 0.3 Fixed Direction / Open Path | Sections 2.1, 2.3 |
| 0.4 Handoff Contract (10 items) | Section 19.2 |
| 0.5 Handoff Boundary | P4, 19.3 |
| 0.6 Need Before Solution | P1 |
| 0.7 Traceability Principle | P3 |
| 0.8 Independent Build-Readiness Test | Section 2.4 closing obligation |
| 1 Non-Negotiable Guardrail | Sections 5.1 |
| 1.1 Owner-Claude vs Owner-Hermes | P6, 5.2 |
| 1.2 Scope of Phase -2 Rules | Section 5.2 preamble |
| 1.3 Minimum Execution Baseline | Section 5.2 + 5.4 |
| 1.4 Phase-Local Collaboration | P6 note; rules are phase-local by construction |
| 1.5 Separation Principle | P6, X10 |
| 2 Research Context | Section 2.2, 2.3, P7 |
| 2.1 Explicit Source: SomeClaudeSkills | Section 15.1 |
| 3 Research Surfaces (Apify/SCS + optional discovered public-project sources) | Sections 6.3, 15 |
| 4 Core Research Principle | P2 |
| 5 Research Domains / Seeds | Section 7 |
| Stage -2.1 Search Domain Definition | Section 8, G1 |
| Stage -2.2 Skill Discovery | Section 8, 9.1, B.1, G2 |
| Stage -2.3 Repository Discovery | Section 8, 9.2, 15.2, G3 |
| Stage -2.4 Deep Repository Audit | Section 8, 9.3, A.3, G4 |
| Stage -2.5 Pattern Extraction | Section 8, 9.4, G5 |
| Stage -2.6 Capability Matrix | Section 8, A.4, G6 |
| Stage -2.7 Evidence Synthesis | Section 8, P5, G7 |
| 7 Scoring Framework | Section 10 |
| 8 Deduplication Rules | Section 11 |
| 9 Source Quality Rules | Section 12 |
| 10 Research Source Register | Section 9.6 |
| 11 Rejected Candidate Register | Section 9.7 |
| 12 SomeClaudeSkills Focus | Section 15.1 |
| 13 Open Repository / Public Project Discovery | Section 15.2 |
| 14 Required Negative Research | Section 13 |
| 15 Research Team Roles | Section 14 |
| 16 Required Deliverables | Section 16.1 |
| 17 Capstone Report Structure | Section 16.2 |
| 18 REUSE-STACK Structure | Section 16.3 |
| 19 Exit Gate | Section 18.1 |
| 20 Exit Decision | Section 18.2 |
| 21 Handoff to Phase -1 | Section 19 |
| 22 VPS Repository Structure | Section 6.1 |
| 23 CLAUDE.md Guardrail | Section 25 |
| 24 Definition of Success | Section 26 |
| 25 Revision History (R1.1-R1.3) | Reflected throughout; R1.3 source handling in 15.1 |

---

## Document Control

| Field | Value |
|---|---|
| Plan ID | HERMES-M2-PLAN v1.1 |
| Source spec | HERMES-M2 SPEC R1.3 |
| Coverage of spec sections | All sections 0 through 25 mapped (Appendix C) |
| Execution mode | Claude Code on Owner VPS, research-only |
| Canonical workspace | `/root/m2-research-workspace` (see Section 6.1) |
| Next action on approval | WP0 Bootstrap |
| Companion file | `/root/m2-research-workspace/CLAUDE.md` — standalone operational layer (Section 25); this document remains the full Source of Truth |
| v1.1 changes from v1.0 | Fixed Gate G1 domain-count contradiction; fixed Gate G2 undefined "L1 skills" term; fixed Section 10 sub-criterion numbering; clarified "IMPORTANT decision" scope (Section 14); added mandatory Owner checkpoint after Stage -2.1 (Section 8); added information-value-based saturation backstop (Section 21.1); defined canonical absolute workspace path (Section 6.1); moved CLAUDE.md content to a standalone file (Section 25). No principles, guardrails, stages, or schemas were altered. |

END OF HERMES PHASE -2 EXECUTION MASTER PLAN
