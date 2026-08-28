# Hermes Phase -2 Research Domains

Revision: 3 | Updated: 2026-08-29 | Stage: -2.7 (Synthesis, post-phase-end)

**Revision 3 note (2026-08-29):** OQ-01 is resolved. The Owner confirmed
DOM-23 (community management / audience engagement automation) is
**explicitly out of scope** for Hermes: no comment-or-DM-reply
functionality exists in the current system design, and this was never
part of the intended scope. DOM-23's status changes from BLOCKED
(open question, scope undetermined) to **EXCLUDED** (deliberate scope
boundary, Owner-confirmed) — see the updated DOM-23 entry below and the
Revision 3 reconciliation log row. This is a scope-clarifying resolution,
not new research; no discovery work was performed or is warranted for
this domain. Full correction record: `HERMES_RESEARCH.md`,
2026-08-29 entry.

**Revision 2 note:** at the Stage -2.1 Owner Checkpoint, the Owner confirmed the
overall registry and the two contested drops (Spec-driven development, Architecture
documentation), and disclosed a fact this revision incorporates: Hermes will be built
on top of the open-source framework `NousResearch/hermes-agent`, as a final Owner
decision made outside Phase -2. See `## Known Base Architecture` below and the
Seed Reconciliation Log for how this changes the registry.

Priority scale used throughout (not prescribed by the Master Plan; defined here for
consistency): **HIGH** = directly named or clearly implied by the raw idea's two core
agent types or its three recurring behavioral principles; **MEDIUM** = supports a HIGH
domain or is a reasonably inferable extension of the raw idea; **LOW** = plausible but
speculative, or dependent on unresolved scope.

This registry is derived from Section 7.1 seeds, challenged against
`source/raw-hermes-idea.md` per Master Plan P1 (Need -> Capability -> Evidence ->
Pattern). The seed list is a starting hypothesis set, not a checklist — see
`## Seed Reconciliation Log` at the end of this file for what was kept, merged, split,
dropped, or added, and why. The registry below, not the original seed list, is the
active source of truth (Section 7.3).

---

## Domain Registry

| ID | Cluster | Name | Priority | Status |
|----|---------|------|----------|--------|
| DOM-01 | A — Core Agent Architecture | Multi-agent orchestration architecture | HIGH | IN-PROGRESS |
| DOM-02 | A — Core Agent Architecture | Agent role & contract design | HIGH | IN-PROGRESS |
| DOM-03 | A — Core Agent Architecture | Task decomposition for narrative/chained content workflows | HIGH | IN-PROGRESS |
| DOM-04 | A — Core Agent Architecture | Skill design patterns | MEDIUM | IN-PROGRESS |
| DOM-05 | A — Core Agent Architecture | Prompt / system-instruction architecture for behavioral constraints | HIGH | IN-PROGRESS |
| DOM-06 | A — Core Agent Architecture | Tool-use & MCP integration patterns | MEDIUM | IN-PROGRESS |
| DOM-07 | B — Human Control, Safety & Trust | Human-in-the-loop approval gates for irreversible actions | HIGH | IN-PROGRESS |
| DOM-08 | B — Human Control, Safety & Trust | Permissions & least-privilege scoping | MEDIUM | IN-PROGRESS |
| DOM-09 | B — Human Control, Safety & Trust | Ambiguity detection & clarification-seeking behavior | HIGH | IN-PROGRESS |
| DOM-10 | B — Human Control, Safety & Trust | Progressive autonomy / trust calibration over time | HIGH | IN-PROGRESS |
| DOM-11 | C — State, Memory & Reliability | Append-only memory & audit-log architecture | HIGH | IN-PROGRESS |
| DOM-12 | C — State, Memory & Reliability | Context engineering for long-running, narratively-continuous agents | MEDIUM | IN-PROGRESS |
| DOM-13 | C — State, Memory & Reliability | Long-running agent reliability & failure recovery | MEDIUM | IN-PROGRESS |
| DOM-14 | C — State, Memory & Reliability | Observability for autonomous-agent trust | MEDIUM | IN-PROGRESS |
| DOM-15 | C — State, Memory & Reliability | Agent evaluation & pre-publish quality gating | HIGH | IN-PROGRESS |
| DOM-16 | C — State, Memory & Reliability | Cost control & model-routing governance | HIGH | IN-PROGRESS |
| DOM-17 | D — Security & Governance | Security & governance patterns for multi-account social automation | MEDIUM | IN-PROGRESS |
| DOM-18 | E — Social-Media Operations | Competitive & audience research automation | HIGH | IN-PROGRESS |
| DOM-19 | E — Social-Media Operations | Content strategy, planning & brand consistency | MEDIUM | IN-PROGRESS |
| DOM-20 | E — Social-Media Operations | Multi-modal content generation (text/image/video, narrative continuity) | HIGH | IN-PROGRESS |
| DOM-21 | E — Social-Media Operations | Publishing workflow operations | HIGH | IN-PROGRESS |
| DOM-22 | E — Social-Media Operations | Analytics & experimentation feedback loops | MEDIUM | IN-PROGRESS |
| DOM-23 | E — Social-Media Operations | Community management / audience engagement automation | N/A | EXCLUDED (2026-08-29, Owner-confirmed out of scope) |
| DOM-24 | F — Scaling & Self-Maintenance | Multi-tenant / multi-instance onboarding patterns | HIGH | IN-PROGRESS |
| DOM-25 | F — Scaling & Self-Maintenance | Self-updating ecosystem-intelligence agent design | HIGH | IN-PROGRESS |

25 active domains (24 IN-PROGRESS, 1 BLOCKED pending Owner scope confirmation).
4 seed topics evaluated and not carried forward (see reconciliation log).

---

## Known Base Architecture (Owner-Supplied Input)

| Item | Value |
|---|---|
| Repo | `NousResearch/hermes-agent` |
| URL | github.com/NousResearch/hermes-agent |
| Status | **Known base architecture, not a discovered candidate** |
| Priority | HIGH |
| Reserved ID | REPO-001 (formal Repository Triage record per Section 9.2 to be created when Stage -2.3 opens; Triage Decision is pre-determined as **DEEP AUDIT**, not reached through the normal triage funnel) |
| Decided by | Owner, final and non-negotiable — disclosed 2026-08-23 at the Stage -2.1 checkpoint, outside this phase's decision process |
| Deep-audit precedence | First and most important candidate for Stage -2.4, ahead of any repo Stage -2.3 discovers — not queued behind ordinary triage scoring |

**How Phase -2 treats this fact (Section 2.3 / 5.1 / P1 / P6 / Section 13):**

Section 2.3 lists "Base architecture repo" among decisions Phase -2 must not make.
That constraint is unchanged: **Phase -2 did not choose this repo and does not
formally approve it as an architecture decision here.** What changed is that the
Owner supplied a fact external to Phase -2's own decision process — analogous to how
`source/raw-hermes-idea.md` itself is a given input, not a Phase -2 invention. Phase
-2's job with this fact is to *research around a known input*, not to ratify it:

- It still receives full adversarial/negative review at deep audit (Section 13) —
  being the mandated substrate is not evidence of quality.
- Its internal mechanisms are still classified REUSE / ADAPT / REFERENCE / REJECT per
  capability (P2), not accepted wholesale.
- Any capability it lacks or implements poorly is still an open gap for Phase -1,
  not something Phase -2 papers over because "it's the chosen framework."
- P1 (Need before solution) still governs: the research question for each affected
  domain starts from the Hermes need, not from the repo's existence.

