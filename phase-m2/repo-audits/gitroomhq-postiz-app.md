# Deep Repository Audit — gitroomhq/postiz-app (REPO-036)

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Date: 2026-08-24. Triage record: `repo-catalog.md` Cluster E, DEEP AUDIT for DOM-21.

**Method:** `git clone --depth 1` of the live repo; direct reading of
`apps/orchestrator/src/workflows/post-workflows/post.workflow.v1.0.9.ts` (the
current production publish workflow) and its activity proxies, plus
`gh repo view`/`gh api` for maintenance signals. README/marketing claims were
NOT taken at face value (Section 12.1) — the Stage -2.3 discovery pass flagged
retry/rollback semantics as inferred-not-confirmed; this audit closes that gap
with direct code evidence.

## A — Architecture
Monorepo (pnpm workspaces): `apps/backend` (NestJS API), `apps/frontend`,
`apps/orchestrator` (separate NestJS service running a Temporal worker),
`libraries/`. Publishing is architecturally isolated into its own
orchestrator service, not embedded in the request-handling backend — a
deliberate separation between "accept a publish request" and "durably execute
it," which is exactly the kind of boundary DOM-21 asks about (distinct from
DOM-07's approval decision).
**Verdict: Strong — real service-level separation between API and durable execution, not a monolith.**

## B — Agent design
Not applicable in the LLM-agent sense — this is a scheduling/publishing
platform, not an autonomous agent. It has a `copilot.controller.ts` (an
AI-assisted content-suggestion feature) but no agent roles, mandates, or
decision-authority model to evaluate. FACT: no agent architecture exists here
to compare against DOM-01/02.
**Verdict: Absent — not an agent system; this dimension does not apply to what postiz-app actually is.**

## C — Context & memory
No persistent "memory" concept in the Hermes sense (DOM-11/12) — state is
conventional relational data (Postgres via Prisma, referenced throughout) plus
Temporal's own workflow-history durability. Not a comparison source for
DOM-11/12.
**Verdict: Absent — different problem domain (transactional app state, not agent memory).**

## D — Reliability
**This is the dimension Stage -2.3 flagged as unresolved, and it is now
resolved with direct evidence.** FACT (verified by reading
`post.workflow.v1.0.9.ts` lines 1-100 and its `catch` blocks): the workflow
defines FOUR distinct Temporal activity-proxy configurations with materially
different retry policies, deliberately differentiated by whether the
underlying operation is safely repeatable:
- Read-only/status-check activities (`checkPostStatus`): `maximumAttempts: 3`,
  fast 10s backoff — safe to retry, "retrying it can never duplicate a post"
  (verbatim code comment).
- Long-running media/comment publishing (`postComment`): `maximumAttempts: 3`,
  30-minute timeout, explicitly configured WITHOUT a heartbeat timeout because
  "heartbeat reporting proved unreliable in production and false heartbeat
  timeouts retried the activity, which can duplicate a comment" — a
  production-learned engineering decision, not a generic default.
- **Irreversible publish mutations** (`postSocialPending`/`finalizePost`):
  `maximumAttempts: 1` — explicitly NOT retried, because "a retried activity
  whose previous (timed-out) attempt still completed in the background would
  publish twice." A timeout here is treated as "outcome unknown," not silently
  retried.
- General activities: standard 3-attempt/2-minute-backoff policy.

The workflow body also contains an explicit duplicate-prevention check
(`changeState(firstPost.id, 'ERROR', 'Already posted', [firstPost])`) and a
code comment at the "already accepted" boundary stating the catch handler
"must never retry" past that point. This is genuine, production-informed
partial-failure handling distinguishing retryable-safe operations from
non-retryable irreversible ones — directly analogous to the retry-vs-no-retry
distinction Hermes' own publish step would need for DOM-21, and a concrete
worked example of the "irreversible action" boundary DOM-07 cares about at the
mechanics layer.
**Verdict: Strong — confirmed by reading the actual retry-policy code and its accompanying engineering rationale, not inferred from Temporal usage alone.**

