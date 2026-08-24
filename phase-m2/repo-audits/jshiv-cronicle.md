# Deep Audit: jshiv/cronicle

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo: https://github.com/jshiv/cronicle | Cloned (depth=1) 2026-08-24 and read directly (Go source, HCL configs, docs, tests) — not README-only.
Triage source: `repo-catalog.md` REPO-016, DEEP AUDIT. Relevant to DOM-13 (primary), DOM-11, DOM-16, DOM-06 (secondary).

## A — Architecture
Single-binary Go daemon (`cronicle.go`, `internal/cronicle/`). HCL-declared task definitions (`Cronicle.hcl`) with explicit `depends_on` DAG edges (`internal/cronicle/dag.go`), cron-triggered (`cron.go`) or listener-fired (`listen.go`) execution. State is split cleanly: `cronicle.jsonl` (slog-based structured event log, explicitly documented in code comments as authoritative) + an SQLite "state plane" (`internal/cronicle/state/store.go`) explicitly described in its own package doc as a "retention-windowed... projection" that "rebuilds from event ingest" — i.e., disposable/derived, not authoritative.
**Verdict: Strong — clean, explicit separation between authoritative log and derived/disposable projection, documented in code, not just inferred.**

## B — Agent Design
Task-level `agent` blocks in HCL (`internal/cronicle/config.go`) wrap an LLM-driven agent runner (`pkg/agent/agent.go`) with explicit `BudgetUSD`, model config, and tool access per task. No cross-task role/contract abstraction beyond the DAG dependency graph — each task is an independent unit, not a multi-role system.
**Verdict: Moderate — real per-task agent config, but no higher-level multi-agent role/contract layer; DAG dependency is the only coordination primitive.**

## C — Context & Memory
No persistent cross-run memory abstraction found (this is a scheduler, not a memory system) — DOM-11 relevance is specifically about its own operational audit trail, not agent memory. See Evidence section below for the DOM-11 finding.
**Verdict: Absent (as a memory system) / Moderate (as an audit-trail mechanism, see Evidence) — cronicle does not implement agent memory; its relevance to DOM-11/12 is limited to its own event-log architecture.**

## D — Reliability
Per-run JSONL transcripts (`internal/cronicle/transcript.go`) written to `.cronicle/runs/{run_id}-{task}.jsonl`, three-line schema (request/response/accounting), env values redacted by default (`redactEnv`, explicit secret-exposure comment in source). DAG dependency-gated execution with automatic downstream-skip on failure (confirmed via `dag.go`/`cron.go` structure, not independently unit-traced line-by-line this pass). `BudgetUSD` abort-on-exceed confirmed real and wired end-to-end: `config.go:151-153` (HCL field) → `exec.go:321` (passed to agent) → `pkg/agent/agent.go:318-320` (`ErrBudgetExceeded` raised when `currentCost > cfg.BudgetUSD`). Distributed mode claim (SQLite-durable job queue) not independently verified this pass — flagged as UNKNOWN, not confirmed.
**Verdict: Strong for budget enforcement (code-verified, real abort path) / Moderate for the rest (structurally present, not exhaustively traced).**

## E — Human Control
No explicit human-approval-gate mechanism found for task execution (this is a cron scheduler, not an interactive agent) — out of scope for cronicle's own design; not a gap relative to its stated purpose.
**Verdict: Absent — not a claimed capability of this project.**