**Effect on affected domains:** for any domain whose capability this framework is
likely to already implement, the research question shifts from *"what is the best
pattern that exists anywhere?"* to *"how does `hermes-agent` implement this
capability, does that implementation satisfy Hermes' needs (the three behavioral
principles, the cost constraint, the multi-page/narrative requirements), and — if
not — what needs to be adapted or sourced elsewhere to fill the gap?"* Outside
evidence for these domains is now sought specifically as a *comparison baseline* to
evaluate the framework's implementation against, not as a green-field "what's out
there" search. Eight domains are reframed below on this basis: DOM-01, DOM-02, DOM-04,
DOM-06, DOM-11, DOM-13, DOM-16, DOM-24. Any other domain later found, during Stage
-2.4 audit, to be governed by the framework will be reframed the same way at that
point — this is an empirical question to resolve during audit, not something to
pre-guess for the remaining 17 domains today.

**STANDING REQUIREMENT FOR STAGE -2.4 — additional deliverable, logged 2026-08-23,
not to be forgotten when this stage opens:**

When REPO-001 (`NousResearch/hermes-agent`) reaches deep audit, produce the standard
audit record (Master Plan Section 9, specifically **Section 9.3** — Deep Audit
Dimensions A–J, which is the schema Stage -2.4 actually uses; the Owner's checkpoint
message referenced "Section 9.1," which is the Stage -2.2 Skill Record Schema —
corrected here for accuracy, same intent) **plus one additional standalone
deliverable**:

> A precise, complete reference/cheat-sheet document of this framework's *actual*
> capabilities — real CLI commands, real `config.yaml` structure, real
> memory/skills/MCP architecture — built **only** from:
> 1. Official docs at `hermes-agent.nousresearch.com/docs`
> 2. The actual repo code (never guessed, never reconstructed from memory/training
>    data)

**Why this exists (Owner's stated reason, preserved verbatim in intent):** the Owner
previously had a "Hermes Agent Cheat Sheet" PDF that turned out to be inaccurate and
likely hallucinated — it contained things like a `hermes memory reindex` command and
a "GEPA reflection loop" concept that do not exist in the official docs. That file
has been discarded and **must not be used as a source, referenced, or treated as
prior knowledge to confirm/build on** — any overlap between this new document and
that discarded one must come from independently verifying the same claim against
docs/code, not from carrying the old claim forward.

**Standard this document must meet:** every claim traceable directly to the official
docs or the code (source-level, per Section 12 evidence hierarchy) — no inference,
no generalization from other agent frameworks, no filling gaps from general
"how agent frameworks usually work" knowledge. If official docs and code disagree,
or a capability can't be verified in either, say so explicitly (P5 — FACT vs.
UNKNOWN) rather than smoothing it over. This document is meant to outlive Phase -2 —
a durable, trustworthy reference for "what Hermes Agent actually does" for the rest
of the project, not a Phase -2-scoped artifact.

**Where this deliverable lives:** not yet named/pathed — decide the filename when
Stage -2.4 opens (likely `phase-m2/repo-audits/hermes-agent-capability-reference.md`
or similar, alongside the standard `phase-m2/repo-audits/nousresearch-hermes-agent.md`
audit record — both should exist since they serve different purposes: one is a Phase
-2 scored audit record, the other is a durable project-wide reference).

**STAGE -2.3 FINDING — confirmed gap in REPO-001 relevant to DOM-24, logged
2026-08-24, to be resolved (not re-discovered) at Stage -2.4:**

A Stage -2.3 discovery pass searching for DOM-24 comparison baselines surfaced
`NousResearch/hermes-agent` issue #34352, "Solving the Multi-Tenant Hermes
Problem." This claim was independently verified by the primary Phase -2
session directly against GitHub (`gh issue view 34352 --repo
NousResearch/hermes-agent`, 2026-08-24) before being treated as fact — per the
same discipline that discarded the Owner's earlier hallucinated cheat-sheet
PDF, no claim about this framework is accepted without direct verification.

**Verified FACT:** the issue is real, open, has 24 comments, and states that
stock hermes-agent has no tenant isolation — memory is global, sessions do not
scope by tenant/context. It documents 12+ related open issues clustering into
four sub-problems (gateway adapter multi-instance, profile routing,
memory/context isolation, session key correctness), none of which have a
merged or open PR addressing them as of access date. One commenter
self-reports a production incident (a content agent leaking
competitor-monitoring memory into a public article) — this incident report
itself is a third-party testimonial within a verified-real issue, not
independently confirmed beyond the comment existing (see `source-register.md`
SRC-028 for the FACT/CLAIM distinction preserved explicitly).

This directly and materially affects DOM-24's research question ("does
hermes-agent support multi-tenant instances as a config change, or would
Hermes need to build a multi-tenancy layer on top"): the honest current answer,
pending Stage -2.4's own independent code audit of REPO-001, is **no, not
natively** — this is now a documented, source-level starting hypothesis for
that audit, not something to re-derive from scratch. Two third-party projects
addressing this exact gap were found and independently verified real
(`gh repo view`) by the primary Phase -2 session: `NimbleCoAI/hermes-agent`
(a production multi-tenant fork, REPO-040 in `repo-catalog.md`) and
`NimbleCoAI/hermes-swarm-map` (a multi-tenant orchestration control plane,
REPO-041), both reserved as DEEP AUDIT candidates for Stage -2.4, to be
audited after REPO-001 itself per the sequencing note on REPO-040.

This is reported as a finding for Stage -2.4 to formally confirm/audit, not as
an escalation — it does not require Owner authorization to proceed with
research, and Phase -2 still does not treat it as license to decide anything
about Hermes' actual multi-tenancy design (Section 5.1/2.3 unchanged). It is
flagged prominently here, and in the Stage -2.3 report to the Owner, because
Section 5.1 forbids treating an unresolved high-impact assumption as fact —
and the inverse also applies: a *resolved*, verified fact about the known base
architecture should not be left buried in a discovery-pass transcript either.

---

## Owner-Approved Decisions (2026-08-25)

Six additional Owner-supplied facts about Hermes itself were disclosed
2026-08-25, mid Stage -2.4->-2.5, following the same handling precedent as
`## Known Base Architecture` above: recorded as FACT, external to Phase -2's
own decision process, not converted into implementation design this phase
(per the Owner's own explicit instruction accompanying them). Full records —
each with the verbatim statement, INTERPRETATION of its research
implications kept visibly separate from the FACT itself, and affected
domains — live in `decisions/OD-001` through `OD-006`. Summary:

| ID | Decision | Domains Affected |
|----|----------|-------------------|
| OD-001 | Hermes is a private, single-user system | DOM-08, DOM-17, DOM-24 |
| OD-002 | Shared global memory + separate per-project memory | DOM-11, DOM-12, DOM-19, DOM-24 |
| OD-003 | Agent-to-agent access rules deferred to Phase -1 | DOM-08, DOM-01, DOM-02 |
| OD-004 | "Hermes Control" performs quarterly reviews (knowledge/guidelines/workflows/tools/integrations/code/technical components) | DOM-25, DOM-15, DOM-14 |
| OD-005 | Hermes Control may only suggest; Owner approval required for any update/removal | DOM-25, DOM-07 |
| OD-006 | Every approved update requires backup + reliable rollback | DOM-11, DOM-13, DOM-25 |

Each affected domain below carries a short "**Owner Decision Note**" line
cross-referencing the relevant OD ID(s) — the domain's Research Question
itself is left as originally written except where noted, since these six
decisions sharpen evaluation criteria for Stage -2.5 onward rather than
replacing the underlying research questions the way the base-architecture
disclosure did.

---

## Per-Domain Definitions

### DOM-01 — Multi-agent orchestration architecture
**Research Question:** How does `NousResearch/hermes-agent` (REPO-001, known base
architecture) implement coordination between distinct agent roles, and does that
implementation adequately support Hermes' fixed two-role design (content-generation
agent + research agent, sharing context/history, with a human approval gate between
generation and publishing) — or does it need adaptation/supplementing? Outside
orchestration patterns are researched as a comparison baseline to evaluate the
framework's approach against, not as a green-field search.
**Why Hermes May Need It:** The raw idea names exactly two agent types with different
jobs and risk profiles. Since the base framework is fixed, how *it specifically*
coordinates agents — not the abstract best-in-world pattern — determines what Hermes
gets for free versus what must be built on top.
**Evidence Needed:** `hermes-agent`'s actual orchestration mechanism (source-level,
not just README claims — Section 12 evidence hierarchy); its handoff/shared-state/
failure-isolation behavior; gap analysis against Hermes' two-role, approval-gated
need; a small set of comparison implementations to judge whether the framework's
approach is sound or should be adapted.
**Likely Source Types:** `hermes-agent` source code and docs (primary); secondarily,
open-source multi-agent frameworks/repos and Anthropic/Claude agent-architecture
documentation as comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s orchestration code first (Stage
-2.4, Dimension A). Then search "multi-agent orchestration," "agent handoff pattern,"
"orchestrator-worker agents" for comparison examples, prioritizing small fixed-agent
-count systems over large dynamic swarms (different scale problem).
**Exclusion Criteria:** Pure academic multi-agent-systems (MAS) theory papers with no
inspectable implementation; frameworks whose only orchestration example is >10 agents
(different scale problem).
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Agent architecture,"
"Single-agent vs multi-agent decisioning," and "Agent orchestration" — all three point
at the same underlying question once scoped to Hermes' fixed two-role case (Section
7.1 merge permission). Evidence source: raw idea, 2026-08-23. Reframed 2026-08-23
around the known base architecture per Owner Stage -2.1 checkpoint response — see
`## Known Base Architecture` above.
**Owner Decision Note (2026-08-25):** OD-003 — the specific *access-control*
rules between agents are deferred to Phase -1; handoff/contract mechanics
themselves remain in scope. See `decisions/OD-003`.

