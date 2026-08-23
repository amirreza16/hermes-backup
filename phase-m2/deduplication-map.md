# Hermes Phase -2 Deduplication Map

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.5.
Dedup pass run per Section 11 trigger (a): after Stage -2.2 completion, 2026-08-23.
Canonical selection order (Section 11.2.3): evidence depth > generalizability >
architectural quality > maintenance > popularity.

---

## Cluster 1 — Claude Skill authoring/packaging methodology
```
Capability: Designing and packaging a well-formed Claude Skill (structure, progressive disclosure, validation) — relevant to DOM-04
Candidates: SKL-008 (Agent Creator), SKL-009 (Skill Architect), SKL-010 (Skill Creator), SKL-022 (Skill Coach)
Shared Coverage: All four use the same underlying 6-7 step authoring loop (understand -> plan -> initialize -> edit -> validate/package -> iterate), the same progressive-disclosure loading model, and near-identical inputs/outputs (a skill directory with SKILL.md + scripts/references/assets).
Unique Coverage: SKL-008 (Agent Creator) adds MCP-integration and a 3-template-category framework (Technical Expert/Creative/Orchestrator) and targets agents broadly, not only skills. SKL-009 (Skill Architect) uniquely names concrete validation tooling (`validate_skill.py`, `check_self_contained.py`) and the "shibboleths" (expert-judgment-encoding) concept, plus explicit mandatory "NOT for" exclusion clauses. SKL-010 (Skill Creator) uniquely emphasizes packaging/distribution (`init_skill.py`/`package_skill.py` producing a distributable .zip) and the Scripts/References/Assets resource taxonomy. SKL-022 (Skill Coach) uniquely contributes a "should this even be a skill" necessity decision tree (3+ projects -> skill; single task -> execute directly; external API -> MCP; multi-step -> subagent).
Conflicts: None — these are near-duplicate variants from the same author/ecosystem, not competing/contradictory approaches.
Canonical Candidate: SKL-009 (Skill Architect) — highest Architectural Quality and Evidence Quality among the four (named validation scripts, explicit anti-pattern clauses), per the ordered selection criteria.
Secondary References: SKL-010 (Skill Creator, for the resource taxonomy), SKL-022 (Skill Coach, for the necessity decision tree). SKL-008 (Agent Creator) is broader in scope than pure skill-authoring (also covers full agent/MCP creation) and is kept as an independent record rather than folded fully into this cluster, though it overlaps here for the skill-authoring portion of its scope.
Rejected Redundancy: None formally rejected — all four retain distinct value as noted above; this is a "canonical + secondary references" resolution, not an elimination.
```

## Cluster 2 — LLM cost governance pipeline
```
Capability: Enforcing and tracking a hard compute/model-spend budget across an LLM-driven pipeline — relevant to DOM-16 (reframed around hermes-agent)
Candidates: SKL-015 (Cost Optimizer), SKL-016 (LLM Router), SKL-025 (Cost Accrual Tracker), SKL-031 (Cost Verification Auditor)
Shared Coverage: All four operate on the same underlying cost-governance problem and are explicitly designed by their own documentation to compose together (each names the others as dependencies).
Unique Coverage: SKL-025 (Cost Accrual Tracker) is the real-time data-capture layer (function-level API: recordUsage/getCurrentCost/finalize). SKL-015 (Cost Optimizer) is the enforcement/decision layer (tiered waterfall: normal -> downgrade -> skip -> halt). SKL-016 (LLM Router) is the model-selection mechanism the Optimizer's "downgrade" action invokes (task-tier classification, 3 routing strategies). SKL-031 (Cost Verification Auditor) is the estimate-accuracy feedback loop closing back onto the Accrual Tracker's data.
Conflicts: None.
Canonical Candidate: N/A — this cluster is intentionally NOT resolved to a single canonical pick. Unlike Cluster 1, these four are complementary pipeline stages (capture -> enforce -> route -> verify), not competing implementations of the same capability. Forcing a single "canonical" choice here would lose real, distinct coverage. Documented as an explicit exception to the usual canonical-selection procedure.
Secondary References: N/A (see above).
Rejected Redundancy: None.
```

