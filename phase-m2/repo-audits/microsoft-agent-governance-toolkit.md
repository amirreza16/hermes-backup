# Deep Audit — microsoft/agent-governance-toolkit (REPO-010)

Stage -2.4. Schema: Master Plan Section 9.3 (Dimensions A-J).
Cloned `--depth 1` on 2026-08-24 to a scratch dir; inspected structure, source,
tests, docs, license — not README alone.

**Scale correction vs. Stage -2.3 triage note:** this is not a single focused
"governance toolkit" — it is a large monorepo bundling ~15 sub-projects
(agent-mesh, agent-hypervisor, agent-marketplace, agent-lightning, agent-sre,
agent-rag-governance, mcp-trust-server, crypto-attestation, decision-bom,
spendguard, etc.) across Python/TS/.NET/Go/Rust, plus ~30 example
integrations and a full docs site (ADRs, compliance mappings, specs). Treat
sub-project maturity as uneven — this audit focuses on `agent-mesh` (the
`govern()` core) and `agent-hypervisor` (privilege rings), the two pieces
DOM-05/07/08 actually depend on.

## A — Architecture
`agent-mesh` provides `govern(fn, *, policy, ...)` (`agent-governance-python/
agent-mesh/src/agentmesh/governance/govern.py:664`), which wraps any callable
into a `GovernedCallable` that evaluates a YAML policy engine *before*
execution and raises `GovernanceDenied` by default on deny (confirmed by
reading the function body and docstring, not just the README). This is a
structural interception point, not a prompt-level suggestion — matches the
README's central claim.
Verdict: Strong — real interception mechanism, code-verified.

## B — Agent design
Roles are expressed via `agent_id` on `govern()` calls and a
zero-trust-identity layer (SPIFFE/DID references found in `agentmesh`
trust-record code — `TRACE v0.2 Trust Record`, `close_session()` emits a
signed record keyed to a SPIFFE URI or DID). Contracts are policy-file-based
(YAML), not typed schemas.
Verdict: Moderate — identity/role concept is real but SPIFFE/DID integration
depth not fully traced (would need Dimension-level follow-up on the identity
module itself).

## C — Context & memory
Out of scope for this toolkit — it does not manage agent memory/context; it
governs tool-call execution. No claim to audit here.
Verdict: Absent — not this toolkit's concern.

## D — Reliability
`agent-hypervisor/src/hypervisor/rings/elevation.py` implements time-bounded
privilege elevation (`RingElevationError`, trust-score-gated, auto-expiring
via `tick()`), plus a `breach_detector.py` and `rate_limiter.py` in the same
package — real, specific reliability/safety code, not just a claim.
Verdict: Strong — inspected source directly.

## E — Human control
`require_approval` is real: `agent-mesh/tests/test_approval.py`,
`test_govern_approval_coordinator.py`, and `src/agentmesh/lifecycle/
models.py`/`server/policy_server.py` reference an `ApprovalCoordinator` /
`ApprovalTransport` wired directly into `govern()`'s parameters
(`approval_handler`, `approval_coordinator`, `approval_ttl_seconds=300.0`
default). This is DOM-07-relevant: a real, code-level approval-gate hook, not
just a design doc.
Verdict: Strong — approval flow is a first-class `govern()` parameter with
tests.

## F — Evaluation
`benchmarks/`, `docs/benchmarks/`, and a `.clusterfuzzlite` fuzzing setup
exist at the repo root; `policy-engine/generator/tests` suggests generated
policy conformance testing. Did not trace a business-level (Hermes-relevant)
eval framework — this toolkit evaluates policy conformance, not content
quality.
Verdict: Moderate — real infra, different evaluation target than DOM-15 needs.

## G — Operations
Cost governance appears as its own example (`examples/cost-governance`,
`examples/spendguard-composite`) — DOM-16-adjacent but not this toolkit's
core claim; not independently verified beyond file existence this pass.
Verdict: Weak (for this dimension specifically) — presence confirmed, depth
not verified.

## H — Reusability
Genuinely modular: `govern()` is a 2-line wrapper per the README's own
quickstart example, confirmed structurally decoupled from any one agent
framework (integrations exist for LangChain, CrewAI, OpenAI Agents SDK,
Google ADK, Flowise, smolagents — each as a separate `examples/*-governed`
directory). Coupling to the policy-engine's own YAML DSL is the main adoption
cost.
Verdict: Strong — designed for cross-framework reuse, evidenced by breadth of
integration examples.

## I — Evidence (docs vs. code)
**Self-claims verified as accurate on direct inspection:**
- "992 conformance tests" (README:361) — FACT-adjacent: found 739 test *files*
  across the monorepo (`find . -iname "test_*.py" -o ... | wc -l` = 739);
  since a single file commonly holds multiple test functions, 992 individual
  test cases is plausible and not contradicted, but the exact figure was NOT
  independently counted at the test-case level — label as UNVERIFIED-BUT-
  PLAUSIBLE, not confirmed FACT.
- "10/10 OWASP Agentic Top 10 Covered" (README badge) — INTERPRETATION only:
  a mapping doc exists (`docs/compliance/owasp-agentic-top10-architecture.md`)
  but this audit did not independently verify each of the 10 categories maps
  to an enforced (not just documented) control. Flag for a dedicated
  compliance-mapping read if this claim becomes load-bearing for Hermes.
- `govern()` "enforces policy before execution" — FACT, confirmed by reading
  the function source directly (raises `GovernanceDenied`, not a log-only
  side effect).
**Gap found:** the toolkit's own README doesn't clearly signal how uneven
sub-project maturity is (agent-mesh and agent-hypervisor read as the mature
core; several sibling directories like `agent-marketplace`, `agent-os`,
`agent-lightning` were not inspected this pass and their maturity is UNKNOWN)
— a reader taking the top-level README at face value could over-credit the
whole monorepo based on agent-mesh's real quality.

## J — License
MIT (`Copyright (c) Microsoft Corporation`), confirmed by reading `LICENSE`
directly. No reuse restriction found.
Verdict: Strong — clear, permissive, org-backed.

## Overall
The core claim (structural, not prompt-level, policy enforcement) is
code-verified true for `agent-mesh`. DOM-05, DOM-07, DOM-08 all have real,
inspectable mechanisms here, not just documentation. Recommend this remain the
primary comparison baseline for those three domains at Stage -2.5, scoped
explicitly to `agent-mesh` + `agent-hypervisor`, not the full monorepo.