### DOM-02 — Agent role & contract design
**Research Question:** What role-definition and structured-I/O contract mechanism
does `hermes-agent` (REPO-001) provide, and is it expressive enough to define clean
boundaries between a content-generation agent, a research agent, and the human
approver — or must Hermes layer its own contract discipline on top?
**Why Hermes May Need It:** The two agent types must exchange well-formed artifacts
(research findings -> content briefs; drafts -> approval requests) without ambiguity
leaking across the boundary — directly relevant to the "stop and ask, don't guess"
principle at the interface level. Since the framework is fixed, this is now a
question of what it offers versus what Hermes must add.
**Evidence Needed:** `hermes-agent`'s actual role/contract/structured-output
mechanism (source-level); whether it enforces or merely suggests schema validation
at role boundaries; comparison contract patterns from other frameworks to judge
sufficiency.
**Likely Source Types:** `hermes-agent` source/docs (primary); secondarily,
agent-framework docs on structured outputs/tool schemas, MCP tool-contract specs, as
comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s role/contract code first (Stage
-2.4, Dimension B). Then search "agent contract schema," "structured output agent
handoff" for comparison examples.
**Exclusion Criteria:** Generic API-contract material with no agent-specific framing.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Agent role design," "Agent
contracts," and "Structured outputs" — same underlying problem (defining the
interface, not just the actors). Evidence source: raw idea, 2026-08-23. Reframed
2026-08-23 around the known base architecture per Owner Stage -2.1 checkpoint
response.
**Owner Decision Note (2026-08-25):** OD-003 — access-control rules between
agents deferred to Phase -1; role/contract *shape* research (this domain)
remains fully in scope. See `decisions/OD-003`.

### DOM-03 — Task decomposition for narrative/chained content workflows
**Research Question:** How do agent systems decompose a multi-step, narratively
continuous content series into schedulable subtasks while preserving continuity
(tone, plot/thread state, prior-post references) across steps?
**Why Hermes May Need It:** The raw idea explicitly states content is "اغلب
به‌صورت زنجیره‌ای/روایی (نه قطعات مستقل)" — often chained/narrative rather than
independent pieces. This is a distinct decomposition problem from generating
one-off, unrelated posts.
**Evidence Needed:** Examples of serialized/episodic content generation with explicit
state-carryover between generation steps.
**Likely Source Types:** Serialized-content or storytelling agent repos, workflow/
pipeline orchestration examples with persistent step-to-step state.
**Search Strategy:** Search "serialized content generation agent," "episodic content
pipeline," "narrative continuity agent state" against repo hosts and agent-framework
examples.
**Exclusion Criteria:** Generic task-decomposition/planning material with no
continuity-carryover element (that's just DOM-01/DOM-12 territory).
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Seed "Task decomposition" kept but narrowed to the
specific narrative/chained requirement named in the raw idea, to avoid a generic,
low-yield research question. Evidence source: raw idea, 2026-08-23.

### DOM-04 — Skill design patterns
**Research Question:** What is `hermes-agent`'s (REPO-001) native skill/capability
unit — its shape, scoping rules, and invocation mechanism — and how well does it
match (or how would it need to be bridged to) the Claude Skills model, given both
named agent types will likely be composed of smaller invocable capabilities? Which
existing skills (Claude Skills or otherwise) cover sub-tasks Hermes would otherwise
build from scratch on top of that native mechanism?
**Why Hermes May Need It:** Both named agent types will likely be composed of
smaller invocable capabilities; this is also the explicit target of Campaign SCS
(Master Plan Section 15.1). Since the base framework is fixed, "skill design" is now
partly a compatibility/bridging question, not a pure green-field pattern search.
**Evidence Needed:** `hermes-agent`'s native skill/capability abstraction
(source-level); real skill definitions elsewhere with visible structure and scoping
discipline, used as comparison and as candidate content to bridge in.
**Likely Source Types:** `hermes-agent` source/docs (primary for the native
mechanism); Claude Skills marketplace/registry and community skill repos (for
comparison and candidate content, per Campaign SCS).
**Search Strategy:** Deep-audit `hermes-agent`'s skill/capability code first (Stage
-2.4). In parallel, run Section 15.1 campaign — direct inspection of skill catalogs
plus adjacent/related-skill discovery from any strong candidate found.
**Exclusion Criteria:** Skills that are thin wrappers with no inspectable internal
logic or decision structure.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept as-is from seed list; directly tied to a
named campaign (Section 15.1), not merged since it has its own dedicated discovery
procedure. Evidence source: Master Plan Section 15.1. Reframed 2026-08-23 around the
known base architecture per Owner Stage -2.1 checkpoint response.

### DOM-05 — Prompt / system-instruction architecture for behavioral constraints
**Research Question:** How do production agent systems reliably encode hard
behavioral rules (always ask under ambiguity; always confirm before irreversible
action; never self-delete history) into system instructions so they hold under
pressure/drift rather than degrading over a long-running session?
**Why Hermes May Need It:** All three of the raw idea's recurring behavioral
principles are instruction-architecture problems as much as orchestration problems —
a rule that isn't robustly encoded is a rule that gets silently dropped over time.
**Evidence Needed:** Documented instruction-hardening techniques (constraint framing,
repetition/anchoring strategies, guardrail-instruction placement) with evidence they
hold up in long sessions, not just single-turn demos.
**Likely Source Types:** Agent-framework prompting guides, published system-prompt
case studies, Anthropic first-party guidance on agent instruction design.
**Search Strategy:** Search "system prompt hard constraint," "instruction drift long
session," "agent guardrail instruction design."
**Exclusion Criteria:** Generic prompt-engineering tips with no long-running or
constraint-robustness angle.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list, scoped explicitly to the
three named behavioral principles for higher expected information value. Evidence
source: raw idea, 2026-08-23.

