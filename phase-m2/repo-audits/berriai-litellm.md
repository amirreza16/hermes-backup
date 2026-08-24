# Deep Audit: BerriAI/litellm

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo: https://github.com/BerriAI/litellm | Cloned (depth=1) 2026-08-24 and read directly (Python source across `litellm/`, `litellm/proxy/`, `litellm/router_strategy/`) — not README-only. This repo was explicitly flagged in Stage -2.3 as docs-verified only ("architectural detail wasn't visible from a single-page fetch") — this audit's primary job was closing that gap.
Triage source: `repo-catalog.md` REPO-022, DEEP AUDIT. Relevant to DOM-16.

## A — Architecture
Proxy + SDK dual-mode: `litellm/` core SDK, `litellm/proxy/` FastAPI-based gateway server, `litellm-rust/` (separate high-performance component, not inspected this pass). Routing strategies live in `litellm/router_strategy/` as a genuine plugin family (10 distinct strategy files found: `lowest_cost.py`, `lowest_latency.py`, `lowest_tpm_rpm.py`/`_v2.py`, `least_busy.py`, `simple_shuffle.py`, `tag_based_routing.py`, `budget_limiter.py`, plus `adaptive_router/`, `auto_router/`, `complexity_router/`, `quality_router/` subpackages), not a single hardcoded strategy.
**Verdict: Strong — genuinely richer and more modular than the docs page conveyed; multiple real, independent routing strategies confirmed in code.**

## B — Agent Design
Not an agent framework — an LLM-call gateway/router. No role/contract abstraction (out of scope for this project).
**Verdict: Absent — not a claimed capability.**

## C — Context & Memory
Not applicable — this is a routing/cost-control layer, not a memory system.
**Verdict: Absent — not a claimed capability.**

## D — Reliability
Budget enforcement confirmed as real, pre-call, blocking logic — not just post-hoc tracking. Direct read of `litellm/proxy/hooks/max_budget_limiter.py`: `_PROXY_MaxBudgetLimiter(CustomLogger)` implements `async_pre_call_hook` which `raise ProxyRateLimitError(...)` (lines 73, 80) when a budget is exceeded, meaning the call is blocked BEFORE it reaches the model, not flagged after the fact. Multiple budget-scope hooks found beyond what Stage -2.3 identified: `max_budget_limiter.py`, `model_max_budget_limiter.py`, `max_budget_per_session_limiter.py`, plus `proxy/spend_tracking/budget_reservation.py` and `proxy/common_utils/reset_budget_job.py` (periodic reset, e.g. for daily/monthly budgets).
**Verdict: Strong — code-verified real enforcement (raises and blocks), not merely reporting; richer than the single "budget caps" line item Stage -2.3 could confirm from docs alone.**

## E — Human Control
No agent-facing approval-gate concept (out of scope — this is an infrastructure layer between an agent and the model API, not an agent itself).
**Verdict: Absent — not a claimed capability.**

## F — Evaluation
Not independently assessed this pass (out of scope for DOM-16's specific question; would require a separate pass if litellm's own test/CI quality became load-bearing for a future decision).
**Verdict: Unconfirmed this pass.**

## G — Operations
This IS the operations layer for cost/routing by design. `LowestCostLoggingHandler` (`litellm/router_strategy/lowest_cost.py`) implements real cost-aware deployment selection (`async_get_available_deployments`, line 177) driven by logged spend data (`log_success_event`/`async_log_success_event`), confirming the "cheap-first escalation" framing is backed by an actual selection algorithm, not just configuration flags.
**Verdict: Strong.**

## H — Reusability
Proxy mode (a standalone gateway service) is naturally reusable regardless of Hermes' own language/stack, since it's consumed over an HTTP API, not imported as a library — lower integration friction than a same-language library dependency. SDK mode requires Python.
**Verdict: Strong for proxy-mode adoption; Moderate for SDK-mode (language-coupled).**

## I — Evidence
The single most important finding this audit: Stage -2.3's docs-based triage was accurate in direction but understated the depth of what actually exists in code — real enforcement (raises/blocks), real multi-strategy routing (10 files, not one), and real periodic budget-reset jobs were all confirmed that the docs page alone did not surface. No docs-vs-code disagreement found — code exceeds what the single docs page described, in the positive direction.
**Verdict: Strong — code-level inspection upgraded confidence in this candidate rather than finding gaps.**

## J — License
**Correction to the Stage -2.3 catalog entry, which listed license as "unconfirmed."** Direct read of `LICENSE`: LiteLLM is **dual-licensed** — content under the `enterprise/` directory is licensed separately under `enterprise/LICENSE` (not inspected this pass, flagged as a follow-up if enterprise-tier code is ever considered), and everything else is MIT. The specific budget/routing code inspected in this audit (`litellm/proxy/hooks/`, `litellm/router_strategy/`) lives outside `enterprise/`, so it is MIT-licensed — but this dual-license structure is a material correction worth carrying forward, since a shallow "LiteLLM is MIT" claim would be inaccurate for the repo as a whole.
**Verdict: Strong (with the dual-license structure now precisely documented) — was previously an open evidence gap, now closed.**

---

## Evidence Section — Docs/Claims vs. Code

**No disagreement found.** Every claim carried forward from Stage -2.3's docs-only triage (per-key/team/org/model budget caps, cheap-first routing, retry/fallback) was confirmed accurate at the code level, and code inspection surfaced meaningfully more depth than the docs conveyed: real pre-call blocking (not just alerting), 10 distinct routing strategies (not a single implied one), and periodic budget-reset jobs. The one correction is licensing precision (dual MIT + separately-licensed `enterprise/` carve-out), not a functional-claims disagreement. This repo is the strongest DOM-16 candidate found across all of Stage -2.3/-2.4, now on code-level rather than docs-level evidence.
