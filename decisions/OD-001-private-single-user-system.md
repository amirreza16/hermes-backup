# OD-001 — Hermes Is a Private, Single-User System

**Statement (Owner, verbatim intent):** "Hermes is a private, single-user
system."

**Decided by:** Owner, final — disclosed 2026-08-25, outside Phase -2's own
decision process. Same status as the `NousResearch/hermes-agent` base
architecture disclosure at the Stage -2.1 checkpoint (see
`phase-m2/research-domains.md` `## Known Base Architecture`).

**Classification:** FACT (Owner-stated, external input).

**What this establishes:** Hermes is operated by one owner. It is not a
multi-tenant SaaS product serving multiple distinct external customers, each
with their own account/subscription/administrative boundary from every other
customer.

**INTERPRETATION — how this reframes existing research, not what to build:**
Hermes can still manage many social pages/projects (see OD-002) — this
decision is about *who operates Hermes*, not about how many things Hermes
manages. It resolves a terminology risk that ran through Stage -2.3/-2.4:
research repeatedly used "multi-tenant" language (e.g. the `hermes-agent`
tenant-isolation investigation in `phase-m2/repo-audits/nousresearch-hermes-agent.md`,
`nimblecoai-hermes-agent.md`, `nimblecoai-hermes-swarm-map.md`) borrowed from
comparison sources built for actual multi-customer SaaS use (many different
external operators, each needing isolation from every other). Hermes' actual
need is narrower and simpler: one owner, multiple projects/pages, needing
isolation *between projects*, not between different owners' accounts. The
technical mechanisms found (profile-based routing, `context_id` memory
scoping) remain directly relevant as comparison patterns for *project-level*
isolation — this decision does not invalidate that research, it clarifies
which axis of isolation actually matters for Hermes.

**Domains affected:**
- **DOM-08** (Permissions & least-privilege scoping) — the threat model
  simplifies: no risk of one external customer's agent instance attacking
  another external customer's data via a shared platform. Per-project
  credential isolation (one owner, many pages) is still the real need.
- **DOM-17** (Security & governance for multi-account social automation) —
  remains relevant (multiple real platform credentials, one per page/account)
  but the "multi-account" framing was always about platform accounts per
  page, not about isolating different human operators from each other — this
  decision confirms that reading was correct and removes any residual
  ambiguity.
- **DOM-24** (Multi-tenant / multi-instance onboarding patterns) — the
  domain's own name uses "multi-tenant" loosely; per this decision, "tenant"
  in Hermes' context means "project/page," not "external customer." No
  change to the domain's research question, which was already about adding a
  new page without a from-scratch project — this decision confirms that
  framing rather than changing it.

**Phase -2 handling:** No new research triggered. This is a scoping
clarification applied to how existing and future DOM-08/17/24 evidence is
read and reported, not a new capability need. No implementation design
follows from this record (Section 2.3/P7) — Phase -1 decides how the
single-owner, multi-project boundary is actually enforced.
