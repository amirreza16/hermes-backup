# Hermes Phase -2 Research Journal

Phase: HERMES -2 / Ecosystem Intelligence & Reuse Discovery
Workspace root: /root/m2-research-workspace
Phase start date: 2026-08-23

This is the living research journal/index for Phase -2, per Master Plan Section 6.1.
Updated once per session with: what was inspected, key findings, next step.
Stage completions, escalations, and saturation calls are logged here as they occur
(Master Plan Sections 21.1, 24).

---

## Session Log

### 2026-08-23 — Session 1: Bootstrap

**What was inspected:**
- Master Plan (`HERMES-PHASE-M2-EXECUTION-PLAN-v1.1.md`) Section 6 (Environment Setup &
  Workspace Bootstrap) and Section 25 (CLAUDE.md Guardrail File Content).
- Existing workspace state: `CLAUDE.md` and the Master Plan were already present at
  workspace root; no other workspace structure existed yet.
- Git state (`git status`, `git log`, `git config --global user.name/email`).
- Tool authorization: Apify MCP tools (available), GitHub CLI (`gh auth status`).
- Filesystem search for a pre-existing `raw-hermes-idea.md` or equivalent source concept
  document.

**Key findings:**
- Directory tree from Section 6.1 did not yet exist (only `CLAUDE.md` and the Master Plan
  were present). Created: `source/`, `phase-m2/`, `phase-m2/repo-audits/`, `decisions/`.
- `CLAUDE.md` at workspace root matches the Section 25 pointer (standalone authoritative
  operational layer) — no changes needed.
- Git is initialized locally on branch `master`, no commits yet, no remote configured.
  `git config --global user.name`/`user.email` are unset.
- Apify MCP tools are available and authorized per the Tool Authorization Matrix
  (Section 6.3).
- GitHub CLI (`gh`) is authenticated as `amirreza16` (token scopes reported as "none" —
  sufficient for unauthenticated-equivalent public reads; may not support authenticated
  actions if ever needed, though none are authorized for this phase regardless per
  Section 6.3).
- No `source/raw-hermes-idea.md` (or equivalent) was found inside the workspace.
  Filesystem search outside the workspace surfaced an unrelated, pre-existing
  `/root/hermes-project-docs` tree and other `/root/.hermes*` / `hermes-*` paths — these
  were located by search only, not opened or copied, since they sit outside the
  Section 6.1 workspace root and their relationship (if any) to this phase's required
  source input is unconfirmed by the Owner.

**Next step:**
Await Owner input for `source/raw-hermes-idea.md` (verbatim original concept — see
Bootstrap report). Do not proceed to Stage -2.1 until this is resolved and the Owner
gives explicit go-ahead.

### 2026-08-23 — Session 1 (cont.): Source import, Bootstrap complete

**What was inspected:**
- Owner-provided verbatim source concept text (Persian), received in chat.

**Key findings:**
- Imported verbatim to `source/raw-hermes-idea.md`. No edits, translation, or
  paraphrase applied — content preserved exactly as provided.
- Bootstrap (Master Plan Section 6.2) is now fully complete: workspace tree created,
  `CLAUDE.md` verified, `source/raw-hermes-idea.md` imported, journal initialized, tool
  authorization verified, git-init confirmed.
- Raw idea names two core agent types (content-generation, research/intelligence) and
  three recurring behavioral principles (stop-and-ask under ambiguity; explicit
  confirmation for irreversible actions; no self-initiated deletion from memory/history)
  plus two constraints (quality-over-throughput; cost/compute control as a hard
  constraint). Per CLAUDE.md / Master Plan P8, this is a non-binding research seed, not
  a locked requirement — it will inform Stage -2.1 domain formation, not be treated as
  a decision.

**Next step:**
Bootstrap complete. Awaiting explicit Owner approval to begin Stage -2.1 (Research
Scope Formation).

### 2026-08-23 — Session 2: Stage -2.1 Research Scope Formation

**What was inspected:**
- Master Plan Section 7 (Research Seed Map & Approved Domain Registry), Section 8
  Stage -2.1 procedure/exit criteria/Owner Checkpoint, Section 3 objectives/
  non-objectives, Gate G1 (Section 17), Appendix A.1 skeleton (Section 27).
- `source/raw-hermes-idea.md` re-read closely against every Section 7.1 seed topic.

**Key findings:**
- Produced `phase-m2/research-domains.md`: 25 active domains across 6 clusters (Core
  Agent Architecture; Human Control, Safety & Trust; State, Memory & Reliability;
  Security & Governance; Social-Media Operations; Scaling & Self-Maintenance).
- 4 seed topics dropped (Product discovery, Product requirements, Spec-driven
  development, Architecture documentation) as out of Phase -2 scope or redundant with
  this phase's own process — full rationale in the file's Seed Reconciliation Log.
- 11 merges performed where seeds pointed at the same underlying problem once scoped
  to Hermes' specific two-agent-type design (full list in reconciliation log).
- 4 new domains added, not present in the seed list, because the raw idea names them
  explicitly with no seed coverage: DOM-09 (ambiguity/clarification-seeking), DOM-10
  (progressive autonomy/trust calibration over time), DOM-24 (multi-tenant onboarding),
  DOM-25 (self-updating ecosystem-intelligence agent).
- 1 domain (DOM-23, Community management) kept but marked BLOCKED rather than silently
  dropped or included — raw idea is genuinely ambiguous on whether engagement
  automation is in scope. Logged as OQ-01 in `phase-m2/open-questions.md`.
- Gate G1 self-check: every active domain has question/evidence/search-strategy/
  exclusion fields filled per Section 7.2; no duplicate domains; registry size is not
  fixed to any target count.

**Next step:**
Present the Approved Domain Registry to the Owner for the mandatory Stage -2.1
Owner Checkpoint (Section 8). Do not begin Stage -2.2 (Skill Discovery) until the
Owner responds — silence is not approval (Section 5.3).

### 2026-08-23 — Session 3: Owner Checkpoint response, registry Revision 2

**What was inspected:**
- Owner's Stage -2.1 checkpoint response (Persian).
- Master Plan Section 2.3 (Forbidden Premature Decisions — "Base architecture repo"
  is explicitly listed) and Section 5.1/5.2 (guardrails), to reconcile the Owner's new
  disclosure against Phase -2's no-architecture-lock rule.

