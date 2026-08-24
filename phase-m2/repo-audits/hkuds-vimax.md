# Deep Audit: HKUDS/ViMax

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo-catalog record: REPO-030 (Cluster E). Relevant domains: DOM-03, DOM-20.
Audited: 2026-08-24. Method: `git clone --depth 1`, structural read of
`agents/`, `agent_runtime/`, `pipelines/`, `tests/`; full read of
`character_extractor.py` and partial read of `novel_compressor.py`,
`context_compactor.py`; `gh repo view` for maintenance signals.

## A — Architecture
Multi-stage pipeline over LangChain (`langchain_core`, `init_chat_model`),
organized as `agents/` (13 specialized single-purpose modules:
`novel_compressor`, `character_extractor`, `event_extractor`,
`scene_extractor`, `screenwriter`, `script_planner`, `script_enhancer`,
`storyboard_artist`, `character_portraits_generator`,
`camera_image_generator`, `best_image_selector`, `reference_image_selector`,
`global_information_planner`) plus a separate `agent_runtime/` layer
(`loop.py`, `tool_executor.py`, `session_index.py`, `context_compactor.py`,
`vimax_adapters.py`) that appears to be a general-purpose agent-loop runtime
distinct from the pipeline-specific agents. Two top-level pipeline shapes:
`main_idea2video.py` and `main_script2video.py`, plus `main_agent.py` for a
more general agent-loop entry point.
**Doc-vs-code nuance:** the README markets this as "Director, Screenwriter,
Producer, and Video Generator — All-in-One" (README line 43) — this is
marketing/capability framing, not four literal agent classes. The actual code
implements a **much finer-grained ~13-stage specialized pipeline**, not 4
role-classes. This isn't a contradiction (the marketing framing groups
capabilities, not classes) but the Stage -2.3 catalog record's "4-agent role
separation" characterization is an oversimplification worth correcting here.
Verdict: Strong — real, substantially more granular multi-stage architecture
than the marketing copy implies, with a separate general agent-runtime layer.

## B — Agent design
Each `agents/*.py` module is a narrow, single-purpose LLM-calling unit with
its own system prompt and a Pydantic response schema (verified directly in
`character_extractor.py`: `ExtractCharactersResponse(BaseModel)` with a typed
`characters: List[CharacterInScene]` field). This is real schema-first output
contracting, not free-text parsing (contrast with GOAT-Storytelling-Agent's
regex-based `Plan` class, audited separately). Uses
`TrailingCommaTolerantPydanticOutputParser` — a custom parser subclass built
specifically to tolerate a known LLM failure mode (trailing commas in JSON) —
a concrete, specific reliability patch, not a generic claim.
Verdict: Strong — real per-agent structured-output contracts with an observed,
specific hardening measure.

## C — Context & memory (DOM-03 focus)
**CONFIRMED (read directly):** `character_extractor.py`'s system prompt
explicitly separates "static features" (physical appearance, physique —
relatively unchanging) from "dynamic features" (attire, accessories, carried
items — easily changeable), and instructs the model to "Group all names
referring to the same entity under one character" — a real, specific
character-consistency mechanism directly relevant to DOM-20's cross-modal/
cross-episode consistency need, not just a generic "extract characters" call.
`agent_runtime/context_compactor.py` (254 lines, not fully read line-by-line
but confirmed to exist and be a real module, not a stub) suggests a separate
context-compaction mechanism for the long-running agent-loop path — cross-
relevant to DOM-12, flagged for a future DOM-12 pass since it's outside this
audit's DOM-03/DOM-20 focus.
Verdict: Strong — real, specific character-consistency and narrative-
decomposition (`novel_compressor`, `scene_extractor`) mechanisms confirmed in
code, directly on-point for both DOM-03 and DOM-20.

## D — Reliability
`tenacity`'s `@retry(stop_after_attempt(...))` decorator used directly on LLM
calls (`character_extractor.py` imports and uses it). Test files named
`test_crash_regressions.py`, `test_hang_guards.py`, `test_wrong_output_guards.py`,
`test_hygiene_guards.py` (25 test files total, confirmed via `find`) indicate
deliberate, named reliability-regression testing — not just happy-path tests.
Verdict: Strong — retry logic + a real regression-test suite specifically
targeting failure modes (crashes, hangs, malformed output), not just feature
tests.

