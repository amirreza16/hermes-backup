# OD-002 — Shared Global Memory + Separate Per-Project Memory

**Statement (Owner, verbatim intent):** "Hermes will have shared global
memory and separate memory for each project."

**Decided by:** Owner, final — disclosed 2026-08-25, outside Phase -2's own
decision process.

**Classification:** FACT (Owner-stated, external input) — a concrete memory-
architecture shape decision, analogous in weight to the base-architecture
disclosure (Section 2.3 forbids Phase -2 from *choosing* this; the Owner
already has, and Phase -2's job is to research around it, not ratify or
re-derive it).

**What this establishes:** at least two memory tiers exist by design — one
shared/global tier (visible across all of Hermes' work) and one per-project
tier (scoped to a specific page/brand/project, not visible to others).

**INTERPRETATION — direct validation of Stage -2.4 evidence, not new
architecture work:** this is materially the same shape already found,
independently, as the real mechanism underlying the strongest DOM-24 evidence
from Stage -2.4:
- `NousResearch/hermes-agent`'s `profile_routing` system (merged 2026-08-10/11)
  gives each routed profile a fully separate memory/session/tool home —
  a coarse version of "separate per-project memory."
- The still-unmerged upstream PR #47552 and its production implementation in
  `cyborg-garden/hermes-agent-mt` (REPO-040) add `context_id`-scoped memory
  *within* a profile, merging global + scoped views on read — this is a much
  closer structural match to "shared global + separate per-project," since it
  explicitly merges a global layer with a scoped layer rather than requiring
  a fully separate profile (and its whole separate `HERMES_HOME`) per project.
- `getzep/graphiti` (REPO-017, DOM-12 comparison baseline) and `mem0ai/mem0`
  (REPO-018) were both catalogued as temporal/fact-scoped memory systems —
  worth re-evaluating specifically against this two-tier shape at Stage -2.5.

This decision does not change what Stage -2.4 found; it gives Stage -2.5
pattern extraction a concrete target shape to evaluate found mechanisms
against, sharpening (not replacing) the existing DOM-11/DOM-12 research
questions.

**Domains affected:**
- **DOM-11** (Append-only memory & audit-log architecture) — the audit-log
  question ("does anything get deleted") now applies to *both* tiers; a
  design that satisfies never-delete for the global tier but not the
  per-project tier (or vice versa) would be a real, reportable gap.
- **DOM-12** (Context engineering for long-running, narratively-continuous
  agents) — continuity now has an explicit two-tier shape to evaluate
  against: does a candidate mechanism cleanly separate global/general
  knowledge from project-specific narrative state, or does it conflate them?
- **DOM-19** (Content strategy, planning & brand consistency) — "project" in
  this decision plausibly maps to "page/brand" in the raw idea's framing;
  Stage -2.5/-2.6 should note this mapping as an INTERPRETATION, not assume
  it as FACT, since the Owner did not explicitly equate the two terms.
- **DOM-24** (Multi-tenant / multi-instance onboarding patterns) — "add a new
  page without a from-scratch project" (the domain's original framing) now
  has a specific memory-architecture shape to satisfy: provisioning a new
  project must yield an isolated per-project memory tier without duplicating
  the shared global tier.

**Phase -2 handling:** Stage -2.5 pattern extraction for DOM-11/12/24 should
explicitly evaluate cataloged patterns (Graphiti, mem0, hermes-agent's
profile/context_id mechanisms) against this two-tier shape and note fit or
gap. No implementation design follows from this record — Phase -2 documents
which existing patterns fit this shape and how well; Phase -1 decides how
Hermes actually implements it.
