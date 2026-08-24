# Hermes Phase -2 Rejected Candidates

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.7.
First populated at Stage -2.2 (Skill Discovery), 2026-08-23.

---

```
Candidate ID: REJ-001
Candidate: SKL-018 — Launch Readiness Auditor
Source: SomeClaudeSkills, https://someclaudeskills.com/docs/skills/launch_readiness_auditor/
Reason Rejected: Evaluates whether a software codebase is production-ready to ship (feature completeness, test coverage, blocker triage) — this is a build-process/SDLC concern, not a Hermes runtime capability. None of the 25 active research domains in research-domains.md map to "is a codebase launch-ready." Same category of out-of-scope reasoning already applied at Stage -2.1 to the dropped seeds "Spec-driven development" and "Architecture documentation" (Section 2.4's build-readiness test is a downstream Phase -1/specification concern, not Phase -2 research scope).
Potentially Useful Parts: The 8-dimension health-scoring framework and the Ship-It/Sprint-It/Defer-It/Cut-It triage matrix could plausibly be reused much later, outside Phase -2, as a template for Hermes' own eventual build-readiness review (Section 2.4's North Star) — but that is explicitly out of scope for this phase and not something Phase -2 should pursue or recommend acting on now.
What Would Change the Decision: Nothing within Phase -2's current scope — this would only become relevant if the Owner explicitly expanded scope to include build-process tooling, which would itself require an escalation per Section 5.2 (major research-scope change), not a unilateral Stage -2.2 decision.
Date: 2026-08-23
```

```
Candidate ID: REJ-002
Candidate: SKL-032 — Modern Auth 2026
Source: SomeClaudeSkills, https://someclaudeskills.com/docs/skills/modern_auth_2026/
Reason Rejected: Title and category (Security/DevOps) suggested relevance to DOM-08 (Permissions & least-privilege scoping), but the actual mechanism is end-user consumer authentication (WebAuthn passkeys, OAuth social login, magic links) for people logging into an application. DOM-08's real need is machine-to-machine credential isolation between an agent instance and a social platform's own API, per social page — a completely different problem (no end users are authenticating into anything in Hermes' architecture as described in the raw idea). Zero component of the WebAuthn/OAuth/magic-link mechanism transfers. Registered explicitly as a demonstration of the "do not rate a skill highly because its title sounds relevant" discipline (Section 15.1 / Stage -2.2 rules) — this is a case where inspection past the title/category was necessary to catch a mismatch that a shallow pass would have missed.
Potentially Useful Parts: None identified for Hermes' actual DOM-08 need.
What Would Change the Decision: If Hermes ever needs end-user-facing login (e.g., a web dashboard for the Owner with multi-factor authentication), this skill's OAuth/passkey mechanics would become directly relevant — but that is a different capability than DOM-08 as currently scoped, and would warrant its own domain if it becomes a real Hermes need later.
Date: 2026-08-23
```

---

**Stage -2.3 additions (2026-08-24)** — full records for the repo candidates
inspected substantively enough to warrant this schema beyond the Triage
Rationale already logged in `repo-catalog.md`. Repos excluded purely by a
domain's own Exclusion Criteria without individual inspection (generic IAM
tools, large-scale workflow engines out of scale, academic-only papers) are
not given records here — see `repo-catalog.md`'s "Coverage Gaps" section and
each domain's Exclusion Criteria in `research-domains.md`.

```
Candidate ID: REJ-003
Candidate: Mattbusel/llm-budget (REPO catalog record, Cluster D)
Source: https://github.com/Mattbusel/llm-budget
Reason Rejected: 3 stars, single contributor, 5 commits, no releases — insufficient evidence maturity per Section 10.4 discipline. Section 12.1 forbids treating a recent/thin repo as production-proven regardless of how directly its concept (fleet-wide cost ledger) matches DOM-16.
Potentially Useful Parts: The `BudgetLedger`/`FleetGovernor`/`CostEvent` naming/structuring concept for fleet-wide budget tracking, if a future pass wants a minimal reference implementation to read alongside the more mature LiteLLM/AgentBudget candidates.
What Would Change the Decision: Real adoption signal (issues, forks, a second contributor, a tagged release) would justify revisiting as a REFERENCE ONLY candidate; the underlying capability is already covered by REPO-022 (LiteLLM, DEEP AUDIT) and REPO-023 (AgentBudget, REFERENCE ONLY), so this would need to add something distinct to be worth promoting.
Date: 2026-08-24
```

