# Deep Audit: NVIDIA-NeMo/Guardrails

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo: https://github.com/NVIDIA-NeMo/Guardrails | Cloned (depth=1) 2026-08-24 and read directly (Python source, Colang flow files, docs) — not README-only.
Triage source: `repo-catalog.md` REPO-024, DEEP AUDIT. Relevant to DOM-17.

## A — Architecture
Colang DSL (a purpose-built flow-description language, not a general scripting language) drives conversation-level guardrail flows; `nemoguardrails/library/` contains ~28 independent guardrail integration modules (confirmed by directory listing: `self_check`, `jailbreak_detection`, `content_safety`, `topic_safety`, `sensitive_data_detection`, `injection_detection`, `factchecking`, plus third-party integrations — ActiveFence, CrowdStrike AIDR, Llama Guard, Trend Micro, Patronus AI, Fiddler, Polygraf, Cleanlab, GLiNER, and more). This is a genuinely pluggable, flow-based architecture, not a single keyword-filter function.
**Verdict: Strong — the "models the entire conversation flow, not a single-turn filter" claim is architecturally real, confirmed by directory structure and actual `.co` Colang files (not just described in marketing copy).**

## B — Agent Design
Not an agent framework — a guardrail layer that wraps/intercepts an existing agent's input/output. No role/contract abstraction of its own.
**Verdict: Absent — not a claimed capability.**

## C — Context & Memory
Not applicable to this project's purpose.
**Verdict: Absent — not a claimed capability.**

## D — Reliability
`jailbreak_detection/` contains both `heuristics/` and `model_based/` subdirectories (confirmed via directory listing) — i.e., a layered detection approach (fast heuristic pass + model-based fallback), not a single brittle check. Not independently traced for failure-mode handling within those modules this pass.
**Verdict: Moderate — layered-detection architecture confirmed structurally; internal failure-handling not fully traced.**

## E — Human Control
Not a human-approval mechanism — this is a content-safety guardrail layer, a different (complementary) mechanism from DOM-07's approval gates. Correctly scoped as DOM-17, not DOM-07, per the original triage.
**Verdict: N/A — different capability than DOM-07, correctly distinguished.**

## F — Evaluation
Real parser test suite confirmed (`tests/colang/parser/v2_x/inputs/*.co` — multiple real Colang test fixtures found and read directly, e.g. a simple `define user express greeting` / `define flow` / `define bot express greeting` fixture, confirming the DSL parser is exercised against real flow syntax, not just unit-tested abstractly).
**Verdict: Moderate — real test fixtures confirmed present and readable; full test-suite breadth not exhaustively assessed.**

## G — Operations
Extensive third-party integration surface (confirmed via directory listing above) suggests this is designed to be an orchestration layer over specialized guardrail vendors/models, not a from-scratch reimplementation of each safety mechanism — a real architectural choice with both a strength (leverages best-in-class detectors) and a dependency-surface cost (many integrations to maintain/trust).
**Verdict: Strong — broad, real integration surface, though this multiplies the trust/maintenance surface if all integrations were adopted (a cost worth noting, not resolving here).**

## H — Reusability
Colang is a genuinely separate DSL layer from any specific host application — the flow definitions are portable in principle. Adopting NeMo Guardrails wholesale means adopting Colang as a new authoring language, which is a real learning-curve cost.
**Verdict: Moderate — clean conceptual separation, but a new DSL to learn/maintain is a genuine adoption cost.**

## I — Evidence
License confirmed Apache 2.0 by direct file read (`LICENSE-Apache-2.0.txt` and `LICENSE.md`, SPDX header, NVIDIA Corporation copyright). Colang flow mechanism confirmed real via actual `.co` file inspection, not just docs. No docs-vs-code disagreement found this pass.
**Verdict: Strong.**

## J — License
Apache 2.0, confirmed by direct file read (dual license files present but both point to the same Apache 2.0 terms — no carve-out found, unlike litellm).
**Verdict: Strong.**

---

## Evidence Section — Docs/Claims vs. Code

**No disagreement found.** The Stage -2.3 characterization ("programmable guardrails... models the entire conversation flow... not a single-turn filter") held up under direct inspection of actual Colang flow files and the `library/` directory's real integration modules. The one nuance worth flagging for Stage -2.5 pattern extraction: this project's strength (breadth of third-party integrations: ActiveFence, CrowdStrike, Llama Guard, etc.) is architecturally a dependency-aggregation strategy — a pattern worth naming distinctly from a from-scratch guardrail implementation, since it trades implementation effort for integration-maintenance and trust-in-third-parties overhead. This is a FACT about the architecture (confirmed via directory structure), not an evaluation of whether that tradeoff suits Hermes (out of scope for Phase -2 to decide).
