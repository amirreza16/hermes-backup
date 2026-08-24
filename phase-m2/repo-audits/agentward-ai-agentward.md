# Deep Audit — agentward-ai/agentward (REPO-012)

Stage -2.4. Schema: Master Plan Section 9.3 (Dimensions A-J).
Cloned `--depth 1` on 2026-08-24; inspected `agentward/policy/`,
`agentward/proxy/`, `agentward/scan/`, tests, LICENSE.

## A — Architecture
A proxy (`agentward/proxy/{http,server,content}.py`) intercepts tool calls and
routes them through `agentward/policy/engine.py`'s `PolicyEngine`, which
exposes `evaluate(tool_name, arguments)` and `evaluate_chaining(source_skill,
target_skill)` — the latter is notable: it evaluates *sequences* of tool
calls, not just individual calls in isolation, which is the mechanism behind
the session-level evasion detection claimed in Stage -2.3 triage.
Verdict: Strong — real interception + sequence-aware policy evaluation,
confirmed by reading `engine.py` directly.

## B — Agent design
Not an agent-role framework — this governs what an already-running agent's
tool calls are permitted to do, agnostic to how the agent itself is
structured.
Verdict: Absent — out of scope by design.

## C — Context & memory
Not applicable — no agent memory management; `evaluate_chaining` tracks
call-sequence state only for evasion detection, not general memory.
Verdict: Absent.

## D — Reliability
`agentward/policy/constraints.py` implements `evaluate_capabilities` and
`evaluate_argument_constraints` as separate, composable checks (path/domain/
CIDR/argument-shape per the original triage description) — confirmed present
as real functions, not just documentation. Did not trace retry/circuit-
breaker behavior specifically (not this tool's concern — it's a gate, not a
caller).
Verdict: Moderate.

## E — Human control
`README.md`'s own documented output vocabulary includes a `△ GAP` state
("No policy rule covers this tool at all — coverage gap"), confirmed present
verbatim in both `README.md:691` and the rendered `docs/Site/docs.html:464` —
i.e., the tool explicitly surfaces its own blind spots to the operator rather
than silently defaulting to allow or silently defaulting to deny. This is a
notable, self-aware design choice relevant to DOM-08's "what is an agent
capable of at all" framing.
Verdict: Moderate — no approval-workflow UI found (that's DOM-07 territory,
out of this repo's stated scope); the coverage-gap signaling is real and
DOM-08-relevant.

## F — Evaluation
`agentward/testing/` (models.py, cli.py, loader.py) appears to be a policy
*testing* harness — for validating an operator's own policy files, not for
evaluating agent output quality. Different target than DOM-15.
Verdict: Weak (for DOM-15 purposes) — real but off-target dimension.

## G — Operations
`agentward/scan/` (python_scanner.py, npm_scanner.py, permissions.py,
chains.py, explainer.py, recommendations.py) is a static-analysis layer that
scans a codebase's dependencies/tool-call chains for risk *before*
deployment — genuine defense-in-depth tooling, evidenced by real per-ecosystem
scanner modules, not a single generic scanner.
Verdict: Strong — concrete, differentiated scanning code.

## H — Reusability
Policy engine is decoupled from any specific agent framework (README
describes `npm`/Python bindings separately: `npm/` directory + Python
package) — genuine cross-language design intent, partially verified (both
directories exist with real content, full functional parity not verified this
pass).
Verdict: Moderate.

## I — Evidence (docs vs. code)
**Maintenance-signal correction to the Stage -2.3 triage record:** the last
commit found in this shallow clone is dated **2026-04-28** ("report: spell out
'control gaps' on each summary card line") — nearly four months stale as of
this audit (2026-08-24), not the "active, v0.4.0" characterization implied by
the original triage's "118 commits" note taken at face value. This is a
material downgrade to the maintenance-signal picture (Section 10.1.7) and
should be weighed accordingly at Stage -2.5 — label the original "active"
characterization as OUTDATED, this audit's 2026-04-28 finding as FACT.
**Test-coverage claim:** found 70 test files under `tests/` — the original
triage's "3,466 passing tests" figure was not independently re-derived at the
test-case level this pass (plausible if each file holds ~50 assertions on
average, but UNVERIFIED, not confirmed).
**No docs-vs-code functional contradiction found** — the `PolicyEngine`,
scanner modules, and `△ GAP` self-reporting all match their documented
behavior on direct inspection.

## J — License
Confirmed by reading `LICENSE` and `LICENSE-CHANGE.md` directly: **Business
Source License 1.1** (MariaDB Corporation's BSL text), effective for all
commits from **2026-04-24** forward, automatically reverting to **Apache
License 2.0 on 2028-04-24** for every version. This is a real, currently-
proprietary restriction (not a rumor) — code from this repo cannot be reused
in a commercial product before that date without a separate commercial
license from the maintainers (standard BSL terms; exact production-use
threshold not independently verified from the LICENSE text alone — read the
full BSL "Additional Use Grant" section before relying on this for any actual
adoption decision, which is out of scope for Phase -2 regardless).
Verdict: Moderate — real, permissive-eventually license, but a genuine current
restriction, correctly flagged by the original triage.

## Overall
Core policy-interception and chain-evasion-detection mechanisms are real and
code-verified — genuinely the most agent-specific (vs. generic IAM) DOM-08
candidate found in Stage -2.3. Maintenance signal is weaker than originally
characterized (4-month-stale commit history) — note this explicitly at
Stage -2.5 pattern extraction rather than carrying forward the "active"
label unexamined.
