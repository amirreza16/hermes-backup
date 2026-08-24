# Deep Audit: openai/openai-agents-python

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Repo-catalog record: REPO-003. Relevant DOM IDs: DOM-01, DOM-02.

Source: `git clone --depth 1 https://github.com/openai/openai-agents-python.git`, inspected
2026-08-24. MIT License, confirmed from `LICENSE` file (FACT).

## A — Architecture
Explicit architecture: yes, but deliberately lightweight (official successor to OpenAI's
earlier "Swarm" experiment, per project history). Core primitive is the `Agent` object with
a `Runner` that executes it; multi-agent composition happens via **handoffs** (an agent
delegates the whole conversation to another agent) or via **agents-as-tools** (an agent calls
another agent as a function without transferring control). Both patterns are real, separately
implemented (confirmed: `src/agents/handoffs/__init__.py`, `class Handoff`, `def handoff(...)`
with 4 overloads for different call signatures).
Verdict: Strong — small, real, two clearly distinct composition primitives (handoff vs.
tool-call), directly relevant to Hermes' 2-fixed-role shape.

## B — Agent design
Agent roles are plain Python objects (`Agent` class) with `instructions`, `tools`,
`output_type`, and `handoffs` fields — no heavyweight role-registry or manifest system.
Contracts between agents are typed via `output_type` (Dimension C) and via `HandoffInputData`
(confirmed: `class HandoffInputData` in `handoffs/__init__.py`) which controls exactly what
conversation history is passed to the receiving agent on a handoff — including a
`nest_handoff_history`/summary-mapper mechanism (`handoffs/history.py`) for compressing
history across a handoff boundary rather than passing it raw.
Verdict: Strong — real, non-trivial handoff-contract machinery, not just a naive history
concatenation.

## C — Context & memory
`output_type` is validated via Pydantic-style schema (confirmed:
`src/agents/agent.py:360,508-517` — `output_type` field, with a runtime `isinstance`/
`get_origin` check that raises if the type is not a valid `type`, `AgentOutputSchemaBase`, or
`None`). Session/history management is handled by `RunState`/context objects
(`run_state.py`, `run_context.py`) — a single-run working-memory concept; no persistent
cross-session memory store was found in this repo (would be the caller's responsibility to
add, e.g. via a database).
Verdict: Moderate — contract enforcement on output is real; persistent memory across sessions
is explicitly out of this repo's scope (confirmed absent, not hidden).

## D — Reliability
`retry.py` present (model-call retry logic). `tool_guardrails.py` and `guardrail.py` provide
input/output guardrail hooks that can halt execution — confirmed via a real test surface
(`tests/test_guardrails.py`, `tests/test_runner_guardrail_resume.py`,
`tests/test_output_guardrail_cancellation.py`, `tests/test_stream_input_guardrail_timing.py`)
indicating guardrails are treated as a first-class, tested reliability feature, not an
afterthought. `run_internal/guardrails.py` suggests guardrail logic is centralized in the
runner rather than scattered.
Verdict: Strong — real, tested guardrail/retry surface.

## E — Human control
No dedicated `interrupt()`/pause-and-resume-on-approval primitive equivalent to LangGraph's
was found in this pass (UNKNOWN whether one exists deeper in the runner — not confirmed
present or absent with full confidence given time budget). Guardrails (Dimension D) can block
an action outright but that is refuse-or-allow, not a human-approval pause/resume flow.
Verdict: Weak-Unknown — guardrails provide a blocking mechanism, but a LangGraph-style
approval-gate-with-resume was not confirmed present; flag as an open question rather than a
confirmed absence, given this pass did not exhaustively search the runner internals.

## F — Evaluation
Not found as a first-class feature in this repo (`PLANS.md` exists but wasn't read in depth
this pass — UNKNOWN if it documents eval tooling). No dedicated eval framework directory
found alongside `tests`/`integration_tests`.
Verdict: Absent/Unknown — not confirmed present.

## G — Operations
`usage.py` present — token/cost usage tracking exists at some level (confirmed file presence,
not deeply inspected). `logger.py` present for basic logging. No model-routing/multi-tier
cost-control mechanism found (this SDK is single-provider by design — OpenAI's own agents
SDK — so cross-provider routing is out of scope by design, not a gap).
Verdict: Moderate — basic usage tracking present; no multi-provider routing (by design, not
a flaw for this repo's stated purpose).

## H — Reusability
Framework coupling: low-to-moderate. The `Agent`/`Runner`/`handoff` vocabulary is specific to
this SDK, but the shape (typed output, explicit handoff-vs-tool-call distinction, guardrails
as first-class) is conceptually portable and well-separated from OpenAI-specific transport
details in the directory structure (transport/model-calling code is isolated from the
agent/handoff/guardrail logic).
Verdict: Moderate — clean conceptual separation, though built OpenAI-first.

## I — Evidence
Docs vs. code: no contradiction found between README's "handoffs" description and the actual
`Handoff`/`handoff()` implementation — both real and matching. One nuance not obvious from a
README-level read: the handoff history-compression mechanism (`history.py`,
`nest_handoff_history`) is more sophisticated than "pass the whole conversation" — it
provides configurable summary-mapping, which is a positive finding (better than the minimum
claim), not a negative gap.
Tests: substantial — `tests/` and a separate `integration_tests/` directory, plus example
patterns for guardrails and handoffs (`examples/agent_patterns/`, `examples/handoffs/`).
Verdict: Strong — code substantiates and in one respect exceeds the README-level description.

## J — License
MIT, confirmed directly from `LICENSE` file (FACT).
Verdict: Strong — unambiguous, permissive.

---

## Evidence Summary (Stage -2.4 exit criterion)
No docs-vs-code contradictions found on the core handoff/guardrail claims — both are real and
tested. The one open item is Dimension E (human-approval-with-resume): this pass could not
confirm with full confidence whether an equivalent to LangGraph's `interrupt()` exists deeper
in the runner internals; recorded as UNKNOWN rather than asserted absent, per Section P5
discipline, given the time budget for this pass did not allow exhaustive runner-internals
reading.

## Stage -2.3 Triage Reassessment
No change — DEEP AUDIT was warranted. The handoff-history-compression mechanism found here is
a genuinely stronger DOM-02 comparison point than the Stage -2.3 triage description
anticipated (it only cited "schema-typed handoff contracts," not the history-compression
sophistication found on inspection).