## E — Human control
Approval/scheduling controls exist at the product level (posts have states
including a pending/scheduled flow before publish), but this audit did not
trace a formal approval-gate mechanism comparable to DOM-07's needs — the
`copilot` and posting flow appear oriented around a human operator directly
using the product UI to schedule/publish, not an autonomous agent being
gated. Not deep-audited further; out of this dimension's primary relevance for
DOM-21's actual research question (publish mechanics, not approval decisions).
**Verdict: Weak — present at product level but not inspected deeply enough to characterize as an agent-approval-gate pattern; not this repo's central relevance to Hermes.**

## F — Evaluation
No agent-output evaluation framework found or expected — not an LLM-content
pipeline in the DOM-15 sense.
**Verdict: Absent.**

## G — Operations
Real: Sentry integration referenced, structured logging conventions visible,
`dynamicconfig/` directory for environment-specific config, Docker Compose for
dev, Jenkins CI files present. Cost/model-routing (DOM-16) not applicable —
no LLM cost surface beyond the copilot feature, not inspected further.
**Verdict: Moderate — real ops tooling present, not deeply audited beyond confirming existence.**

## H — Reusability
Tightly coupled to its own NestJS/Prisma/Temporal stack and its own
per-platform integration adapters (`libraries/nestjs-libraries/integrations/social/`).
The retry-policy *pattern* (differentiated retry by operation reversibility)
is cleanly separable as a concept and directly portable to any publish
pipeline; the code itself is not a drop-in library.
**Verdict: Moderate — pattern generalizes cleanly, code does not.**

## I — Evidence
FACT (verified directly, not inferred): a search of the entire repository for
`*.spec.ts` and `*.test.ts` files, excluding `node_modules`, returned **zero
matches**. This is a real, notable **doc/reality gap** — a mature, 35k-star,
actively-maintained (pushed today, 2026-08-24) repository with no unit test
suite in either conventional naming location. This does not mean no testing
exists at all (e2e or manual QA could exist elsewhere and were not found in
this pass), but it means the "production-proven, reliable" impression created
by the retry-policy code's sophistication is NOT corroborated by an automated
test suite — a real evidence-quality caveat per Section 12.1 (do not let one
strong signal, the retry code, launder the absence of another, tests).
**Verdict: Moderate — code-level evidence for the reliability claim is strong and directly read; but the complete absence of a unit-test suite is a genuine, confirmed gap, not a marketing-vs-code disagreement in the usual sense (no test-related marketing claim was made to contradict) but worth flagging as a maturity caveat.**

## J — License
FACT (verified via `LICENSE` file and `gh repo view`): AGPL-3.0. This is a
strong copyleft license — any Hermes use of postiz-app code directly (not just
the pattern) would trigger AGPL's network-use disclosure requirements. Studying
the architecture/pattern is unrestricted; incorporating code is not
license-free.
**Verdict: Strong (as a license-clarity finding) — unambiguous, correctly identified copyleft license with real reuse implications.**

---

## Evidence Section — Docs vs. Code Disagreements

1. **Confirmed, no disagreement:** Stage -2.3's cautious "use of Temporal
   strongly implies durable-execution/retry semantics ... must be verified at
   the code level" is now CONFIRMED as accurate and, if anything,
   understated — the actual retry design is more sophisticated (four
   differentiated policies keyed to operation reversibility) than a generic
   "Temporal gives you retries" claim would suggest.
2. **Gap not previously flagged:** the repo's popularity/maturity signals
   (35k stars, active development) would ordinarily suggest a mature test
   suite; none was found. This is not a doc-vs-code contradiction (no specific
   testing claim was made in README to check against) but is logged here as
   the closest analog — an expectation gap between apparent maturity and
   verifiable test coverage.

## FACT / INTERPRETATION Summary

- FACT: four distinct, differentiated Temporal retry policies exist in the
  live publish workflow, with the irreversible-mutation path explicitly set
  to `maximumAttempts: 1` and documented in code comments as a deliberate
  double-post-prevention design.
- FACT: zero `.spec.ts`/`.test.ts` files exist in the cloned repository.
- FACT: license is AGPL-3.0.
- INTERPRETATION: the retry-policy design is "production-informed" — this is
  based on the code comments' own stated rationale (e.g. "heartbeat reporting
  proved unreliable in production"), which is the maintainers' claim about
  their own history, not independently corroborated by this audit against
  issue history or release notes.
