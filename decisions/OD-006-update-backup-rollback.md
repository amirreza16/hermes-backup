# OD-006 — Every Approved Update Requires Backup and Rollback

**Statement (Owner, verbatim intent):** "Each approved update requires a
backup and a reliable rollback option."

**Decided by:** Owner, final — disclosed 2026-08-25. Paired with OD-004/OD-005
(same "Hermes Control" update flow: suggest -> Owner approves -> applied with
backup + rollback available).

**Classification:** FACT (Owner-stated, external input) — a hard reliability
constraint on how an approved Hermes Control update is applied.

**What this establishes:** even an Owner-approved update must be backed up
before/as applied, and a reliable rollback path must exist afterward. This is
a reliability/reversibility requirement, not just a human-approval
requirement (OD-005 governs *whether* an update happens; OD-006 governs how
safely it is applied once approved).

**INTERPRETATION — connects directly to two separate Stage -2.4 findings that
should now be read together, not as isolated observations:**
1. `nousresearch-hermes-agent.md` Dimension D found unusually detailed
   crash-safety engineering in `hermes_state.py` (WAL checkpoint discipline,
   with inline comments citing a real past corruption incident) — real
   evidence that this class of concern (safe persistence under
   modification) is one hermes-agent's own maintainers have already taken
   seriously, a positive comparison signal for whatever mechanism ends up
   satisfying OD-006.
2. `nimblecoai-hermes-swarm-map.md` Dimension D noted
   `lib/services/db-snapshot-scheduler.ts` — a scheduled backup mechanism for
   that project's own state — not read in full during Stage -2.4, flagged as
   a follow-up. OD-006 raises the priority of actually reading that file at
   Stage -2.5, since it is now a directly on-point comparison candidate
   (backup-before-update, for a system managing Hermes-adjacent agent
   config), not a tangential detail.

This also connects to the Stage -2.5 procedure's own named pattern category
"checkpointed long-running execution" (Master Plan Section 8) — OD-006 is
effectively asking Phase -2 to evaluate candidates against that category
specifically for the *update-application* moment, not just for general
runtime crash recovery.

**Domains affected:**
- **DOM-11** (Append-only memory & audit-log architecture) — a "backup"
  requirement is closely related to, but distinct from, the never-delete
  history principle: a backup exists specifically to allow reverting a
  *deliberate, approved* change, whereas DOM-11 governs the system never
  deleting anything *on its own*. Keep these conceptually separate at Stage
  -2.5/-2.6 even though the evidence sources overlap.
- **DOM-13** (Long-running agent reliability & failure recovery) — rollback
  is a reliability mechanism; hermes-agent's own crash-safety engineering
  and cron/scheduler reliability posture (Dimension D of its audit) are
  directly relevant comparison evidence.
- **DOM-25** (Self-updating ecosystem-intelligence agent design) — the
  backup+rollback requirement applies specifically to Hermes Control's
  update-application step, sharpening what a satisfactory DOM-25 mechanism
  must include beyond the suggest/approve flow already covered by OD-004/005.

**Phase -2 handling:** Flag `db-snapshot-scheduler.ts`
(`nimblecoai-hermes-swarm-map.md` Open Follow-Up #4) as a priority read at
Stage -2.5 given this decision, rather than a low-priority follow-up. No
implementation design of Hermes' actual backup/rollback mechanism follows
from this record — Phase -2 documents which existing patterns satisfy this
requirement and how well.
