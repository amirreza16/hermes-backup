# OD-004 — "Hermes Control" Performs Quarterly Reviews

**Statement (Owner, verbatim intent):** "Hermes Control will perform
quarterly reviews of knowledge, guidelines, workflows, tools, integrations,
code, technical components, and other useful developments."

**Decided by:** Owner, final — disclosed 2026-08-25.

**Classification:** FACT (Owner-stated, external input) — names a new
concept, "Hermes Control," with a stated cadence (quarterly) and a stated
review surface (knowledge, guidelines, workflows, tools, integrations, code,
technical components, "other useful developments").

**What this establishes, and what it does NOT establish:** the Owner has
named a function and a cadence. **UNKNOWN, not to be inferred:** whether
"Hermes Control" is itself an agent, a subsystem, a scheduled process, or a
role with human involvement — the Owner did not specify, and per Section 5.1
Phase -2 must not infer this as fact. Do not assume it is (or is not) an
autonomous agent; record only what was stated.

**INTERPRETATION — this is a close, direct match to DOM-25's research
subject, not a new domain:** `research-domains.md` DOM-25 ("Self-updating
ecosystem-intelligence agent design") was already researching almost exactly
this — "an agent whose job is continuous external-technology scouting... that
feeds recommendations back into the parent system's own capability set" —
and its own definition explicitly noted this is "structurally the same kind
of activity as the current Phase -2 research process itself." OD-004 confirms
the Owner intends this capability to exist, gives it a name and a concrete
cadence, and — notably — broadens its review surface beyond DOM-25's
original "external repos/tools/patterns" framing to include Hermes' *own*
internal knowledge, guidelines, workflows, and code. This is a materially
useful sharpening of DOM-25's target shape for Stage -2.5 pattern extraction:
candidate patterns (e.g. `unicodeveloper/tech-scouting-agent`, REPO-044) should
now be evaluated not just for external-scouting capability but for whether
they generalize to a self-review-of-own-components function.

**Domains affected:**
- **DOM-25** (Self-updating ecosystem-intelligence agent design) — primary.
  The quarterly cadence and the specific review surface are new, concrete
  target-shape details to evaluate candidate patterns against.
- **DOM-15** (Agent evaluation & pre-publish quality gating) — a periodic
  review of "workflows, tools, integrations, code" overlaps conceptually with
  ongoing quality/capability evaluation, though DOM-15's original framing was
  content-specific (pre-publish gating of generated posts) — these remain
  distinct mechanisms serving related-but-different needs; do not conflate.
- **DOM-14** (Observability for autonomous-agent trust) — a quarterly review
  needs something to review; observability/decision-trace infrastructure
  (Langfuse, Phoenix — REPO-020, REPO-021) is a plausible input source for
  what Hermes Control would look at, worth cross-referencing at Stage -2.6.

**Phase -2 handling:** Stage -2.5 should re-evaluate DOM-25's pattern
candidates against this sharpened target shape. No implementation design of
"Hermes Control" itself follows from this record — Phase -2 catalogs patterns
that could inform its eventual design; Phase -1 decides what Hermes Control
actually is and how it runs.
