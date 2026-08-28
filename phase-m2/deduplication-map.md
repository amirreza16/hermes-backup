# Hermes Phase -2 Deduplication Map

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.5.
Dedup pass run per Section 11 trigger (a): after Stage -2.2 completion, 2026-08-23.
**Process note:** trigger (b) (after Stage -2.4 completion) was not run at the
time — Stage -2.4 completed 2026-08-25 but this file was not revisited until
2026-08-28, during the Stage -2.5 restart. Clusters 6-9 below close that gap,
covering repo-level (not just skill-level) overlap discovered across the 25
deep-audited repos and cross-checked against the finished `pattern-catalog.md`.
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

## Cluster 6 — General-purpose multi-agent orchestration SDKs (repo-level, run after Stage -2.4)
```
Capability: A general-purpose framework for building/composing/orchestrating LLM agents (handoffs, tool-calling, structured output, state) — relevant to DOM-01, DOM-02, DOM-06
Candidates: REPO-002 (langchain-ai/langgraph), REPO-003 (openai/openai-agents-python), REPO-004 (pydantic/pydantic-ai), REPO-005 (google/adk-python)
Shared Coverage: All four are independently-built, actively-maintained, officially-backed (or de-facto standard) general-purpose agent-orchestration SDKs; all four were deep-audited in Cluster A specifically as comparison baselines for Hermes' fixed base architecture (REPO-001), not as adoption candidates in their own right, since Hermes' architecture is already fixed per Owner disclosure. All four converge on schema-enforced output as the answer to reliable structured output (pattern-catalog.md PAT-003) — three of the four (openai-agents-python, adk-python, pydantic-ai) independently implement it; langgraph's channel/state-schema model addresses a related but distinct concern (state-passing, not output validation per se).
Unique Coverage: langgraph (REPO-002) uniquely contributes the general-purpose `interrupt()`/`Command` pause-resume primitive (PAT-004) and graph/DAG-based composition. openai-agents-python (REPO-003) uniquely contributes the explicit handoff-vs-agent-as-tool composition distinction with history compression (PAT-002). pydantic-ai (REPO-004) is the load-bearing source for schema-enforced-output-with-retry (PAT-003) — the cleanest, most-inspected implementation of that mechanism. adk-python (REPO-005) uniquely contributes the most richly-engineered MCP client integration found in this research (PAT-006, session-lifecycle-aware wrapper) and a dedicated tool-confirmation gate (part of PAT-004).
Conflicts: None — each occupies a genuinely different point of technical emphasis within the same broad capability space; no two make contradictory architectural claims.
Canonical Candidate: N/A — this cluster is intentionally NOT resolved to one canonical pick, for a different reason than Cluster 2's pipeline-stage logic: none of these four is being evaluated for adoption as infrastructure at all (Hermes' base architecture, REPO-001, is already fixed per Owner disclosure — see research-domains.md Known Base Architecture section). All four exist in the catalog purely as **comparison baselines**, each contributing a distinct pattern to the catalog (PAT-002/003/004/006) rather than competing for a single "best framework" slot. Forcing a canonical pick here would misrepresent their actual role in this research.
Secondary References: All four remain independent audit files (repo-audits/langchain-ai-langgraph.md, openai-openai-agents-python.md, pydantic-pydantic-ai.md, google-adk-python.md) and independent pattern contributions — no redundancy to fold away.
Rejected Redundancy: None.
```