### DOM-06 — Tool-use & MCP integration patterns
**Research Question:** What tool-calling and MCP-integration mechanism does
`hermes-agent` (REPO-001) provide for invoking external tools/services (image/video
generation APIs, social-platform publishing APIs, repo/doc search), and how robust is
its error handling / blast-radius containment on failure — does it need
hardening or supplementing for Hermes' tool-heavy design?
**Why Hermes May Need It:** Both agent types are tool-heavy by design (content agent
calls generation + publishing tools; research agent calls search/scraping tools).
Since the framework is fixed, its specific tool-calling substrate is what Hermes will
actually inherit.
**Evidence Needed:** `hermes-agent`'s tool-calling/MCP-integration code
(source-level) — retry logic, error handling, permission scoping of what a call can
do; comparison implementations to judge whether it's sufficient or needs hardening.
**Likely Source Types:** `hermes-agent` source/docs (primary); secondarily, MCP
spec/reference servers, other agent-framework tool-use docs, Apify actor integration
patterns (per Campaign APIFY, Section 15.3) as comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s tool-use/MCP code first (Stage -2.4,
Dimension D/G). Then search "MCP server pattern," "agent tool call error handling"
for comparison examples.
**Exclusion Criteria:** Tool lists/catalogs with no reliability or error-handling
discussion.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Tool-use architecture" and
"MCP/integration patterns" — same underlying mechanism (agent-to-external-service
calling), evaluated together to avoid redundant domains. Evidence source: raw idea,
2026-08-23. Reframed 2026-08-23 around the known base architecture per Owner Stage
-2.1 checkpoint response.

### DOM-07 — Human-in-the-loop approval gates for irreversible actions
**Research Question:** What UX/architectural patterns exist for gating irreversible
agent actions (publish, delete) behind explicit human confirmation, without making
every routine action require confirmation (approval fatigue)?
**Why Hermes May Need It:** Directly named: "اقدام برگشت‌ناپذیر ... همیشه تأیید صریح
می‌خواهد" (irreversible action always requires explicit confirmation) — one of the
three recurring behavioral principles, and load-bearing for the content agent's
publish step specifically.
**Evidence Needed:** Concrete approval-gate implementations distinguishing
reversible vs. irreversible actions, and any evidence on avoiding approval fatigue.
**Likely Source Types:** Agent-framework HITL docs, published incident/design
writeups on approval-gate design, CI/CD-style "manual gate" patterns as an analog.
**Search Strategy:** Search "human in the loop irreversible action," "approval gate
agent," "confirm before destructive action agent."
**Exclusion Criteria:** Generic HITL material that treats all actions uniformly with
no reversible/irreversible distinction.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Human-in-the-loop," narrowed
to the irreversible-action framing explicit in the raw idea. Evidence source: raw
idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-005 — for the specific "Hermes
Control" self-review/self-update surface (DOM-25), approval must be
structurally enforced, not a configurable default; a directly evaluable bar
for candidate patterns found under this domain. See `decisions/OD-005`.

