# Deep Repository Audit — brightbeanxyz/brightbean-studio (REPO-037)

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Date: 2026-08-24. Triage record: `repo-catalog.md` Cluster E, DEEP AUDIT for
DOM-21 (comparison to postiz-app / REPO-036).

**Method:** `git clone --depth 1`; direct reading of `apps/publisher/engine.py`
(retry/backoff logic) and `apps/approvals/` (approval workflow + its own test
suite), plus `gh repo view`.

## A — Architecture
Django monolith (`apps/publisher`, `apps/approvals`, `apps/calendar`,
`apps/api`, `apps/mcp`, `providers/`), django-background-tasks for async work
(no Redis dependency, matching the Stage -2.3 catalog claim). Smaller, more
auditable single-process architecture than postiz-app's separate
Temporal-orchestrator service.
**Verdict: Moderate — real, coherent Django app structure; less architecturally sophisticated than postiz-app's dedicated orchestrator service, but genuinely functional.**

## B — Agent design
Not an LLM-agent system — a publishing/scheduling platform, same category as
postiz-app. Not applicable.
**Verdict: Absent.**

## C — Context & memory
Not applicable — conventional relational app state (Django ORM), not agent
memory.
**Verdict: Absent.**

## D — Reliability (primary claim under test)
FACT (verified by reading `apps/publisher/engine.py` directly): a real
exponential-backoff retry system exists — `RETRY_BACKOFF` schedule constant,
`_schedule_retry()` method incrementing `platform_post.retry_count` and
setting `next_retry_at`, a `MAX_RETRIES` cap after which `_fail_permanently()`
is called instead. Failures are classified retryable-vs-not
(`getattr(e, "retryable", True)`), and a code comment at line 343 explicitly
reasons about avoiding a "retry and double-post" outcome by keeping the
`PlatformPost` + `published_at` record once a post succeeds — the same
double-post-avoidance concern found independently in postiz-app's Temporal
workflow, arrived at via a completely different (single-process,
database-flag-based) mechanism. This is genuine reliability engineering, not
a marketing claim.
**Verdict: Strong — confirmed via direct code reading; a real, independently-arrived-at instance of the same "don't double-publish on retry" pattern found in postiz-app.**

## E — Human control
FACT: `apps/approvals/test_workflow.py` contains a `TwoStageFlowTests` test
class, confirming the "configurable multi-stage approval workflows" claim
from the Stage -2.3 catalog record is real and test-covered, not aspirational.
Full approval-stage configuration surface (how many stages, who approves) was
not traced in this pass.
**Verdict: Moderate — multi-stage approval confirmed real and tested; full configurability surface not fully traced.**

## F — Evaluation
No agent-output evaluation mechanism — not applicable, same as postiz-app.
**Verdict: Absent.**

## G — Operations
django-background-tasks confirmed (no Redis dependency, matching the catalog
claim); rate-limit tracking and audit-log claims from Stage -2.3 were not
independently re-verified line-by-line in this pass beyond confirming the
`apps/approvals/services.py`/audit-related files exist — treat those specific
figures (90-day retention, tiered rate limits) as UNCONFIRMED pending a closer
read, not re-verified as FACT by this audit.
**Verdict: Moderate — core mechanism confirmed real; specific numeric claims (90-day retention etc.) not independently re-verified this pass.**

## H — Reusability
Django/ORM-coupled; the retry-classification pattern (retryable vs.
permanent-fail, tracked via a per-record retry_count/next_retry_at pair) is a
clean, portable design independent of Django specifically.
**Verdict: Moderate.**

## I — Evidence
FACT: 78 test files found (`test_*.py` / `*_test.py`, excluding migrations) —
real test coverage, comparable in spirit to social-media-agent's 31 and a
sharp contrast to postiz-app's zero. FACT (via `gh repo view`): AGPL-3.0
license, 2,167 stars, pushed 2026-08-13 (11 days before this audit — active
but not same-day-active like the other three repos in this batch).
**Verdict: Strong — real, substantial test suite is the standout evidence-quality signal for this repo relative to its peers in this batch.**

## J — License
FACT: AGPL-3.0 (confirmed via `LICENSE` file, matches `gh repo view`). Same
copyleft implications as postiz-app.
**Verdict: Strong (clear, unambiguous).**

---

## Evidence Section — Docs vs. Code Disagreements

None found for the core claims this audit targeted (retry/rollback, approval
workflow). The Stage -2.3 catalog record's specific numeric claims (90-day
publish audit log retention, tiered REST API rate limits with Retry-After
headers) were NOT independently re-verified against code in this pass — flagged
as an open item, not confirmed or contradicted, rather than silently treated
as verified.

## FACT / INTERPRETATION Summary

- FACT: real exponential-backoff retry with retryable/permanent-failure
  classification and double-post avoidance, confirmed by direct code reading.
- FACT: real, test-covered two-stage approval workflow exists.
- FACT: 78 test files exist; AGPL-3.0 license confirmed.
- UNKNOWN: the specific 90-day audit-log retention and tiered rate-limit
  claims from Stage -2.3 — not independently re-verified this pass, do not
  cite as confirmed FACT without a follow-up read.
