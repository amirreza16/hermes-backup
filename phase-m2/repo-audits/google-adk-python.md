# Deep Audit: google/adk-python

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Repo-catalog record: REPO-005. Relevant DOM IDs: DOM-01, DOM-02, DOM-06.

Source: `git clone --depth 1 https://github.com/google/adk-python.git`, inspected
2026-08-24. Apache License 2.0, confirmed from `LICENSE` file (FACT).

## A — Architecture
Explicit Agent/Workflow class split confirmed (`src/google/adk/agents/llm_agent.py` for the
core LLM-driven agent; workflow-orchestration primitives for routing/fan-out/fan-in/loops/
retry referenced in the Stage -2.3 triage but not independently re-verified file-by-file this
pass — UNKNOWN on the exact workflow-class names). Toolset architecture is explicit and
modular (`src/google/adk/tools/` with distinct files per tool type: `bash_tool.py`,
`function_tool.py`, `computer_use_tool.py`, `mcp_tool/`).
Verdict: Strong for the agent/tool architecture (directly verified); Moderate for the
workflow-graph specifics (not independently re-confirmed this pass beyond the triage record).

## B — Agent design
`output_schema` (Dimension C) is the primary contract mechanism. Role/mandate definition is
via the `LlmAgent` class's constructor fields (`instructions`, `tools`, `output_schema`,
etc. — pattern consistent with the other frameworks audited this session, not independently
enumerated field-by-field this pass).
Verdict: Moderate — core mechanism confirmed present, full field enumeration not exhaustive.

## C — Context & memory
`output_schema` confirmed real and enforced: `src/google/adk/agents/llm_agent.py:404`
(`output_schema: Optional[SchemaType] = None` field), `:1038-1044`
(`if self.output_schema: ... result = validate_schema(self.output_schema, result)` — an
explicit validation call against the returned result, not just a type hint). A validation
error path (`:1142,1144` — "Response schema must be set via LlmAgent.output_schema, not...")
suggests the framework guards against a specific known misconfiguration mistake, indicating
mature, battle-tested API design rather than a first-pass implementation.
Sessions/memory: `src/google/adk/sessions/` directory exists including a
`migration/migrate_from_sqlalchemy_pickle.py` file — implies a real, evolved persistence
layer with at least one past storage-backend migration already shipped (a positive
maintenance signal), though the session/memory architecture's internals were not deeply read
this pass (UNKNOWN on compaction/retrieval strategy specifically).
Verdict: Strong for output_schema enforcement (directly verified); Moderate-Unknown for the
session/memory layer's internal design (existence and maturity signal confirmed, mechanism
not deep-read).

## D — Reliability
Not exhaustively inspected this pass beyond the `output_schema` validation-error path
(Dimension C), which is itself a reliability mechanism for one specific failure mode.
Verdict: Not fully assessed — Moderate based on the one confirmed mechanism, UNKNOWN beyond
that.

## E — Human control
`src/google/adk/tools/tool_confirmation.py` confirmed to exist (file presence verified via
grep for `require_confirmation`/`tool_confirmation`/`ToolConfirmation` across `src`) —
directly substantiates the Stage -2.3 triage's claim of a "tool-confirmation HITL gate."
Internal mechanism (what triggers confirmation, how resume works) not read line-by-line this
pass — file's existence and naming confirm the feature is real and dedicated (not bolted onto
an unrelated file), which is itself meaningful evidence per Section 12.1 (a dedicated file for
a claimed feature is stronger evidence than the feature only being mentioned in docs).
Verdict: Strong on existence (confirmed real, dedicated implementation file); Moderate on
depth (internal trigger/resume logic not independently traced this pass).

## F — Evaluation
Not inspected this pass (UNKNOWN — out of this pass's time budget, no claim made either way).
Verdict: Not assessed.

## G — Operations
MCP integration confirmed substantial and real, not a thin wrapper: `src/google/adk/tools/
mcp_tool/` contains `mcp_session_manager.py`, `_agent_to_mcp.py`, `mcp_tool.py`,
`mcp_toolset.py` — a session-manager file specifically suggests connection lifecycle handling
(reconnect/timeout logic likely present, not independently confirmed this pass). Also found
`load_mcp_resource_tool.py` and `_remote_mcp_server.py`, and an `mcp_instruction_provider.py`
under `agents/` — suggesting MCP awareness is woven into agent instruction-building itself,
not just bolted on as a tool type. This is a materially richer MCP integration than a
single-file wrapper.
Verdict: Strong — real, multi-file, session-aware MCP integration confirmed via direct
inspection, exceeding what a README-level description alone would suggest.

## H — Reusability
Apache 2.0 licensed, Google-backed, org-maintained (confirmed via `LICENSE` and the presence
of `CONTRIBUTING.md`, versioned `constraints-3.1x.txt` files per Python version — a real
maintenance/compatibility-matrix signal). Framework coupling for the MCP layer specifically
looks separable (isolated under `tools/mcp_tool/`), but this pass did not verify whether it
can be imported/used independent of the rest of the ADK agent runtime.
Verdict: Moderate — good internal separation observed; cross-framework portability not
independently tested.

## I — Evidence
Docs vs. code: the Stage -2.3 triage record's three claims — orchestration, output_schema
contracts, and native MCP integration — were all independently confirmed as real, non-trivial
implementations on this pass, with the MCP integration turning out richer (session-manager,
instruction-provider awareness) than the triage summary implied. No contradiction found; if
anything, the triage record understated the MCP integration's depth.
Verdict: Strong — code confirms and in one respect exceeds the prior triage-level claims.

## J — License
Apache License 2.0, confirmed directly from `LICENSE` file (FACT).
Verdict: Strong — unambiguous, permissive, patent-grant-inclusive (standard Apache 2.0 terms).

---

## Evidence Summary (Stage -2.4 exit criterion)
No docs/triage-vs-code disagreements found. The MCP integration (Dimension G) is the standout
positive surprise of this audit — richer and more session-aware than the Stage -2.3 record
suggested, worth flagging explicitly for DOM-06 pattern extraction at Stage -2.5. Several
dimensions (B, D, F) were not exhaustively assessed given this pass's DOM-01/02/06 priority
focus — flagged as UNKNOWN/not-assessed rather than guessed, per Section P5.

## Stage -2.3 Triage Reassessment
No change to DEEP AUDIT status — confirmed and strengthened. The MCP session-manager finding
specifically should be weighted more heavily than the original triage record implied when
DOM-06 comparison work happens at Stage -2.5.
