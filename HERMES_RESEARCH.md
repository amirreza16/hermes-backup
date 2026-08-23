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