## Cluster 3 — Meta-tools that create other Hermes building blocks
```
Capability: Creating new agents/subagents/MCP servers as capability gaps are identified — relevant to DOM-01, DOM-02, DOM-04, DOM-06
Candidates: SKL-008 (Agent Creator), SKL-021 (Skillful Subagent Creator), SKL-024 (MCP Creator)
Shared Coverage: All three are "meta" skills whose output is another building block (an agent, a subagent, or an MCP server) rather than end-user-facing content; all three include explicit contract/schema-definition steps.
Unique Coverage: SKL-008 creates full agents/personas across 3 template categories. SKL-021 creates subagents specifically pre-loaded with 2-5 existing skills as SOPs, with the most rigorous test-checklist of the three (happy path/edge case/out-of-scope-refusal/skill-adherence/contract-validation). SKL-024 creates MCP servers specifically, with a distinct decision tree for when MCP is the right tool at all.
Conflicts: None — each targets a genuinely different artifact type (agent vs. subagent-with-skills vs. MCP server), so this cluster is registered for completeness/transparency but is not actually redundant.
Canonical Candidate: N/A — distinct artifact types, no canonical needed.
Secondary References: N/A.
Rejected Redundancy: None.
```

## Cluster 4 — Ambiguity/risk detection and escalation
```
Capability: Detecting a risky or ambiguous situation and escalating to a human with calibrated severity before acting — relevant to DOM-09
Candidates: SKL-027 (Crisis Detection Intervention AI), SKL-028 (Crisis Response Protocol)
Shared Coverage: A single two-part mechanism — SKL-027 performs detection/classification, SKL-028 performs the assess-before-generate response gating. They are documented as directly dependent on each other (SKL-028 lists SKL-027 as a dependency).
Unique Coverage: SKL-027 owns the multi-signal detection and severity-classification logic plus the structured output schema. SKL-028 owns the assess-before-generate ordering constraint and the primary/secondary/tertiary indicator hierarchy with trend-escalation logic.
Conflicts: None.
Canonical Candidate: N/A — treat as one extractable pattern with two parts (detect, then respond), not two competing candidates. Both were reviewed jointly under Section 13/14 in skill-catalog.md.
Secondary References: N/A.
Rejected Redundancy: None.
```

## Cluster 5 — Human-approval-gate design
```
Capability: Deciding when/where a human approval gate belongs and validating what passes through it — relevant to DOM-07, DOM-02
Candidates: SKL-012 (Human Gate Designer), SKL-013 (Output Contract Enforcer)
Shared Coverage: Both operate at agent-to-agent or agent-to-human handoff boundaries.
Unique Coverage: SKL-012 decides WHEN a boundary needs a human gate (irreversibility/cost/confidence/ambiguity decision tree) and HOW feedback routes back (approve/modify/reject at 3 granularities). SKL-013 validates WHAT is allowed to pass a boundary regardless of whether a human is involved (JSON schema fail-fast validation).
Conflicts: None — genuinely complementary, different questions (when vs. what).
Canonical Candidate: N/A — distinct sub-capabilities, no canonical needed.
Secondary References: N/A.
Rejected Redundancy: None.
```

---

## Coverage Note

Per Section 11.3, every capability cluster with >=2 candidates is covered above.
Skills not appearing in any cluster (SKL-001 through SKL-007, SKL-011, SKL-014,
SKL-017 through SKL-020, SKL-023, SKL-026, SKL-029, SKL-030) had no second candidate
addressing the same capability surface within this stage's inspected sample and are
therefore singleton records in `skill-catalog.md`, not omissions from this map.
