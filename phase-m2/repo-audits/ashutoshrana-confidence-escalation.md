# Deep Audit — ashutoshrana/confidence-escalation (REPO-013)

Stage -2.4. Schema: Master Plan Section 9.3 (Dimensions A-J).
Cloned `--depth 1` on 2026-08-24; inspected `src/confidence_escalation/`
(scorer.py, middleware.py, handlers.py, policy.py, async_middleware.py,
6 framework adapters), tests, LICENSE.

## A — Architecture
`ConfidenceScorer`/`MultiSignalConfidenceScorer` (scorer.py) computes a
`ConfidenceScore` (0.0-1.0) from one or more `ScoringMethod`s (LOGPROB,
VERBALIZED, SEMANTIC_CONSISTENCY, TOOL_CALL_RISK, COMPOSITE) — confirmed by
reading the dataclass and enum directly, not inferred from docs. A middleware
layer (`middleware.py`) wraps a `score() -> evaluate() -> dispatch() ->
call()` pipeline driven by a `ThresholdPolicy` (e.g. `threshold=0.65,
action=EscalationAction.HUMAN_IN_LOOP`, found verbatim in source).
Verdict: Strong — the trigger logic DOM-10's research question asks for is
real, not a taxonomy-only repo.

## B — Agent design
Six framework adapters exist as separate real files: `adapters/
{openai_agents,pydantic_ai,crewai,autogen,google_adk,langchain}.py` — genuine
cross-framework integration, not a single-framework demo with marketing
copy about portability.
Verdict: Moderate — adapters confirmed to exist; per-adapter functional depth
not individually verified this pass.

## C — Context & memory
Not applicable — this is a per-call decision layer, not a memory system.
Verdict: Absent.

## D — Reliability
`async_middleware.py` provides an async-native path (confirmed by file
existence and export in `__init__.py`: `AsyncConfidenceEscalationMiddleware`)
— suggests the author cared about production integration ergonomics, not
just a sync toy. No explicit retry/backoff logic found in the scorer/
middleware path itself (not this tool's concern — it decides whether to
escalate, not how to retry a call).
Verdict: Moderate.

## E — Human control (DOM-10 primary, DOM-09 secondary)
`handlers.py` implements four real, distinct classes confirmed by direct
read: `HumanInLoopHandler`, `ModelUpgradeHandler` (the triage record's
claimed haiku→sonnet→opus escalation path), `ToolRestrictionHandler`, and
`ComplianceLoggingHandler` — all four exist as actual `EscalationHandler`
subclasses, not stubs referenced only in prose.
**Important distinction, carried forward from the Stage -2.3 triage
instruction and confirmed correct on inspection:** every signal this scorer
computes (logprob, verbalized confidence, semantic consistency, tool-call
risk) is a MODEL-CONFIDENCE signal — a measure of how sure the model itself
is about its own output. None of the four signal types measure TASK
AMBIGUITY (missing required field, conflicting user intent, underspecified
request) — DOM-09's actual research question. This repo is a strong DOM-10
candidate and only a partial, indirect DOM-09 comparison point; do not
present it at Stage -2.5 as filling the DOM-09 gap.
Verdict: Strong (DOM-10) / Weak-as-DOM-09-fit (DOM-09, secondary use only).

## F — Evaluation
No content-quality evaluation — out of scope for this repo.
Verdict: Absent.

## G — Operations
`ComplianceLoggingHandler` (handlers.py:247) implies structured audit-trail
output for escalation events, relevant to DOM-14 as a secondary note; not
independently deep-traced this pass.
Verdict: Weak — presence confirmed, depth not verified.

## H — Reusability
Framework-agnostic core (scorer/middleware) with adapters as a separable
integration layer — clean separation confirmed by the file structure itself
(core has zero adapter-specific imports at the top level inspected).
Verdict: Strong.

## I — Evidence (docs vs. code)
**Maintenance-signal correction:** last commit found is **2026-05-21**
("feat: export AsyncConfidenceEscalationMiddleware from package root") — over
three months stale as of this audit (2026-08-24). `gh repo view` confirms
**0 stars, 0 forks** as of today — unchanged from the Stage -2.3 triage note,
correctly characterized there as a genuine adoption gap, not glossed over.
Only 7 test files found under `tests/` — modest but real (matches the
original "real tests" characterization; "functionally complete for its
scope" from Stage -2.3 is a fair read, not an overstatement).
**No docs-vs-code contradiction found** — the four handler classes, the
`ThresholdPolicy` mechanism, and the six adapters all match what the
Stage -2.3 triage record claimed, verified directly in source rather than
taken from a README description.

## J — License
MIT (`Copyright (c) 2026 Ashutosh Rana`), confirmed by reading `LICENSE`
directly.
Verdict: Strong — no restriction.

## Overall
This remains the closest real-code match found anywhere in Stage -2.3/-2.4
to DOM-10's exact research question (a working confidence-threshold-to-
escalation trigger, not just an autonomy-tier taxonomy). Zero-adoption
signal (0 stars, solo author, 3-month-stale) is a genuine, confirmed limit on
how much weight to place on this as a production-proven pattern — cite the
MECHANISM at Stage -2.5, not the project's maturity.
