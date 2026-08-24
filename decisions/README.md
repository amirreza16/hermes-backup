# Owner Decision Records

Per Master Plan Section 6.1's directory tree, this directory holds phase-local
decision records — specifically, facts and decisions the Owner has supplied
directly about Hermes itself (the future product), as distinct from Phase -2's
own research findings, recommendations, or internal process choices.

## Why these exist and how Phase -2 treats them

Per Master Plan Section 2.3 and 5.1, Phase -2 does not decide Hermes'
architecture, lock in requirements, or infer missing requirements as facts.
But the Owner can — and the precedent for handling an Owner-supplied fact
mid-phase was already established at the Stage -2.1 checkpoint, when the
Owner disclosed `NousResearch/hermes-agent` as Hermes' base architecture
(recorded in `phase-m2/research-domains.md` under `## Known Base
Architecture`). The decisions in this directory follow the identical
handling:

- They are recorded as **FACT** (Owner-stated, external to Phase -2's own
  decision process) — not as a Phase -2 recommendation, and not something
  Phase -2 "approved" or "chose."
- Phase -2 still does not design their implementation. Per **P4 (Handoff
  Boundary)** and **P7 (No Premature Architecture)**, and the Owner's own
  explicit instruction accompanying this batch ("do not convert these
  decisions into implementation design during Phase 2"), each decision below
  reframes *which research questions matter and how to read existing
  evidence* for the domains it touches — it does not trigger new
  architecture, scaffolding, or design work in Phase -2 itself.
- Where a decision materially changes how a `research-domains.md` domain
  should be read, a short **Owner Decision Note** is appended to that
  domain's entry, cross-referencing the relevant `OD-###` record here — the
  domain's Research Question itself is not rewritten unless the change is
  as structural as the "Known Base Architecture" reframing was.
- FACT / INTERPRETATION / HYPOTHESIS / UNKNOWN labeling (Section P5) still
  applies within each record: the Owner's statement itself is FACT; anything
  Phase -2 infers about its *implications* for a given domain is labeled
  INTERPRETATION and kept visibly separate.

## Index

| ID | Decision | Date | Domains Affected |
|----|----------|------|-------------------|
| [OD-001](OD-001-private-single-user-system.md) | Hermes is a private, single-user system | 2026-08-25 | DOM-08, DOM-17, DOM-24 |
| [OD-002](OD-002-memory-global-plus-per-project.md) | Shared global memory + separate per-project memory | 2026-08-25 | DOM-11, DOM-12, DOM-19, DOM-24 |
| [OD-003](OD-003-agent-to-agent-access-deferred.md) | Agent-to-agent access rules deferred to Phase -1 | 2026-08-25 | DOM-08, DOM-01, DOM-02 |
| [OD-004](OD-004-hermes-control-quarterly-review.md) | "Hermes Control" performs quarterly reviews across knowledge/guidelines/workflows/tools/integrations/code/technical components | 2026-08-25 | DOM-25, DOM-15, DOM-14 |
| [OD-005](OD-005-hermes-control-suggest-only.md) | Hermes Control may only suggest; owner approval required for any update/removal | 2026-08-25 | DOM-25, DOM-07 |
| [OD-006](OD-006-update-backup-rollback.md) | Every approved update requires a backup and reliable rollback | 2026-08-25 | DOM-11, DOM-13, DOM-25 |

All six were supplied by the Owner in a single message on 2026-08-25, alongside
an explicit instruction (itself not a separate decision record, since it
governs Phase -2's *handling* of these facts rather than being a fact about
Hermes): keep approved facts, Phase -2 recommendations, and Phase -2
assumptions clearly separated, and do not convert these into implementation
design during this phase.
