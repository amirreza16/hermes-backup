# Deep Audit — REPO-040: NimbleCoAI/hermes-agent (multi-tenant fork)

Schema: Master Plan Section 9.3. Stage -2.4, 2026-08-24.

**CORRECTION to `repo-catalog.md` — verify before citing elsewhere:** this
repo has moved. **FACT (verified via `gh repo view`/`gh api`):** the owning
org renamed `NimbleCoOrg` → `cyborg-garden`; the canonical repo is now
**`cyborg-garden/hermes-agent-mt`** (`https://github.com/cyborg-garden/hermes-agent-mt`).
Git clone/remote URLs auto-redirect from the old `NimbleCoAI/hermes-agent`
path (confirmed — the clone in this audit succeeded via the old URL), so the
repo itself remains reachable, but **container images do NOT redirect**: per
the repo's own `FORM-NOTICE.md` (read directly), `ghcr.io/nimblecoai/*`
packages are frozen at their last build (2026-08-06 / 2026-07-21) and pull
successfully but silently return stale pre-rename code — a real trap for
anyone who pinned a deploy to the old GHCR path. `repo-catalog.md` should be
updated to point at `cyborg-garden/hermes-agent-mt` going forward.

**Method:** `git clone --depth 50` (deep enough to see rebase-journal
divergence from upstream) inspected directly — `FORK-NOTICE.md`,
`docs/rebase-journal.md`, `tools/memory_tool.py`, `git log`, and the relevant
test files. Audited against the REPO-001 baseline already established in
`nousresearch-hermes-agent.md` — dimensions identical to upstream are noted
briefly; this audit focuses on the delta.

---

## A — Architecture

**FACT:** "Thin fork" model, self-described and code-confirmed: 27 fork
commits sit on top of 410 absorbed upstream commits (per `docs/rebase-journal.md`,
read in full) — not a divergent rewrite. Weekly automated rebase via CI. Same
narrow-waist plugin architecture as REPO-001 (Dimension A there applies
unchanged).

**Verdict: Strong — genuinely thin, well-maintained fork discipline, not
architectural drift.**

## B/C — Agent Design / Context & Memory (the core delta)

**FACT (verified directly in code, not just the journal's narrative):**
`tools/memory_tool.py` implements `_global_path_for()`, `_scoped_path_for()`,
and `_path_for()` — a real per-context memory routing layer, wired via a
`_context_id_for_source` static method in `gateway/run.py` at the `AIAgent()`
construction call sites (per the journal's "Lessons" section, cross-checked
against the file's actual method list). Dedicated tests exist:
`tests/tools/test_memory_scoping.py`, `tests/tools/test_memory_scoping_legacy.py`,
`tests/gateway/test_context_id_derivation.py` — this is tested code, not a
documentation-only claim.

**FACT (verified via `gh pr view 47552` from the REPO-001 audit):** this same
patch is the basis of upstream PR #47552 ("feat(memory): add opt-in
`context_id` scoping..."), opened by NimbleCoAI, still OPEN/unmerged in
mainline hermes-agent as of 2026-08-24.

**FACT:** the fork's own commit history shows this patch is not static —
recent commits (`f3bf7e1` "fix(memory): scope DMs and stop persisting the
merged view into scoped files," `d3078fb` "fix(memory): pool a thread's
memory into its parent channel") indicate active, ongoing correctness
hardening of the scoping logic post-initial-implementation, i.e. this has hit
and fixed real edge cases in production use, not a one-shot patch left
unmaintained.

**INTERPRETATION:** This directly and concretely answers DOM-24's research
question for the specific "memory leaking across contexts" failure mode named
in issue #34352: a working, tested fix exists and runs in production (per the
fork's own multi-tenant operational claims), it is simply not yet merged
upstream. Whether Hermes should consume this fork directly, wait for
upstream merge, or reimplement the same `_path_for()`-style routing itself is
a Stage -2.5/-2.6 recommendation question, not resolved here.

**Verdict: Strong — the fork's core value proposition is real, tested,
independently verified code, not marketing.**

## D — Reliability / H — Reusability

**FACT:** Same underlying `hermes_state.py`/`cron/` reliability posture as
REPO-001 (not independently re-audited — no upstream changes to these paths
were surfaced by the journal for this fork's patch set). Reusability: the
"thin fork, weekly rebase, format-patch regeneration" workflow
(`docs/rebase-journal.md` "Process for future rebases" section) is itself a
notable pattern — low-conflict-surface fork maintenance discipline that kept
3 conflicts across 410 upstream commits — worth citing at Stage -2.5 as a
pattern for maintaining any Hermes-side fork/patch set against a fast-moving
upstream, independent of whether the memory-scoping patch itself is adopted.

## E — Human Control

**FACT:** Adapter-level gating additions beyond upstream: Telegram group
session isolation + admin resolution, Mattermost channel join/leave gating +
per-channel allowlist, Signal UUID-based allowlisting + group invite policy
(all per `FORK-NOTICE.md`, cross-checked against commit log entries like
`f4ffa8e` "category snowflakes match in channel allow/ignore/free-response
lists"). These are real, additional access-control surface beyond stock
hermes-agent, relevant to DOM-08.

## I — Evidence

**FACT:** `docs/rebase-journal.md` is an unusually high-quality piece of
evidence — a dated, quantified account of an actual rebase operation (commit
counts, conflict counts, resolution time, test pass counts, specific file
conflicts and how each was resolved) rather than a marketing claim. This
counts as source-level evidence per Section 12.2, not README-tier.

**Verdict: Strong.**

## J — License

**FACT:** MIT, "same as upstream" (`FORK-NOTICE.md`, and independently
confirmed the fork's own `LICENSE` file was not separately checked this pass
— flag as a small residual gap, low risk given the explicit statement).

---

## Summary

REPO-040 (now canonically `cyborg-garden/hermes-agent-mt`) is the strongest
single piece of evidence found in Stage -2.3/-2.4 for how DOM-24's specific
memory-isolation gap in REPO-001 gets closed in practice: real, tested code,
actively maintained, with the upstreaming PR (#47552) still pending. Treat
this fork as a live reference implementation to compare against if/when
REPO-001's own PR #47552 merges, and reconcile the repo-catalog.md URL to the
new `cyborg-garden` org name.
