# Deep Audit — REPO-041: NimbleCoAI/hermes-swarm-map ("Swarm Map" / SM / formerly HSM)

Schema: Master Plan Section 9.3. Stage -2.4, 2026-08-25.

**Note on authorship:** the fork originally assigned to audit REPO-001/040/041
together completed REPO-001 (`nousresearch-hermes-agent.md`) and REPO-040
(`nimblecoai-hermes-agent.md`) before hitting a session limit. This file
completes the trio, written directly by the primary Phase -2 session using the
same clone (`git clone --depth 1 https://github.com/NimbleCoAI/hermes-swarm-map.git`,
old URL — auto-redirects; see Dimension I) and the same method: read actual
code, not README claims, with FACT/INTERPRETATION/UNKNOWN labeling per
Section P5. Cross-references REPO-001 and REPO-040's audits, both read first.

---

## A — Architecture

**FACT:** Next.js (App Router) web application — `app/api/`, `lib/services/`,
`middleware.ts`, `components/`. Not a Hermes agent itself; a control-plane
dashboard/API that deploys and manages **containers running the hermes-agent
runtime**, one container per agent (`lib/services/harness.ts`,
`lib/services/docker.ts`). `docs/architecture/image-vs-hsm-boundary.md`
(read in full) formally separates three layers: the immutable Docker image
(hermes-agent runtime), per-deployment "HSM scaffolding" (config/plugins/hooks
installed at agent-creation time), and opt-in git-sourced "artefact" packages
(indexed in a separate `cyborg-garden/artefact-registry`).

**Verdict: Strong — a genuinely distinct architectural layer (orchestration/
fleet-management), not a hermes-agent fork or a duplicate of REPO-001/040's
concerns. Clean separation of what belongs in the image vs. the control plane.**

## B — Agent Design

**FACT:** Does not define its own agent roles/contracts — it deploys and
configures hermes-agent instances (each with its own `SOUL.md`,
`config.yaml`) via a setup wizard (`app/api/setup/deploy/route.ts`) and a
harness service (`lib/services/harness.ts`). Per-agent identity is scaffolded
via `defaultSoulContent()` in `harness.ts` (read directly, lines ~262-303),
which writes a templated system prompt describing the agent's platform
surfaces, memory-isolation behavior, session lifecycle, and admin
relationship — a real, inspectable onboarding template, not just marketing
prose.

**Verdict: N/A for agent-contract design (out of this repo's scope by
architecture — see Dimension A) — Moderate for the operational
identity-scaffolding mechanism it does own.**

## C — Context & Memory (the DOM-24 load-bearing dimension)

**FACT (default deployed runtime, verified directly in code, not inferred):**
`lib/services/harness.ts` line 23: `const DEFAULT_IMAGE_REPO =
'cyborg-garden/hermes-agent-mt'`; `lib/services/config.ts` line 70:
`defaultImage: 'ghcr.io/cyborg-garden/hermes-agent-mt:latest'`. Confirmed
consistently across `lib/types.ts`, `lib/services/registry.ts`,
`lib/services/harness-compose.ts`, and test assertions in
`lib/services/__tests__/local-build.test.ts` that explicitly assert the
compose output does **NOT** contain `image: nousresearch/hermes-agent` (i.e.
this is a deliberate, tested choice, not an accident). **This resolves an
open question from Dimension C of `nimblecoai-hermes-agent.md`:** Swarm Map
does not run plain upstream REPO-001 — it deploys REPO-040
(`cyborg-garden/hermes-agent-mt`, the fork with the real, tested `context_id`
memory-scoping patch) by default.