## F — Evaluation
95 `*_test.go` files found across the repo (`find . -name "*_test.go" | wc -l` = 95), including dedicated tests for the agent/budget path (`agent_test.go`) and DAG/listener behavior. No LLM-output-quality evaluation framework (not this project's job).
**Verdict: Moderate — substantial unit-test coverage for a project this size; no agent-output-quality eval layer (not claimed).**

## G — Operations
Real, standards-based skill loading confirmed: `internal/cronicle/skill.go` implements "Anthropic's Agent Skills open standard with progressive disclosure" — SKILL.md frontmatter parsed eagerly, body fetched on demand via a `load_skill` meta-tool (source comment, lines 1-16). MCP server support present (`internal/cronicle/mcp.go`, referenced in file listing; not independently line-traced this pass). Structured JSON logging (slog + lumberjack rotation) confirmed as the default observability path.
**Verdict: Strong — real, spec-compliant skill loading is a genuinely notable finding, directly relevant to DOM-04/DOM-06 bridging questions beyond what Stage -2.3 flagged.**

## H — Reusability
Single Go binary, no heavy external framework coupling found. Multi-domain relevance (DOM-13/11/16/06/04) in one small codebase is real and independently verified, not just claimed — this is a strong reusability signal (a small number of files answer several Hermes questions at once). Not evaluated for direct code reuse into a Python-based Hermes stack (cross-language — patterns only, not code).
**Verdict: Moderate — patterns are cleanly separable and cross-language-portable in principle; direct code reuse would require a Go runtime, which may not fit Hermes' stack (unconfirmed what Hermes' stack is at this research stage).**

## I — Evidence
License confirmed MIT via direct file read (`LICENSE`, copyright Jason Shiverick 2019). Recent commit activity real (431 commits per Stage -2.3 catalog entry; not independently re-counted this pass, consistent with what was found). No doc/code mismatch found for the claims actually re-verified this pass (skill loading, budget enforcement, log/state-plane split) — all held up under direct code inspection.
**Verdict: Strong — every claim re-checked this pass was confirmed in code, not just docs.**

## J — License
MIT, confirmed by direct file read. No carve-outs or dual-licensing found (unlike litellm's enterprise/ split, see that audit).
**Verdict: Strong — clean, unrestricted MIT.**

---

## Evidence Section — Docs/Claims vs. Code (required per Stage -2.4 exit criterion)

**CONFIRMED, code-level (not just Stage -2.3's docs-based flag) — DOM-11 conflict is real and more precise than initially characterized:**

Direct read of `internal/cronicle/log.go:397-404`:
```go
file := &lumberjack.Logger{
    Filename:   filepath.Join(logDir, "cronicle.jsonl"),
    MaxSize:    500, // MB per file before rotation
    MaxBackups: 3,   // keep up to 3 rotated files
    MaxAge:     28,  // days; older files deleted
    Compress:   true,
}
```
This is FACT, not inference — read directly from source, confirming the Stage -2.3 discovery pass's flag was accurate.

**Stronger finding than Stage -2.3 surfaced:** the package doc comment at the top of `internal/cronicle/state/store.go` states explicitly: *"Logs remain authoritative for what happened (cronicle.jsonl on disk). The projection is a derived, retention-windowed view... Delete the state DB and the log on disk still has the truth."* This means cronicle's own architecture treats the rotated-and-deleted `cronicle.jsonl` file as the **authoritative record of truth**, not a disposable debug mirror — the SQLite "state plane" is explicitly the disposable one. This is a direct, code-and-comment-confirmed conflict with Hermes' never-delete principle (DOM-11): cronicle's authoritative audit trail is designed to self-truncate after 28 days / 3×500MB, by the project's own architectural intent, not an oversight.

**Nuance not previously flagged:** per-run transcripts (`.cronicle/runs/{run_id}-{task}.jsonl`, one file per run) were NOT found to have any automatic rotation/deletion mechanism in this pass (no cleanup code found in `transcript.go` or elsewhere for the `runs/` directory) — these appear to grow unbounded rather than being deleted, which is a different operational concern (disk growth) than the never-delete conflict, and would need explicit confirmation this file is truly never pruned anywhere else in the codebase before treating it as FACT (kept as INTERPRETATION here, not FACT, since absence-of-evidence for a cleanup path is not proof none exists).

**No other docs-vs-code disagreement found** this pass — the budget enforcement, skill-loading, and log/state-plane-split claims all held up exactly as characterized when checked against actual source.