## Cluster 7 — Narrative/multi-modal content-generation pipelines (repo-level)
```
Capability: Generating a sequence of narrative content (comic panels, story scenes, illustrated/video content) across multiple generation steps while maintaining character/style consistency — relevant to DOM-03, DOM-20
Candidates: REPO-029 (GOAT-AI-lab/GOAT-Storytelling-Agent), REPO-030 (HKUDS/ViMax), REPO-031 (ChrisChen667788/wind-comic)
Shared Coverage: All three solve the same underlying two-part problem — sequential narrative generation, and keeping generated visual/textual content consistent across that sequence — via three genuinely different engineering maturity levels and mechanisms, making this a real spectrum rather than three interchangeable implementations.
Unique Coverage: GOAT-Storytelling-Agent (REPO-029) is the simplest baseline — fixed-window literal-text scene carryover (PAT-044), no schema enforcement, no checkpointing; useful only as a lower bound, and independently confirmed stale (9+ months, a maintenance-signal downgrade from Stage -2.3's "active" characterization). ViMax (REPO-030) is the most architecturally elaborate — a 13-module schema-contracted pipeline (PAT-042) with a dedicated static/dynamic character-feature-separation extraction step (PAT-041), the strongest reliability engineering of the three (25 targeted regression-test files). wind-comic (REPO-031) uniquely contributes a post-hoc verification mechanism — the dual-threshold vision-LLM consistency audit (PAT-043) — that is complementary to, not competing with, ViMax's at-generation-time approach (PAT-041 aims for consistency by construction; PAT-043 verifies after the fact). wind-comic's Director-agent coordination role (`types/agents.ts`) also remains an unresolved cross-cluster flag to DOM-01 (see pattern-catalog.md's Cluster E Unresolved Cross-References).
Conflicts: None — the three are complementary points on a maturity/approach spectrum (naive baseline / elaborate schema-first pipeline / post-hoc verification), not contradictory designs.
Canonical Candidate: REPO-030 (ViMax) — highest architectural quality and evidence depth (schema-enforced outputs throughout, dedicated regression-test suite, 13 well-specified modules vs. GOAT's single unstructured script), per the ordered selection criteria. Its README's "4-agent" framing was independently corrected during audit to the real ~13-module structure — a case where the corrected finding still favors this repo as canonical, not against it.
Secondary References: REPO-031 (wind-comic, for its complementary post-verification mechanism, PAT-043 — a genuinely distinct pipeline stage ViMax does not have, not redundant with it) and REPO-029 (GOAT-Storytelling-Agent, kept only as the documented lower-bound baseline, PAT-044, explicitly not recommended as a default).
Rejected Redundancy: None — all three retain distinct value as noted; this is a "canonical + secondary references" resolution, consistent with Cluster 1's pattern.
```

## Cluster 8 — Social-media publish-mechanics platforms (repo-level)
```
Capability: Managing the actual mechanics of publishing content to external social platforms — retry/rollback safety, approval-workflow staging — relevant to DOM-21, DOM-07
Candidates: REPO-036 (gitroomhq/postiz-app), REPO-037 (brightbeanxyz/brightbean-studio)
Shared Coverage: Both independently arrived at the same core reversibility-differentiated retry design (pattern-catalog.md PAT-035, this project's strongest convergent-evidence finding in the whole social-media-operations domain) — safely-retryable operations get bounded retries, irreversible publish mutations get effectively zero retries and are treated as "outcome unknown" on timeout rather than retried. Both are AGPL-3.0 licensed (a real, confirmed constraint on direct code reuse for either).
Unique Coverage: postiz-app (REPO-036) implements this via a distributed workflow engine (Temporal) with four differentiated activity-proxy retry policies — the more architecturally sophisticated of the two, but with a confirmed zero-test-coverage gap (0 `.spec.ts`/`.test.ts` files) despite that sophistication. brightbean-studio (REPO-037) implements the same underlying design via a simpler single-process Django/DB-flag mechanism (`RETRY_BACKOFF`/`MAX_RETRIES`/`_fail_permanently()`), and uniquely contributes a test-covered configurable multi-stage human-approval workflow (PAT-040, `TwoStageFlowTests`) that postiz-app's audit did not find an equivalent of.
Conflicts: None — genuinely convergent designs solving the same problem two structurally unrelated ways, which is itself the notable finding (see PAT-035's Strengths field).
Canonical Candidate: N/A for the shared retry-policy capability specifically — per Section 11.2.3's ordering (evidence depth first), postiz-app's design is architecturally richer but has a real evidence-quality gap (zero tests) that brightbean-studio's simpler design does not share (test-covered, per PAT-040's evidence). Rather than force a single canonical pick against genuinely offsetting strengths, both are retained as co-primary sources for PAT-035, consistent with how that pattern record already cites both jointly.
Secondary References: brightbean-studio (REPO-037) is additionally the sole source for PAT-040 (multi-stage approval), a capability postiz-app does not appear to have an equivalent of within this audit's scope.
Rejected Redundancy: None.
```

