# Deep Audit: getzep/graphiti

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo: https://github.com/getzep/graphiti | Cloned (depth=1) 2026-08-24 and read directly (Python source, driver implementations, docs) — not README-only.
Triage source: `repo-catalog.md` REPO-017, DEEP AUDIT. Relevant to DOM-12 (primary), DOM-11 (secondary).

## A — Architecture
`graphiti_core` is a temporal knowledge-graph library over pluggable graph backends (Neo4j, FalkorDB, Kuzu, Neptune — multiple driver implementations found under `graphiti_core/driver/`). Entities/facts are represented as timestamped nodes/edges; an MCP server (`mcp_server/`) and a REST server (`server/`) wrap the core library for external use.
**Verdict: Strong — genuinely backend-agnostic (4 independent driver implementations found, not just claimed), real architectural separation between core logic and storage.**

## B — Agent Design
Not an agent framework itself — a memory substrate other agents call into. No role/contract abstraction (out of scope for this project's purpose).
**Verdict: Absent — not a claimed capability.**

## C — Context & Memory (primary domain: DOM-12)
Bi-temporal fields confirmed by direct read of `graphiti_core/edges.py:271-277`: `expired_at`, `valid_at`, `invalid_at` are real `datetime | None` fields on the edge model, serialized/deserialized in `to_dict`/`from_record` (lines 352-354, 998-1000) — this is FACT, not a docs claim. The mechanism genuinely supports "a fact was true, then became false" temporal reasoning rather than crude overwrite.
**Verdict: Strong — the headline bi-temporal continuity mechanism is real, code-verified, and matches its documentation.**

## D — Reliability
No dedicated retry/circuit-breaker layer found in `graphiti_core` itself this pass (would rely on the underlying graph driver's own reliability); not independently traced further given time budget.
**Verdict: Weak/Unconfirmed — not evaluated in depth this pass, flagged as a gap in this audit rather than assumed absent.**

## E — Human Control
No approval-gate mechanism (not an agent-facing decision point, it's a memory store).
**Verdict: Absent — not a claimed capability.**

## F — Evaluation
Test suite present (`tests/`) but not independently sized/assessed this pass.
**Verdict: Unconfirmed this pass.**

## G — Operations
MCP server present and real (`mcp_server/` directory with its own structure) — provides a standard tool-call interface for agents to read/write graph memory.
**Verdict: Moderate — real MCP integration exists; depth of its tool surface not fully traced this pass.**

## H — Reusability
Cleanly separated core library vs. server wrappers; genuinely multi-backend (portable across 4 graph databases) — low framework lock-in for the core temporal-modeling logic itself, though adopting Graphiti wholesale means adopting a graph-database dependency, which is a real operational cost to weigh, not evaluated further here (out of Phase -2's scope to recommend).
**Verdict: Moderate — good separation, but graph-DB dependency is non-trivial infrastructure to inherit.**

## I — Evidence
License confirmed Apache 2.0 by direct file read (`LICENSE`). Bi-temporal claim confirmed FACT via code (see Dimension C). See Evidence section below for a DOM-11-relevant nuance found beyond the original triage record's framing.
**Verdict: Strong for the core claim re-checked; other claims (stars, exact adoption figures cited in `repo-catalog.md`) remain unverified secondary-source numbers, unchanged from Stage -2.3.**

## J — License
Apache 2.0, confirmed by direct file read. Permissive, no carve-outs found.
**Verdict: Strong.**

---

## Evidence Section — Docs/Claims vs. Code

**Nuance found, relevant to DOM-11 comparison-baseline use (not a contradiction of Graphiti's own docs, but a correction to how the Stage -2.3 catalog entry characterized it):**

The Stage -2.3 record described Graphiti's "fact invalidation instead of overwrite" model as comparison-worthy for DOM-11's never-delete principle. Direct code inspection this pass found that alongside the bi-temporal invalidation mechanism (real, confirmed above), Graphiti's edge classes ALSO implement genuine hard-delete methods: `EntityEdge.delete()` and `delete_by_uuids()` in `graphiti_core/edges.py` (lines 59-124, 710, 843) issue real `DELETE`/`DETACH DELETE` Cypher-family queries, implemented consistently across every driver backend (Neo4j/FalkorDB/Kuzu/Neptune each have their own `delete_by_uuids` implementation — not a single stray method). Most significantly, `Graphiti.remove_episode()` (`graphiti_core/graphiti.py:1765`) is a public, top-level, first-class API method on the main library class — this is not an internal test-cleanup utility, it is a documented consumer-facing capability.

**FACT:** Graphiti's default temporal-reasoning mechanism for handling contradictory/updated facts is non-destructive invalidation (confirmed).
**FACT:** Graphiti also exposes a public hard-delete API (`remove_episode`) and internal hard-delete operations across all backends (confirmed).
**INTERPRETATION:** if Graphiti (or its pattern) were ever adopted as a comparison baseline or component for a Hermes never-delete memory layer, the hard-delete API surface would need to be explicitly avoided/disabled at the integration boundary — Graphiti's "fact invalidation, not deletion" framing describes its default behavior for contradiction-handling, not a structural guarantee that nothing can ever be deleted. This is a more precise, code-verified characterization than the Stage -2.3 catalog entry's summary, which described the invalidation mechanism without noting the coexisting delete API.
