# OD-005 — Hermes Control May Only Suggest; Owner Approval Required

**Statement (Owner, verbatim intent):** "Hermes Control may only suggest
updates. Nothing can be updated or removed without the explicit approval of
the owner."

**Decided by:** Owner, final — disclosed 2026-08-25. Directly paired with
OD-004 (same "Hermes Control" function).

**Classification:** FACT (Owner-stated, external input) — a hard human-
control constraint on the review function named in OD-004.

**What this establishes:** Hermes Control's output is advisory only.
Suggestions require explicit Owner approval before anything is updated or
removed — no autonomous update or deletion path exists for this function, by
Owner mandate.

**INTERPRETATION — this directly informs how Stage -2.4's biggest
cross-cutting finding should be read for DOM-25 specifically:**
`nousresearch-hermes-agent.md`'s Cross-Cutting Observation flagged a recurring
pattern: hermes-agent ships real safety/approval mechanisms
(`write_approval.py`) but defaults them **off**, meaning a stock deployment
writes memory/skill changes autonomously unless an operator explicitly
enables the gate. OD-005 makes explicit, for Hermes Control specifically, that
this must NOT be the case — the suggest-only/approval-required behavior is
mandatory, not an optional hardening step. This is a concrete instance of the
"maker-checker" / "human approval gate" pattern category named in Master Plan
Section 8's Stage -2.5 procedure, and should be evaluated at Stage -2.5
against exactly that bar: does a candidate pattern enforce approval
structurally (cannot be silently bypassed), or does it only suggest approval
as a configurable default (as hermes-agent's own `write_approval.py` does)?
The latter would not satisfy OD-005 as stated.

**Domains affected:**
- **DOM-25** (Self-updating ecosystem-intelligence agent design) — primary;
  see above.
- **DOM-07** (Human-in-the-loop approval gates for irreversible actions) —
  a concrete real-world instance of DOM-07's general research question,
  applied specifically to the self-review/self-update surface. Evidence
  gathered for DOM-07 (e.g. `microsoft/agent-governance-toolkit`'s
  `require_approval` policy action, `langchain-ai/social-media-agent`'s
  `interrupt()`-based HITL node with a genuine reject path) should be
  cross-checked against this specific bar: structurally enforced, not merely
  configurable.

**Phase -2 handling:** No implementation design follows from this record.
Stage -2.5/-2.6 should flag, for any pattern proposed as relevant to DOM-25,
whether it meets a "structurally enforced approval, not configurable default"
bar — this is now a concrete evaluation criterion for those two domains, not
a new research direction.