**Key findings:**
- Owner confirmed the overall Stage -2.1 registry and both contested drops
  (Spec-driven development, Architecture documentation) as final.
- Owner left DOM-23 (Community management) BLOCKED intentionally — OQ-01 remains
  open, no resolution yet.
- Owner disclosed a final, non-negotiable fact external to Phase -2's own decision
  process: Hermes will be built on the open-source framework
  `NousResearch/hermes-agent`. Recorded in `phase-m2/research-domains.md` under a new
  `## Known Base Architecture` section, reserved as REPO-001, explicitly marked
  "known base architecture, not a discovered candidate," and flagged as the mandatory
  first Stage -2.4 deep-audit target (ahead of the normal triage funnel).
- Confirmed this does not conflict with Section 2.3's "Base architecture repo" ban:
  that section forbids *Phase -2* from choosing/approving the architecture; it does
  not forbid the Owner from having already decided it and disclosing it as a known
  research input. Phase -2 still owes it full adversarial review (Section 13) and
  REUSE/ADAPT/REFERENCE/REJECT classification per capability (P2) — not a rubber
  stamp.
- Reframed 7 domains around this fact: the six the Owner named explicitly (DOM-01
  multi-agent orchestration, DOM-04 skill design, DOM-06 MCP/tool-use, DOM-11 memory
  architecture, DOM-13 long-running reliability/cron scheduling, DOM-16 cost
  control/model routing) plus DOM-02 (agent contracts, tightly coupled to DOM-01/04).
  Also extended the same reframing to DOM-24 (multi-tenant onboarding) on my own
  inference, flagged explicitly as an extension beyond the Owner's named list rather
  than silently folded in.
- For each reframed domain, the Research Question now asks "how does hermes-agent
  implement this, does it satisfy Hermes' needs, what's the gap" instead of "what's
  the best pattern in the world" — outside evidence becomes a comparison baseline,
  not a green-field search. Full detail and rationale in `research-domains.md`
  Revision 2 changelog.
- Registry bumped to Revision 2; 25 domains unchanged in count, none added/dropped
  this round (only reframed + one new known-input entry).

**Next step:**
Report the Revision 2 summary to the Owner, then proceed to Stage -2.2 (Skill
Discovery) once acknowledged — this was not itself flagged as a second blocking
checkpoint by the Owner, but the summary is being surfaced before proceeding per
their instruction ("خلاصه‌ی تغییرات را قبل از رفتن به Stage -2.2 گزارش بده").

### 2026-08-23 — Session 4: Stage -2.2 Skill Discovery

