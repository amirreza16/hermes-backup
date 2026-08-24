# Deep Audit — REPO-001: NousResearch/hermes-agent

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4, 2026-08-24.
Status: Known base architecture (Owner-disclosed, not a discovered candidate —
see `research-domains.md` `## Known Base Architecture`). Full adversarial
review still applies per Section 13; being the mandated substrate is not
evidence of quality.

**Method:** shallow clone (`git clone --depth 1`) inspected directly — repo
structure, `docs/*.md`, `AGENTS.md`, source files across `gateway/`, `agent/`,
`hermes_state.py`, `plugins/memory/*`, `cron/`, `skills/*`, `evals/*`, `tests/*`
— plus direct GitHub API/CLI queries (`gh api`, `gh issue view`, `gh pr view`)
for facts not visible in a shallow clone (commit dates, issue/PR state, star
counts). No claim below is taken from README prose alone; each cites its
concrete source. Per Section P5 discipline, claims are labeled **FACT**
(directly verified in code/docs/API), **INTERPRETATION** (a reasonable reading
of verified facts), or **UNKNOWN** (not resolved at this depth) — never stated
as confident prose without that label, given this project's established
history of hallucinated hermes-agent claims (a prior "cheat sheet" PDF was
discarded for fabricating a `hermes memory reindex` command and a "GEPA
reflection loop" that do not exist).

---

## A — Architecture

**FACT:** `AGENTS.md` states the design philosophy explicitly: "The core is a
narrow waist; capability lives at the edges... Most new capability should
arrive as a CLI command + skill, a service-gated tool, or a plugin — not as
core surface." This is corroborated by the actual layout: a large `agent/`
core (~40+ single-purpose modules: `context_engine.py`, `tool_executor.py`,
`native_compaction.py`, `conversation_compression.py`, etc.), a `plugins/`
tree with pluggable subsystems (8 distinct memory backends alone — see
Dimension C), and a `skills/` tree of natural-language-invoked capabilities.

**FACT:** Single-agent-with-subagent-delegation model, not a fixed multi-role
graph. `agent/delegation_context.py`, `hermes_state.py`'s
`_delegate_from`/`parent_session_id` marker chain (see `_collect_delegate_child_ids`,
line ~313), and `tests/test_background_review_session_isolation.py` all point
to one agent core that can spawn delegate subagent sessions (tracked via a
parent/child session marker in the same SQLite state DB), not the
two-fixed-named-roles (content-generation + research) shape Hermes' raw idea
describes. There is no evidence of a first-class "role" or "contract" type
distinct from a session/delegation relationship.

**FACT:** State is centralized in one SQLite database per profile
(`hermes_state.py`, `DEFAULT_DB_PATH = get_hermes_home() / "state.db"`) plus
on-disk transcript files, not a distributed/event-sourced architecture.

**Verdict: Moderate — real narrow-waist plugin architecture with genuine
separation of concerns, but its native unit is "one agent + delegated
subagents + plugins/skills," not "fixed named roles with explicit contracts,"
which is the shape DOM-01/DOM-02 actually ask about. Hermes would need to
build its two-role, approval-gated shape on top of this substrate, not find
it pre-built.**

## B — Agent Design

**FACT:** No first-class "role" or typed inter-agent contract abstraction was
found. Delegation (`agent/delegation_context.py`) passes context to a subagent
session; there is no schema-enforced handoff object analogous to
PydanticAI's `output_type` or OpenAI Agents SDK's typed handoffs (see
`repo-catalog.md` REPO-003, REPO-004 for what that looks like elsewhere).

**FACT:** `write_approval.py` (`tools/write_approval.py`) implements a real
per-subsystem (memory vs. skills) approval gate with staged pending records
under `<HERMES_HOME>/pending/{memory,skills}/<id>.json`, distinguishing
foreground (interactive) writes from `background_review` (an autonomous
self-improvement fork that runs after a turn and decides what to save
unsupervised — the module's own docstring names this as "the source of the
'wrong assumptions' users complained about"). **The gate defaults to
disabled**: "`false` (default) — write freely (the pre-gate behaviour)."

**INTERPRETATION:** This is directly relevant to DOM-07 — a real, mature
approval-gate mechanism exists natively, but ships opt-in/off, meaning a
stock hermes-agent deployment writes memory/skills autonomously (including via
the background_review fork) unless an operator explicitly turns
`write_approval` on. This is the same "capability exists, ships opt-in-off"
pattern found again in Dimension C/D below — worth flagging as a recurring
posture across the codebase, not a one-off.

**Verdict: Moderate — a real, well-designed approval-gate primitive exists
(better evidence than most Stage -2.3 comparison candidates), but it is not
Hermes' default behavior and there is no typed role/contract system at all.**

## C — Context & Memory

**FACT (memory backends):** `plugins/memory/` contains 8 pluggable memory
backends: `holographic` (native default — SQLite-backed, `store.py`),
`mem0`, `honcho`, `supermemory`, `openviking`, `retaindb`, `hindsight`,
`byterover`. Each is a real plugin with `plugin.yaml`, `README.md`, and
implementation, not a stub.

**FACT (deletion, holographic backend):** `plugins/memory/holographic/store.py`
contains real, unconditional `DELETE FROM facts` / `DELETE FROM fact_entities`
/ `DELETE FROM memory_banks` statements (lines 338, 366, 368, 561) — i.e. the
native memory backend supports hard deletion of stored facts, not just
soft-delete/append-only. **UNKNOWN** at this depth whether these deletes are
only reachable via explicit user command (e.g. "forget X") or can also fire
autonomously; the call sites were not traced this pass — flag for a follow-up
grep before treating this as either a violation or a non-issue for DOM-11.

**FACT (session/transcript auto-deletion — directly relevant to DOM-11):**
`hermes_state.py` defines `maybe_auto_prune_and_vacuum(retention_days: int =
90, ...)` (line ~14375), explicitly documented as "Designed to be called once
at startup from long-lived entrypoints (CLI, gateway, cron scheduler)." It
permanently deletes ended sessions inactive for `retention_days` (default 90)
**and their on-disk transcript files** (`.json`/`.jsonl`/`request_dump_*`) via
`prune_sessions()`. **FACT:** its only call site in `gateway/run.py` (line
~7188) is gated: `if _sess_cfg.get("auto_prune", False):` — **disabled by
default**. A sibling checkpoint-pruning path (`gateway/run.py` line ~7208,
`checkpoints.auto_prune`) is gated the same way, also default `False`.

**INTERPRETATION:** This is the single most direct, code-verified finding for
DOM-11. Stock hermes-agent ships a real, permanent, self-initiated
history-deletion mechanism (not soft-delete, not archival — DB rows and
transcript files are removed) that would directly violate Hermes' "the system
never on its own deletes anything from memory/history" principle **if
enabled**. As shipped, it is off by default, so a default deployment does not
violate the principle — but Hermes would need to either explicitly never set
`auto_prune: true`/`checkpoints.auto_prune: true` (a config discipline to
document and enforce, not a structural guarantee) or fork/patch this path
entirely for a hard guarantee. This is a genuine, actionable gap for Stage
-2.5/-2.6, not resolved by "default is safe" alone, since a documented default
is one config change away from violation.

**FACT (tenant/context isolation — the DOM-24 finding, verified beyond the
issue thread as instructed):**
1. `gateway/profile_routing.py`, documented at `docs/profile-routing.md`
   (read directly), implements profile-based inbound message routing:
   `config.yaml`'s `profile_routes` maps platform + `guild_id`/`chat_id`/
   `thread_id` combinations to named profiles. Each profile gets a fully
   separate `HERMES_HOME` (via `_profile_runtime_scope` in `gateway/run.py`),
   meaning separate `MEMORY.md`, `USER.md`, `SOUL.md`, sessions, and tools.
   Requires `gateway.multiplex_profiles: true`; with it off, `profile_routes`
   is ignored entirely (docs, verbatim).
2. **FACT (verified via `gh api`):** the first commit touching
   `gateway/profile_routing.py` is `c8f235a`, "feat(gateway): allow selective
   multiplex profile serving," dated 2026-08-10/11 — i.e. this is a recent
   mainline addition, not long-standing.
3. **FACT (verified via `gh issue view 34352 --repo NousResearch/hermes-agent`):**
   issue #34352, opened 2026-05-29, states "one agent = one tenant. Memory is
   global, sessions don't scope by tenant." This was accurate when filed but
   is **now partially outdated** given (1)-(2) above.
4. **FACT (verified via `gh pr view 47552`):** the issue thread names a
   finer-grained fix — PR #47552, "feat(memory): add opt-in `context_id`
   scoping for per-channel/tenant memory isolation" — as "the core fix this
   issue is about," because profile-based isolation requires a whole separate
   profile per context (heavier-weight), whereas `context_id` scoping would
   isolate memory *writes* automatically within one profile (so a fact
   learned in a DM does not leak into a group session, without provisioning a
   new profile per DM). **This PR is OPEN, not merged**, as of 2026-08-24. It
   was opened by NimbleCoAI (`headRepositoryOwner: NimbleCoAI`,
   `feat/memory-context-id-scoping`) — the same organization behind REPO-040
   (see that audit for the actual `context_id` implementation, pre-upstream).
5. **FACT:** `docs/ADR.md`'s 2026-07-13 entry ("Scope plugin manager state by
   Hermes home/profile") independently confirms cross-profile state leakage
   was a real, actively-worked bug class at the plugin-manager layer (not just
   memory) — the fix scopes the plugin manager singleton per resolved home
   path to stop "a profile switch... silently keep serving a previous
   profile's already-imported submodule code/state."

**Verdict: Moderate — real, mainline, documented per-profile isolation exists
and is actively being hardened (ADR evidence of ongoing bug fixes in this
exact area), but it is opt-in/config-heavy (a whole profile per isolation
boundary) rather than the lighter automatic per-context scoping the community
explicitly asked for, which remains an open, unmerged PR. Treat DOM-24 as
"partially solved, actively in motion" — not "solved" and not "absent."**

## D — Reliability

**FACT:** `cron/scheduler.py` plus `cron/jobs.py`, `cron/executions.py`,
`cron/lifecycle_guard.py`, `cron/monitor.py` form a real internal cron/job
scheduling subsystem (not delegated to an external scheduler). `docs/chronos-managed-cron-contract.md`
exists as a named architecture doc for this subsystem (not opened in full this
pass — flag for a follow-up read before treating its contents as verified).

**FACT:** `hermes_state.py` contains extensive, hard-won crash-safety
engineering around its own SQLite usage — WAL checkpoint discipline
(`PRAGMA wal_checkpoint(PASSIVE)` vs. `TRUNCATE`, with inline comments
documenting a real production incident: a `TRUNCATE` checkpoint strategy
"caused B-tree corruption on large concurrent-access databases" and was
replaced), lock-contention handling for concurrent cron-triggered connections,
and idempotent auto-maintenance (`min_interval_hours` throttling on
`maybe_auto_prune_and_vacuum`). This reads as a mature, battle-tested
persistence layer, not a naive one.

**Verdict: Strong — real internal scheduler, and unusually detailed
crash-safety/corruption-avoidance engineering in the state layer, with
comments citing specific past incidents rather than aspirational claims.**

## E — Human Control

**FACT:** `write_approval.py` (Dimension B) is the primary approval-gate
mechanism found — per-subsystem (memory/skills), staged review, distinguishes
foreground vs. autonomous-background origin. **Off by default.**

**UNKNOWN at this depth:** whether an equivalent approval gate exists for
*publishing*-class actions specifically (vs. memory/skill writes) — no
`publish_approval` or platform-send-confirmation module was found in this
pass's targeted searches, but a full `tools/` directory sweep was not
completed. This is a material open question for whoever picks up Hermes'
content-agent design: DOM-07's specific need (confirm before an irreversible
publish) may not have a native analog here at all, distinct from the
memory/skill write-approval gate that does exist.

**Verdict: Moderate — a real, non-trivial approval-gate primitive exists for
memory/skill writes (off by default); publish-specific approval gating is
UNKNOWN, not confirmed absent, and needs a dedicated follow-up pass before
Stage -2.5 treats this dimension as settled.**

## F — Evaluation

**FACT:** `evals/` contains real eval harnesses with a consistent
fixtures/runner/report pattern for internal mechanisms: `evals/readtool/`,
`evals/compaction/` (includes `test_region_scoping.py`, `policies.py`),
`evals/browser_use/`. These evaluate hermes-agent's own core capabilities
(does the read tool behave correctly, does compaction preserve the right
content), not content-domain quality.

**INTERPRETATION:** This is capability-regression evaluation, not the
pre-publish content quality gate DOM-15 needs (reviewer/critic agent
gating a content draft before a human sees it) — expected, since that is a
domain-specific concern Hermes' own content pipeline would need to add on
top, not something a general-purpose agent framework would ship natively.

**Verdict: Moderate for internal-capability evals (real, structured); Absent
for anything resembling DOM-15's specific content-quality-gate need.**

## G — Operations

**FACT:** `agent/billing_usage.py`, `agent/billing_view.py`,
`agent/usage_pricing.py`, and `agent/aux_accounting.py` exist and form a real
usage/cost-tracking subsystem; `docs/billing-lifecycle.md` is a named
architecture doc for it (not opened in full this pass).

**UNKNOWN at this depth:** whether this amounts to DOM-16's specific need
(active budget caps / cheap-first model-routing enforcement, not just
usage tracking/reporting) — the module names suggest tracking and display,
not necessarily enforcement; this needs a dedicated read of
`docs/billing-lifecycle.md` and the actual billing modules before Stage -2.5
treats DOM-16 as either satisfied or gapped by this repo. Flag explicitly as
open, not resolved.

**Verdict: Moderate-Weak (provisional) — real cost-tracking infrastructure
confirmed to exist; whether it enforces budgets (vs. just reports usage) is
UNKNOWN pending a follow-up read, not yet a Weak/Absent verdict by inspection.**

## H — Reusability

**FACT:** The plugin/skill architecture (Dimension A) and the profile
multiplexing system (Dimension C) both point toward genuine modularity —
`skills/` uses `SKILL.md` files (e.g. `skills/creative/ascii-video/SKILL.md`,
`skills/social-media/xurl/SKILL.md`) matching the Claude Skills shape closely
(directly relevant to DOM-04's bridging question — native compatibility looks
strong, not requiring a translation layer).

**FACT:** Multi-instance/multi-tenant support exists (Dimension C) but via
profile routing/multiplexing (config-heavy, one profile per isolation
boundary) rather than a lightweight "drop a config, get a new tenant" model
like `repo-catalog.md` REPO-043 (`yerdaulet-damir/langgraph-sales-agent`).
Hermes' "add a new page without a from-scratch project" goal (DOM-24) is
achievable with this framework, but the operational weight of "one profile
per page" (separate HERMES_HOME, separate memory/skills/sessions per profile)
should be weighed against a lighter per-context scoping approach if/when PR
#47552 or an equivalent lands.

**Verdict: Strong for skill/plugin modularity (DOM-04); Moderate for
multi-instance reusability (DOM-24) — real and native, but heavier-weight than
some comparison baselines found in Stage -2.3.**

## I — Evidence

**FACT:** Documentation quality is unusually high for an open-source agent
framework — `docs/ADR.md` records real architecture decisions with dated
entries, explicit context/decision/consequences structure, and citations to
specific production incidents (the WAL TRUNCATE corruption incident, the
plugin-manager cross-profile leak). `docs/profile-routing.md` is precise and
matches the actual code paths cited (`gateway/profile_routing.py`,
`gateway/run.py`'s `_profile_name_for_source`) — verified these functions
exist at the stated locations.

**No doc-vs-code disagreement found in the areas inspected this pass**
(profile routing, auto-prune, write-approval) — docs describe real, current
behavior accurately where checked. This is a materially different picture
than the discarded "cheat sheet" PDF, which fabricated commands/concepts
outright; the *official* in-repo docs inspected here held up under direct
code verification.

**UNKNOWN:** whether this holds across the full docs tree (`docs/` has ~10
files; only 2-3 were read in full this pass) — do not generalize "docs are
reliable" beyond the specific files verified here.

**Verdict: Strong for the specific docs verified (ADR.md, profile-routing.md)
against code; UNKNOWN/not yet assessed for the remaining docs tree.**

## J — License

**FACT (read directly from the cloned `LICENSE` file):** MIT License,
Copyright (c) 2025 Nous Research. No restrictions on study or reuse of
concepts; standard MIT terms for code reuse.

**Verdict: Strong — maximally permissive, no ambiguity.**

---

## Cross-Cutting Observation

A pattern recurs across Dimensions B, C, and D: hermes-agent repeatedly ships
the *mechanism* for safety/isolation properties Hermes needs (write-approval
gating, session auto-pruning guard rails, profile-based tenant isolation) but
defaults them **off** or requires explicit multi-step configuration to
activate. This is a defensible framework-design choice (permissive defaults,
opt-in hardening) but means Hermes cannot rely on hermes-agent's defaults
alone to satisfy its behavioral principles (DOM-05/07/11) — it would need a
documented, enforced configuration profile (or a fork) that turns these
protections on, and ideally structural verification that they cannot be
silently turned off later. This is a **recommendation-relevant pattern for
Stage -2.5/-2.6, not a Phase -2 decision** — Phase -2 does not choose how
Hermes resolves this, only documents that the gap exists and where.

## Summary Table

| Dim | Verdict |
|---|---|
| A — Architecture | Moderate |
| B — Agent design | Moderate |
| C — Context & memory | Moderate |
| D — Reliability | Strong |
| E — Human control | Moderate (publish-specific gating UNKNOWN) |
| F — Evaluation | Moderate (internal) / Absent (content-domain) |
| G — Operations | Moderate-Weak (provisional, needs follow-up) |
| H — Reusability | Strong (skills) / Moderate (multi-tenancy) |
| I — Evidence | Strong (for files checked) |
| J — License | Strong |

## Open Follow-Ups for Stage -2.5/-2.6 (not resolved this pass)

1. Trace call sites of `holographic/store.py`'s fact-deletion statements —
   user-command-only, or reachable autonomously?
2. Read `docs/billing-lifecycle.md` in full — does the billing subsystem
   enforce budget caps, or only track/report usage?
3. Search specifically for a publish/send-confirmation approval gate distinct
   from `write_approval.py` (memory/skills) — confirmed absent from targeted
   searches, not from a full sweep.
4. Read `docs/chronos-managed-cron-contract.md` in full for DOM-13's actual
   reliability/crash-recovery contract, beyond what was inferred from
   `hermes_state.py`'s WAL-handling comments.