**FACT:** The default `SOUL.md` template (`harness.ts`, quoted in full):
"**Memory isolation:** Your memory is scoped per-context. What you learn in
one group chat stays in that group... Never reference or leak information
between different conversations." **INTERPRETATION, now resolved rather than
left as a concern:** on first read this looked like it could be a purely
prompt-based (soft) isolation claim with no structural backing — but given the
confirmed default image is `hermes-agent-mt` (which has the tested,
code-verified `context_id` routing per `nimblecoai-hermes-agent.md`
Dimension B/C), this system-prompt text functions as the agent's own
awareness of a real underlying structural guarantee, not a substitute for one.
The isolation is real at the runtime layer; the prompt text reinforces it at
the behavior layer. This distinction matters and should not be conflated —
Stage -2.5 pattern extraction should cite the underlying `context_id` patch
(REPO-040) as the mechanism, not this SOUL.md text.

**FACT:** `docs/architecture/image-vs-hsm-boundary.md`'s "Decision Framework"
explicitly classifies "Approval system, path security... dangerous-command
detection" as things that "→ Image. Security patterns must be immutable...
can't be optional, can't be overridden by config" — i.e. this project's own
stated design philosophy agrees with the Stage -2.4 cross-cutting observation
already flagged in `nousresearch-hermes-agent.md` (that opt-in/off-by-default
safety mechanisms are a real gap) — Swarm Map's contributors have
independently arrived at "security boundaries belong in the immutable layer,
not config," which is corroborating evidence for that same design principle
from a second, independent source.

**Verdict: Strong — this repo, combined with REPO-040, is the clearest
evidence found across Stage -2.3/-2.4 that DOM-24's memory-isolation gap has
a real, structurally-enforced (not merely prompted) solution in active
production use, deployed by default, not as an opt-in afterthought.**

## D — Reliability

**FACT:** `lib/services/db-snapshot-scheduler.ts` exists (a scheduled backup
mechanism for Swarm Map's own state DB — not hermes-agent's). Not read in
full this pass — **UNKNOWN** whether this is cron-based, its retention
policy, or whether backups are themselves subject to deletion/rotation
(relevant if Swarm Map's own operational state were ever treated as an
audit-log source for DOM-11 — flag as a follow-up, not resolved here).

**FACT:** `middleware.test.ts` (6KB) and 100 total `*.test.ts`/`*.spec.ts`
files exist across the repo (counted directly via `find`), indicating a real,
non-trivial test culture, not a thin veneer.

**Verdict: Moderate (provisional) — real test investment confirmed; deeper
reliability claims (backup/recovery specifics) not verified this pass.**

## E — Human Control

**FACT:** `docs/surface-permissions.md` exists as a named doc (not opened in
full this pass). The default `SOUL.md` template states: "**Group approval:**
You only respond in groups that your admin has approved. If you're added to a
new group, you'll check with HSM before engaging" — an explicit,
templated group-approval gate description.

**FACT:** `app/api/harnesses/[id]/policy/route.ts` implements a real
`budget-check` action (verified by reading the route directly): it sums
`budgetUsd` across all API keys assigned to a harness/agent, compares against
month-scoped spend, and returns `{budget, exceeded}`. **UNKNOWN — not
resolved this pass despite a targeted search:** whether `exceeded: true` is
ever automatically *acted on* (pausing/stopping the agent container) versus
only being available for a caller (dashboard UI, or an as-yet-unfound
scheduled job) to poll and act on manually. Grepped for `budget-check` callers
across `app/` and `lib/` and found only the route itself, its test file, and
`lib/services/usage.ts` (which the route likely calls into, not a caller of
it) — no automatic-enforcement call site was found, but a full `components/`
(dashboard UI) sweep was not completed, so this is UNKNOWN, not confirmed
absent. This directly mirrors the same "claims tracking, enforcement
mechanism uncertain" pattern flagged for REPO-001's billing subsystem
(Dimension G there) — worth resolving together at Stage -2.5/-2.6 rather than
treating as two unrelated open questions.

**Verdict: Moderate — real, real-code group-approval concept and a real
budget-check computation exist; whether either is automatically enforced
(vs. advisory/dashboard-only) is UNKNOWN pending a fuller sweep, consistent
with this audit's discipline of not inflating an unverified claim to FACT.**

## F — Evaluation