### DOM-08 — Permissions & least-privilege scoping
**Research Question:** How do systems scope what an agent is *capable of doing at
all* (as distinct from when it must ask before doing something it's capable of),
particularly across multiple isolated credential sets (one per social account/page)?
**Why Hermes May Need It:** Multiple pages likely means multiple platform credential
sets; a compromised or misbehaving agent instance for one page should not be able to
touch another page's account.
**Evidence Needed:** Credential/capability-scoping patterns for multi-tenant agent
deployments.
**Likely Source Types:** Agent-framework permissions docs, secrets-management
patterns for multi-account automation.
**Search Strategy:** Search "agent least privilege," "multi-tenant credential
isolation agent," "scoped API token per agent instance."
**Exclusion Criteria:** General IAM/secrets-management material with no agent-specific
framing.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list, distinguished from DOM-07
(capability scoping vs. runtime confirmation are different mechanisms). Evidence
source: raw idea, 2026-08-23 (multi-page framing).
**Owner Decision Note (2026-08-25):** OD-001 — Hermes is single-owner/
single-user; the threat model is per-project credential isolation for one
owner's pages, not isolation between different external customers. OD-003 —
specific agent-to-agent access rules deferred to Phase -1; pattern research
here continues. See `decisions/OD-001`, `decisions/OD-003`.

### DOM-09 — Ambiguity detection & clarification-seeking behavior
**Research Question:** How do agent systems detect that they're operating under
ambiguity and should stop to ask, rather than proceeding on a guess — what triggers
the stop (confidence threshold, missing required field, conflicting signals), and how
is the clarification request formed?
**Why Hermes May Need It:** Directly named, and repeated across the interview per the
raw idea: "در ابهام، سیستم متوقف می‌شود و می‌پرسد؛ حدس نمی‌زند" (under ambiguity, the
system stops and asks; it does not guess) — called out as one of three principles
important to *both* agent types' shape.
**Evidence Needed:** Concrete ambiguity-detection mechanisms (not just "the agent can
ask questions" — the trigger logic for *when* it should).
**Likely Source Types:** Agent-framework docs on clarification/confidence handling,
published agent-eval work on over-confidence/under-asking failure modes.
**Search Strategy:** Search "agent ask clarifying question," "confidence threshold
agent action," "agent ambiguity handling pattern."
**Exclusion Criteria:** Simple chatbot FAQ-style clarification with no
action-consequence framing (Hermes' need is specifically about avoiding wrong
irreversible/costly action, not conversational politeness).
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** New domain, not present in Section 7.1 seed list.
Added because this principle is repeated three times in the raw idea and is distinct
enough from general HITL (DOM-07) to warrant focused evidence-gathering. Evidence
source: raw idea, 2026-08-23.

### DOM-10 — Progressive autonomy / trust calibration over time
**Research Question:** How do systems safely increase an agent's operating autonomy
over time as it demonstrates reliability, and what mechanisms let a human dial
autonomy back down if trust is violated?
**Why Hermes May Need It:** Explicit goal in the raw idea: "کاهش دخالت تکراری مالک در
طول زمان" (reduce the owner's repetitive involvement over time) — this is a
trajectory, not a fixed autonomy level, and is distinct from any single-point-in-time
HITL mechanism.
**Evidence Needed:** Concrete trust/autonomy-ramp mechanisms (e.g., graduated
permission tiers keyed to track record, rollback-on-violation designs).
**Likely Source Types:** Agent-framework or agentic-product design writeups on
autonomy levels/tiers; safety/reliability literature on staged autonomy.
**Search Strategy:** Search "progressive autonomy agent," "trust calibration AI
agent," "graduated agent permissions track record."
**Exclusion Criteria:** Static permission-tier documentation with no
evidence/track-record-driven escalation logic.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** New domain, not present in Section 7.1 seed list.
Added because the raw idea frames reduced owner involvement as a goal *over time*,
which existing seeds (static "Human-in-the-loop") don't capture. Evidence source: raw
idea, 2026-08-23.

### DOM-11 — Append-only memory & audit-log architecture
**Research Question:** What memory/history storage architecture does `hermes-agent`
(REPO-001) actually implement — is it append-only / immutable / soft-delete-only, or
does it perform any self-initiated deletion or overwrite? If the latter, this is a
direct conflict with a named Hermes behavioral principle and must be flagged as a gap
requiring adaptation, not something to route around silently.
**Why Hermes May Need It:** Directly named: "سیستم هرگز به‌خودی‌خود چیزی از
حافظه/تاریخچه حذف نمی‌کند" (the system never on its own deletes anything from
memory/history) — the third recurring behavioral principle. Because the framework is
fixed, whether it structurally honors this constraint (versus needing to be
adapted/wrapped) is now a specific, checkable audit finding rather than an open
pattern question.
**Evidence Needed:** `hermes-agent`'s actual memory/storage code (source-level) —
does it ever call delete/truncate/overwrite on history data, and under what
conditions; its growth-management strategy if any; comparison append-only/audit-log
designs to judge what a fix would look like if a gap is found.
**Likely Source Types:** `hermes-agent` source/docs (primary); secondarily,
event-sourcing/audit-log architecture docs and other agent-memory framework docs as
comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s memory/persistence code first (Stage
-2.4, Dimension C), specifically grepping for delete/truncate/overwrite paths against
history data. Then search "append only agent memory," "immutable audit log
architecture" for comparison examples if a gap is found.
**Exclusion Criteria:** Generic database design material with no agent or
audit-integrity framing.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Memory architecture" and
"Decision history" — decision-history logging is a specific instance of the
append-only/audit-log requirement, not a separate underlying problem. Evidence
source: raw idea, 2026-08-23. Reframed 2026-08-23 around the known base architecture
per Owner Stage -2.1 checkpoint response — this domain now carries a compliance-check
character, not just a pattern search.
**Owner Decision Note (2026-08-25):** OD-002 — memory has (at least) two
tiers by design: shared global + separate per-project. Evaluate whether a
candidate's never-delete guarantee holds across both tiers, not just one.
OD-006 — a *backup* requirement (for approved Hermes Control updates) is
related but distinct from this domain's never-delete-on-its-own principle;
keep the two conceptually separate. See `decisions/OD-002`, `decisions/OD-006`.

### DOM-12 — Context engineering for long-running, narratively-continuous agents
**Research Question:** How do agents maintain coherent working context (narrative
state, brand voice, prior research findings) across sessions that are too long or too
numerous to fit in a single context window?
**Why Hermes May Need It:** Chained/narrative content generation and an
ever-accumulating research knowledge base both require continuity beyond a single
context window.
**Evidence Needed:** Concrete context-compaction, retrieval, or summarization
strategies with evidence they preserve the specific kind of continuity needed
(narrative/voice, not just factual recall).
**Likely Source Types:** Agent-framework context-management docs, RAG/memory-retrieval
implementations built for continuity rather than pure Q&A.
**Search Strategy:** Search "context compaction agent," "long-running agent memory
retrieval," "narrative continuity context window."
**Exclusion Criteria:** Generic RAG tutorials with no continuity-over-time framing.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Context engineering," scoped
to the narrative-continuity need. Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-002 — evaluate candidates against a
concrete two-tier shape: does the mechanism cleanly separate global/general
knowledge from project-specific narrative state, or conflate them? See
`decisions/OD-002`.

### DOM-13 — Long-running agent reliability & failure recovery
**Research Question:** What scheduling and reliability mechanism does `hermes-agent`
(REPO-001) provide for unattended, recurring execution — specifically, does it
include cron-style scheduling, and how does it handle crash recovery, scheduling
drift, and partial-failure — and is that sufficient for the research agent's
continuous ecosystem-watch role and the overall reduced-involvement goal?
**Why Hermes May Need It:** The research agent's ecosystem-watch role and the overall
goal of reduced owner involvement both imply agents operating unattended for extended
periods, where failures must be recoverable without silent data loss (which would
also violate the never-delete-history principle, DOM-11). Because the framework is
fixed, its actual scheduling/reliability substrate — not an abstract best-practice
survey — determines what Hermes gets for free.
**Evidence Needed:** `hermes-agent`'s scheduling/cron mechanism and crash-recovery/
checkpointing code (source-level); evidence of graceful partial-failure handling;
comparison durable-execution patterns to judge sufficiency.
**Likely Source Types:** `hermes-agent` source/docs (primary, especially any cron/
scheduler module); secondarily, agent-framework reliability docs and
workflow-orchestration durable-execution patterns as comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s scheduling and reliability code
first (Stage -2.4, Dimension D), locating its cron/scheduler implementation
specifically. Then search "durable agent execution," "agent scheduling reliability"
for comparison examples if gaps are found.
**Exclusion Criteria:** General distributed-systems reliability material with no
agent-specific adaptation.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Long-running agents" and
"Failure recovery" — same underlying problem (keeping an unattended agent correct
over time) once scoped to Hermes' continuous research-agent role. Evidence source:
raw idea, 2026-08-23. Reframed 2026-08-23 around the known base architecture
(specifically its cron-scheduling capability, named by the Owner) per Owner Stage
-2.1 checkpoint response.
**Owner Decision Note (2026-08-25):** OD-006 — rollback/recovery evidence
gathered here (crash-safety engineering, checkpoint discipline) is directly
relevant comparison evidence for the backup+rollback requirement on approved
Hermes Control updates (DOM-25). See `decisions/OD-006`.

### DOM-14 — Observability for autonomous-agent trust
**Research Question:** What observability patterns (logging, dashboards, decision
traces) let a human owner verify an agent is behaving correctly *without* being
in the loop for every action — the visibility mechanism that makes reduced
involvement (DOM-10) safe rather than reckless?
**Why Hermes May Need It:** Reduced owner involvement over time is only safe if the
owner retains cheap ways to audit what happened; this is the visibility half of the
trust-calibration problem.
**Evidence Needed:** Concrete agent-observability implementations (decision/action
traces, not just infra metrics) designed for a human auditor rather than an on-call
engineer.
**Likely Source Types:** Agent-framework observability/tracing docs, agent-eval
tooling with human-review dashboards.
**Search Strategy:** Search "agent decision trace," "agent action audit dashboard,"
"agent observability human review."
**Exclusion Criteria:** Generic APM/infra-metrics material with no decision-level
traceability.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Observability," tied
explicitly to DOM-10's trust-calibration need. Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-004 — observability/decision-trace
evidence gathered here is a plausible input source for what "Hermes Control"
(DOM-25) would review quarterly. See `decisions/OD-004`.

### DOM-15 — Agent evaluation & pre-publish quality gating
**Research Question:** What evaluation/self-critique mechanisms let a content
pipeline enforce "quality over throughput" before a human ever sees a draft, and how
is generated content reviewed for quality issues prior to the approval gate?
**Why Hermes May Need It:** Explicit constraint: "کیفیت خروجی بر سرعت/حجم اولویت
دارد" (output quality takes priority over speed/volume) — this is a hard constraint on
the content-generation pipeline, and content review is the concrete mechanism that
enforces it before human approval.
**Evidence Needed:** Concrete self-critique/reviewer-agent implementations, evidence
of quality-gate effectiveness (not just "add a reviewer step" claims).
**Likely Source Types:** Agent-eval framework docs, published reviewer-agent/
critic-agent designs, content-QA pipeline examples.
**Search Strategy:** Search "agent self critique quality gate," "reviewer agent
pattern," "content quality gate before publish agent."
**Exclusion Criteria:** Generic LLM-eval-benchmark material with no
pipeline-integration angle.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Agent evaluation" and
"Content review" — content review is the applied instance of the general
quality-gating question for this pipeline. Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-004 — this domain's content-specific
pre-publish gating is a distinct mechanism from "Hermes Control"'s periodic
review of Hermes' own components (DOM-25) — related but not to be conflated.
See `decisions/OD-004`.

### DOM-16 — Cost control & model-routing governance
**Research Question:** What model-routing and cost/budget-enforcement mechanism does
`hermes-agent` (REPO-001) actually implement — per-task model-tier selection, spend
caps, cheap-first escalation — and does it reconcile cost control with the
co-equal "quality over throughput" constraint, or does it need extension?
**Why Hermes May Need It:** Explicit hard constraint: "کنترل هزینه ... یک قید جدی، نه
یک دغدغه‌ی فرعی است" (cost control is a serious constraint, not a secondary concern) —
named as co-equal in importance to the quality constraint. Because the framework is
fixed, its actual routing/budget mechanism is the real starting point for
reconciling that tension, not an abstract survey of what's possible.
**Evidence Needed:** `hermes-agent`'s model-routing and cost/budget-enforcement code
(source-level); whether/how it avoids silently trading away output quality;
comparison multi-model-tier implementations to judge sufficiency.
**Likely Source Types:** `hermes-agent` source/docs (primary); secondarily,
agent-framework cost-control/model-routing docs and published writeups on
multi-model-tier pipelines as comparison baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s routing/cost code first (Stage -2.4,
Dimension G). Then search "agent cost budget enforcement," "model routing by task
agent" for comparison examples if gaps are found.
**Exclusion Criteria:** Generic LLM-pricing comparison material with no
routing/enforcement mechanism.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Cost control" and "Model
routing" — routing is a mechanism for achieving cost control in this context, not a
separate underlying need, and keeping them merged avoids catalog bloat. Evidence
source: raw idea, 2026-08-23. Reframed 2026-08-23 around the known base architecture
(specifically its model-routing capability, named by the Owner) per Owner Stage -2.1
checkpoint response.

### DOM-17 — Security & governance patterns for multi-account social automation
**Research Question:** What security/governance patterns apply specifically to an
agent system posting on behalf of multiple real social accounts — secrets handling
for per-page platform credentials, and guardrails against generating or publishing
harmful/policy-violating content?
**Why Hermes May Need It:** Multi-page operation implies multiple sets of real,
sensitive platform credentials, and autonomous publishing implies a need for
content-safety guardrails independent of the approval-gate mechanism (DOM-07) — a
defense-in-depth concern.
**Evidence Needed:** Concrete secrets-management and content-safety-guardrail
implementations for social-automation-style agents specifically.
**Likely Source Types:** Social-media-API integration security docs, agent
content-safety/guardrail frameworks.
**Search Strategy:** Search "social media automation credential security," "agent
content safety guardrail," "multi-account bot secrets management."
**Exclusion Criteria:** Generic app-security checklists with no social-automation or
agent-specific framing.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Security and governance
patterns," scoped to the concrete multi-account/publishing context implied by the raw
idea rather than left generic. Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-001 — Hermes is single-owner;
"multi-account" here means multiple platform credentials per page under one
owner, not isolation between different external customers. See
`decisions/OD-001`.

### DOM-18 — Competitive & audience research automation
**Research Question:** How do research agents automate finding "what's working in
the market" for a given content niche/page — competitor monitoring, audience-signal
gathering — in a way that produces actionable input for content strategy rather than
raw data dumps?
**Why Hermes May Need It:** Directly named as research-agent role (b): "تحقیق
محتوایی/رقابتی برای هر صفحه (چه چیزی در بازار جواب داده)" (content/competitive
research for each page — what has worked in the market).
**Evidence Needed:** Concrete competitive/audience-research automation pipelines with
visible output structure (not just "can scrape a competitor's page").
**Likely Source Types:** Social-listening/competitive-intelligence tool docs, Apify
actors for social scraping (Campaign APIFY), published content-research agent
writeups.
**Search Strategy:** Search "competitive content research agent," "social listening
automation," "audience research agent pipeline"; cross-reference Apify Store per
Section 15.3.
**Exclusion Criteria:** Pure scraping tools with no research-synthesis step.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Content research" and
"Audience research" — both are facets of the single named research-agent role (b).
Evidence source: raw idea, 2026-08-23.

