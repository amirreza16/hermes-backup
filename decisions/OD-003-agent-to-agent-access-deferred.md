# OD-003 — Agent-to-Agent Access Rules Deferred to Implementation Design

**Statement (Owner, verbatim intent):** "Agent-to-agent access rules are
outside the scope of Phase 2 and should be deferred to the implementation
design phase."

**Decided by:** Owner, final — disclosed 2026-08-25.

**Classification:** FACT (Owner-stated, explicit scope-narrowing instruction)
— unlike OD-001/002/004/005/006, this is not a decision *about* Hermes'
design; it is a decision about what Phase -2 should and should not attempt to
resolve.

**What this establishes:** the specific rules governing what one Hermes agent
(or agent instance) may access, request, or do with respect to another
agent/instance are explicitly out of scope for Phase -2's research and
recommendations. This is a Phase -1 (implementation design) concern.

**INTERPRETATION:** this mostly reinforces discipline Phase -2 already
follows (P7 — No Premature Architecture; research stays architecture-neutral)
rather than removing a research direction that was actively being pursued.
Phase -2 was never going to prescribe Hermes' actual access-control rules —
this decision makes that boundary explicit for the specific agent-to-agent
axis, which is useful because DOM-08's evidence (permission/policy-engine
repos like `microsoft/agent-governance-toolkit`, `agentward-ai/agentward`)
could otherwise tempt a Stage -2.6/-2.7 recommendation to get more
prescriptive than Phase -2's mandate allows.

**Domains affected:**
- **DOM-08** (Permissions & least-privilege scoping) — most directly
  affected. Phase -2 continues to catalog *patterns* for capability/permission
  scoping (per P2 — Extract Patterns, Not Products) but must not draft
  specific agent-to-agent access rules for Hermes. The Stage -2.6 capability
  matrix and Stage -2.7 synthesis should note found patterns' applicability
  and explicitly flag rule-design as deferred, rather than silently omitting
  the domain or silently overstepping into rule design.
- **DOM-01 / DOM-02** (Orchestration architecture; agent role & contract
  design) — agent-to-agent access is adjacent to, but distinct from,
  handoff/contract mechanics (which remain in scope — e.g. evaluating
  whether `hermes-agent`'s delegation model or PydanticAI's typed
  handoffs are sound patterns). The *access-control* dimension specifically
  (what one agent is permitted to request of another) is what's deferred,
  not the general contract/handoff research.

**Phase -2 handling:** Continue cataloging DOM-08 patterns and evidence as
normal (this is not a directive to stop researching DOM-08 entirely — only to
stop short of designing Hermes' specific access rules). Every DOM-08 mention
in `capability-matrix.md`, the pattern catalog, and the capstone report must
carry an explicit note that rule-design is deferred to Phase -1, so this
boundary is never silently crossed nor silently lost by omission.