**FACT:** No content-quality or agent-output evaluation harness found in this
pass's targeted searches (`lib/services`, `app/api`) — expected, since this
repo's job is fleet orchestration, not content generation; DOM-15 is out of
scope for this repo by design, not a gap in it.

**Verdict: Absent — but not applicable; this repo doesn't claim to cover
DOM-15 and the omission is consistent with its actual architectural role.**

## G — Operations

**FACT:** `lib/model-catalog.ts` and `lib/pricing.ts` exist, and the most
recent commit in the repo (`c95cebb`, verified via clone, dated
2026-08-24T12:17:10+12:00) is literally a pricing/model-catalog update
("feat(catalog): add GLM-5.3 as fleet primary; price at $1.40/$4.40 (#229)")
— real, current, actively-maintained cost/model-routing infrastructure
directly relevant to DOM-16, and evidence of ongoing maintenance investment
specifically in this area.

**FACT:** "Model Cascade — Ordered fallback chains across providers... Per-agent"
is a README claim; `lib/model-catalog.ts` and the harness deploy path
reference cascade/fallback config surfaces, but the actual fallback-execution
logic (does a real API call retry against the next model in the chain on
failure) was not traced to a specific runtime call site this pass — flag as
**UNKNOWN**, not confirmed, consistent with this audit's standard for
distinguishing "the config surface exists" from "the enforcement/execution
path was verified."

**Verdict: Moderate — real, current cost-tracking/pricing infrastructure
confirmed; cascade-fallback *execution* (vs. just config) UNKNOWN pending
follow-up.**

## H — Reusability

**FACT:** AGPL-3.0 licensed (see Dimension J) — this has real reusability
implications distinct from REPO-001/040's permissive MIT: network use of a
modified version triggers source-disclosure obligations under AGPL. Any
future Hermes-side use of this project's *code* (not just its patterns) would
need to account for that, unlike REPO-001/040.

**FACT:** Explicitly designed as a control plane over the container-per-agent
model — `docs/architecture/image-vs-hsm-boundary.md`'s three-layer split
(image / HSM scaffolding / opt-in artefact repos) is itself a reusable
architectural pattern for "how to cleanly separate an immutable runtime from
per-deployment config from optional capability packages," independent of
whether Hermes ever adopts this specific codebase.

**Verdict: Strong for the architectural pattern (image/scaffolding/artefact
separation); Moderate for direct code reuse given the AGPL license's
copyleft obligations, which need explicit Owner attention if code reuse
(not just pattern study) is ever considered — flagged for Stage -2.5/-2.6,
not decided here per Section 2.3/5.1.**

## I — Evidence

**FACT (verified via `gh repo view NimbleCoAI/hermes-swarm-map`):** 20 stars,
1 fork, created 2026-05-13, **last push 2026-08-24T00:17:12Z** (i.e. pushed to
the day before this audit) — genuinely active, not stale. 260 total commits
(verified via `gh api .../commits` pagination header, `rel="last"` page 260 at
1 commit/page). Not archived.

**FACT:** `README.md`'s own framing is unusually candid about limitations —
"**Runtime support is not symmetrical yet.** Hermes is the mature path; Letta
support is read-only plus send-a-message... we would rather you read a boring
matrix than discover the gap after deploying" — this kind of self-disclosed
limitation (rather than uniform marketing confidence) is a positive
evidence-quality signal per the same logic already applied to `agentward` in
`agentward-ai-agentward.md`.

**One naming/URL correction, consistent with REPO-040's audit:** this repo's
own README refers to itself as "Swarm Map (SM) — formerly Hermes Swarm Map /
HSM" and is a project of "NimbleCo" — the org-rename noted in
`nimblecoai-hermes-agent.md` (NimbleCoAI → cyborg-garden) applies to the
*deployed image* (`cyborg-garden/hermes-agent-mt`), but this repository
itself, as of the clone/`gh` check performed 2026-08-25, is still hosted
under the `NimbleCoAI` org (`github.com/NimbleCoAI/hermes-swarm-map`) — do
NOT assume it moved to `cyborg-garden` too without independently checking;
these are two different repos with two different current locations, verified
separately.