```
Candidate ID: REJ-004
Candidate: anomalyco/opencode — Issue #13952 "Immutable Audit Logs for Agent Actions via Local Merkle Tree" (REPO catalog record, Cluster C)
Source: https://github.com/anomalyco/opencode/issues/13952
Reason Rejected: No shipped code exists — this is a closed, unmerged feature proposal, not an implementation. Section 12.2's evidence hierarchy places an unmerged proposal below even docs/examples; nothing exists to deep-audit.
Potentially Useful Parts: The hash-chained append-only mechanism itself (H(n)=SHA256(Action_n+H(n-1)), runtime-appends-only/tools-cannot-modify, a verify-audit integrity command) is a well-specified, on-point design for DOM-11 and is preserved for Stage -2.5 pattern extraction with this issue cited as the design's origin, independent of the repo-rejection.
What Would Change the Decision: If this proposal (or an equivalent) is ever actually merged and shipped in some repo, it would immediately warrant a DEEP AUDIT re-triage — it is presently the most on-point mechanism found anywhere in Stage -2.3 for DOM-11's exact need, blocked only by non-existence of real code.
Date: 2026-08-24
```

```
Candidate ID: REJ-005
Candidate: dakshjain-1616/Agent-Memory-Compressor (REPO catalog record, Cluster C)
Source: https://github.com/dakshjain-1616/Agent-Memory-Compressor
Reason Rejected: No evidence of maintenance, adoption, or testing found beyond the repo's own README description — single-author, no corroborating signal (Section 12.1). Graphiti (REPO-017) covers the same DOM-12 need with materially stronger evidence.
Potentially Useful Parts: The importance-scoring + forgetting-curve-trigger compaction mechanism is a distinct approach from Graphiti's temporal-graph model and mem0's fact-extraction model — worth a second look as a lighter-weight alternative if either proves insufficient for narrative/voice continuity specifically at deep audit.
What Would Change the Decision: If Stage -2.4's audit of Graphiti finds it insufficient for narrative/voice continuity, revisit this repo as a lighter-weight alternative — explicit reversal condition carried over from the discovering fork's own recommendation.
Date: 2026-08-24
```

```
Candidate ID: REJ-006
Candidate: handrew/agentic_gpt (REPO catalog record, Cluster B)
Source: https://github.com/handrew/agentic_gpt
Reason Rejected: Provides only a thin `ask_user_fn` callback hook with no visible trigger logic for *when* to invoke it — DOM-09's actual research question is about the trigger (confidence threshold, missing required field, conflicting signals), not the existence of an escape hatch. Dated, minimal activity.
Potentially Useful Parts: None identified — the callback-hook pattern itself is trivial and not a meaningful mechanism to extract.
What Would Change the Decision: Nothing about this specific repo; it would need substantial new trigger-logic code to become relevant, at which point it would effectively be a different project. DOM-09 remains a confirmed coverage gap (see `repo-catalog.md`) independent of this rejection.
Date: 2026-08-24
```

```
Candidate ID: REJ-007
Candidate: open-gitagent/gitagent (REPO catalog record, Cluster F — rejected for DOM-24 purposes only)
Source: https://github.com/open-gitagent/gitagent
Reason Rejected: The repo's own FAQ explicitly states "no multi-tenant support" — a direct, self-reported disqualification for DOM-24's exact research question, not a judgment call requiring further inspection.
Potentially Useful Parts: Its git-native version-controlled agent identity/rules/memory/tools pattern and MCP auto-discovery/plugin-manifest system are real and inspectable (658 stars, active) — potentially relevant to DOM-04 (skill design) or DOM-06 (tool-use/MCP) in a future pass, entirely independent of this DOM-24 rejection.
What Would Change the Decision: If the project ships multi-tenant support in a future release, it would need fresh triage for DOM-24 at that point — this rejection is scoped to the capability, not the project's overall quality.
Date: 2026-08-24
```

```
Candidate ID: REJ-008
Candidate: younis-ali/market-research-agent (REPO catalog record, Cluster E)
Source: https://github.com/younis-ali/market-research-agent
Reason Rejected: The claimed "synthesis" step is LLM generation from a static, pre-populated PostgreSQL sector/address seed table, not real market/competitive data gathering — fails DOM-18's exclusion criteria in substance (real research-synthesis mechanism required) despite superficially having a synthesis-shaped step. Minimal commit history (5 commits), no evidence of a working research capability.
Potentially Useful Parts: None identified.
What Would Change the Decision: Real external data-gathering (scraping, API integration, live search) feeding the synthesis step would change this from a REJECT to at least a REFERENCE ONLY candidate — but as inspected, it does not do this.
Date: 2026-08-24
```