### DOM-19 — Content strategy, planning & brand consistency
**Research Question:** How do multi-page/multi-brand content systems maintain a
distinct strategy and voice per page while still reusing planning infrastructure
across pages?
**Why Hermes May Need It:** Each social page likely represents a distinct brand/voice,
and the system must plan content (potentially narrative arcs) at a strategic level
before task decomposition (DOM-03) or generation (DOM-20) begins.
**Evidence Needed:** Concrete per-brand/per-page strategy-configuration patterns
reused across a shared underlying content system.
**Likely Source Types:** Multi-brand content-management/strategy tooling docs,
agent-driven content-calendar/planning tools.
**Search Strategy:** Search "multi brand content strategy system," "content calendar
agent," "brand voice consistency automation."
**Exclusion Criteria:** Single-brand content-strategy material with no
multi-tenant/multi-voice angle (that's DOM-24's territory, not this one).
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Content strategy," "Content
planning," and "Brand consistency" — all describe the same strategic layer above
execution-level task decomposition. Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-002 — "project" in the Owner's
memory-architecture decision plausibly maps to "page/brand" here; treat this
mapping as INTERPRETATION, not confirmed FACT, until the Owner states it
explicitly. See `decisions/OD-002`.

### DOM-20 — Multi-modal content generation (text/image/video, narrative continuity)
**Research Question:** How do generation pipelines produce coherent multi-modal
content (text, image, and possibly video) as part of a single narrative unit, keeping
style/character/tone consistent across modalities and across a series?
**Why Hermes May Need It:** Directly named as the content agent's core job: "تولید
محتوا (متن، تصویر، احتمالاً ویدیو)... اغلب به‌صورت زنجیره‌ای/روایی."
**Evidence Needed:** Concrete multi-modal generation pipelines with explicit
cross-modal or cross-episode consistency mechanisms (e.g. persistent style/character
references), not just single-shot image/text generation demos.
**Likely Source Types:** Multi-modal generation agent repos, published pipelines for
serialized visual content (comics/story generation as an analog).
**Search Strategy:** Search "multi-modal content generation pipeline agent,"
"consistent character generation series," "text to image to video narrative
pipeline."
**Exclusion Criteria:** Single-modality generation demos with no series/continuity
element.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Content generation," made
explicitly multi-modal and narrative per the raw idea rather than left generic.
Evidence source: raw idea, 2026-08-23.

### DOM-21 — Publishing workflow operations
**Research Question:** What operational patterns handle the mechanics of publishing
approved content across social platforms — scheduling, cross-platform API
differences, retry/rollback on partial failure — as distinct from the approval
decision itself (DOM-07)?
**Why Hermes May Need It:** Publishing is the concrete irreversible action the whole
approval-gate principle protects; its operational reliability (not just the gate) is
its own capability need — a failed or double-posted publish is itself a
trust-damaging failure mode.
**Evidence Needed:** Concrete publish-pipeline implementations with visible
scheduling, multi-platform abstraction, and partial-failure/rollback handling.
**Likely Source Types:** Social-media-management tool docs/repos, publishing-API
wrapper libraries with reliability features.
**Search Strategy:** Search "social media publishing pipeline reliability,"
"scheduled post retry rollback," "cross platform publishing API abstraction."
**Exclusion Criteria:** Simple single-platform posting scripts with no
reliability/rollback handling.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Kept from seed list "Publishing workflows,"
explicitly distinguished from DOM-07 (decision-to-publish vs. mechanics-of-publishing
are different failure surfaces). Evidence source: raw idea, 2026-08-23.