**Verdict: Strong — active, current, candid about its own gaps, all load-bearing
claims checked in this pass held up or were explicitly marked UNKNOWN rather
than assumed.**

## J — License

**FACT (read directly from the cloned `LICENSE` file):** GNU Affero General
Public License v3.0 (AGPL-3.0), confirmed independently via
`gh repo view`'s `licenseInfo: {key: "agpl-3.0", ...}`. Materially different
from REPO-001/040's MIT — copyleft, with network-use disclosure triggers.
A `NOTICE` file also exists (960 bytes, not read in full this pass).

**Verdict: Moderate — clear and unambiguous (Strong on clarity), but the
license itself imposes real reuse constraints (Moderate on permissiveness)
that don't apply to the other two repos in this trio.**

---

## Cross-Cutting Observation (ties together the REPO-001/040/041 trio)

Read together, the three audits in this trio tell one coherent, evidence-backed
story about DOM-24:

1. **REPO-001** (upstream): tenant/memory isolation exists but is
   config-heavy (whole profile per boundary) and the lighter automatic
   `context_id` fix is a still-open, unmerged PR (#47552).
2. **REPO-040** (`cyborg-garden/hermes-agent-mt`): is that exact fix, real
   and tested, running in production, pending upstream merge.
3. **REPO-041** (this repo): is the orchestration layer built specifically
   to deploy REPO-040 (not REPO-001) by default, at fleet scale, with its
   own per-agent budget/model-cascade/group-approval config surface layered
   on top.

This is a complete, verifiable answer to DOM-24's research question for the
specific memory-isolation failure mode the community raised: **the fix
exists, runs in production, and is packaged into a deployable control plane
— it has just not yet been merged into the framework the Owner named as
Hermes' base architecture.** Whether Hermes should wait for the upstream
merge, adopt the fork directly, or build an equivalent mechanism itself is a
Stage -2.5/-2.6 recommendation question, explicitly not decided here (Section
2.3/5.1 — Phase -2 documents, does not choose).

Two open UNKNOWNs recur across all three audits and should be resolved
together, not separately, at Stage -2.5/-2.6: (a) whether *any* of the three
repos' budget/cost-control mechanisms actually enforce (block/throttle) vs.
only track/report, and (b) whether hermes-agent's memory hard-delete paths
(Dimension C, `nousresearch-hermes-agent.md`) are reachable autonomously or
user-command-only.

## Summary Table

| Dim | Verdict |
|---|---|
| A — Architecture | Strong |
| B — Agent design | N/A (out of scope) / Moderate (identity scaffolding) |
| C — Context & memory | Strong |
| D — Reliability | Moderate (provisional) |
| E — Human control | Moderate (enforcement UNKNOWN) |
| F — Evaluation | Absent (not applicable by design) |
| G — Operations | Moderate (cascade execution UNKNOWN) |
| H — Reusability | Strong (pattern) / Moderate (AGPL code reuse) |
| I — Evidence | Strong |
| J — License | Moderate (clear but copyleft) |

## Open Follow-Ups for Stage -2.5/-2.6 (not resolved this pass)

1. Resolve whether `budget-check`'s `exceeded: true` result is ever
   automatically acted on (pause/stop) — search `components/` (dashboard UI)
   and any scheduled-job code not covered by this pass's targeted searches.
2. Trace the model-cascade *execution* path (not just the config/catalog
   surface) to confirm real fallback-on-failure behavior.
3. Read `docs/plans/opinionated-config.md` and `docs/patterns/use-case-packages.md`
   in full — named but not opened this pass; may bear on DOM-04 (skill/plugin
   packaging) given the "artefact repo" concept described in Dimension A.
4. Read `db-snapshot-scheduler.ts` in full for Swarm Map's own state-backup
   retention policy (relevant if ever treated as an audit-log source).
