# Deep Audit: langchain-ai/langgraph

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Repo-catalog record: REPO-002. Relevant DOM IDs: DOM-01, DOM-02, DOM-13 (comparison
baseline for hermes-agent, per DOM-13's reframing).

Source: `git clone --depth 1 https://github.com/langchain-ai/langgraph.git`, inspected
2026-08-24. MIT License, confirmed from `LICENSE` file (FACT).

## A — Architecture
Explicit architecture: yes. Graph-based execution model (`libs/langgraph/langgraph/graph`,
`pregel`, `channels`). The runtime is the "Pregel" engine (bulk-synchronous-parallel graph
execution, named after Google's Pregel paper) — nodes read/write named "channels," supporting
both simple linear chains and cyclic graphs with conditional edges. State management is
channel-based (each channel has an update/reduce function), separate from the checkpoint
persistence layer (`libs/checkpoint*`). Boundaries between nodes are explicit (a node is a
function or Runnable taking/returning partial state).
Verdict: Strong — real, documented multi-file implementation, not a thin wrapper.

## B — Agent design
LangGraph itself is graph-orchestration infrastructure, not an opinionated "agent role"
framework — roles are whatever the graph author defines as nodes. `libs/prebuilt` supplies
higher-level agent constructors (e.g. ReAct-style) on top of the graph primitive. No built-in
concept of "agent contracts" beyond the state schema passed between nodes (see Dimension C).
Verdict: Moderate — flexible but unopinionated; contract discipline is left to the graph
author, not enforced by the framework itself (contrast with pydantic-ai, REPO-004).

## C — Context & memory
Two distinct layers, confirmed in code: (1) **channels** — in-graph working state during one
run, typed via the graph's state schema; (2) **checkpoints** — `libs/checkpoint`'s
`BaseCheckpointSaver` (confirmed: `libs/checkpoint/langgraph/checkpoint/base/__init__.py`,
`class BaseCheckpointSaver`, methods `get`/`get_tuple`/`put`/`put_writes`) persists a full
state snapshot after each "superstep," with `checkpoint-postgres` and `checkpoint-sqlite`
as production-grade backends (confirmed present as separate published libs, not just an
in-memory toy). Retrieval/compaction beyond raw checkpoint replay was not found in this pass
— UNKNOWN whether any narrative/summarization-style long-term memory exists natively (likely
delegated to the graph author or LangChain's separate memory packages, not this repo).
Verdict: Strong for durable state/checkpointing; Absent/Unknown for narrative-continuity
memory specifically (out of this repo's scope as inspected).

## D — Reliability
Confirmed real human-in-the-loop primitive: `langgraph/types.py`, `def interrupt(value)` —
raises a resumable `GraphInterrupt` exception mid-node, surfaces a value to the client, and
resumes via a `Command` primitive. IMPORTANT confirmed nuance (FACT, from the function's own
docstring): "The graph resumes from the start of the node, **re-executing** all logic" — this
means any non-idempotent side effect before the `interrupt()` call in a node will re-run on
resume. This is a real reliability caveat, not evident from a README-level read.
Checkpointing (Dimension C) doubles as crash-recovery — a saved checkpoint can be resumed
after a process restart, per the `BaseCheckpointSaver` interface.
Verdict: Strong, with one documented gotcha (re-execution-on-resume) that any Hermes
comparison should account for explicitly, not silently assume away.

## E — Human control
`interrupt()`/`Command` (Dimension D) is the core HITL primitive — pause-and-resume gated on
an external decision, which is exactly Hermes' "approval before irreversible action" shape.
No built-in notion of reversible-vs-irreversible action classification was found — that
distinction, if wanted, is left to the graph author (call `interrupt()` only before the
irreversible nodes).
Verdict: Moderate-Strong — the mechanism is real and general-purpose, but the
reversible/irreversible policy layer itself is not something LangGraph ships opinionated
defaults for.

## F — Evaluation
Not found in this repo (LangChain publishes a separate `langsmith`/evaluation product,
outside this repo's scope). UNKNOWN/Absent for this specific repository.
Verdict: Absent (in-repo) — evaluation tooling lives elsewhere in the LangChain ecosystem,
not verified this pass.

## G — Operations
No explicit cost-tracking/model-routing code found in `libs/langgraph` itself (would live in
`langchain-core`/model-provider integration packages, not this repo). Tracing/observability
hooks exist via LangSmith integration points referenced in docs but not independently
verified this pass.
Verdict: Weak-Unknown for this repo specifically — cost/routing/observability are adjacent-
package concerns, not confirmed present here.

## H — Reusability
Framework coupling: moderate. The graph/channel/Pregel abstraction is LangGraph-specific
vocabulary, but the checkpoint interface (`BaseCheckpointSaver`) is a clean, separately
published, storage-agnostic abstraction (Postgres/SQLite backends confirmed to exist as
separate packages) — this piece specifically is well-separated and would transplant cleanly
as a durable-execution pattern reference independent of adopting the whole graph runtime.
Verdict: Moderate — good separation for the checkpoint layer specifically; the orchestration
layer itself is more framework-coupled.

## I — Evidence
Docs vs. code: README/docs market "durable execution" and "human-in-the-loop" prominently;
both were verified to have real, non-trivial implementations (not just wrapper stubs) — no
disagreement found on those two headline claims. One under-documented-at-README-level detail
surfaced by reading the actual docstring: the re-execution-on-resume behavior (Dimension D) —
this is documented in the code's own docstring but is easy to miss from marketing-level
material, which is exactly the kind of gap Section 8/15.2 asks this stage to catch.
Tests: substantial (`libs/langgraph/tests`, `libs/checkpoint/tests` both present with many
files, e.g. `test_store.py`, `test_memory.py`, `test_encrypted.py`, `test_redis_cache.py`).
Verdict: Strong — code substantiates the headline claims; one real (not severe) doc-depth
gap found and reported per the exit criterion.

## J — License
MIT, confirmed directly from the `LICENSE` file (FACT, not inferred). No restriction on
studying or reusing concepts/code.
Verdict: Strong — unambiguous, permissive.

---

## Evidence Summary (Stage -2.4 exit criterion)
Docs/README claims for "durable execution" and "human-in-the-loop" are substantiated by real
code (FACT, verified directly). The one gap between marketing-level description and actual
behavior is the re-execution-on-resume semantic of `interrupt()` — present in the code's own
docstring (so not a docs-vs-code contradiction, but a marketing-vs-implementation-detail gap
worth flagging for anyone using this as a comparison baseline for hermes-agent's own
checkpointing/resume behavior at Stage -2.5). Evaluation and cost/operations tooling were not
found in this specific repo (UNKNOWN/likely-elsewhere, not a false claim — this repo simply
doesn't claim to include them).

## Stage -2.3 Triage Reassessment
No change — DEEP AUDIT was warranted and confirmed on inspection. If anything, the checkpoint
layer's real production backends (Postgres/SQLite) make this a stronger DOM-13 comparison
baseline than the Stage -2.3 triage anticipated.