## E — Human control
Not directly inspected this pass (out of this audit's assigned DOM-03/DOM-20
focus) — no approval-gate code was noticed incidentally during the character/
narrative-mechanism inspection, but this is UNKNOWN rather than confirmed
absent; a dedicated pass would need to read `main_agent.py` and
`agent_runtime/loop.py` in full.
Verdict: UNKNOWN — not adequately inspected this pass, flag for a follow-up
if DOM-07 needs ViMax specifically (it was not flagged as a DOM-07 candidate
in repo-catalog.md, so this gap is likely low-priority).

## F — Evaluation
**CONFIRMED:** 25 real test files under `tests/`, with names indicating
targeted regression coverage (crash, hang, wrong-output, hygiene guards;
provider-specific tests for OpenRouter image/video generators and Minimax
integration). This is a substantially more mature test posture than
GOAT-Storytelling-Agent (0 tests) or, pending audit, most other repos in this
cluster.
Verdict: Strong.

## G — Operations
`agent_runtime/config.py`, `provider_presets` test file, and
multiple provider-specific test files (OpenRouter, Minimax, Omni-Yunwu)
indicate a real multi-provider abstraction layer for image/video generation
— relevant as an operational pattern (provider abstraction) though not
directly a DOM-16 cost-routing mechanism (not inspected for cost/budget logic
this pass — UNKNOWN).
Verdict: Moderate — real provider abstraction confirmed, cost/budget
mechanism not verified.

## H — Reusability
The `agents/` modules are individually fairly self-contained (own prompt, own
schema, own retry logic) and could plausibly be lifted as reference examples
for a Hermes-side character-extraction or narrative-compression step, though
they are LangChain-coupled (not framework-agnostic). The `agent_runtime/`
layer looks like a more general, potentially separately-extractable agent-loop
runtime, but was not audited in enough depth to confirm decoupling from the
video-specific pipeline code.
Verdict: Moderate.

## I — Evidence
**CONFIRMED via `gh repo view`:** 12,087 stars, 1,814 forks, last pushed
2026-07-29 (i.e., genuinely active as of ~4 weeks before this audit), 30 open
issues, MIT license — this corroborates the Stage -2.3 catalog's "mature,
popular" characterization; no maintenance-signal correction needed here
(unlike GOAT-Storytelling-Agent, audited separately).
**Doc-vs-code disagreement found:** the README's "Director, Screenwriter,
Producer, and Video Generator" framing (4 roles) does not match the actual
~13-module pipeline structure — see Dimension A. This is a marketing
simplification, not a false claim, but should not be repeated uncritically in
Stage -2.5 pattern extraction as "a 4-agent architecture."
Verdict: Strong overall evidence quality, with the one framing correction
noted above.

## J — License
**CONFIRMED:** MIT License. No conflicting bundled-dependency licenses
identified in this pass (not exhaustively audited against `pyproject.toml`'s
full dependency tree — flagged as UNKNOWN for transitive licenses).
Verdict: Strong.

---

## Evidence Section (Section 9.3 exit requirement — docs vs. code disagreements)

1. **Role-count framing**: README markets "Director, Screenwriter, Producer,
   Video Generator" (4 roles); actual code is a ~13-module specialized
   pipeline plus a separate general agent-runtime layer. Not a false claim
   (marketing groups capabilities), but a real granularity mismatch worth
   flagging so Stage -2.5 doesn't cite "4 agents" as the mechanism.
2. Maturity/activity claims in repo-catalog.md were CONFIRMED accurate (12k+
   stars, pushed within the last month) — no correction needed there, in
   contrast to the sibling GOAT-Storytelling-Agent audit.

## Summary for Stage -2.5 Pattern Extraction

Two patterns worth carrying forward distinctly: (1) the **static/dynamic
character-feature separation** prompt technique for cross-scene/cross-episode
visual consistency (DOM-20) — a specific, reusable prompt-design idea, not
just "extract characters"; (2) the **fine-grained specialized-pipeline**
architecture itself (13 narrow single-purpose LLM modules with individual
Pydantic contracts and per-module retry, versus a monolithic agent) as a
DOM-03/DOM-01 comparison point against `ChrisChen667788/wind-comic`'s
different consistency approach (audited separately) — Stage -2.5 should
compare these two repos' consistency mechanisms directly, since both are
DEEP AUDIT candidates for the same underlying need (multi-modal narrative
continuity) with materially different designs (static/dynamic trait
extraction here vs. wind-comic's "character-DNA" claim, to be verified in that
audit).