**What was inspected:**
- Owner approved Revision 2 of research-domains.md and confirmed continuing to
  Stage -2.2, plus logged a standing requirement for Stage -2.4 (see the "STANDING
  REQUIREMENT FOR STAGE -2.4" note added to `research-domains.md`'s Known Base
  Architecture section: produce an additional, durable capability-reference document
  for `hermes-agent` sourced only from official docs + code, explicitly because the
  Owner's prior "Hermes Agent Cheat Sheet" PDF was found to contain hallucinated
  content — e.g. a nonexistent `hermes memory reindex` command and a fictitious "GEPA
  reflection loop" — and was discarded; that file must not be used as a source).
- Executed Stage -2.2 per Section 8/9.1/15.1: fetched the full someclaudeskills.com
  gallery (181 skills), then inspected 32 skills beyond title/description — the 18
  Section 15.1 suggested leads in full, plus 14 selected via Hidden Pattern Mining
  against Hermes' behavioral principles and the domain registry.

**Key findings:**
- `phase-m2/skill-catalog.md` created: 32 Section 9.1 records. Classification:
  24 ADAPT, 6 REFERENCE, 2 REJECT, 0 REUSE (expected — all evidence is single-source
  docs, not code-verified, so nothing cleared the bar for direct adoption).
- 5 Strong Candidates (score >=80) completed full Section 13 adversarial review +
  Section 14 role-simulation notes per the mandatory rule: SKL-012 Human Gate
  Designer (82), SKL-021 Skillful Subagent Creator (80), SKL-027 Crisis Detection
  Intervention AI (80) + SKL-028 Crisis Response Protocol (81, reviewed jointly),
  SKL-030 Checklist Discipline (84, best-evidenced candidate in the pass — grounded
  in independently-verifiable real-world outcomes, not just vendor claims).
- Best hidden-pattern-mining win: the Crisis Detection/Response pair (mental-health
  crisis-intervention skills) transplants a mature "detect risk, assess before
  acting, escalate to human with calibrated severity" mechanism directly onto DOM-09
  (ambiguity/clarification). Explicitly flagged one part NOT to carry forward: that
  pair's 30-day auto-delete data policy directly conflicts with DOM-11's never-delete
  principle — noted so it isn't accidentally adapted in at Stage -2.5.
- `phase-m2/deduplication-map.md` created: 5 capability clusters. One genuine
  redundancy resolved (Cluster 1, four near-identical skill-authoring-methodology
  skills — canonical SKL-009 Skill Architect, two kept as secondary references for
  distinct contributions). Two "pipeline" clusters (cost governance; crisis
  detect+respond) explicitly NOT resolved to a single canonical, since their members
  are complementary stages, not competing implementations — documented as an
  exception to the usual canonical-selection rule rather than forced.
- `phase-m2/rejected-candidates.md` created: 2 rejections. REJ-001 Launch Readiness
  Auditor (out of Phase -2 scope — SDLC/build-readiness tool, not a Hermes runtime
  capability). REJ-002 Modern Auth 2026 (title suggested DOM-08 relevance;
  actual mechanism is end-user consumer login, not the machine-to-machine
  platform-credential isolation DOM-08 actually needs — a deliberate example of the
  "don't rate by title" discipline).
- `phase-m2/source-register.md` created (first use this phase): 3 entries, including
  an explicit flag that the underlying `erichowens/some_claude_skills` GitHub repo
  was never cloned/inspected — every skill record's Evidence Quality is capped at
  Medium for this reason, and that repo is registered as a Stage -2.3 candidate to
  raise the evidence ceiling later if warranted.
- Documented, not papered over: 3 real coverage gaps from this stage — DOM-11
  (append-only memory/audit-log architecture — no skill in the 181-title gallery
  addresses this at all), DOM-03/DOM-20 (narrative/multi-modal content generation —
  same), DOM-08 (one candidate screened and rejected as a mismatch, still open).
  Domains DOM-05, DOM-12, DOM-21, DOM-24, DOM-25 also got no coverage this stage
  (DOM-23 untouched, remains BLOCKED per Owner instruction on OQ-01).
- No escalations triggered. No new open questions logged (the auto-delete/DOM-11
  tension was handled as an inline adaptation caveat within SKL-027's record, not
  escalated, since it's a "don't copy this part" flag rather than an unresolved
  scope question).

**Next step:**
Stage -2.2 exit criteria met (high-signal coverage across most of the registry;
alternate-query passes on the cost/reliability/human-control clusters were producing
diminishing new signal by the third batch). Report Stage -2.2 summary to Owner; await
direction on Stage -2.3 (Open Repository / Project Discovery) — noting REPO-001
(`NousResearch/hermes-agent`) is already reserved as the mandatory first Stage -2.4
deep-audit target regardless of Stage -2.3's own discovery funnel.

### 2026-08-24 — Session 5: Stage -2.3 Open Repository / Project Discovery

**What was inspected:**
- Owner acknowledged the Stage -2.2 summary, confirmed OQ-01 (DOM-23) stays BLOCKED
  pending a separate answer, and directed continuation to Stage -2.3, restating that
  REPO-001 (`NousResearch/hermes-agent`) remains the mandatory first Stage -2.4
  deep-audit target regardless of Stage -2.3's own discovery.
- Executed Stage -2.3 per Section 8/9.2/15.2: split the 23 active (non-BLOCKED)
  domains into 6 clusters and ran parallel discovery passes on each, per Section 15.2
  (no mandatory repo list, no assumed relevance, broad category search seeds only).
  Each pass triaged candidates against the Section 9.2 repository schema and declared
  per-domain saturation independently (>=2 alternate-query rounds before stopping).
  REPO-001 itself was explicitly excluded from re-discovery in every pass (already
  reserved); passes for the 8 domains reframed around it (DOM-01/02/04/06/11/13/16/24)
  were instructed to find *comparison baselines*, not to re-litigate the base
  architecture choice.

**Key findings:**
- `phase-m2/repo-catalog.md` created: 49 records (REPO-002 through REPO-050).
  Classification: 24 DEEP AUDIT, 19 REFERENCE ONLY, 6 REJECT. Every one of the 23
  active domains has >=1 candidate or a documented gap (Stage -2.3 exit criterion
  met).
- `phase-m2/source-register.md` extended: 28 new non-repo sources (SRC-004 through
  SRC-031) — official docs, papers, vendor writeups, and curated indices cited
  alongside the repo candidates.
- `phase-m2/rejected-candidates.md` extended: 6 new full Section 9.7 records (REJ-003
  through REJ-008) for the substantively-inspected rejections.
- **Verification catch:** one discovery pass (Cluster F, scaling/self-maintenance)
  surfaced a GitHub issue on REPO-001 itself (`NousResearch/hermes-agent` #34352)
  making a striking claim — stock hermes-agent has no tenant isolation, with a cited
  production data-leak incident. Given this project's prior burn history with
  hallucinated hermes-agent claims (the discarded cheat-sheet PDF, see Revision 2 of
  `research-domains.md`), this was independently verified directly against GitHub via
  `gh issue view`/`gh repo view` before being accepted rather than taken from the
  discovering fork's summary alone. Confirmed real: the issue, its 24 comments, and
  two derivative third-party projects (`NimbleCoAI/hermes-agent` fork and
  `NimbleCoAI/hermes-swarm-map`) all genuinely exist. This is now logged as a
  verified, source-level fact in `research-domains.md`'s Known Base Architecture
  section (not an escalation — informational, doesn't require Owner authorization to
  proceed research, but too significant to leave buried in a fork transcript) and as
  SRC-028, with the specific incident claim inside the issue kept distinctly labeled
  as reported/unverified per the FACT vs. CLAIM discipline (Section P5).
- Three domains got their coverage explicitly confirmed as **thin/gap, not silently
  skipped**: DOM-09 (ambiguity-detection trigger logic — no dedicated repo found
  anywhere, consistent with Stage -2.2's identical finding), DOM-22 (analytics
  feedback loops — concept discussed everywhere, no inspectable implementation
  found), DOM-18 (competitive/audience research — only thin embedded-subsystem
  coverage via a DOM-19 candidate, open question for Stage -2.5/-2.6 whether that
  satisfies the domain).
- Strongest candidates this stage (cross-cutting multiple domains, real code, real
  maintenance signal): `microsoft/agent-governance-toolkit` (DOM-05/07/08),
  `google/adk-python` (DOM-01/02/06), `jshiv/cronicle` (DOM-13/11/16/06),
  `indranilbanerjee/digital-marketing-pro` (DOM-19/18), `langchain-ai/social-media-agent`
  (DOM-07/21/19/20 — an unusually close structural analog to Hermes' entire
  content-generation-agent shape, found via a cross-cluster flag and independently
  verified before being added to the catalog).
- No escalations triggered this session. No new open questions logged — the DOM-24
  finding above is a resolved/verified fact, not an unresolved question.

**Next step:**
Stage -2.3 exit criteria met (all materially relevant candidates triaged; every
active domain has source coverage or a documented gap; all 6 discovery clusters
independently declared saturation). Report the Stage -2.3 summary — including the
REPO-001 tenant-isolation finding — to the Owner; proceed to Stage -2.4 (Deep
Repository Audit) once acknowledged, auditing REPO-001 first per the standing
requirement, before its two derivative forks (REPO-040, REPO-041).

### 2026-08-24/25 — Session 6: Stage -2.4 Deep Repository Audit

**What was inspected:**
- Owner directed continuation to Stage -2.4, with three explicit instructions:
  keep all existing decisions/constraints, independently verify the REPO-001
  memory-isolation concern with direct evidence (not just the GitHub issue),
  clearly separate confirmed findings from assumptions, and stop after the
  stage for approval before Stage -2.5.
- Before delegating, the primary session personally cloned `NousResearch/
  hermes-agent` and directly verified the tenant-isolation question via code
  (`gateway/profile_routing.py`, `docs/profile-routing.md`) and GitHub API
  (`gh api`/`gh issue view`/`gh pr view`) rather than trusting the Stage -2.3
  fork's summary of the issue. Finding: the blanket "no tenant isolation"
  reading is partially outdated — a profile-routing/multiplexing mechanism was
  merged into mainline 2026-08-10/11 (after the issue was filed), giving real
  per-profile isolated memory/sessions, but it is opt-in and config-heavy. The
  finer-grained automatic fix the issue's own thread names as "the core fix"
  (PR #47552, `context_id` memory scoping, opened by NimbleCoAI from their
  fork) remains open/unmerged in mainline as of access date.
- Executed Stage -2.4 per Section 8/9.3: all 24 DEEP AUDIT repos from
  `repo-catalog.md` plus REPO-001 itself (25 repos total) were deep-audited via
  actual `git clone` + direct source/test/doc reading — never README alone —
  across 6 parallel passes (one per Stage -2.3 cluster, plus a dedicated
  REPO-001+REPO-040+REPO-041 pass given their priority and interdependency).
  One fork (the REPO-001 trio) hit a session-limit API error partway through;
  it had already written 3 of its 4 required files (REPO-001's audit, the
  capability-reference document, and REPO-040's audit) before failing — the
  primary session completed the missing 4th file (REPO-041,
  `hermes-swarm-map`) directly, continuing the same clone-and-verify method
  and cross-referencing the other three files' findings.

**Key findings:**
- `phase-m2/repo-audits/` created: 26 files (25 A-J audit records + the
  standing-requirement capability-reference document for REPO-001). Every DEEP
  AUDIT repo has a completed audit with FACT/INTERPRETATION/UNKNOWN labeling
  per Section P5 and an Evidence section stating doc-vs-code (dis)agreement —
  Stage -2.4's exit criterion.
- **DOM-24 finding, now fully resolved with direct multi-source evidence:**
  the three-repo REPO-001/040/041 story is coherent and verified end-to-end.
  REPO-001 (upstream): isolation exists but is config-heavy, the lighter
  automatic fix is an open PR. REPO-040 (`cyborg-garden/hermes-agent-mt` — org
  renamed from NimbleCoAI, a real correction caught this stage, GHCR images at
  the old org are frozen/stale, a real deployment trap): is that exact fix,
  real and tested (dedicated test files, active edge-case-hardening commits),
  running in production, pending upstream merge. REPO-041
  (`hermes-swarm-map`): a fleet-orchestration control plane that deploys
  REPO-040 (not plain REPO-001) **by default** — verified directly in its
  Docker image config and test assertions, not assumed from its README.
- **REPO-001 itself:** narrow-waist plugin architecture (Strong), no typed
  role/contract abstraction for DOM-02 (Moderate), a real but off-by-default
  approval-gate for memory/skill writes (Moderate for DOM-07, publish-specific
  gating UNKNOWN — not found, not confirmed absent), and — a new, actionable
  finding — `hermes_state.py` ships a real, permanent session/transcript
  auto-deletion mechanism (`maybe_auto_prune_and_vacuum`, default 90-day
  retention) that is off by default but would directly violate Hermes' never-
  delete principle if an operator ever enables it. A recurring cross-cutting
  pattern was flagged across three dimensions: hermes-agent repeatedly ships
  the *mechanism* for safety/isolation properties Hermes needs, but defaults
  it off — meaning Hermes cannot rely on defaults alone and would need an
  enforced configuration profile or a fork.
- Several Stage -2.3 triage characterizations were corrected on real
  inspection (both directions — some strengthened, some weakened): AgentWard
  and confidence-escalation are staler than "active" suggested (commits from
  April/May 2026, not current); pr-agent's auto-approve/block logic exists in
  code but is disabled on the live path (advisory comment-poster, not an
  enforced gate — a correction to its DOM-15 characterization); ALwrity has no
  LICENSE file at all (catalog incorrectly said MIT); LiteLLM is dual-licensed
  (MIT core + separately-licensed enterprise/ carve-out); postiz-app's
  retry/rollback for publishing was CONFIRMED real and unusually sophisticated
  (differentiated Temporal retry policies by operation reversibility) —
  resolving Stage -2.3's biggest open evidence gap; cronicle's log-rotation
  conflict with DOM-11 was CONFIRMED and found stronger than flagged (its own
  code/docs treat the rotated-and-eventually-deleted log as the authoritative
  record, not just a disposable cache); DOM-18's coverage gap was RESOLVED
  (digital-marketing-pro's competitive-research code is real, verified
  non-trivial synthesis, not a static-data wrapper).
- `phase-m2/repo-catalog.md` updated in place with 4 factual corrections
  surfaced by deep audit: ALwrity license, LiteLLM license, the NimbleCoAI ->
  cyborg-garden org rename (with the GHCR staleness trap noted), and DOM-18's
  gap status changed from open to resolved.
- No escalations triggered. No new open questions logged as ESCALATIONS —
  several genuine UNKNOWNs were logged as explicit Stage -2.5/-2.6 follow-ups
  inside the relevant audit files instead (e.g. whether hermes-agent's
  memory-deletion call sites are user-command-only or autonomously reachable;
  whether any of the three cost-tracking subsystems found this stage
  [hermes-agent's billing, LiteLLM's — already confirmed enforcing — and
  Swarm Map's budget-check] actually enforce vs. only report).

**Next step:**
Stage -2.4 exit criteria met (every DEEP AUDIT repo has a completed A-J file
with Evidence-section doc-vs-code findings; the standing capability-reference
deliverable is complete). Per the Owner's explicit instruction, STOP here and
report to the Owner for approval before proceeding to Stage -2.5 (Pattern
Extraction).

### 2026-08-25 — Session 7: Stage -2.5 first attempt — failed, unrecovered (retroactive entry)

**What was inspected:**
- All 26 `phase-m2/repo-audits/` files plus `skill-catalog.md`, in six parallel
  forks split by the Stage -2.3 cluster structure (A-F), attempting Stage -2.5
  pattern extraction per Section 8/9.4.

**Key findings:**
- All six forks completed their extraction work and reported back a combined
  44 pattern records in chat, but none of the six ever called `Write` — no
  fork persisted its output to a file. The coordinator accepted the chat
  summaries, made follow-up `SendMessage` calls asking forks to re-paste
  content already covered (re-billing each fork's full inherited context per
  round-trip), and eventually moved on without ever creating
  `phase-m2/pattern-catalog.md` or any equivalent file.
- Result: the entire 44-record catalog is unrecoverable — it exists nowhere
  on disk. ~1.95M fresh tokens were spent producing output that was then
  lost. Verified directly from local session transcripts under
  `/root/.claude/projects/-root-m2-research-workspace/.../subagents/`.
- Root cause and fix are recorded in full in `AGENT-OPERATIONS.md` (Changelog
  entry "2026-08-25 — Write-before-return rule adopted; Stage -2.5
  incident"), which was created *because of* this incident. That file's Active
  Rule 1 (write-before-return) is now mandatory for all sub-agents; Active
  Rule 5 (RTK, opt-in) and the lean-ctx/document-graph evaluations were
  decided the same day as follow-on tooling work, unrelated to this failure.
- **Process note (why this entry is retroactive):** this session's outcome
  was recorded in `AGENT-OPERATIONS.md` but never logged here in the Session
  Log at the time, breaking the "update once per session" journal rule
  (Master Plan Section 6.1/24). Caught and backfilled 2026-08-28 during a
  routine status check, at the Owner's request.

**Next step (as of 2026-08-25, superseded by Session 8):**
Stage -2.5 needed to be redone from scratch under the new write-before-return
rule. Not attempted again until Session 8 below.

### 2026-08-28 — Session 8: Stage -2.5 redone; Stage -2.4(b) dedup catch-up

**What was inspected:**
- Owner directed a full autonomous continuation: redo Stage -2.5 from the 26
  audit files under the write-before-return rule, backfill the Session 7
  journal gap (done above), and proceed through subsequent stages on my own
  judgment, reporting progress rather than waiting for a go-ahead at each
  step.
- Re-executed Stage -2.5 per Section 8/9.4: six parallel forks, one per
  Stage -2.3/-2.4 cluster (A-F), each scoped to its cluster's audit files
  plus relevant skill-catalog records, each bound by the mandatory
  write-before-return rule (AGENT-OPERATIONS.md Active Rule 1) — write to a
  scratch file before returning, return only a short chat confirmation. All
  six wrote successfully this time; verified by reading each scratch file
  directly rather than trusting the chat summaries.
- Merged all six clusters' raw records into the canonical
  `phase-m2/pattern-catalog.md`, assigning final sequential `PAT-001`
  through `PAT-051` IDs (cluster order A-F), fixing internal
  "Alternative Patterns" cross-references to the new IDs, and reconciling
  each cluster's "Cross-Cluster Notes" against what the target cluster
  actually extracted.
- Also closed a process gap found while reviewing Section 11.1: the
  mandatory dedup pass after Stage -2.4 completion (trigger b) was never
  run — `deduplication-map.md` still only reflected the Stage -2.2
  skill-level pass. Ran it now, at repo level, using the just-finished
  pattern catalog as supporting evidence.

**Key findings:**
- `phase-m2/pattern-catalog.md` created: 51 pattern records (21 STRONG
  CANDIDATE, 21 CANDIDATE, 5 CONTEXT-DEPENDENT, 1 AVOID, 3 INSUFFICIENT
  EVIDENCE — the 3 INSUFFICIENT EVIDENCE records are deliberate
  gap-documentation, not weak candidates forced to fill a slot). All 21
  STRONG CANDIDATE records carry completed Adversarial Review (Section 13)
  and three-role Role Notes (Section 14) with disagreements preserved, not
  averaged away. Every record has Failure Modes and Human-Control
  Implications populated. Gate G5 self-check included in the file.
- 23 of 24 active domains (all except BLOCKED DOM-23) have >=1 pattern
  record. 3 of those 23 (DOM-11, DOM-22, DOM-25) have only
  gap-documentation, no positive candidate — carried forward explicitly per
  Section P2/P5, not silently dropped. DOM-11 in particular is now backed
  by two independent code-verified negative examples (REPO-001's
  `maybe_auto_prune_and_vacuum`, cronicle's lumberjack log rotation) naming
  the exact failure mode the domain guards against, sharper than Stage
  -2.2/-2.3's identical "no solution found" finding.
- Best cross-cutting finding this stage: DOM-02's research question ("does
  hermes-agent enforce or merely suggest a structured-output contract?") now
  has a direct, confirmed answer — no, REPO-001 has no such mechanism
  (PAT-003's "Observed In" list conspicuously excludes it) — while three
  independently-built comparison frameworks (pydantic-ai, adk-python,
  openai-agents-python) converge on the same well-evidenced solution. A
  second recurring cross-cutting theme, now confirmed independently in three
  separate places (PAT-020/write-approval, PAT-021/auto-prune, PAT-046/
  profile-routing, PAT-048/Swarm Map's own structural answer to the same
  problem): hermes-agent repeatedly ships the *mechanism* for a safety/
  isolation property Hermes needs, but defaults it off — meaning Hermes
  cannot rely on defaults alone and needs an enforced configuration profile
  or a fork.
- The six forks' own "Cross-Cluster Notes" were reconciled during merge: 11
  flags were confirmed resolved by the target cluster's actual extraction
  (documented in pattern-catalog.md's Cross-Cluster Reconciliation table); 6
  remain genuinely unresolved open items, logged explicitly rather than
  assumed closed (e.g. agentward's pre-deployment dependency scanner never
  independently verified against DOM-17; wind-comic's Director-agent role
  never read in full against DOM-01; a three-way orchestration-granularity
  comparison — PAT-001 vs. PAT-034 vs. PAT-042 — that no single cluster's
  evidence is positioned to resolve).
- `phase-m2/deduplication-map.md` extended with 4 new repo-level clusters
  (Clusters 6-9), closing the Section 11.1 trigger-(b) gap: general-purpose
  agent-orchestration SDKs (langgraph/openai-agents-python/pydantic-ai/
  adk-python — all four kept as independent comparison-baseline sources, no
  canonical needed, since none is an adoption candidate against the already-
  fixed REPO-001 base architecture); narrative/multi-modal content-generation
  pipelines (ViMax canonical, wind-comic and GOAT-Storytelling-Agent as
  secondary references); social-media publish-mechanics platforms
  (postiz-app and brightbean-studio kept co-primary — offsetting evidence
  strengths, not a forced single pick); human-control/governance-policy
  frameworks (agent-governance-toolkit/humanlayer/agentward, again no
  canonical since none is adoptable as-is). One considered-but-rejected
  cluster (digital-marketing-pro vs. ALwrity) logged for transparency rather
  than silently dropped.
- No escalations triggered. No new open questions logged as ESCALATIONS —
  the 6 unresolved cross-cluster flags were logged as Stage -2.6/-2.7
  follow-ups inside `pattern-catalog.md` itself, consistent with how Stage
  -2.4's own genuine UNKNOWNs were handled.

**Next step (superseded below, same session):**
Stage -2.5 exit criteria met (Gate G5 self-check complete in
`pattern-catalog.md`). Per the Owner's standing instruction to continue
autonomously and report progress rather than pause for a go-ahead,
proceeding directly to Stage -2.6 (Capability Matrix).

### 2026-08-29 — Session 8 (cont.): Stage -2.6 Capability Matrix, Stage -2.7 Synthesis, Exit Gate — Phase -2 end-of-phase

**What was inspected:**
- Continued the same autonomous run after a session-usage-limit reset;
  re-verified Stage -2.5's output was intact and committed (git log showed
  it auto-backed-up) before continuing, per no-repeat-completed-work
  discipline.
- Built Stage -2.6 per Section 8/A.4: one capability-matrix row per
  Hermes research need x best-evidenced candidate, drawn directly from the
  finished `pattern-catalog.md`, citing PAT-/REPO-/SKL-/SRC- IDs throughout.
- Built Stage -2.7 per Section 8: assembled the capstone report and
  decision file, ran a synthesis-level Skeptic pass across the whole reuse
  stack (in addition to the per-pattern Section 13/14 review already
  completed at Stage -2.5), and self-checked the Section 18 Exit Gate.

**Key findings:**
- `phase-m2/capability-matrix.md` created: ~55 rows across 24 active
  domains (DOM-23 excluded, BLOCKED). Only 3 rows use REUSE (PAT-001,
  PAT-005, PAT-024) — mechanisms confirmed present and functioning in
  REPO-001 with no off-by-default caveat. A deliberate matrix rule: a
  shipped-but-disabled-by-default mechanism (write-approval, tenant
  isolation, etc.) is scored ADAPT/LIGHT, not REUSE, since the Owner's
  behavioral principles require it to actually be turned on and verified —
  a config flip is not zero-cost reuse. Gate G6 self-check included in the
  file.
- `HERMES-REUSE-STACK.md` (root) created: REUSE/ADAPT/REFERENCE/REJECT/
  UNKNOWN buckets mirroring the matrix's candidate set, each entry citing
  record IDs per Section 16.3. The synthesis-level Skeptic pass surfaced
  three cross-cutting items no single pattern's own review could see on its
  own: (1) the "ships mechanism, defaults off" theme recurs 5 separate
  times across REPO-001/derivatives (write-approval, auto-prune, profile
  isolation, context-scoped memory, cost enforcement) — Hermes needs one
  deliberate, audited configuration profile turning all of them on
  together, not five independent opt-ins assumed safe in isolation, and
  this is now flagged as the single highest-leverage early Phase -1 action;
  (2) AGPL-3.0 exposure clusters around both of PAT-035's source repos,
  worth one licensing review rather than per-candidate; (3) the
  orchestration-granularity question (PAT-001 vs. PAT-034 vs. PAT-042) is
  asked three times across the catalog and answered zero times — surfaced
  once here as a single open design question.
- `phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md` created: full 24-section
  capstone per Section 16.2, synthesizing all nine prior deliverables into
  an executive narrative without duplicating their full detail.
- `phase-m2/downstream-handoff.md` created with all 10 required contract
  items (Section 19.2) and a full Section 18 Exit Gate self-check: **X1
  through X10 all HOLD.** Exit status determined as
  **M2-CONDITIONALLY-COMPLETE** — not M2-COMPLETE, because real, non-
  blocking unknowns remain (OQ-01/DOM-23 still BLOCKED on an Owner scope
  question; DOM-11/DOM-22/DOM-25 have documented gaps, not candidates) —
  and not M2-INCOMPLETE, since X1-X7 all hold and none of those unknowns
  blocks Phase -1's fit/adaptation analysis from starting on everything
  else. Full rationale and per-condition verification in the file itself.
- No escalations triggered this session. OQ-01 remains the one standing
  blocking item, unchanged from Stage -2.1 — not newly raised, just
  reconfirmed still open at phase-end per the handoff's own Section 8 (Open
  Questions) requirement to distinguish blocking from non-blocking.

**Next step:**
Phase -2 exit criteria met at CONDITIONALLY-COMPLETE status. Per CLAUDE.md's
reporting cadence, this is the end-of-phase report: capstone + reuse stack +
exit status + handoff summary, reported to the Owner in this session with
the mandatory Owner-Relay Block. Awaiting Owner acknowledgment/direction on
OQ-01 and the three documented gaps before Phase -1 begins — that decision
belongs to the Owner and to Phase -1's own scope, not to this phase.

### 2026-08-29 — Session 8 (cont.): Post-phase-end accuracy correction — PAT-021 conflation

**What was inspected:**
- The Owner asked for a detailed breakdown of the "five ships-mechanism-
  defaults-off" findings cited in the phase-end report. Answering that
  question directly surfaced that PAT-021 (the session/transcript
  auto-prune guard) had been incorrectly grouped with the other four
  findings under one "needs to be turned on" framing — PAT-021 is a
  destructive mechanism whose off-by-default state is the *correct,
  currently-protective* one; it must be locked off, never enabled. The
  Owner then asked whether this error was only in the chat summary or
  also written into the completed deliverables.
- Grepped and read the exact surrounding text in all three deliverables
  named in the Owner's question — `HERMES-REUSE-STACK.md`,
  `phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md` (Executive Summary and
  Section 22 Risks, checked separately since they're independent
  passages), and `phase-m2/downstream-handoff.md` Section 4 — before
  reporting back, rather than answering from memory of having written
  them.

**Key findings:**
- The imprecise framing was confirmed present in **four** locations across
  three files, not just the chat recap:
  1. `HERMES-REUSE-STACK.md`, Synthesis-Level Skeptic Pass item 1 (no
     hedge — called PAT-021 a "real protective mechanism" in the same
     sentence that correctly labels it REJECT).
  2. `phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md`, Executive Summary
     (no hedge).
  3. `phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md`, Section 22 Risks
     (partially self-corrected — already hedged the cost-enforcement case
     with "or leave its enforcement status unconfirmed" — but still ended
     with "turn all of them on together," which still misstated PAT-021).
  4. `phase-m2/downstream-handoff.md`, Section 4 (Candidate Assumptions
     Register) — no hedge; contained the clearest single misstatement,
     "none of them protect anything," which is backwards for PAT-021
     specifically.
- Root cause: the original synthesis-level Skeptic pass (Stage -2.7)
  correctly labeled PAT-021 as REJECT everywhere it was scored
  individually, but when writing the *cross-cutting* cumulative-risk
  finding across all five REPO-001 "ships mechanism" instances, the
  individual-record correctness didn't carry through to the summary
  language — a compression error at the synthesis layer, not a finding
  that was wrong at the source (every individual PAT-021 record, in
  `pattern-catalog.md` and `HERMES-REUSE-STACK.md`'s own REJECT section,
  was and remains correctly stated).
- Fixed all four locations per the Owner's explicit correction, which also
  sharpened a related, previously-blurred distinction: PAT-028/PAT-051
  (cost enforcement) is not "off by default" in the same sense as
  PAT-020/PAT-046/PAT-047 — its enforcement status is genuinely
  UNCONFIRMED in either direction, not confirmed-present-but-disabled.
  All four corrected passages now distinguish three cases (protective/
  needs-enabling; destructive/needs-locking-off; status-unconfirmed/
  needs-investigation) instead of one uniform bucket, and each correction
  is marked inline with a "[Corrected 2026-08-29]" note pointing back to
  this entry, per the Owner's instruction that this be a traceable,
  non-silent edit to a completed deliverable.

**Next step:**
No further action required on this correction — all four flagged
locations fixed and cross-referenced to this entry. Phase -2 remains at
M2-CONDITIONALLY-COMPLETE; the correction changes the framing of one
cross-cutting risk finding, not the exit status or any individual pattern
record's classification (PAT-021 was already correctly scored REJECT
everywhere except the four cross-cutting summary passages just fixed).
Still awaiting Owner direction on OQ-01 and the three documented gaps
before Phase -1 begins.

### 2026-08-29 — Session 8 (cont.): OQ-01 resolved — DOM-23 excluded

**What was inspected:**
- The Owner resolved OQ-01 directly: DOM-23 (community/audience-engagement
  automation — replying to comments or DMs) is explicitly out of scope for
  Hermes. No comment-or-DM-reply functionality exists in the current
  system design; this was never part of the intended scope.
- Updated the three files the Owner named — `phase-m2/open-questions.md`,
  `phase-m2/research-domains.md`, `phase-m2/downstream-handoff.md` — to
  record this as a deliberate, resolved scope boundary, not an unresolved
  gap, per the Owner's explicit instruction on the distinction.

**Key findings:**
- `phase-m2/open-questions.md`: OQ-01 moved from "Open Questions" to a new
  "Resolved Questions" section, full resolution text recorded, dated
  2026-08-29.
- `phase-m2/research-domains.md`: bumped to Revision 3. DOM-23's registry-
  table status changed BLOCKED -> EXCLUDED; its full domain definition
  block rewritten to state the resolution plainly (Research Question now
  N/A/moot, Priority N/A, no further discovery work warranted); added a
  Revision 3 reconciliation log entry per Section 7.3's change-control
  requirement (date, justification, affected record, source of change).
- `phase-m2/downstream-handoff.md`: three updates. (1) Exit Gate
  Determination section rewritten — OQ-01 no longer cited as a reason for
  CONDITIONALLY-COMPLETE; the sole remaining reason is now DOM-11/22/25's
  documented gaps. Exit status itself is unchanged (still
  M2-CONDITIONALLY-COMPLETE — those three gaps are real, non-blocking
  unknowns independent of OQ-01). (2) X7's verification text updated to
  say OQ-01 is RESOLVED as an exclusion, not merely "preserved, not
  dropped." (3) Section 8 (Open Questions) — the "Blocking" category now
  reads "none remain," with OQ-01's resolution stated directly.
- **Flagging, not fixing, a related but distinct issue noticed while
  editing:** `downstream-handoff.md` Section 9 (Hermes Implications)
  contains "Hermes' fixed base architecture ships real mechanisms for all
  three of its named behavioral principles, but none is safe to trust as a
  default" — this was not one of the four locations covered by today's
  earlier PAT-021 correction (that pass covered the reuse-stack synthesis
  item, the capstone's Executive Summary and Section 22, and this same
  file's Section 4). This sentence has the same shape of imprecision
  applied to "principles" rather than "mechanisms": the never-delete
  principle's own mechanism (the auto-prune guard) being off by default is
  *currently* what's trustworthy about that principle specifically, so
  "none is safe to trust as a default" overstates it for that one case.
  Left unchanged pending explicit direction, consistent with not expanding
  today's requested scope unprompted.

**Next step:**
No further action required on the OQ-01 resolution — all three requested
files updated and cross-referenced to this entry. Phase -2 remains at
M2-CONDITIONALLY-COMPLETE, now solely on the strength of the DOM-11/22/25
documented gaps. The Section 9 imprecision noted above is reported to the
Owner for a decision, not acted on unilaterally.

**Addendum (same session, moments later): Section 9 imprecision fixed.**
The Owner confirmed the flagged `downstream-handoff.md` Section 9 sentence
should be corrected on the same three-case logic as the earlier PAT-021
fix. Rewrote the sentence: it no longer applies one uniform "not safe to
trust as a default" framing across all three behavioral principles.
Irreversible-action confirmation and cost control keep the original
implication (shipped mechanisms are off by default, genuinely need
enabling and verifying). Never-delete is now stated correctly as the
inverse: its shipped mechanism (auto-prune) being off *is* the currently-
trustworthy, protective default, and the early Phase -1 action for that
one is confirming it stays locked off, not enabling it — explicitly
naming the risk that treating all three as equally untrustworthy could
lead to enabling auto-prune, which is the one case where that would be
wrong. Tagged inline with the same "[Corrected 2026-08-29 — see
`HERMES_RESEARCH.md`]" convention used at the four earlier locations.
This is the fifth location total carrying this correction across the
phase's deliverables (the four from earlier this session, plus this one),
all traceable to the same root cause: the synthesis-layer cross-cutting-
finding language didn't carry through the individual-record correctness
that was already present everywhere PAT-021 was scored on its own.

### 2026-08-29 — Session 8 (cont.): Third-round accuracy correction — PAT-047 conflation, exhaustive-search overclaim, repo-count error

**What was inspected:**
- A dedicated skeptical-reviewer pass was run against the same three
  synthesis-level deliverables as the earlier corrections this session —
  `HERMES-REUSE-STACK.md`, `phase-m2/HERMES-CAPABILITY-INTELLIGENCE-M2.md`,
  `phase-m2/downstream-handoff.md` — deliberately given no prior context
  (no access to this journal or `AGENT-OPERATIONS.md`) and instructed to
  distrust confident-sounding prose and hunt specifically for (a) a
  destructive-but-currently-safe mechanism grouped with genuinely
  protective ones as needing the same treatment, or (b) any other blanket
  generalization applied across a set of items that doesn't hold for
  every member. Read-only; findings reported back, then fixed in a
  separate, explicitly-authorized follow-up pass.

**Key findings:**
- **PAT-046/PAT-047 conflation, surviving the earlier PAT-021 fix:** the
  same-day PAT-021 correction (previous entry) split "destructive" from
  "protective" cleanly, but the resulting case (a) — "genuinely
  protective, off, needs deliberate verified enabling" — still silently
  grouped PAT-047 in with PAT-020/PAT-046 under "operator explicitly
  configures them on." PAT-047 is not merged into REPO-001 mainline at
  all — it exists only as an open, unmerged upstream PR (#47552) and as a
  running fix in a third-party fork (`cyborg-garden/hermes-agent-mt`,
  REPO-040). There is no stock-deployment switch to flip; the real choice
  is wait for the PR to merge, depend on the fork, or reimplement
  independently — categorically different from a config flip, and already
  reflected correctly in PAT-047's own individual record (MEDIUM
  adaptation, "depending on the cyborg-garden fork's ongoing maintenance,
  or reimplementing the fix independently") the whole time. Found in the
  same three locations the PAT-021 correction touched (reuse-stack.md's
  Skeptic Pass item 1, the capstone's Executive Summary and Section 22,
  downstream-handoff.md Section 4), plus a fourth the PAT-021 pass didn't
  touch (downstream-handoff.md Section 10's "configuration profile (or
  targeted fork)" phrasing, which still described PAT-047 as an
  off-by-default REPO-001 mechanism).
- **"Exhaustively-searched" overclaim:** the capstone's Executive Summary
  and Section 21 header labeled all three knowledge gaps (DOM-11, DOM-22,
  DOM-25) "exhaustively-searched" as a set. This was already contradicted
  by wording elsewhere in the same document set — `HERMES-REUSE-STACK.md`'s
  own DOM-22 entry says "flagged as a real, not exhaustively-searched,
  gap," and the capstone's own DOM-25 bullet, two lines below the
  overclaim in the same section, names a specific unexamined internal
  candidate (`hermes curator`/`hermes journey`) as "a real remaining
  follow-up before concluding this is a true external gap." Only DOM-11 —
  backed by a consistent no-solution finding across three separate stages
  — actually supports the claim.
- **Repo-count error:** "26 deep-audited repos" appeared three times
  (`HERMES-REUSE-STACK.md`'s DOM-22 entry; capstone Sections 15 and 21),
  every time specifically when citing DOM-22's search coverage,
  contradicting the correct count of 25 (24 discovered + REPO-001, with
  explicit supporting arithmetic in Section 7) stated in the capstone's
  Executive Summary and Section 7.

**Why the PAT-047 issue survived the earlier correction round:** the
PAT-021 correction was scoped exactly to the axis the Owner's follow-up
question had surfaced — is a given mechanism destructive or protective —
and it re-audited every location where *that* conflation appeared,
correctly fixing all of them (five locations, then a sixth in the
same-session addendum). It did not re-audit the other axis buried inside
the same "case (a)" bucket: whether every member of that bucket actually
ships in REPO-001 at all. PAT-047 passed the destructive/protective check
cleanly (it genuinely is protective), so nothing about the PAT-021
correction would have touched it — it fails a different, unasked
question. This is the same root cause named in the PAT-021 entry above —
a compression error at the synthesis layer — recurring in a new spot:
fixing one specific misstatement in a cross-cutting summary doesn't
automatically re-verify that summary's surrounding generalization against
every *other* way it could be wrong. The exhaustive-search overclaim and
the repo-count error are unrelated to PAT-021 entirely and were never in
scope for either earlier correction pass — they live in different
sections (Knowledge Gaps; Social-Media-Specific Findings) that neither
prior pass had reason to touch. All three were caught this time only
because this pass was deliberately scoped to hunt for *any* set-level
overgeneralization, not the one specific issue already on record —
methodologically closer to Section 13's per-pattern adversarial review,
just applied to the synthesis layer for the first time, which is exactly
where every round of this error has occurred so far.

**Fixes applied:**
- All three deliverables' PAT-046/PAT-047 split into a four-way (was
  three-way) breakdown, applied consistently: PAT-047 now has its own
  case/bullet describing the real three-way choice (wait for merge /
  depend on the fork / reimplement independently), not "turn it on."
  `HERMES-REUSE-STACK.md` Skeptic Pass item 1 (new case (d), "Taken
  individually"/"Taken together" summary sentences updated); capstone
  Executive Summary and Section 22 Risks (case renumbered to four,
  now-redundant trailing PAT-047 mention in Section 22 folded into the
  new case (3)); downstream-handoff.md Section 4 (new PAT-047 bullet) and
  Section 10 (dependency decision named explicitly instead of "or
  targeted fork").
- Capstone Section 21 header and DOM-22/DOM-25 bullets reworded: states
  plainly that only DOM-11 was exhaustively searched, and names each
  remaining gap's specific unattempted follow-up (DOM-22: a dedicated
  platform-analytics-ingestion discovery pass; DOM-25: inspecting the
  `hermes curator`/`hermes journey` CLI commands).
- All three "26 deep-audited repos" occurrences corrected to 25.
- All edits marked inline with "[Corrected 2026-08-29 — see
  `HERMES_RESEARCH.md`]" per the established convention, pointing back to
  this entry.

**Next step:**
No further action required — all three requested fixes applied across
all three files, cross-referenced to this entry. Phase -2 remains
M2-CONDITIONALLY-COMPLETE; none of today's corrections change the exit
status or any individual pattern's classification, only the accuracy of
cross-cutting synthesis prose. Worth flagging to the Owner as a pattern
rather than three unrelated slips: this is the third same-day round of
synthesis-layer language drifting away from individually-correct records
underneath it. A possible standing-rule candidate for `AGENT-OPERATIONS.md`
— not adopted here, since it wasn't asked for and isn't this entry's
call to make — is that any cross-cutting paragraph summarizing >=3 items
gets its own explicit per-member re-check before being treated as final,
separate from adversarial review of the individual records it draws
from.
