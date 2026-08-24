# Deep Audit: pydantic/pydantic-ai

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Repo-catalog record: REPO-004. Relevant DOM ID: DOM-02 (primary — is the output contract
enforced-or-fails, or merely suggested?).

Source: `git clone --depth 1 https://github.com/pydantic/pydantic-ai.git`, inspected
2026-08-24. MIT License, confirmed from `LICENSE` file (FACT).

## A — Architecture
Multi-package monorepo: `pydantic_ai_slim` (core agent library), `pydantic_graph` (a separate
graph-execution primitive, notably distinct from the agent library itself — reusable for
non-agent workflows), `pydantic_evals` (a dedicated evaluation package — see Dimension F).
The `Agent` class is the central abstraction; sub-agent composition is via "capabilities" per
the Stage -2.3 triage description (not independently re-verified this pass beyond confirming
the `Agent` class exists — UNKNOWN on capabilities' exact mechanism, out of time budget).
Verdict: Strong for the core Agent/output-validation architecture (directly verified); Unknown
for the sub-agent "capabilities" composition detail specifically.

## B — Agent design
Not the focus of this pass (DOM-02 is the assigned priority) — role/contract design is
covered under Dimension C below, which is where this framework's actual differentiator lives.
Verdict: Not independently assessed this pass — see Dimension C.

## C — Context & memory
**This is the load-bearing finding for DOM-02.** Confirmed via `pydantic_ai_slim/pydantic_ai/
_output.py`: output validation is enforced through a real retry loop, not a
suggestion-and-hope mechanism. Specifically: `class OutputValidator` runs the model's output
through Pydantic's `ValidationError`/`TypeAdapter` machinery; on failure, a `ModelRetry`
exception is raised and caught by a wrapping handler (`_output.py:151,168` — confirmed
`except (ValidationError, ModelRetry) as e:` blocks) which triggers a re-prompt to the model,
up to `max_retries` (confirmed: `max_retries: int | None` field, plus a documented per-tool
override mechanism via `ToolOutput(max_retries=N)`). This directly answers DOM-02's research
question: the contract is **enforced-or-retried-until-exhausted**, not merely suggested and
silently accepted if violated — a materially stronger guarantee than a framework that just
asks the model to "please output JSON" with no validation loop.
Verdict: Strong — directly confirmed, code-level, exactly matching DOM-02's stated question.

## D — Reliability
The retry-on-validation-failure loop (Dimension C) is itself a reliability mechanism for the
specific failure mode of malformed structured output. Beyond that, no additional
checkpointing/crash-recovery mechanism was inspected this pass (out of scope for this
domain's priority; UNKNOWN).
Verdict: Strong for output-validation reliability specifically; Unknown for broader
process-level reliability (not this pass's focus).

## E — Human control
Not inspected this pass (out of DOM-02's scope; UNKNOWN).
Verdict: Not assessed.

## F — Evaluation
`pydantic_evals` exists as a **separate, dedicated package in this same monorepo** — a
positive, confirmed finding (directory presence verified) beyond what the Stage -2.3 triage
description mentioned. Contents not deeply inspected this pass (UNKNOWN on internal
mechanism), but its existence as a first-class sibling package to the agent library itself is
itself informative — this project treats evaluation as core, not an afterthought.
Verdict: Moderate-Strong (existence confirmed, depth not verified) — worth a follow-up look if
DOM-15 (evaluation/quality-gating) research revisits this project specifically.

## G — Operations
Not inspected this pass (out of DOM-02's scope; UNKNOWN).
Verdict: Not assessed.

## H — Reusability
The retry/validation mechanism (Dimension C) lives in a clearly separated module
(`_output.py`) with its own class (`OutputValidator`) — reasonably well-isolated from
model-provider transport code, suggesting the validation-contract pattern itself could be
studied/extracted independent of adopting the whole framework.
Verdict: Moderate — clean separation observed for the audited piece specifically.

## I — Evidence
Docs vs. code: the Stage -2.3 triage record described this project's "design philosophy" as
"the contract moves from suggestion to enforced-or-fails" based on documentation-level
framing. This pass converted that documentation claim into a CONFIRMED, code-verified FACT —
the retry-and-eventually-fail loop is real, not just a stated philosophy. No contradiction
found between the claimed philosophy and the actual implementation.
Verdict: Strong — the specific claim this repo was audited to check is confirmed at the
source-code level, not just from docs.

## J — License
MIT, confirmed directly from `LICENSE` file (FACT).
Verdict: Strong — unambiguous, permissive.

---

## Evidence Summary (Stage -2.4 exit criterion)
No docs-vs-code disagreement found on the one claim this audit specifically targeted
(enforced vs. suggested output contracts) — confirmed accurate. Several dimensions (B, D
partial, E, G) were not exhaustively assessed this pass, consistent with this repo's Stage
-2.3 triage rationale ("best direct hit found for DOM-02's exact question") — depth was
concentrated on Dimension C rather than spread evenly across all ten dimensions, which is an
explicit scoping choice given DOM-02 is this repo's sole assigned relevance; flagged as
UNKNOWN rather than asserted for the unassessed dimensions, per Section P5.

## Stage -2.3 Triage Reassessment
No change — DEEP AUDIT was warranted and the specific claim it was chosen for is now verified
FACT rather than an untested documentation claim. The presence of a dedicated `pydantic_evals`
sibling package is a new finding not mentioned in the original triage record, worth a note for
whoever later works DOM-15.