### DOM-22 — Analytics & experimentation feedback loops
**Research Question:** How do systems close the loop from published-content
performance back into content strategy (DOM-19) and research (DOM-18) — measurement,
A/B-style experimentation on formats/hooks, and feeding results back as
strategy-adjustment signal?
**Why Hermes May Need It:** The "what has worked in the market" research role (b) and
a genuinely autonomous system both imply a feedback loop from actual performance data,
not just external market research.
**Evidence Needed:** Concrete analytics-to-strategy feedback implementations, not just
dashboards (a dashboard alone doesn't close the loop back into agent decisions).
**Likely Source Types:** Social-analytics tool docs/APIs, agent-driven experimentation
frameworks.
**Search Strategy:** Search "content performance feedback loop agent," "social media
analytics agent experimentation," "automated A/B test content."
**Exclusion Criteria:** Pure analytics/dashboard tools with no evidence of feeding
back into an automated decision.
**Priority:** MEDIUM
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** Merge of seed topics "Analytics" and
"Experimentation" — both describe the same measurement-to-strategy feedback
mechanism. Evidence source: raw idea, 2026-08-23.

### DOM-23 — Community management / audience engagement automation
**Status: EXCLUDED (2026-08-29) — resolved out of scope by explicit Owner
confirmation. Not researched; no discovery work performed or warranted.**

**Research Question:** N/A — moot. The question this domain would have asked
(how do agent systems handle audience engagement — replies, comments, DMs —
autonomously while respecting the same ambiguity/irreversibility/no-delete
principles as the two named agent types) is no longer applicable, since
Hermes will not perform this function at all.
**Why Hermes May Need It:** It does not. Owner-confirmed 2026-08-29: no
comment-or-DM-reply functionality exists in the current system design, and
audience engagement was never part of the intended scope — the raw idea's
broad framing ("managing multiple social pages as autonomously as
possible") that originally made this ambiguous does not extend to
engagement automation. This closes OQ-01 (`phase-m2/open-questions.md`)
with a definitive answer, not a guess either direction.
**Evidence Needed:** N/A — scope resolved, no further evidence required.
**Likely Source Types:** N/A.
**Search Strategy:** N/A. No Stage -2.2/-2.3/-2.4/-2.5 discovery work was
performed for this domain at any point, and none is warranted going
forward — this is a deliberate scope boundary, not a gap to fill.
**Exclusion Criteria:** N/A — the domain itself is the exclusion.
**Priority:** N/A (excluded domains are not prioritized)
**Rationale for Inclusion/Change:** Originally kept from the seed list as
"Community management" but marked BLOCKED (2026-08-23) rather than
silently dropped or included, since the raw idea neither named nor
excluded it — logged as OQ-01 for Owner resolution at the Stage -2.1
checkpoint. Resolved 2026-08-29: Owner explicitly confirmed this
capability area is out of scope. Status changes from BLOCKED (open
question) to EXCLUDED (deliberate, resolved scope boundary) — this
distinction matters for Phase -1: BLOCKED would have meant "still to be
decided," EXCLUDED means "decided, do not build this." Full correction
record: `HERMES_RESEARCH.md`, 2026-08-29 entry. Evidence source: raw idea,
2026-08-23 (originally ambiguous); Owner direct confirmation, 2026-08-29
(resolving).

### DOM-24 — Multi-tenant / multi-instance onboarding patterns
**Research Question:** Does `hermes-agent` (REPO-001) support running multiple
independent instances (one per social page) as a configuration change over shared
code — templated configs, tenant-scoped credentials/memory — or would Hermes need to
build a multi-tenancy layer on top of a framework designed for a single instance?
**Why Hermes May Need It:** Directly named as a goal: "افزودن یک صفحه‌ی جدید بدون
نیاز به یک پروژه‌ی از نو" (adding a new page without needing a from-scratch project).
Because the framework is fixed, whether this goal is achievable depends first on
what `hermes-agent` itself was designed to support, not on an abstract survey of
multi-tenant patterns.
**Evidence Needed:** `hermes-agent`'s configuration/deployment model (source-level) —
is per-instance state (config, credentials, memory) already isolated and
parameterized, or hard-coded/singleton-assumed; comparison multi-tenant
agent-configuration patterns to judge what a supplementing layer would need to look
like if the framework doesn't natively support it.
**Likely Source Types:** `hermes-agent` source/docs/deployment examples (primary);
secondarily, other agent-framework multi-instance/multi-config docs as comparison
baseline.
**Search Strategy:** Deep-audit `hermes-agent`'s config/deployment code first (Stage
-2.4, Dimension H — reusability/coupling). Then search "multi-tenant agent
configuration," "templated agent deployment" for comparison examples if a gap is
found.
**Exclusion Criteria:** Generic SaaS multi-tenancy material (database
row-level-security, etc.) with no agent-configuration angle — different problem
layer.
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** New domain, not present in Section 7.1 seed list.
Added because this is an explicit named goal in the raw idea with no existing seed
covering it. Evidence source: raw idea, 2026-08-23. Reframed 2026-08-23 around the
known base architecture per Owner Stage -2.1 checkpoint response — not one of the six
capabilities the Owner listed by name, but extended here on the same logic since
per-instance configuration is squarely a framework-architecture property, to be
confirmed empirically at Stage -2.4 rather than left generically framed.
**Owner Decision Note (2026-08-25):** OD-001 — "multi-tenant/multi-instance"
means multiple projects/pages under one owner, not multiple external
customers — confirms, does not change, this domain's existing framing. OD-002
— a new project/page must get an isolated per-project memory tier without
duplicating the shared global tier; a concrete provisioning requirement to
evaluate candidates against. See `decisions/OD-001`, `decisions/OD-002`.

### DOM-25 — Self-updating ecosystem-intelligence agent design
**Research Question:** How do systems architect an agent whose job is continuous
external-technology scouting (new repos, tools, patterns) that feeds recommendations
back into the parent system's own capability set — as distinct from scouting content
research (DOM-18), which looks outward at the *market*, not at Hermes' own tooling?
**Why Hermes May Need It:** Directly named as research-agent role (a): "رصد منابع
بیرونی (ریپو، ابزار، الگوهای تازه) برای به‌روز نگه‌داشتن خود هرمس" (monitoring
external sources — repos, tools, new patterns — to keep Hermes itself up to date).
Notably, this is structurally the same kind of activity as the current Phase -2
research process itself — a genuinely novel, self-referential capability need worth
its own focused domain.
**Evidence Needed:** Concrete "self-updating" or "technology-scouting" agent
implementations, or close analogs (dependency-update bots, changelog-watching agents,
research-digest agents) with visible recommendation/integration logic, not just
scraping.
**Likely Source Types:** Autonomous research-agent repos, dependency/technology
-radar automation tools, AI-research-digest agent projects.
**Search Strategy:** Search "autonomous technology scouting agent," "self-updating AI
system agent," "changelog watch agent recommend."
**Exclusion Criteria:** Simple RSS/changelog aggregators with no
recommendation/synthesis step (that's just a feed reader, not a research agent).
**Priority:** HIGH
**Status:** IN-PROGRESS
**Rationale for Inclusion/Change:** New domain, not present in Section 7.1 seed list.
Added because the raw idea names this as a distinct research-agent role with no
existing seed covering it, and it is distinctive enough (self-referential,
recommendation-producing) to warrant separate treatment from general "Knowledge
management." Evidence source: raw idea, 2026-08-23.
**Owner Decision Note (2026-08-25):** OD-004 gives this domain a name
("Hermes Control"), a concrete cadence (quarterly), and a broadened review
surface (Hermes' own knowledge/guidelines/workflows/tools/integrations/code,
not just external repos/tools) — sharpens, does not replace, the Research
Question above. OD-005 requires suggest-only behavior with structurally
enforced Owner approval (not a configurable default) for any candidate
pattern. OD-006 requires backup + reliable rollback specifically for the
update-application step. See `decisions/OD-004`, `decisions/OD-005`,
`decisions/OD-006`.

---

## Seed Reconciliation Log

Per Section 7.3, every material change from the Section 7.1 seed list is logged here
with justification, date, affected IDs, and change source.

| Date | Change | Seeds Affected | New/Affected Domain ID(s) | Source of Change | Justification |
|------|--------|----------------|---------------------------|-------------------|----------------|
| 2026-08-23 | DROPPED | Product discovery | — | Redundancy/irrelevance | This Phase's own scope-formation process (interview -> raw idea -> this registry) already performs the equivalent of product discovery for Hermes' concept; generic product-discovery methodology is not a Hermes *runtime capability* need, and researching it here would drift toward Phase -1 process work (out of scope per Section 3.2). |
| 2026-08-23 | DROPPED | Product requirements | — | Redundancy/irrelevance | Same reasoning as above; requirements traceability is already handled structurally by this Master Plan's own schemas (Section 9, P3), not by external research. |
| 2026-08-23 | DROPPED | Spec-driven development | — | Irrelevance (scope boundary) | Concerns the methodology for *building* Hermes (a Phase -1 engineering-process question), not a capability Hermes *needs at runtime*. Borderline call — flagged for Owner override if the intended scope is broader. |
| 2026-08-23 | DROPPED | Architecture documentation | — | Irrelevance (scope boundary) | Same reasoning as "Spec-driven development" — a build-process concern, not a Hermes runtime capability. Borderline call — flagged for Owner override. |
| 2026-08-23 | MERGED | Agent architecture; Single-agent vs multi-agent decisioning; Agent orchestration | DOM-01 | Redundancy (same underlying problem once scoped to Hermes' fixed 2-role case) | See DOM-01 rationale. |
| 2026-08-23 | MERGED | Agent role design; Agent contracts; Structured outputs | DOM-02 | Redundancy | See DOM-02 rationale. |
| 2026-08-23 | MERGED | Tool-use architecture; MCP/integration patterns | DOM-06 | Redundancy | See DOM-06 rationale. |
| 2026-08-23 | MERGED | Memory architecture; Decision history | DOM-11 | Redundancy | See DOM-11 rationale. |
| 2026-08-23 | MERGED | Long-running agents; Failure recovery | DOM-13 | Redundancy | See DOM-13 rationale. |
| 2026-08-23 | MERGED | Agent evaluation; Content review | DOM-15 | Redundancy | See DOM-15 rationale. |
| 2026-08-23 | MERGED | Cost control; Model routing | DOM-16 | Redundancy | See DOM-16 rationale. |
| 2026-08-23 | MERGED | Content research; Audience research | DOM-18 | Redundancy | See DOM-18 rationale. |
| 2026-08-23 | MERGED | Content strategy; Content planning; Brand consistency | DOM-19 | Redundancy | See DOM-19 rationale. |
| 2026-08-23 | MERGED | Analytics; Experimentation | DOM-22 | Redundancy | See DOM-22 rationale. |
| 2026-08-23 | ADDED | (new) | DOM-09 Ambiguity detection & clarification-seeking behavior | Evidence (raw idea) | Behavioral principle repeated 3x in raw idea, not covered by any seed. |
| 2026-08-23 | ADDED | (new) | DOM-10 Progressive autonomy / trust calibration over time | Evidence (raw idea) | Explicit "reduce owner involvement over time" goal; distinct from static HITL seed. |
| 2026-08-23 | ADDED | (new) | DOM-24 Multi-tenant / multi-instance onboarding patterns | Evidence (raw idea) | Explicit "add a page without a from-scratch project" goal; no seed covered it. |
| 2026-08-23 | ADDED | (new) | DOM-25 Self-updating ecosystem-intelligence agent design | Evidence (raw idea) | Explicit research-agent role (a); no seed covered it; distinctive/self-referential enough to separate from Knowledge management. |
| 2026-08-23 | FLAGGED (kept, not dropped) | Community management | DOM-23 (BLOCKED) | Newly discovered need — ambiguous | Raw idea's overall framing ("manage pages as autonomously as possible") could imply engagement automation, but neither named agent type covers it. Not silently dropped or included — see Open Questions. |
| 2026-08-23 | KEPT, narrowed | Task decomposition | DOM-03 | Evidence (raw idea) | Narrowed to narrative/chained-content framing for higher expected information value. |
| 2026-08-23 | KEPT, narrowed | Human-in-the-loop | DOM-07 | Evidence (raw idea) | Narrowed to irreversible-action framing explicit in raw idea. |
| 2026-08-23 | KEPT, narrowed | Content generation | DOM-20 | Evidence (raw idea) | Narrowed to multi-modal + narrative-continuity framing explicit in raw idea. |
| 2026-08-23 | KEPT as-is | Skill design; Prompt/system-instruction architecture; Permissions & least privilege; Context engineering; Observability; Security and governance patterns; Publishing workflows | DOM-04, DOM-05, DOM-08, DOM-12, DOM-14, DOM-17, DOM-21 | No change needed | Seed already well-scoped to a distinct, non-redundant Hermes need. |

**Not carried forward but not formally "domains":** the four dropped seeds above never
received a Domain ID (Section 7.2 records are only created for domains entering the
active registry) and are not tracked with DROPPED status for that reason — this table
row is their complete record.

### Revision 2 (2026-08-23) — Owner Stage -2.1 checkpoint response

| Date | Change | Affected | Source of Change | Justification |
|------|--------|----------|-------------------|----------------|
| 2026-08-23 | CONFIRMED | Overall registry scope; drops of Spec-driven development and Architecture documentation | Owner checkpoint response | Owner explicitly approved the registry and both contested drops as-is; no structural change from this confirmation. |
| 2026-08-23 | HELD (no change) | DOM-23 (Community management) | Owner checkpoint response | Owner has not yet decided; explicitly instructed to leave BLOCKED. OQ-01 in `open-questions.md` remains open. |
| 2026-08-23 | ADDED | REPO-001 `NousResearch/hermes-agent`, entered as `## Known Base Architecture` | Owner-supplied fact (final, non-negotiable, decided outside Phase -2) | Owner disclosed Hermes will be built on this framework. Per Section 2.3/5.1, Phase -2 does not choose or formally approve architecture — but a known input from the Owner changes what "best available pattern" research means for framework-governed domains. Flagged explicitly as "known base architecture, not a discovered candidate" and reserved as the mandatory first Stage -2.4 deep-audit target, ahead of normal triage-discovered repos. |
| 2026-08-23 | REFRAMED | DOM-01, DOM-02, DOM-04, DOM-06, DOM-11, DOM-13, DOM-16 | Owner-supplied fact (named these six capability areas explicitly) | Research Question shifted from "what's the best pattern in the world" to "how does hermes-agent implement this, does it satisfy Hermes' needs, what's the gap" — see each domain's updated Research Question and Rationale for Inclusion/Change. |
| 2026-08-23 | REFRAMED (extended) | DOM-24 | Inference from Owner-supplied fact, not explicitly named by Owner | Multi-tenant onboarding is squarely a framework-architecture property (per-instance config/credential isolation); reframed on the same logic as the six named domains. Flagged as an extension beyond the Owner's explicit list for visibility — to be confirmed, not assumed, at Stage -2.4. |

**Domains considered for reframing and left unchanged:** all other 17 domains retain
their original green-field research questions. Several (e.g. DOM-05 prompt/
instruction architecture, DOM-07/09/10 human-control layer, DOM-12 context
engineering, DOM-14 observability, DOM-15 evaluation/quality gating, DOM-17 security)
plausibly touch framework internals too, but the Owner named a specific six and this
revision did not want to guess a broader boundary unprompted. Per the `## Known Base
Architecture` section above, any of these found during Stage -2.4 audit to be
governed by `hermes-agent` will be reframed at that point on the same basis.

### Revision 3 (2026-08-29) — OQ-01 resolved, post-phase-end

| Date | Change | Affected | Source of Change | Justification |
|------|--------|----------|-------------------|----------------|
| 2026-08-29 | RESOLVED — status change BLOCKED -> EXCLUDED | DOM-23 (Community management / audience engagement automation) | Owner direct confirmation | Owner explicitly confirmed DOM-23 is out of scope: no comment-or-DM-reply functionality exists in the current system design, and this was never part of the intended scope. Closes OQ-01 (`phase-m2/open-questions.md`) with a definitive answer. This is a scope resolution, not a research finding — no discovery work was performed for this domain at any stage, and none is warranted now that it is excluded. Full record: `HERMES_RESEARCH.md`, 2026-08-29 entry. |
