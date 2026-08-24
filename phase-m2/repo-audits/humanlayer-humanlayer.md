# Deep Audit — humanlayer/humanlayer (REPO-011)

Stage -2.4. Schema: Master Plan Section 9.3 (Dimensions A-J).
Cloned `--depth 1` on 2026-08-24; inspected structure, source (Go `hld/`
daemon, TS `hlyr/` CLI), license, README.

## A — Architecture
A local daemon (`hld/`, Go) manages sessions/approvals/events via an event bus
(`hld/bus`) and a SQLite-backed store (`hld/store`); `hlyr/` is a TS CLI/SDK
layer. Approval routing beyond the local daemon (Slack/email escalation
claimed by Stage -2.3 triage) was NOT directly located in this pass within
the depth searched — the local-approval path is confirmed, the
external-channel routing code was not found/verified. Label as UNKNOWN pending
deeper search, not confirmed absent.
Verdict: Moderate — local mechanism confirmed strong, external-routing claim
unverified.

## B — Agent design
No agent-role abstraction — this is a tool-call approval layer that sits
below whatever framework drives the agent; role definition is out of scope by
design.
Verdict: Absent — not this project's concern (by design, not a gap).

## C — Context & memory
`hld/store` persists conversation/session state (SQLite), but only as far as
needed to correlate an approval request back to a run — not a general agent
memory system.
Verdict: Weak — narrow, purpose-specific persistence only.

## D — Reliability
Not deeply inspected this pass beyond confirming the store/bus separation
exists; no explicit retry/circuit-breaker code located in the approval path
files read.
Verdict: Weak — insufficient evidence gathered this pass to rate higher;
UNKNOWN rather than confirmed absent.

## E — Human control (primary dimension for DOM-07)
Confirmed real and functional: `hld/approval/manager.go` implements
`CreateApproval(ctx, runID, toolName, toolInput)`, checks an auto-accept flag,
looks up the session by run ID, and persists the approval via the store —
this is a genuine, structural approval-gate implementation, not a stub.
`hld/api/handlers/approvals.go` and `hld/rpc/approval_handlers.go` expose it
over both REST and RPC. Tests exist (`hld/approval/manager_test.go`,
`hld/daemon/daemon_approval_integration_test.go`,
`hld/store/sqlite_approval_test.go`) — not just documentation.
Verdict: Strong — this is the single most concrete, on-point DOM-07 mechanism
found across all of Stage -2.3/-2.4, independent of the project's current
maintenance status.

## F — Evaluation
No evaluation/quality-gating mechanism found — out of this project's scope.
Verdict: Absent.

## G — Operations
Event bus + structured store suggest basic operational hygiene, but no
cost/model-routing/rate-limit code found (not a claimed feature).
Verdict: Weak — not this project's focus.

## H — Reusability
Go daemon + TS CLI is a real separation of concerns; adopting just the
approval-manager pattern (not the whole daemon) is plausible given how
self-contained `hld/approval/` reads, but this repo's own deprecation notice
(see Dimension I) is the dominant reusability concern, not architecture.
Verdict: Moderate.

## I — Evidence (docs vs. code) — THE LOAD-BEARING FINDING FOR THIS REPO
**CONFIRMED FACT:** `README.md` line 3 states verbatim: "public issues repo
for humanlayer - the code here is pretty much all deprecated - you can try
the rebuild of humanlayer at https://humanlayer.com". This is the repo's own,
current, top-of-README statement — not an inferred or stale signal.
**CONFIRMED FACT:** `gh api repos/humanlayer/humanlayer/commits` returns
HTTP 404 ("Not Found") as of 2026-08-24 — the commits API endpoint itself is
inaccessible for this repository (consistent with the repo having been
archived, renamed, or otherwise restricted following the pivot announced in
the README; this audit did not determine which).
**CONFIRMED FACT:** the local shallow clone's single visible commit
(2026-06-18) is "Update README.md" — i.e., the last change visible in this
audit's clone was adding the deprecation notice itself, not a feature commit.
**Distinct findings, not to be conflated (per the original triage
instruction):**
1. The approval-gate MECHANISM (Dimension E above) is real, tested,
   architecturally sound, and worth citing as a pattern at Stage -2.5.
2. The PROJECT `humanlayer/humanlayer` is NOT a currently viable adoption
   target — it is self-declared deprecated with a redirect to a commercial
   rebuild (`humanlayer.com`) whose code is not in this repository and was
   NOT audited in this pass (out of scope: a different, unaudited product).
No docs-vs-code contradiction was found beyond this — the deprecation notice
and the actual commit/API state agree with each other.

## J — License
Apache License 2.0 (`Copyright (c) 2024, humanlayer Authors`), confirmed by
reading `LICENSE` directly.
Verdict: Strong — clear, permissive; irrelevant in practice given deprecation,
but the pattern extracted from this code carries no license encumbrance.

## Overall
Audit the MECHANISM, not the PROJECT: `hld/approval/manager.go` and its
tests are a genuine, worked example of a tool-call approval gate suitable for
DOM-07 pattern extraction at Stage -2.5. Do not recommend `humanlayer/
humanlayer` itself as an adoptable dependency — it is deprecated, and its
successor product (humanlayer.com) is unaudited and out of scope here.
