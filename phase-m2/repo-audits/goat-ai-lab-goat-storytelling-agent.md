# Deep Audit: GOAT-AI-lab/GOAT-Storytelling-Agent

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo-catalog record: REPO-029 (Cluster E). Relevant domains: DOM-03.
Audited: 2026-08-24. Method: `git clone --depth 1`, full read of all 6 source
files (735 lines total — small enough to read in full, not sampled), `gh repo
view` / `gh api` for maintenance signals. README + blog claims cross-checked
against the actual code in `goat_storytelling_agent/`.

## A — Architecture
Single-file-per-concern script architecture, not a framework: `plan.py` (Plan
class, pure text-parsing utility, no state), `storytelling_agent.py`
(`StoryAgent` class driving the pipeline), `prompts.py` (prompt templates),
`utils.py` (helpers), `config.py` (1 line — effectively unused as a real
config layer). No agent framework dependency (LangChain/LangGraph/etc.) — this
is a bespoke sequential pipeline: `enhance_book_spec` -> `enhance_plot_chapters`
(produces the act/chapter plan via `Plan.parse_text_plan`) -> per-chapter,
per-scene generation in `generate_story`. No multi-agent orchestration; single
LLM-calling class, sequential loop.
Verdict: Moderate — real, coherent single-agent pipeline architecture, but
simple (no framework, no parallelism, no state machine beyond the loop itself).

## B — Agent design
One implicit role (`StoryAgent`) with no explicit role/contract abstraction —
methods are pipeline stages, not separate agents or roles. No tool-use, no
external tool calls found. No escalation/handoff concept — this is a
single-actor generation loop, not a multi-role system.
Verdict: Weak — no agent-role or contract design to speak of; DOM-03 relevance
is about the *decomposition/continuity* mechanism, not agent design per se.

## C — Context & memory
**CONFIRMED (read directly, `storytelling_agent.py` lines 405-434, 474-490):**
scene-to-scene continuity is real and works exactly as the Stage -2.3 catalog
record described: `generate_scene(..., previous_scene=None)` accepts the prior
scene's text, truncates it to the last N words via
`utils.keep_last_n_words`, and injects it into the prompt via
`self.prompt_engine.prev_scene_intro`. `generate_story`'s main loop passes
`form_text[-1]` (the last generated scene) forward as `previous_scene` for the
next call. This is genuinely a chained, state-carrying generation loop, not a
sequence of independent one-shot calls.
**Important nuance not visible from the README:** continuity is a fixed-window
word-truncation of the *literal previous scene's text*, not a structured or
compressed narrative-state object (no character/plot-state model, no
`Plan`-level continuity beyond the initial act/chapter plan). This is a much
simpler mechanism than DOM-03's research question implies systems in general
might use (e.g., no world-state tracking as in the CANVAS/StoryState papers
registered as SRC-024/SRC-025).
Verdict: Moderate — the continuity mechanism is real and directly on-point for
DOM-03, but simpler/cruder (literal-text-window carryover) than the domain's
research question anticipates a mature system might implement.

## D — Reliability
`Plan.split_by_act`/`parse_act` use regex parsing of free-form LLM text output
with multiple fallback attempts (`print('Fail: split_by_act, attempt 1', ...)`
then a second regex attempt) and silently return an empty list `[]` on total
failure — no exception raised, no retry-with-different-prompt, no schema
validation (no Pydantic/JSON-schema enforcement anywhere in the codebase).
Callers of `parse_text_plan` do not appear to check for the empty-list failure
case in the main `generate_story` loop (not fully traced end-to-end, flagged as
UNKNOWN rather than confirmed). No checkpointing — a crash mid-`generate_story`
loses all progress (in-memory `form_text` list, no persistence).
Verdict: Weak — real but fragile regex-based structured-output extraction with
silent failure paths and no crash recovery.

## E — Human control
No approval gates, no human-in-the-loop hooks, no permission model found
anywhere in the code. This is a fully autonomous generate-to-completion script.
Verdict: Absent.

## F — Evaluation
**CONFIRMED:** no `tests/` directory, no test files of any kind found in the
repository (`find . -iname "*test*"` returned nothing). No CI configuration
file found. No self-critique, scoring, or quality-gate step in the pipeline —
generated text is not reviewed or scored before being returned.
Verdict: Absent.

## G — Operations
No logging framework (only ad-hoc `print()` statements, several used for error
reporting rather than logging — see Dimension D). No cost tracking, no model
routing (`config.py` is a single line and does not implement tiered routing).
No rate-limit handling visible.
Verdict: Absent.

## H — Reusability
The `Plan` class (pure string/dict transformation, no I/O, no LLM calls) is
cleanly separable and could be lifted independently of the rest of the
package. The `StoryAgent` class is more coupled — prompts are hardcoded to a
specific book/chapter/scene narrative shape, not parameterized for a different
domain (e.g., social-media post series) without rewriting `prompts.py`.
Verdict: Moderate — the continuity *pattern* is easy to extract into a design
note (Stage -2.5), but the code itself is not a drop-in library for a
different content shape.

## I — Evidence
**CONFIRMED gap between the Stage -2.3 catalog record and reality:** the
repo-catalog.md entry (written before this audit) characterizes this repo as
"active" based on a 2024 release blogpost; direct verification via
`gh repo view` shows the last push was **2025-11-12** — over 9 months before
this audit date (2026-08-24), and the repo has only 2 open issues total (low
signal either way — could mean stable/finished or abandoned, cannot
distinguish from issue count alone). This is a **maintenance-signal
correction to record explicitly**, not a reason to discount the mechanism
itself, which was independently verified by direct code reading regardless of
the project's current activity level.
Docs-vs-code: the README's description of the pipeline stages matches the
actual code structure (`enhance_book_spec`, `enhance_plot_chapters`,
`generate_story`) — no material discrepancy found there. The one gap is the
maintenance-activity characterization above.
Verdict: Moderate — code matches docs on mechanism; catalog's activity
characterization needed correction.

## J — License
**CONFIRMED:** MIT License, Copyright (c) 2023 GOAT.AI. No bundled
dependencies with conflicting licenses found in `requirements.txt` (standard
packages: transformers, etc. — not individually license-audited here, flagged
as UNKNOWN for transitive dependency licenses, out of scope for a repo-level
license check).
Verdict: Strong — clear, permissive, no ambiguity for concept/code reuse.

---

## Evidence Section (Section 9.3 exit requirement — docs vs. code disagreements)

1. **Maintenance activity**: Stage -2.3's repo-catalog.md record says "active,
   small/focused" based on external blog/HF-dataset signals; direct
   verification shows the repo has not been pushed to since 2025-11-12 (FACT,
   via `gh repo view`). This is corrected here rather than left standing.
2. No other material doc-vs-code disagreement found — the README's pipeline
   description is accurate to the code.

## Summary for Stage -2.5 Pattern Extraction

The DOM-03 mechanism worth carrying forward as a named pattern is the
**fixed-window literal-text scene-carryover** technique (`previous_scene`
truncated to last N words, injected into the next prompt) — simple, real,
verifiably working, but a naive baseline rather than a sophisticated
narrative-state model. Recommend citing this alongside `HKUDS/ViMax` and the
CANVAS/StoryState papers (SRC-024/025) as a spectrum from "simple text-window
carryover" (this repo) to "explicit world-state tracking" (the academic
papers) — useful range for Stage -2.5's pattern write-up, not a single
best-answer.