## Cluster 9 — Human-control/governance-policy frameworks (repo-level)
```
Capability: A structural (code-level, not prompt-level) mechanism for intercepting and gating agent tool-calls/actions against a declared policy, with a human-approval escalation path — relevant to DOM-07, DOM-08
Candidates: REPO-010 (microsoft/agent-governance-toolkit), REPO-011 (humanlayer/humanlayer), REPO-012 (agentward-ai/agentward)
Shared Coverage: All three implement the same core structural pre-execution interception concept (pattern-catalog.md PAT-010) — a wrapper/proxy sits between the agent and the actual tool-call boundary, evaluating a declarative policy before the call proceeds, not after. agent-governance-toolkit and humanlayer additionally share the approval-coordinator-as-execution-parameter design (PAT-011) — an actual persisted, API-exposed pending-approval object the call blocks on, not a fire-and-forget notification.
Unique Coverage: agent-governance-toolkit (REPO-010) is the only one of the three with a demonstrated time-bounded auto-expiring privilege-elevation mechanism (PAT-012, ring-based, trust-score-gated) — though this finding is scoped to one sub-project of an otherwise-uneven monorepo, a caveat carried through to PAT-012's own record. humanlayer (REPO-011) has the most concretely-verified approval-coordinator implementation of the three (direct Go-daemon test coverage: `manager_test.go`, `daemon_approval_integration_test.go`, `sqlite_approval_test.go`) but the humanlayer/humanlayer project itself is self-declared deprecated — the mechanism is sound evidence, the specific codebase is not an adoptable dependency. agentward (REPO-012) uniquely contributes the explicit coverage-gap self-reporting refinement (PAT-013, the `△ GAP` signal) and sequence-aware multi-call chain evaluation (PAT-014) — both real extensions beyond simple per-call allow/deny — but carries its own adoption frictions independent of mechanism quality (stale maintenance signal as of audit, Business Source License 1.1 restricting commercial reuse until 2028-04-24).
Conflicts: None — the three converge on the same base mechanism (structural interception) while each contributing genuinely distinct refinements on top of it; no contradictory design claims.
Canonical Candidate: N/A — deliberately not resolved to one canonical pick, for the same reason as Cluster 6: none of the three is being evaluated as adoptable infrastructure as-is (agent-mesh's monorepo unevenness, humanlayer's deprecation, and agentward's license/staleness each independently rule out wholesale adoption per their own pattern records' Weaknesses fields). All three exist in the catalog as comparison/pattern sources, each contributing distinct, non-redundant mechanism refinements (PAT-010/011 shared; PAT-012 unique to REPO-010; PAT-013/014 unique to REPO-012) rather than competing for a single "best governance framework" slot.
Secondary References: All three remain independent audit files and independent pattern contributions — no redundancy to fold away, consistent with Cluster 6's reasoning.
Rejected Redundancy: None.
```

## Considered but not clustered — noted for transparency

**REPO-033 (digital-marketing-pro) vs. REPO-034 (ALwrity)**: both are marketing/content-creation toolkits and were considered for a dedup cluster, but their actual capability surfaces diverge enough on direct inspection that forcing a cluster would misrepresent them — digital-marketing-pro's differentiated strength is real fetch-then-synthesize competitive research (PAT-036, the domain's strongest finding); ALwrity's audit did not surface an equivalent competitive-research mechanism, and no second pattern record was extracted from it in Cluster E's pass. Not clustered; each remains an independent record.

---

## Coverage Note

Per Section 11.3, every capability cluster with >=2 candidates is covered above.
Skills not appearing in any cluster (SKL-001 through SKL-007, SKL-011, SKL-014,
SKL-017 through SKL-020, SKL-023, SKL-026, SKL-029, SKL-030) had no second candidate
addressing the same capability surface within this stage's inspected sample and are
therefore singleton records in `skill-catalog.md`, not omissions from this map.
