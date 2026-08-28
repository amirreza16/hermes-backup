# Hermes Phase -2 Pattern Catalog
Revision: 1 | Updated: 2026-08-28 | Stage: -2.5 (Pattern Extraction)

Per Master Plan Section 8, this catalog is organized by **mechanism**, not by
source repository/skill. Every pattern below was extracted from the 26
Stage -2.4 deep-audit files and/or the 32 Stage -2.2 skill records, cross-
checked against the Section 8 example pattern-category list. Schema: Section
9.4. IDs are final (`PAT-001`...`PAT-051`), assigned during this merge from
six cluster-scoped raw extraction passes (Cluster A-F, matching the Stage
-2.3 domain-cluster structure). Every STRONG CANDIDATE pattern carries a
completed Adversarial Review (Section 13, Q1-Q7) and Role Notes from at
least Repository/Skill Auditor + Reliability Reviewer + Skeptic (Section 14),
with disagreements preserved rather than averaged away. Every pattern,
regardless of rating, has Failure Modes and Human-Control Implications
populated (Stage -2.5 exit criterion / Gate G5).

**Process note:** This is a full redo of Stage -2.5 after a first attempt
(2026-08-25) lost all 44 of its records to a persistence failure — see
`HERMES_RESEARCH.md` Session 7 and `AGENT-OPERATIONS.md`'s write-before-return
rule. This catalog was produced by six parallel forks, each writing its
cluster's records to a scratch file before returning, per that rule.

---

## Summary Table

| PAT-ID | Name | Cluster | Domains | Recommendation | Confidence |
|---|---|---|---|---|---|
| PAT-001 | Narrow-Waist Core + Plugin/Skill Edges | A | DOM-01/04/06 | STRONG CANDIDATE | 75 |
| PAT-002 | Handoff-vs-Agents-as-Tools Composition + History Compression | A | DOM-01/02 | CANDIDATE | 65 |
| PAT-003 | Schema-Enforced Output With Retry-Until-Valid Loop | A | DOM-02/01 | STRONG CANDIDATE | 85 |
| PAT-004 | Pause-and-Resume Execution Primitive for HITL | A | DOM-01/02/07/09 | STRONG CANDIDATE | 70 |
| PAT-005 | Progressive-Disclosure Skill Packaging (SKILL.md + Validation Gate) | A | DOM-04/01/06 | STRONG CANDIDATE | 70 |
| PAT-006 | Session-Lifecycle-Aware MCP Client Wrapper | A | DOM-06/01 | STRONG CANDIDATE | 70 |
| PAT-007 | Explicit 4-Section Agent Contract Prompt + Typed I/O + Test Checklist | A | DOM-02 | CANDIDATE | 55 |
| PAT-008 | Structured-Adversarial-Synthesis for Rare, High-Stakes Decisions | A | DOM-02/15 | CONTEXT-DEPENDENT | 60 |
| PAT-009 | When-to-Use-MCP Decision Tree + Security-Hardening Sequence | A | DOM-06 | CANDIDATE | 45 |
| PAT-010 | Structural Pre-Execution Policy Gate (govern()/proxy interception) | B | DOM-08/05 | STRONG CANDIDATE | 78 |
| PAT-011 | Approval-Coordinator as First-Class Execution Parameter (maker-checker) | B | DOM-07 | STRONG CANDIDATE | 74 |
| PAT-012 | Time-Bounded Auto-Expiring Privilege Elevation | B | DOM-08 | CANDIDATE | 55 |
| PAT-013 | Explicit Coverage-Gap Self-Reporting (△ GAP) | B | DOM-08 | CANDIDATE | 58 |
| PAT-014 | Sequence-Aware Tool-Call Chain Evaluation | B | DOM-08 | CANDIDATE | 48 |
| PAT-015 | Confidence-Threshold-to-Handler Escalation Pipeline | B | DOM-10/16 | CANDIDATE | 55 |
| PAT-016 | Multi-Factor Risk/Ambiguity Gate, Assess-Before-Generate + Rolling-History | B | DOM-09/07 | STRONG CANDIDATE | 68 |
| PAT-017 | Gate Format Calibrated to Task Novelty (DO-CONFIRM/READ-DO) + Killer-Item Checklists | B | DOM-07/15 | STRONG CANDIDATE | 72 |
| PAT-018 | Urgency-Tiered Owner-Notification Escalation | B | DOM-10/14 | CANDIDATE | 50 |
| PAT-019 | Authoritative Event Log + Disposable Derived Projection | C | DOM-11/13 | CANDIDATE | 70 |
| PAT-020 | Per-Subsystem Staged Write-Approval Gate | C | DOM-07/11 | CANDIDATE | 75 |
| PAT-021 | Time-Gated Auto-Deletion of Session/Transcript/Log History | C | DOM-11 | AVOID | 90 |
| PAT-022 | Bi-Temporal Fact Invalidation over Destructive Update | C | DOM-11/12 | STRONG CANDIDATE | 72 |
| PAT-023 | DAG-Scheduled Task Execution with Wired Hard Budget-Abort | C | DOM-13/16 | STRONG CANDIDATE | 65 |
| PAT-024 | WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed Agent State | C | DOM-13 | CONTEXT-DEPENDENT | 80 |
| PAT-025 | Urgency-Tiered Human-Facing Status Digest | C | DOM-14/10 | CANDIDATE | 55 |
| PAT-026 | Pre-Call Blocking Budget Enforcement | D | DOM-16 | STRONG CANDIDATE | 85 |
| PAT-027 | Task-Classified Multi-Strategy Cost-Aware Model Routing | D | DOM-16 | STRONG CANDIDATE | 75 |
| PAT-028 | Reported-Only Cost Tracking (gap pattern) | D | DOM-16 | INSUFFICIENT EVIDENCE | 40 |
| PAT-029 | Composable Cost-Governance Pipeline (Capture->Enforce->Route->Verify) | D | DOM-16 | CANDIDATE | 55 |
| PAT-030 | Dependency-Aggregation Guardrail Architecture (Flow-DSL over Specialized Detectors) | D | DOM-17 | STRONG CANDIDATE | 70 |
| PAT-031 | Advisory Critique-Before-Decision (Non-Blocking Structured Review) | D | DOM-15 | CONTEXT-DEPENDENT | 75 |
| PAT-032 | Entropy-Threshold Secret Detection | D | DOM-17 | CANDIDATE | 55 |
| PAT-033 | Structured HITL Brief With Typed Multi-Action Response (Edit/Rewrite/Accept/Reject) | E | DOM-07/21/09/19/20 | STRONG CANDIDATE | 85 |
| PAT-034 | Decomposed-Subgraph Content Pipeline With Degrade-Not-Fail Fallback | E | DOM-03/20/01 | CANDIDATE | 65 |
| PAT-035 | Reversibility-Differentiated Retry/No-Retry Publish Policy | E | DOM-21/07 | STRONG CANDIDATE | 88 |
| PAT-036 | Fetch-Then-Tag Competitive/Audience Research Synthesis | E | DOM-18/19/05/07 | STRONG CANDIDATE | 82 |
| PAT-037 | Brand-Isolated Storage Path Convention | E | DOM-24/19 | CANDIDATE | 60 |
| PAT-038 | Snapshot-vs-Monitoring Dual-Mode Research Agent | E | DOM-18/19 | CANDIDATE | 55 |
| PAT-039 | Prompt-Level-Only Behavior Rules Without Structural Enforcement (risk pattern) | E | DOM-05/07 | CONTEXT-DEPENDENT | 65 |
| PAT-040 | Configurable Multi-Stage Human-Approval Workflow | E | DOM-07/21 | CANDIDATE | 45 |
| PAT-041 | Static/Dynamic Character-Feature Separation for Cross-Scene Consistency | E | DOM-20 | STRONG CANDIDATE | 78 |
| PAT-042 | Fine-Grained Specialized Pipeline With Per-Module Schema Contracts | E | DOM-20/03/01 | CANDIDATE | 68 |
| PAT-043 | Dual-Threshold Vision-LLM Consistency Audit (hard-regen/soft-warn, fail-open) | E | DOM-20 | STRONG CANDIDATE | 80 |
| PAT-044 | Fixed-Window Literal-Text Scene-Carryover Baseline | E | DOM-03 | CONTEXT-DEPENDENT | 70 |
| PAT-045 | Skill-Invocation Quality Index Retargeted Toward Content-Performance (gap pattern) | E | DOM-22 | INSUFFICIENT EVIDENCE | 30 |
| PAT-046 | Profile-Based Tenant Isolation (whole-instance boundary) | F | DOM-24/08 | CANDIDATE | 85 |
| PAT-047 | Automatic Per-Context Memory Scoping (`context_id` routing) | F | DOM-24/08 | STRONG CANDIDATE | 80 |
| PAT-048 | Three-Layer Deployment Separation (Image/Scaffolding/Artefact) | F | DOM-24/05/07/11 | STRONG CANDIDATE | 75 |
| PAT-049 | Hardened-Fork-as-Default-Deployment-Target | F | DOM-24 | CANDIDATE | 70 |
| PAT-050 | Thin-Fork Weekly-Rebase Maintenance Discipline | F | DOM-24 | CANDIDATE | 70 |
| PAT-051 | Cost-Tracking-Without-Confirmed-Enforcement (gap pattern) | F | DOM-16 | INSUFFICIENT EVIDENCE | N/A |

**Distribution:** 51 records. 21 STRONG CANDIDATE, 21 CANDIDATE, 5
CONTEXT-DEPENDENT, 1 AVOID, 3 INSUFFICIENT EVIDENCE. All 3 INSUFFICIENT
EVIDENCE records (PAT-028, PAT-045, PAT-051) are deliberate gap-documentation
records, not weak candidates forced to fill a slot — see "Documented Gaps"
below.

---

## Cluster A — Core Agent Architecture (DOM-01, 02, 04, 06)

Sources read in full: repo-audits/{nousresearch-hermes-agent, hermes-agent-capability-reference,
langchain-ai-langgraph, openai-openai-agents-python, pydantic-pydantic-ai, google-adk-python,
modelcontextprotocol-servers}.md; skill-catalog.md records SKL-001, SKL-007, SKL-009, SKL-013,
SKL-020, SKL-021, SKL-024; research-domains.md DOM-01/02/04/06 definitions.

### PAT-001

Pattern Name: Narrow-Waist Core + Plugin/Skill Edges (Extensibility Architecture)
Problem Solved: How to let a single agent core grow large amounts of capability
(memory backends, skills, tools, scheduling) over time without the core itself
becoming an unmaintainable monolith or every new capability requiring a core change.
Observed In: REPO-001 (nousresearch-hermes-agent, deep-audited, high confidence)
Mechanism: A deliberately small, stable core (`agent/` — single-purpose modules like
`context_engine.py`, `tool_executor.py`) that exposes defined extension points; new
capability is required to arrive as a CLI command + skill, a service-gated tool, or a
plugin (`plugins/` tree — 8 independent memory backends alone) — never as new core
surface. Stated explicitly as design philosophy in `AGENTS.md` and corroborated by the
actual module layout, not just asserted.
Required Conditions: A stable core team/owner willing to enforce the boundary
(nothing structurally prevents a contributor from adding core surface instead of a
plugin — this is a discipline, not a compiler-enforced constraint); a real plugin/skill
loading mechanism.
Strengths: Keeps the core auditable as capability grows; isolates blast radius of a
bad plugin/skill from the core; matches Hermes' own two-fixed-role shape (the core
doesn't need to know about "content agent" vs "research agent" specifics if those
differences live in skills/plugins layered on top).
Weaknesses: The boundary is a documented convention, not a structurally enforced one
— nothing in the audit found a lint/CI check that rejects a PR for adding core surface
instead of a plugin. Discipline can erode over time without enforcement.
Failure Modes: Core scope creep if the convention isn't actively defended in code
review; a plugin with elevated access (e.g. a memory backend) can still cause
core-level damage if the plugin boundary itself isn't sandboxed (not verified either
way this pass).
Complexity: Low to adopt as a philosophy; Medium to defend over time (process
discipline, not a one-time engineering cost).
Token/Cost Implications: Neutral/positive — a smaller core means less system-prompt
and less code to load/reason about for any given task; plugins/skills can be loaded
selectively rather than the whole system context inflating with every added
capability.
Human-Control Implications: Indirect but real — a narrow core makes it easier for a
human (or Hermes' own approval layer) to reason about what the "trusted" surface is
versus what runs at reduced trust in a plugin/skill sandbox, which is a prerequisite
for any later least-privilege work (DOM-08).
Hermes Relevance: DOM-01 (this is hermes-agent's actual orchestration substrate —
Hermes inherits it, does not choose it); DOM-04 (this is the mechanism skills load
into); DOM-06 (tools are one of the three sanctioned extension surfaces).
Alternative Patterns: None observed as a direct alternative in this cluster — the
comparison frameworks (langgraph, openai-agents-python, adk-python) are orchestration
libraries, not "core vs. plugin" extensibility philosophies; not a fair apples-to-apples
alternative.
Recommendation: STRONG CANDIDATE
Confidence: 75
Evidence: `AGENTS.md` design-philosophy statement, cross-checked against ~40+ single-purpose
`agent/` modules and the 8-backend `plugins/memory/` tree (repo-audits/nousresearch-hermes-agent.md,
Dimension A, FACT-labeled).

Adversarial Review (Section 13):
Q1 (assumptions): Assumes whoever operates/extends Hermes on this substrate actually
respects the CLI-command/skill/plugin boundary; assumes the plugin loading mechanism
itself doesn't silently grant plugins core-equivalent trust.
Q2 (failure for Hermes): If Hermes' own two-role design gets built as ad hoc core
changes instead of skills/plugins (easy to do under deadline pressure), the narrow-waist
benefit is lost entirely and Hermes inherits a monolith anyway — the pattern doesn't
protect against this on its own.
Q3 (complexity introduced): Low direct complexity — it's an architectural discipline,
not new infrastructure to build.
Q4 (lock-in): This is inherited, not chosen (REPO-001 is the fixed base architecture)
— lock-in framing doesn't apply the normal way; the relevant question is whether
deviating from the philosophy later (adding Hermes-specific core surface) is costly to
reverse, which is UNKNOWN without a concrete attempt.
Q5 (evidence missing): No evidence this pass on whether the plugin loading mechanism
enforces any sandboxing/permission boundary between plugin and core at runtime, or if
"plugin vs core" is purely an authoring-time convention with equal runtime trust.
Q6 (simpler competing approach): A monolithic single-file agent is simpler to reason
about at small scale but does not survive Hermes' stated ambition ("multiple pages,
ecosystem intelligence, self-maintenance") — the narrow-waist tradeoff is justified by
Hermes' own stated scale ambitions, not a default preference.
Q7 (marketing vs. engineering): Real engineering — the module layout and plugin count
corroborate the stated philosophy; not just an `AGENTS.md` claim.
Reasoning Summary: Rated STRONG CANDIDATE primarily because it is not really a choice
— it is the actual, deep-audited, high-confidence shape of the fixed base architecture
Hermes will build on. The adversarial review's main finding (Q1/Q5) is that the
boundary is a convention, not a runtime-enforced guarantee — worth carrying into DOM-08
(least-privilege) research rather than assuming the plugin/core split implies a trust
boundary.

Role Notes (Section 14):
- Repository Auditor: Confirmed directly from `AGENTS.md` text plus
  independent module-count/plugin-count inspection in the underlying audit file — this
  is not a documentation-only claim, the module layout matches. Verdict: Strong.
- Reliability Reviewer: The pattern says nothing about what happens when a
  plugin fails or misbehaves (crash isolation, timeout, resource caps) — the audit
  found real crash-safety engineering elsewhere in hermes-agent (Dimension D, WAL
  handling) but not specifically at the plugin boundary. Flag as an open reliability
  question, not a confirmed gap.
- Skeptic: Attempted rejection — "this is just normal modular software
  design, not a distinctive pattern worth a STRONG rating." Counter: the distinctive
  part isn't modularity in the abstract, it's the explicit, documented, three-way-only
  extension contract (CLI+skill / service-gated tool / plugin) with no fourth path —
  that specificity is what's reusable as a rule Hermes can adopt verbatim, not just
  "write modular code." Rejection does not succeed, but the Skeptic's framing (don't
  over-credit ordinary modularity) is preserved as a calibration note for Stage -2.6.

---

### PAT-002

Pattern Name: Handoff-vs-Agents-as-Tools Composition With History Compression
Problem Solved: How multiple agents combine work — transferring full control of a
conversation to another agent (handoff) vs. calling another agent as a bounded
function without giving up control (agent-as-tool) — and how to avoid blowing up
context size when a handoff carries the full prior conversation forward.
Observed In: REPO-003 (openai-openai-agents-python, deep-audited, high confidence);
comparison: REPO-002 (langchain-ai-langgraph, channel/state-schema composition, no
equivalent named handoff-vs-tool distinction); REPO-001 (nousresearch-hermes-agent) has
neither — delegation is a session/parent-child marker, not a typed handoff or
agent-as-tool call.
Mechanism: Two explicitly separate, independently implemented composition primitives:
`handoff()` (transfers the whole conversation to another agent) and calling an agent as
a tool (bounded, no control transfer). A `HandoffInputData`/history-compression layer
(`handoffs/history.py`) lets a handoff pass a *summarized* view of prior conversation
instead of the raw transcript, configurable per handoff.
Required Conditions: A framework or hand-built layer that can distinguish "this
message needs to run in the other agent's full context" from "this is a bounded
subtask" at the call site; a summarization/compression step if avoiding raw-transcript
forwarding matters at Hermes' scale.
Strengths: Clean separation of two genuinely different use cases (Hermes' own
content-agent <-> research-agent split plausibly needs both: research-agent
handing off a fully-formed brief to content-agent looks like a handoff; content-agent
asking research-agent one narrow fact-check looks like agent-as-tool); the
history-compression option directly addresses token/cost growth across repeated
handoffs.
Weaknesses: Framework-specific vocabulary and machinery (`Handoff` class,
`HandoffInputData`) — not present in REPO-001, so this would need to be built as a
Hermes-specific layer on top of hermes-agent's own delegation mechanism rather than
imported.
Failure Modes: If the two composition modes aren't kept genuinely distinct in Hermes'
implementation (e.g. every research-agent call is treated as a full handoff "just in
case"), the benefit collapses into the same undifferentiated-context-growth problem
the pattern exists to solve; a history-compression/summarization step is itself a
lossy operation and could drop information the receiving agent actually needed —
untested failure mode, not observed either way in the audit.
Complexity: Medium — building an equivalent layer on hermes-agent's substrate is real
design/implementation work, not a config flag.
Token/Cost Implications: Directly cost-relevant — the explicit reason
history-compression exists is to avoid forwarding an ever-growing raw transcript
across every agent-to-agent call, which is a real DOM-16 (cost control) lever if
Hermes' two agents call each other frequently.
Human-Control Implications: Indirect — cleaner agent-to-agent boundaries make it
easier to insert a human approval point at a well-defined handoff moment (e.g. gate
"research-agent hands off to content-agent" specifically) rather than needing to
intercept an undifferentiated stream of subagent calls.
Hermes Relevance: DOM-01 (composition shape for the two-role design), DOM-02 (this is
literally what a typed handoff contract looks like when built with real engineering
depth, per the audit finding that this SDK's history-compression mechanism exceeded
what the Stage -2.3 triage record anticipated).
Alternative Patterns: PAT-003 (schema-enforced output validation) is complementary, not
competing — PAT-002 is about *when/how* control transfers, PAT-003 is about *what shape* the
data crossing that boundary must take.
Recommendation: CANDIDATE
Confidence: 65
Evidence: `src/agents/handoffs/__init__.py` (`class Handoff`, `def handoff(...)`,
4 call-signature overloads) and `handoffs/history.py`
(`nest_handoff_history`/summary-mapper), both confirmed present and tested
(`tests/test_guardrails.py` family) per repo-audits/openai-openai-agents-python.md
Dimension B/I.

Reasoning for CANDIDATE (not STRONG): only one deep-audited source implements this
exact handoff-vs-tool-call distinction with named machinery (openai-agents-python);
langgraph's channel/state-schema composition is a related but materially different
mechanism (state-passing between graph nodes, not an explicit two-primitive
distinction), so the ">=2 independent sources" bar is not comfortably met for the
specific mechanism as described, and REPO-001 (the one source that would matter most)
has no equivalent at all — this is a gap-filling comparison idea for Hermes to
consider building, not a corroborated cross-source pattern.

---

### PAT-003

Pattern Name: Schema-Enforced Output With Retry-Until-Valid Loop
Problem Solved: Getting an agent's output to reliably conform to a required structure
(so a downstream agent, tool, or human-approval step can consume it without ad hoc
parsing/guessing) rather than hoping the model happens to comply.
Observed In: REPO-004 (pydantic-pydantic-ai, deep-audited, high confidence — the
load-bearing finding of that entire audit); REPO-005 (google-adk-python, deep-audited,
`output_schema` field with an explicit runtime validation call, high confidence);
REPO-003 (openai-openai-agents-python, deep-audited, `output_type` with a runtime type
check, high confidence). Three independent deep-audited sources, all converging on the
same mechanism shape. REPO-001 (nousresearch-hermes-agent) was searched for an
equivalent by the reframing question DOM-02 poses and **none was found** — no
schema-enforced-output/typed-contract abstraction exists in hermes-agent; this is a
confirmed, direct gap between what Hermes' fixed base architecture provides and what
DOM-02 needs.
Mechanism: Output is validated against a declared schema immediately after generation;
on validation failure, instead of silently accepting malformed output or hard-failing
once, the framework raises a typed retry signal (pydantic-ai's `ModelRetry` /
`ValidationError` handling) that triggers a re-prompt to the model, up to a configurable
retry limit. This is "enforced-or-retried-until-exhausted," not "suggested and hoped
for."
Required Conditions: A validation library/schema system (Pydantic-style or
equivalent); a runtime willing to spend an extra model call on a retry rather than
failing fast — a real cost/latency tradeoff, not free.
Strengths: Directly, code-confirmed (not just documented) solves DOM-02's exact stated
research question ("enforced or merely suggested?") with a materially stronger answer
than a framework that just asks the model to "please output JSON." Converging
evidence across three independently-built frameworks (OpenAI's own SDK, Google's ADK,
and the Pydantic ecosystem) is unusually strong corroboration that this is a settled,
non-controversial best practice, not one team's idiosyncratic choice.
Weaknesses: Retry-on-failure means variable latency and variable cost per call — a
content-agent -> research-agent handoff that repeatedly fails validation could silently
inflate cost (ties directly to DOM-16). None of the three audits inspected what happens
when `max_retries` is exhausted (crash? fallback? surface to human?) — flagged as
UNKNOWN, not assumed benign.
Failure Modes: Retry-storm cost blowup if the schema is miscalibrated against what the
model can reliably produce; silent behavior at retry-exhaustion if not explicitly
handled (UNKNOWN across all three sources at this audit depth — a real open question,
not resolved this pass).
Complexity: Low-Medium — this is a well-trodden, narrowly-scoped mechanism (a
validation library + a retry wrapper), not a large subsystem.
Token/Cost Implications: Directly cost-relevant, both ways — prevents *downstream*
cost waste from consuming malformed data, but *itself* costs extra tokens on every
retry; net effect depends on how often validation actually fails in practice, not
measured in any of the three audits.
Human-Control Implications: Makes a human approval gate more trustworthy — a human (or
an automated approval check) reviewing a research-agent's handoff to a content-agent
can rely on the handoff's shape being correct, reducing the chance a malformed artifact
silently reaches a publish-adjacent step.
Hermes Relevance: DOM-02 (direct, primary — this is the single clearest evidenced
answer to DOM-02's exact research question) and DOM-01 (a contract this reliable is a
precondition for a clean two-role handoff, per PAT-002 above).
Alternative Patterns: PAT-002 (handoff/history-compression) — complementary, not
competing, as noted there.
Recommendation: STRONG CANDIDATE
Confidence: 85
Evidence: `pydantic_ai_slim/pydantic_ai/_output.py` (`class OutputValidator`,
`ModelRetry`/`ValidationError` handling, `max_retries`); `src/google/adk/agents/llm_agent.py`
(`output_schema` field + explicit `validate_schema()` call + a guarded misconfiguration
error path); `src/agents/agent.py` (`output_type` field with runtime type check) —
all FACT-labeled, source-line-cited in their respective repo-audits/*.md files.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes the model can eventually produce valid output within
`max_retries` — for a genuinely hard/ambiguous schema this may not hold, and none of
the three sources document what the fallback behavior is at exhaustion.
Q2 (failure for Hermes): If Hermes adopts this pattern but doesn't explicitly decide
what happens at retry-exhaustion (silent failure? escalate to human? drop the turn?),
it could violate the "stop and ask under ambiguity" principle by defaulting to
whatever the underlying library does unexamined.
Q3 (complexity introduced): Low-Medium, as above — genuinely one of the cheaper
patterns in this cluster to adopt.
Q4 (lock-in): Low if built as a thin validation+retry wrapper; higher if Hermes adopts
a specific framework's exact class hierarchy wholesale rather than the general
mechanism.
Q5 (evidence missing): No source in this pass measured real-world retry-failure rates
or cost impact in production — all three findings are code-structure evidence
(the mechanism exists and is real), not production-outcome evidence (how often it's
actually needed).
Q6 (simpler competing approach): A single-shot "ask nicely for JSON, parse leniently"
approach is simpler and cheaper per-call but reintroduces exactly the unreliability
DOM-02 was raised to solve — not a real competitor for Hermes' stated needs, only for
low-stakes use cases Hermes doesn't have.
Q7 (marketing vs. engineering): Real engineering, confirmed at the source-code level
in all three cases, including one case (pydantic-ai) where the audit explicitly
converted a documentation-level design-philosophy claim into a code-verified FACT.
Reasoning Summary: The single best-evidenced pattern in this cluster — three
independent, deep-audited, high-confidence sources converge on the same mechanism,
and it directly answers a HIGH-priority Hermes research question (DOM-02) with a
confirmed gap in the fixed base architecture (REPO-001 has nothing equivalent). The
open question (retry-exhaustion behavior) is a real gap in the *evidence*, not a
reason to downgrade the pattern's recommendation strength — it is logged as a Stage
-2.6/-2.7 follow-up instead.

Role Notes (Section 14):
- Repository Auditor: All three citations are specific file/line/class
  references independently confirmed in their audit files, not paraphrased from
  README text — this is the strongest evidence chain of any pattern in this cluster.
  Verdict: Strong.
- Reliability Reviewer: The unexamined retry-exhaustion behavior is a
  real gap — a reliability reviewer would not sign off on adopting this pattern
  without first tracing what happens when `max_retries` is hit in whichever framework
  Hermes ends up building on. Verdict: Strong mechanism, incomplete reliability
  picture — recommend closing this specific gap before Stage -2.6 treats it as fully
  vetted.
- Skeptic: Attempted rejection — "three frameworks agreeing doesn't mean
  it's right for Hermes specifically, it might just mean it's an industry default
  that nobody has questioned." Counter: the pattern isn't recommended here because
  three frameworks agree in the abstract, it's recommended because it directly and
  specifically answers a Hermes research question (DOM-02) that was raised
  independently of this finding, and the fixed base architecture (REPO-001)
  demonstrably lacks it — the convergence is corroborating evidence for a
  independently-motivated need, not the sole justification. Rejection does not
  succeed.

---

### PAT-004

Pattern Name: Pause-and-Resume Execution Primitive for Human-in-the-Loop
Problem Solved: Stopping agent execution mid-task at a specific point to wait for a
human decision, then resuming (rather than the human only being able to intervene
before or after a run completes).
Observed In: REPO-002 (langchain-ai-langgraph, deep-audited, `interrupt()`/`Command`,
high confidence); REPO-005 (google-adk-python, deep-audited, `tool_confirmation.py`,
confirmed to exist as a dedicated file, internal trigger/resume logic not traced —
Moderate confidence on depth); REPO-001 (nousresearch-hermes-agent, deep-audited,
`write_approval.py` — a related but structurally different mechanism: a staged
pending-record gate for memory/skill writes specifically, not a general mid-execution
pause primitive, and off by default — see PAT-020 for the full extraction of this
mechanism from Cluster C's pass).
Mechanism: Three variants of the same underlying idea, at different levels of
generality: (1) langgraph's `interrupt(value)` raises a resumable exception mid-node,
surfaces a value to the caller, and resumes via `Command` — general-purpose, works at
any point in a graph; (2) adk-python's tool-confirmation gate — scoped specifically to
tool calls; (3) hermes-agent's write-approval gate — scoped specifically to
memory/skill writes, staged as pending JSON records rather than an in-process
pause/resume.
Required Conditions: An execution model that can actually suspend and later resume
state (checkpointing or an equivalent durability mechanism) for the general-purpose
variant; for the narrower write-approval-style variant, only a staging area and a
review UI/command are needed.
Strengths: This is directly, materially relevant to Hermes' explicit behavioral
principle ("explicit confirmation for irreversible actions") — three real,
independently-built implementations exist to study, at different scopes (whole-graph
vs. tool-call vs. write-specific), giving Hermes options rather than one rigid model.
Weaknesses: langgraph's variant has a documented, non-obvious gotcha — resuming
re-executes all logic from the start of the node, meaning any non-idempotent side
effect before the `interrupt()` call re-runs on resume (a real correctness risk if
Hermes adopts this shape carelessly). hermes-agent's variant is real but **off by
default** — a stock deployment writes memory/skills without any human gate at all
unless explicitly configured on, which the audit calls out as a recurring posture
across that codebase.
Failure Modes: Silent double-execution of a non-idempotent action on resume
(langgraph-style, confirmed in the framework's own docstring, not assumed); an
approval gate present in code but never actually activated at deployment time
(hermes-agent-style, confirmed default-off) — a "capability exists, protection
doesn't apply" failure mode distinct from the mechanism simply not existing.
Complexity: Medium (general-purpose pause/resume, like langgraph's) to Low (a staged
pending-review file, like hermes-agent's) depending on which variant is adopted.
Token/Cost Implications: A resumed-with-re-execution model (langgraph-style) can
double-spend tokens for any model-call-containing logic that sits before the
interrupt point in the same node — a real, non-obvious cost implication tied directly
to the correctness gotcha above.
Human-Control Implications: This pattern family *is* the human-control mechanism —
directly load-bearing for DOM-07/DOM-09. The critical finding is that having the
mechanism in the codebase is not the same as it protecting anything: hermes-agent
ships a real gate that is inert unless an operator turns it on.
Hermes Relevance: DOM-01/DOM-02 (this is an execution-control/composition-boundary
mechanism, hence tracked here); directly cross-references DOM-07 (approval gates, see
PAT-011/PAT-016/PAT-017) and DOM-09 (ambiguity escalation, PAT-016) in Cluster B.
Alternative Patterns: None found that solve the same problem without some form of
pause/resume or staged-review — the three variants are points on one spectrum, not
competing alternatives.
Recommendation: STRONG CANDIDATE
Confidence: 70
Evidence: `langgraph/types.py` `def interrupt(value)` docstring (re-execution
behavior, FACT); `src/google/adk/tools/tool_confirmation.py` (file existence
confirmed via grep, FACT; internal logic UNKNOWN); `tools/write_approval.py` (staged
pending records under `<HERMES_HOME>/pending/{memory,skills}/`, default-disabled
config flag, FACT) — all per their respective repo-audits/*.md files.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes Hermes will actually enable/enforce whichever variant it
adopts — the hermes-agent evidence specifically demonstrates this is not automatic.
Q2 (failure for Hermes): Adopting hermes-agent's write-approval mechanism as-is
without explicitly turning it on would silently fail to deliver Hermes' stated
"explicit confirmation for irreversible actions" principle — the single highest-risk
finding in this pattern.
Q3 (complexity introduced): Ranges Low (staged file review) to Medium (general
pause/resume with checkpointing) depending on variant chosen.
Q4 (lock-in): Low for the general concept; Medium if Hermes builds directly against
one framework's specific `interrupt()`/`Command` API rather than a portable
abstraction.
Q5 (evidence missing): adk-python's tool-confirmation internal trigger/resume logic
was not traced this pass — UNKNOWN whether it shares langgraph's re-execution gotcha
or avoids it; a real follow-up item before treating any one variant as safely
copyable.
Q6 (simpler competing approach): A synchronous "always ask before every tool call"
policy is simpler than any of these three mechanisms but does not scale to Hermes'
autonomy goals — these patterns exist specifically to allow selective, not blanket,
human gating.
Q7 (marketing vs. engineering): Real engineering in all three cases — none of this is
asserted only in docs; each has a corresponding, inspected code artifact.
Reasoning Summary: Rated STRONG CANDIDATE because the underlying need (pause for
human decision, then resume) is unambiguously central to Hermes' stated behavioral
principles and three independently-built, deep-audited implementations corroborate
that it's a solved, well-understood problem space — but the adversarial review's
central finding (hermes-agent's variant ships inert-by-default) is the single most
actionable, non-obvious risk surfaced in this entire cluster and must carry forward
as an explicit Stage -2.6 configuration requirement, not just a footnote.

Role Notes (Section 14):
- Repository Auditor: All three code artifacts independently confirmed
  present with specific file/line citations; adk-python's internal logic is the one
  genuine depth gap (existence confirmed, mechanism not traced). Verdict: Strong on
  existence across all three, Moderate on completeness for adk-python specifically.
- Reliability Reviewer: The langgraph re-execution-on-resume gotcha is a
  real, confirmed (not hypothetical) reliability risk that a naive adoption would
  walk straight into — this is exactly the kind of README-invisible detail Stage -2.4
  exists to surface, and it did. Verdict: Strong finding, must be an explicit design
  constraint if this variant is chosen.
- Skeptic: Attempted rejection — "hermes-agent's version being
  off-by-default isn't a flaw in the pattern, it's just a config default; don't
  penalize the pattern for how one implementation ships it." Counter: the pattern
  being rated STRONG is specifically about its value *for Hermes' stated principles*
  — and a mechanism that must be remembered to be turned on is a materially weaker
  guarantee than one that is structurally on, which is exactly the kind of
  scope-relevant caveat Section 13 exists to surface, not an unfair penalty.
  Rejection does not succeed, but its distinction (pattern quality vs. shipped
  default) is preserved in the Weaknesses/Failure Modes fields above rather than
  smoothed over.

---

### PAT-005

Pattern Name: Progressive-Disclosure Skill Packaging (SKILL.md + Validation Gate)
Problem Solved: Packaging a capability unit so an agent only loads the metadata it
needs to decide relevance, then the full instructions only when actually invoked,
instead of every capability's full content permanently inflating context.
Observed In: SKL-009 (Skill Architect, SomeClaudeSkills, doc-only, Medium evidence);
REPO-001 (nousresearch-hermes-agent, deep-audited, high confidence — native `skills/`
tree uses `SKILL.md` files, e.g. `skills/creative/ascii-video/SKILL.md`,
`skills/social-media/xurl/SKILL.md`, matching the same shape). Two independent
sources, one of them a deep-audited direct confirmation on the fixed base
architecture itself — this is a real compatibility win, not just a doc-level
similarity claim.
Mechanism: A skill is a directory containing metadata + a `SKILL.md` body, with
additional resources (`/scripts`, `/references`, `/assets`) loaded on demand rather
than upfront (progressive disclosure); SKL-009 additionally proposes a validation
script gate (errors -> warnings -> suggestions) and a "shibboleths" discipline —
encode real expert judgment and explicit anti-pattern ("NOT for") clauses, not
generic filler, to keep skills high-signal.
Required Conditions: A runtime that actually respects the on-demand-loading
contract (loads metadata for relevance-matching, defers full content) — confirmed to
exist in Hermes' fixed base architecture per the REPO-001 finding, not merely assumed.
Strengths: Directly answers DOM-04's reframed compatibility question with a positive
finding — hermes-agent's native skill shape appears compatible with the Claude Skills
convention without requiring a translation layer, which was flagged as an open,
unresolved dependency as recently as Stage -2.2's skill-catalog entries.
Weaknesses: SKL-009's specific tooling (`validate_skill.py`, `check_self_contained.py`)
is Claude-ecosystem-specific and was not found or confirmed to exist inside
hermes-agent's own skill tooling (`hermes skills` CLI audit/publish subcommands exist
per the capability reference, but their internal validation logic was not inspected)
— the packaging *shape* compatibility is confirmed; validation-*tooling* compatibility
is not.
Failure Modes: A skill authored to SKL-009's discipline (shibboleths, exclusion
clauses) could still fail to activate correctly if hermes-agent's own skill-matching/
activation logic (not inspected this pass) differs materially from Claude's, even
with matching file shape — a structural-shape match does not guarantee a
behavioral-activation match.
Complexity: Low — this is primarily an authoring discipline plus confirmed-compatible
file structure, not new infrastructure.
Token/Cost Implications: Positive — the entire point of progressive disclosure is
to avoid loading unused skill content into every turn's context, directly reducing
per-turn token cost as the skill catalog grows.
Human-Control Implications: Indirect — well-scoped, single-purpose skills with
explicit "NOT for" exclusion clauses reduce the chance an agent silently misapplies a
skill outside its intended boundary, which is a soft form of scope containment.
Hermes Relevance: DOM-04 (direct, primary — this is the closest thing to a "yes, it's
compatible" finding this domain has produced); DOM-01/DOM-06 (skills are one of
REPO-001's three sanctioned extension surfaces, per PAT-001).
Alternative Patterns: PAT-001 (narrow-waist architecture) is the containing pattern this
one plugs into, not a competing alternative.
Recommendation: STRONG CANDIDATE
Confidence: 70
Evidence: repo-audits/nousresearch-hermes-agent.md Dimension H ("skills/ uses SKILL.md
files... matching the Claude Skills shape closely... directly relevant to DOM-04's
bridging question — native compatibility looks strong"); skill-catalog.md SKL-009
record (Core Method, Dependencies fields).

Adversarial Review (Section 13):
Q1 (assumptions): Assumes file-shape compatibility implies (or at least strongly
suggests) behavioral/activation compatibility — not independently verified; hermes-agent's
own skill-activation/matching logic was not read this pass.
Q2 (failure for Hermes): If hermes-agent's skill activation logic differs materially
from Claude's underlying model, skills authored to SKL-009's discipline could sit
inert or misfire despite structurally correct packaging — a real, untested risk.
Q3 (complexity introduced): Low.
Q4 (lock-in): Low — this is a portable authoring convention, not infrastructure.
Q5 (evidence missing): SKL-009 itself is single-source, doc-only evidence (no code
inspected for the skill-authoring methodology, only for hermes-agent's skill file
shape) — the *authoring discipline* half of this pattern carries lower evidence
weight than the *file-shape compatibility* half.
Q6 (simpler competing approach): Loading full skill content unconditionally is
simpler to implement but reintroduces the context-bloat problem this pattern exists
to solve, and doesn't match what hermes-agent already appears to support natively —
not a real competitor given the confirmed native shape.
Q7 (marketing vs. engineering): The hermes-agent half is confirmed engineering (real
file structure, code-level); the SKL-009 half is a documented methodology, genuine but
unverified by code/adoption evidence — a mixed-confidence pattern, reflected in the
70 (not higher) confidence score.
Reasoning Summary: Rated STRONG CANDIDATE mainly on the strength of the deep-audited
REPO-001 half of the evidence (a real, direct, positive compatibility finding on the
fixed base architecture, resolving what was an open question as of Stage -2.2) — the
SKL-009 half adds a ready-made authoring discipline but is lower-confidence,
doc-only evidence and should not be over-credited on its own.

Role Notes (Section 14):
- Repository Auditor: Confirmed the specific SKILL.md file paths cited
  in the source audit are real repo paths, not paraphrased — solid confirmation.
  Verdict: Strong for the compatibility claim specifically.
- Reliability Reviewer: No evidence either way on activation-logic
  compatibility (Q1/Q2 above) — this is the one open reliability question that
  should gate treating DOM-04 as "resolved" at Stage -2.6. Verdict: Moderate — real
  finding, real open gap.
- Skeptic: Attempted rejection — "matching file structure is a weak
  signal; two systems can use identically-named files for very different runtime
  behavior." Counter: agreed as a real limitation (reflected in Q1/Q2/Weaknesses), but
  the finding is still meaningfully more informative than the prior state (a fully
  open, unverified question as of Stage -2.2) — a partial answer with a clearly
  flagged remaining gap is more useful than treating the question as still fully
  open. Rejection does not succeed in full but narrows the confidence score
  (70, not 85+).

---

### PAT-006

Pattern Name: Session-Lifecycle-Aware MCP Client Wrapper
Problem Solved: Integrating MCP tool servers into an agent robustly — not just
calling a tool once, but managing connection lifecycle (reconnect, timeout) and
weaving MCP awareness into the agent's own instruction-building, rather than treating
MCP as a bolted-on, fire-and-forget tool type.
Observed In: REPO-005 (google-adk-python, deep-audited, high confidence — the
standout positive finding of that audit); comparison/contrast: REPO-006
(modelcontextprotocol/servers, deep-audited, but the maintainers' own README
explicitly self-discloses these are reference/educational, "not production-ready" —
directly disqualifying it as evidence for this pattern's reliability half, per
Section 12.1's ban on treating a recent/official repo as automatically
production-proven); REPO-001 (nousresearch-hermes-agent) confirmed to have an
`optional-mcps/` directory and an `hermes mcp` CLI command, but internal
implementation depth was not read this pass — UNKNOWN, not confirmed comparable.
Mechanism: A dedicated session-manager component (`mcp_session_manager.py`) handling
MCP server connection lifecycle, separate from the tool-calling logic itself
(`mcp_tool.py`, `mcp_toolset.py`, `_agent_to_mcp.py`); additionally, an
`mcp_instruction_provider.py` under the agent-construction path suggests MCP
awareness is surfaced into how the agent's own instructions/system prompt are built,
not just exposed as an interchangeable tool type.
Required Conditions: An MCP client implementation with actual connection-lifecycle
code (reconnect/timeout handling) — the specific reconnect/timeout logic was not
independently line-verified this pass (flagged in the source audit as "likely
present, not independently confirmed").
Strengths: This is a materially richer MCP integration than a single-file wrapper —
confirmed by direct multi-file inspection, not asserted from a README. Directly
useful as a comparison baseline for evaluating whatever depth hermes-agent's own
`optional-mcps/` integration turns out to have on a future, deeper pass.
Weaknesses: The specific reconnect/timeout behavior inside `mcp_session_manager.py`
was not read line-by-line this pass — the "session-aware" characterization rests on
the file's existence and naming (itself real evidence per Section 12.1 — a dedicated
file for a claimed feature is stronger evidence than a docs-only mention) but not on
confirmed internal logic.
Failure Modes: If Hermes' actual MCP-heavy tool calls (image/video generation APIs,
publishing APIs, search/scraping) hit a flaky MCP server and hermes-agent's own MCP
layer turns out to lack equivalent session-lifecycle handling (unverified either way),
Hermes could inherit silent connection-failure behavior directly relevant to DOM-06's
error-handling/blast-radius question.
Complexity: Medium — a session-manager abstraction is real engineering, not a config
flag, if built from scratch on top of hermes-agent's substrate.
Token/Cost Implications: Indirect — a poorly-handled MCP disconnect/retry storm could
waste tokens on repeated failed tool-call attempts; a session-aware wrapper is a
mitigation, not eliminating the cost risk entirely.
Human-Control Implications: Indirect — robust connection handling reduces the chance
of a tool call silently failing in a way that produces a misleading "success" state
requiring human debugging after the fact, tangential to but supportive of DOM-08's
least-privilege/blast-radius concerns.
Hermes Relevance: DOM-06 (direct, primary — this is exactly the "how robust is
tool-use error handling" comparison DOM-06 asks for); indirectly DOM-01 (instruction-
building integration touches how the agent core is structured).
Alternative Patterns: REPO-006's reference-server collection is explicitly the wrong
comparison for this specific question (self-disclosed as non-production) — kept as a
contrast note, not an alternative pattern.
Recommendation: STRONG CANDIDATE
Confidence: 70
Evidence: `src/google/adk/tools/mcp_tool/` directory listing (`mcp_session_manager.py`,
`_agent_to_mcp.py`, `mcp_tool.py`, `mcp_toolset.py`, `load_mcp_resource_tool.py`,
`_remote_mcp_server.py`) plus `agents/mcp_instruction_provider.py` — all FACT-labeled
file-existence findings per repo-audits/google-adk-python.md Dimension G.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes file existence + naming is a reliable proxy for the claimed
internal behavior (reconnect/timeout handling) — a real inferential step, not a
line-by-line confirmation.
Q2 (failure for Hermes): If hermes-agent's own `optional-mcps/` turns out to be
shallow by comparison, Hermes would need to either supplement it with adk-python-style
session management or accept weaker MCP reliability than this comparison baseline
suggests is achievable — a genuine, currently-unresolved gap-sizing question.
Q3 (complexity introduced): Medium if built from scratch; unknown/lower if
hermes-agent's own `optional-mcps/` already has equivalent depth (unverified).
Q4 (lock-in): Low — MCP itself is a portable, vendor-neutral protocol; a
session-manager wrapper built for it is not inherently ADK-specific in concept.
Q5 (evidence missing): Internal reconnect/timeout logic not read; hermes-agent's own
MCP integration depth not read — both real, named gaps for a Stage -2.6 follow-up
before this domain is treated as resolved.
Q6 (simpler competing approach): A single-file, fire-and-forget MCP tool wrapper
(closer to what REPO-006's reference servers demonstrate) is simpler but explicitly
self-disclosed as not production-ready — not a real competitor for Hermes' stated
reliability needs.
Q7 (marketing vs. engineering): Real engineering — multi-file, specifically-named
components exceeding what the Stage -2.3 triage record's README-level description
implied, per the audit's own explicit note.
Reasoning Summary: Rated STRONG CANDIDATE on the strength of a single deep-audited,
high-confidence source whose evidence (multiple specifically-named, purpose-built
files) exceeds README-level claims — satisfying the Stage -2.5 exit criterion's
"one deep-audited high-confidence source" branch. The clearly-flagged gap (internal
logic not traced; hermes-agent's own comparable depth unknown) is preserved as an
explicit follow-up rather than smoothed into false confidence.

Role Notes (Section 14):
- Repository Auditor: File-level evidence is genuinely strong and
  specific — six distinctly-named, purpose-built files is meaningfully different from
  a single `mcp_wrapper.py` catch-all. Verdict: Strong on existence/breadth.
- Reliability Reviewer: The core reliability claim (reconnect/timeout
  handling) is inferred from file naming, not confirmed from logic — flag this
  explicitly as the weakest link before anyone treats "robust MCP reliability" as a
  settled fact for adk-python, let alone as a bar hermes-agent is assumed to meet or
  miss. Verdict: Moderate — plausible, not confirmed.
- Skeptic: Attempted rejection — "a session-manager *file* existing
  doesn't prove session management actually works correctly; this could be dead code
  or a thin wrapper with an ambitious name." Counter: fair, and explicitly not
  overclaimed in the Evidence/Weaknesses fields above — the STRONG rating is
  calibrated to "richer, more purpose-built structure than a comparison baseline,
  confirmed via multi-file inspection," not to "proven to work flawlessly," which is
  an appropriately narrower claim. Rejection does not succeed but keeps the
  Confidence score at 70 rather than higher.

---

### PAT-007

Pattern Name: Explicit 4-Section Agent Contract Prompt + Typed I/O + Test Checklist
Problem Solved: Defining a subagent's boundaries with enough rigor (role, skill
scope, input/output schema, and a systematic test pass including "out-of-scope
refusal") that the boundary is verifiable, not just implied by prose.
Observed In: SKL-021 (Skillful Subagent Creator, SomeClaudeSkills, doc-only, Medium
evidence, test checklist "unusually concrete for this source type" per its own
catalog record); SKL-013 (Output Contract Enforcer, SomeClaudeSkills, doc-only, Medium
evidence) — complementary: SKL-021 defines the contract at design time, SKL-013
validates it at runtime.
Mechanism: A 6-step authoring process culminating in an explicit JSON input/output
contract per subagent, plus a mandatory test checklist (happy path, edge cases,
out-of-scope refusal, skill adherence, contract validation) run before the subagent
is considered ready; SKL-013 supplies the runtime-side validation gate (sequential
fail-fast: JSON-parseable? required fields? correct types? constraints satisfied?)
that checks whether output actually matches the contract SKL-021's process defined.
Required Conditions: Willingness to write and maintain explicit schemas per
agent-to-agent boundary (a discipline cost); a validation gate at runtime to actually
enforce what's declared (SKL-013 or equivalent, e.g. PAT-003's mechanism).
Strengths: The "out-of-scope refusal" test case specifically maps to Hermes' "stop
and ask, don't guess" principle at the agent-boundary level — an explicit, testable
check that an agent correctly declines work outside its declared scope rather than
silently attempting it.
Weaknesses: Both sources are single-vendor documentation with no code or field-adoption
evidence inspected — Evidence Quality is capped at Medium per Stage -2.2's own scoring
discipline (Section 10.4). SKL-021's skill-preloading-tier component depends on the
same open Claude-Skills-compatibility question flagged for SKL-009/PAT-005.
Failure Modes: A written contract with no enforcement mechanism behind it is just
documentation — this pattern only delivers its value if paired with an actual runtime
validator (SKL-013, or PAT-003's schema-enforced-retry mechanism); adopting the prompt
template alone without the test checklist or the runtime gate would be a partial,
weaker adoption easy to mistake for the full pattern.
Complexity: Low-Moderate — a structured prompt/contract-design methodology and a
validation gate, not new infrastructure, per SKL-021's own catalog assessment.
Token/Cost Implications: Neutral to positive — catching an out-of-scope or malformed
subagent response via a fast, explicit runtime check is cheaper than letting a bad
response propagate further into a longer pipeline before being caught.
Human-Control Implications: Direct — the out-of-scope-refusal test case is
specifically a form of self-imposed boundary discipline that reduces the surface
area needing human review, by design.
Hermes Relevance: DOM-02 (direct — this is a full design-time-to-runtime contract
discipline, complementary to PAT-003's runtime-enforcement mechanism and PAT-002's
composition-primitive question).
Alternative Patterns: PAT-003 (schema-enforced retry loop) supplies stronger,
code-verified runtime enforcement than SKL-013 alone provides evidence for; pairing
PAT-007's design-time discipline with PAT-003's runtime mechanism (rather than SKL-013's
un-code-verified version) is a stronger combined recommendation than either alone —
noted for Stage -2.6 capability-matrix construction.
Recommendation: CANDIDATE
Confidence: 55
Evidence: skill-catalog.md SKL-021 record (Core Method, Role Notes already completed
at Stage -2.2 for this Strong-scored skill) and SKL-013 record (Core Method,
Generalizable Components) — both doc-only sources, no independent code verification
performed this pass.

Reasoning for CANDIDATE (not STRONG): while SKL-021 was itself rated a Strong
Candidate skill at Stage -2.2 (score 80, with completed adversarial review and role
notes already on file), that rating was for the *skill* under Stage -2.2's own rubric;
at the *pattern* level, both contributing sources remain single-vendor,
doc-only-evidence, uncorroborated by any deep-audited repository finding on the same
specific mechanism (unlike PAT-003, which the same underlying idea — schema-enforced
output — achieves at STRONG CANDIDATE strength via three code-verified sources). This
pattern is downgraded relative to its Stage -2.2 skill score specifically because
Stage -2.5's bar (Section 8 exit criteria) requires either multi-source or
deep-audited-code corroboration, which the design-time-contract half of this pattern
does not yet have independent of SKL-013's similarly doc-only runtime half.

---

### PAT-008

Pattern Name: Structured-Adversarial-Synthesis for Rare, High-Stakes Decisions
Problem Solved: Reaching a well-reasoned, defensible decision on a rare, high-stakes,
contestable question (e.g. a foundational document, a constitution, an architecture
record) where correctness matters far more than speed or cost.
Observed In: SKL-007 (Recursive Synthesis, SomeClaudeSkills, doc-only, Medium
evidence, single source).
Mechanism: A 6-phase process — Setup (select ~10 cognitively diverse simulated
agents), Divergence (parallel independent position papers, no cross-agent
communication), Synthesis (ranked-choice principle hierarchy), Commentary (mandatory
steel-manned adversarial review), Reality Check (a fresh practitioner audit for
actual implementability), Final Merge (Constitution + Practitioner's Guide +
Editorial Notes + Dissenting Appendix, preserving disagreement rather than averaging
it away).
Required Conditions: A genuinely rare, high-stakes decision where the cost of ~10
substantial parallel agent invocations plus multi-phase synthesis is justified —
explicitly NOT for routine, repeated decisions.
Strengths: Structurally mirrors this very Master Plan's own Section 13 (negative
research) and Section 14 (role simulation) protocols — a real, independently-arrived-at
validation that this general shape (diverge, synthesize, adversarially critique,
reality-check, preserve dissent) is a sound approach for high-stakes research
synthesis, not just for Hermes' own decision-making but for how this Phase -2 research
process itself is structured.
Weaknesses: Single source, doc-only evidence, no field-adoption metrics on how often
its "Reality Check" phase actually catches real errors; assumes genuine cognitive
diversity across ~10 simulated agents is achievable, which carries an illusory-
diversity risk if those agents are drawn from the same underlying model family.
Failure Modes: If misapplied to a routine, repeated decision (e.g. per-post content
review) instead of a genuinely rare one, this pattern would directly blow Hermes'
cost budget — a direct conflict with the co-equal quality/cost constraint from the
raw idea, already flagged in this skill's own Stage -2.2 adversarial review.
Complexity: High — 10-agent parallel run, multi-phase synthesis, steel-manning
discipline, multi-document final merge.
Token/Cost Implications: Significant — explicitly one of the more expensive patterns
in the entire research corpus; only justified for genuinely rare decisions (e.g.
defining Hermes' own top-level behavioral charter once, or a single page's brand
constitution once), never for routine per-post work.
Human-Control Implications: The Dissenting Appendix requirement (preserving
unresolved disagreement rather than averaging it away) is itself a human-control-relevant
discipline — it surfaces genuine uncertainty to a human decision-maker instead of
presenting false synthesis-driven confidence.
Hermes Relevance: DOM-02 (rare governance/contract decisions), DOM-15 (as a candidate
mechanism for rare, high-stakes content decisions only — explicitly not routine
per-post review, per the skill's own Stage -2.2 record).
Alternative Patterns: PAT-003/PAT-007 (schema-enforced contracts, design-time discipline)
handle the routine case this pattern explicitly should not be used for.
Recommendation: CONTEXT-DEPENDENT
Confidence: 60
Evidence: skill-catalog.md SKL-007 record (already carries a completed Stage -2.2
Adversarial Review reaching the same narrow-scope conclusion independently).

Reasoning for CONTEXT-DEPENDENT (not STRONG or CANDIDATE): the mechanism itself is
well-specified and independently corroborated by structural similarity to this Master
Plan's own protocols, but it is single-sourced, doc-only, and — critically — the
Stage -2.5 exit criterion for STRONG CANDIDATE (failure modes + human-control
implications documented) is satisfied, but the >=2-source/deep-audit bar is not, and
the pattern's own defining characteristic is that its value is entirely conditional
on rare/high-stakes applicability — CONTEXT-DEPENDENT is the more accurate rating
than a blanket CANDIDATE.

---

### PAT-009

Pattern Name: When-to-Use-MCP Decision Tree + Security-Hardening Sequence
Problem Solved: Deciding whether a given integration actually warrants building an
MCP server (vs. a simpler direct API call), and if so, hardening it in a consistent
order (validation, secrets, rate limiting, auth boundaries) rather than ad hoc.
Observed In: SKL-024 (MCP Creator, SomeClaudeSkills, doc-only, Medium evidence,
single source).
Mechanism: A decision tree (external API + auth? persistent state? rate limiting?
shared credentials? security boundaries? -> if any yes, use MCP) followed by a
7-step build sequence ending in a fixed security-hardening order: input validation,
secret management, rate limiting, auth boundaries.
Required Conditions: A Node/TypeScript-oriented stack (`@modelcontextprotocol/sdk`,
`zod`) as documented — may or may not match hermes-agent's actual implementation
language for its own `optional-mcps/` integration (unverified this pass).
Strengths: A concrete, checkable decision tree is more useful as a design-time
comparison checklist than a vague "use MCP when appropriate" heuristic — directly
usable as an evaluation rubric when Hermes' own tool-integration decisions come up in
Phase -1, regardless of implementation-language match.
Weaknesses: Single source, doc-only, no code inspected; the specific dependency stack
assumption may not transfer to hermes-agent's actual MCP implementation.
Failure Modes: Applying the decision tree mechanically without adapting the
hardening-sequence specifics to hermes-agent's actual stack could produce a false
sense of having "done MCP security properly" when the underlying implementation
details differ.
Complexity: Low as a checklist/decision-aid; the actual server-building work it
guides is separately scoped.
Token/Cost Implications: Neutral — this is a design-time decision aid, not a runtime
mechanism with direct cost implications.
Human-Control Implications: Indirect — a consistent security-hardening order (secrets
before auth boundaries, etc.) reduces the chance a tool integration ships with an
overlooked gap, tangential support for DOM-08.
Hermes Relevance: DOM-06 (direct — a comparison checklist for hermes-agent's own
tool/MCP integration decisions and hardening completeness).
Alternative Patterns: PAT-006 (session-lifecycle-aware MCP wrapper) addresses runtime
robustness once a server is built; PAT-009 addresses the upstream design-time decision
of whether/how to build one at all — complementary, not competing.
Recommendation: CANDIDATE
Confidence: 45
Evidence: skill-catalog.md SKL-024 record (Core Method, Project-Specific Assumptions).

---

## Cluster B — Human Control, Safety & Trust (DOM-05, 07, 08, 09, 10)

Sources read: repo-audits/{microsoft-agent-governance-toolkit, humanlayer-humanlayer,
agentward-ai-agentward, ashutoshrana-confidence-escalation}.md; skill-catalog.md
records SKL-012, SKL-019, SKL-026, SKL-027, SKL-028, SKL-030; research-domains.md
DOM-05/07/08/09/10 definitions.

### PAT-010

Pattern Name: Structural pre-execution policy gate (govern()/proxy interception)
Problem Solved: Prevents relying on prompt-level instructions alone to enforce "the
agent must not do X" — intercepts the actual tool call before it executes and can
deny it outright, so a rule holds even if the model's own judgment drifts or is
manipulated.
Observed In: REPO-010 (microsoft/agent-governance-toolkit — agent-mesh `govern()`),
REPO-012 (agentward-ai/agentward — proxy + `PolicyEngine.evaluate()`)
Mechanism: A wrapper/proxy sits between the agent and the real tool-call boundary.
Every call is evaluated against a declarative policy (YAML in both sources) before
execution; on deny, the call is blocked (agent-mesh raises `GovernanceDenied` by
default; agentward's proxy routes through `evaluate()`/`evaluate_chaining()`).
Neither is a logging/audit layer bolted on after the fact — both are confirmed
in-path, code-verified (not README claims) to run before the underlying action.
Required Conditions: The agent's tool-calling surface must funnel through a single
interception point (a wrapper, proxy, or SDK boundary) — a runtime that lets agents
call tools by arbitrary side-channel (e.g. shelling out directly) defeats this
entirely.
Strengths: Enforcement is structural, not advisory — survives prompt drift, jailbreak
attempts, and simply forgetting to re-state the rule in a long session. Both sources
demonstrate framework-agnostic integration (agent-mesh: LangChain/CrewAI/OpenAI
Agents SDK/Google ADK/smolagents examples; agentward: Python + npm bindings).
Weaknesses: Policy authoring is a new surface with its own failure modes (a
misconfigured YAML rule silently under- or over-blocks); adds a real dependency and
a DSL to learn. agent-mesh's own audit found sub-project maturity uneven across its
monorepo — only the specific pieces used here (agent-mesh, agent-hypervisor) were
verified, not the whole toolkit.
Failure Modes: Silent misconfiguration (a policy gap that isn't visible — see PAT-013
for the specific mitigation one source uses); a gate that's technically present but
default-permissive if the policy author didn't explicitly deny; performance/latency
overhead if the policy engine is invoked synchronously on a hot path (not measured in
either audit).
Complexity: Medium — both sources ship this as a real library, not a from-scratch
build, but adopting either means adopting its policy DSL and wiring every tool call
through the interception point.
Token/Cost Implications: Minimal LLM-token cost (policy evaluation is deterministic
code, not a model call) — cheap to run per-action compared to e.g. an LLM-judge
evaluator pattern.
Human-Control Implications: This is a mechanism *for* human control (it's what makes
a written policy actually binding), but it is not itself a human-facing approval
step — see PAT-011 for the complementary approval-coordinator pattern that adds a human
in the loop rather than a static rule.
Hermes Relevance: DOM-08 (primary — this is a real least-privilege/capability-scoping
mechanism, code-verified in both sources) and DOM-05 (partial answer — sidesteps the
"does the prompt reliably hold" problem entirely by moving enforcement out of the
prompt into code, which is itself a notable answer to DOM-05's research question,
though it doesn't address prompt-level constraints that have no code-level
equivalent, e.g. tone/voice rules).
Alternative Patterns: PAT-011 (approval-coordinator — human-facing complement), PAT-013,
PAT-014 (agentward-specific refinements of this same base mechanism)
Recommendation: STRONG CANDIDATE
Confidence: 78
Evidence: Both sources' Dimension A (Architecture) verdicts were "Strong" in their
audits, code-verified by reading the actual interception functions
(`govern.py:664`, `agentward/policy/engine.py`), not inferred from docs.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes the agent runtime has (or can be given) a single funnel
point for all tool calls — true for both audited sources' target frameworks, unknown
for `hermes-agent` until its own tool-call architecture is checked against this
requirement (already partially covered under DOM-06, Stage -2.4).
Q2 (failure modes for Hermes): A policy gap (untested rule combination) could
silently allow something Hermes shouldn't do; conversely an overzealous default-deny
policy could block legitimate routine actions and create approval fatigue upstream at
whatever human-facing layer sits above this gate.
Q3 (complexity introduced): Real — a policy DSL, policy-authoring workflow, and
policy-testing discipline are all new surface area, not free.
Q4 (lock-in): Low-moderate — the interception *concept* is portable, but the specific
YAML policy files written for one engine's DSL do not transfer to another without
rewriting.
Q5 (evidence missing): Neither source's claimed test-count (agent-mesh's "992
conformance tests," agentward's "3,466 passing tests") was independently re-derived
at the test-case level in their audits — both flagged UNVERIFIED-BUT-PLAUSIBLE, not
confirmed.
Q6 (simpler competing approach): A much simpler allowlist (hardcoded per-tool
permission list, no general policy engine) could cover Hermes' actual v1 tool
surface if it stays small — the general policy-engine approach is justified only if
Hermes' tool surface grows large/varied enough that hardcoding becomes unmanageable.
Q7 (marketing vs. engineering): Genuine engineering in both — agent-mesh's own audit
flagged the risk of over-crediting the surrounding monorepo based on this one
strong core; that risk was carried forward here by scoping this pattern strictly to
the two audited pieces, not the toolkit's README-level claims.

Role Notes (Section 14):
- Repository Auditor: Both interception points were read directly in
  Stage -2.4, not taken from documentation — govern() raises on deny as a genuine
  side effect, not a log line. Verdict: Strong, code-verified in both sources
  independently.
- Reliability Reviewer: The real risk isn't the mechanism, it's
  policy-authoring quality — an interception point that always exists but is
  configured too loosely provides no actual protection. Recommend that any adoption
  decision (Phase -1) require a policy-testing/coverage-check discipline alongside
  the interception mechanism itself, not the mechanism alone.
- Skeptic: Attempted rejection: Hermes is a single-owner system with a
  small, known tool surface (per OD-001) — a general policy-engine dependency may be
  overkill compared to a hardcoded allowlist. Counter: the pattern's value isn't
  scale, it's *structural* (survives prompt drift) vs. a prompt-level "don't do X"
  instruction the raw idea's principles depend on holding reliably — that property
  is needed even at small scale. Rejection attempt does not fully succeed, but the
  scale objection is valid enough to note as a real Phase -1 sizing question (full
  policy-engine adoption vs. a lighter hardcoded interception point implementing the
  same *concept* at smaller scope).

---

### PAT-011

Pattern Name: Approval-coordinator as a first-class execution parameter (maker-checker gate)
Problem Solved: Gives an agent a real, structural way to pause and require explicit
human sign-off before a specific action executes — not a suggestion in a prompt, an
actual code path the action cannot proceed past without a recorded approval.
Observed In: REPO-010 (agent-mesh — `ApprovalCoordinator`/`ApprovalTransport` wired
into `govern()`'s `approval_handler`/`approval_coordinator`/`approval_ttl_seconds`
parameters), REPO-011 (humanlayer — `hld/approval/manager.go`'s `CreateApproval()`)
Mechanism: The action-execution call itself takes an approval dependency as a
parameter (not a separate bolted-on check). Before proceeding, the call blocks on (or
routes through) an approval object that persists the pending request, exposes it over
an API (REST/RPC in humanlayer's case), and only continues execution once approved.
Both implementations are backed by real tests exercising the approval path, not just
documented as a design intent.
Required Conditions: A place in the execution path where "pause and wait for an
external signal" is actually possible — i.e., the agent runtime must support
suspending an in-flight action, which is a real architectural requirement, not free
in every framework.
Strengths: This is the single most concretely-verified DOM-07 mechanism found across
the entire Stage -2.3/-2.4 discovery — humanlayer's audit calls it exactly that,
independent of the humanlayer *project's* own viability. Both sources demonstrate it
with passing tests against the approval path specifically, not just the happy path.
Weaknesses: humanlayer/humanlayer the *project* is self-declared deprecated
(README: "the code here is pretty much all deprecated") with its successor
(humanlayer.com) unaudited — the mechanism is sound, the specific codebase is not an
adoptable dependency as-is. agent-mesh's approval flow is real but its
identity/role layer (SPIFFE/DID) that would attribute *who* approved was only
partially traced.
Failure Modes: A stuck/expired approval request with no clear fallback (what happens
at `approval_ttl_seconds` timeout — deny, retry, escalate? — not fully traced in
either audit); an approval-fatigue failure mode if this gate is applied to too many
routine actions rather than being reserved for genuinely irreversible ones.
Complexity: Medium — requires a persistence layer for pending approvals (both sources
use a real datastore: agent-mesh's policy_server, humanlayer's SQLite-backed
`hld/store`) plus an exposed channel for a human to actually respond.
Token/Cost Implications: Low direct LLM cost (the gate itself is not model-driven);
indirect cost if it stalls a long-running agent session waiting on a human response.
Human-Control Implications: This *is* the human-control mechanism — it is the
concrete implementation of the raw idea's "irreversible action always requires
explicit confirmation" principle, at the code layer rather than the prompt layer.
Hermes Relevance: DOM-07 (primary, direct match to the raw idea's named principle).
Alternative Patterns: PAT-010 (the policy layer this can be wired into), PAT-016/PAT-017
(what determines *when* this gate should trigger and what it should show the human)
Recommendation: STRONG CANDIDATE
Confidence: 74
Evidence: Both sources have direct, code-level confirmation (agent-mesh:
`test_approval.py`, `test_govern_approval_coordinator.py`; humanlayer:
`manager_test.go`, `daemon_approval_integration_test.go`,
`sqlite_approval_test.go`) — genuinely tested code paths, not documentation claims.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes the runtime can suspend/resume an in-flight action rather
than only running to completion — needs verification against `hermes-agent`'s actual
execution model (open item from Stage -2.4's REPO-001 audit: DOM-07 was found
"Moderate," off-by-default, publish-specific gating UNKNOWN).
Q2 (failure modes for Hermes): If Hermes' agent runtime can't cleanly suspend/resume,
adopting this pattern requires re-architecting the execution loop, not just adding a
check function — a materially bigger lift than the pattern description alone
suggests.
Q3 (complexity introduced): A persistence layer + exposed response channel is new,
real infrastructure, not a one-line addition.
Q4 (lock-in): Low for the *concept*; the specific implementations (agent-mesh's
policy_server, humanlayer's Go daemon) are not directly reusable as dependencies
given the toolkit's monorepo unevenness and humanlayer's deprecation respectively.
Q5 (evidence missing): Neither audit traced what happens on approval timeout/expiry
end-to-end — a real gap for a "never guess, always confirm" system where a silent
timeout-to-deny vs. timeout-to-proceed default materially matters.
Q6 (simpler competing approach): A much simpler synchronous "print the pending action
and block on stdin/a Slack message, resume in the same process" design (no separate
persistence/API layer) could satisfy Hermes' actual v1 need — single owner, not a
distributed multi-approver system — without the infrastructure both audited sources
carry.
Q7 (marketing vs. engineering): Genuine engineering in both; humanlayer's audit
explicitly separated the sound mechanism from the non-viable project status rather
than crediting marketing framing.

Role Notes (Section 14):
- Repository Auditor: Confirmed via direct source and test reads in both
  cases (Stage -2.4), independent of humanlayer's project-level deprecation. Verdict:
  Strong on the mechanism.
- Reliability Reviewer: The unresolved timeout/expiry behavior (Q5) is
  the single biggest open reliability question for adopting this pattern — recommend
  it be resolved explicitly in Phase -1 design, not inherited silently from either
  source's default.
- Skeptic: Attempted rejection: given Q6's simpler synchronous
  alternative fully covers a single-owner system's need, the persistence/API
  infrastructure in both sources may be unjustified complexity for Hermes.
  Counter: the *concept* (action blocks structurally on an external approval object,
  not a prompt-level pause) is what's worth taking; the specific infrastructure
  weight is a Phase -1 sizing decision, not a reason to reject the pattern itself.
  Rejection attempt does not succeed against the pattern, but materially informs how
  lightly it could be implemented.

---

### PAT-012

Pattern Name: Time-bounded, auto-expiring privilege elevation
Problem Solved: Lets an agent temporarily gain elevated capability for a specific
need without that elevation becoming a standing, forgotten grant.
Observed In: REPO-010 (agent-mesh — `agent-hypervisor/src/hypervisor/rings/
elevation.py`, trust-score-gated, auto-expiring via `tick()`, paired with a
`breach_detector.py` and `rate_limiter.py` in the same package)
Mechanism: Privilege changes are modeled as rings with an elevation call that is
trust-score-gated (not unconditional) and carries its own expiry, ticked down
independent of whether the elevated action was ever used — the grant lapses on its
own rather than requiring an explicit revoke step.
Required Conditions: A capability/permission model expressive enough to represent
"ring" tiers, plus a trust-score input to gate elevation on.
Strengths: Removes the most common failure mode of manual privilege grants — someone
elevates access for a task and forgets to revoke it. Paired breach-detection and
rate-limiting in the same module suggest this was designed as a cohesive safety
package, not an isolated function.
Weaknesses: Single-source finding — only inspected in one audited repo, and only one
sub-project of a large uneven monorepo (see PAT-010's maturity caveat, same source).
The trust-score input mechanism itself (what produces the score, how it's
calibrated) was not traced in the Stage -2.4 audit.
Failure Modes: An elevation that expires mid-task, interrupting legitimate
in-progress work if the expiry window is miscalibrated against real task duration;
a trust score that is itself gameable or poorly calibrated undermines the whole gate
(same generic risk noted for confidence-based gating elsewhere in this cluster, see
PAT-015/PAT-016).
Complexity: Medium — requires a tiered permission model plus a scoring input, not a
simple boolean flag.
Token/Cost Implications: None direct (deterministic code, not model-driven).
Human-Control Implications: Reduces reliance on a human remembering to revoke access
— a structural safety property complementary to, not a replacement for, an approval
gate (PAT-011) at the moment of the elevated action itself.
Hermes Relevance: DOM-08 — directly relevant to least-privilege scoping, particularly
if Hermes ever needs an agent to temporarily touch a page/credential set outside its
normal scope (e.g. a cross-page action) rather than holding standing broad access.
Alternative Patterns: PAT-010 (the broader interception layer this could sit inside)
Recommendation: CANDIDATE
Confidence: 55
Evidence: Confirmed by direct source read (Dimension D verdict: Strong) but single-
source — does not meet the >=2-independent-source bar for STRONG CANDIDATE, and the
trust-score mechanism it depends on is itself unverified.

---

### PAT-013

Pattern Name: Explicit coverage-gap self-reporting instead of silent default allow/deny
Problem Solved: Makes a policy engine's blind spots visible to the operator rather
than having an uncovered case silently fall through to whatever the engine's default
behavior happens to be (which the operator may not even know).
Observed In: REPO-012 (agentward — documented `△ GAP` output state: "No policy rule
covers this tool at all")
Mechanism: When the policy engine evaluates a tool call that no rule addresses, it
returns a distinct, visible "gap" signal rather than folding that case into either
an implicit allow or implicit deny — the absence of coverage is itself surfaced as
information.
Required Conditions: A policy engine with a closed-world assumption problem in the
first place (i.e., something that evaluates against a rule set that can be
incomplete) — not applicable to a system with only hardcoded allow/deny logic and no
notion of "unaddressed case."
Strengths: A small, cheap addition to a policy engine (PAT-010) that directly prevents
one of that broader pattern's own named failure modes — silent misconfiguration.
Confirmed present verbatim in both the README and rendered docs, and the design
choice (surfacing rather than defaulting) is a deliberate one per the source's own
framing, not an accidental gap in the tool.
Weaknesses: Single-source finding. Verified at the "it exists and is documented"
level; not independently traced how the operator is expected to *act* on a gap
signal once surfaced (does it block, log-only, or something else) — this audit's
Dimension E verdict for it was "Moderate," not "Strong."
Failure Modes: If a gap is surfaced but nothing downstream reads/acts on that signal,
this becomes a false sense of safety — visibility without an enforced response is not
the same as coverage.
Complexity: Low — this is a design refinement to an existing policy-evaluation
mechanism (PAT-010), not a new subsystem.
Token/Cost Implications: None direct.
Human-Control Implications: Directly supports "don't guess" as applied to the policy
layer itself — an unaddressed case is flagged rather than silently resolved one way
or the other.
Hermes Relevance: DOM-08 — a specific, low-cost refinement worth carrying into any
Hermes policy/permission-scoping implementation regardless of which broader
enforcement mechanism (PAT-010) is chosen.
Alternative Patterns: PAT-010 (parent mechanism this refines)
Recommendation: CANDIDATE
Confidence: 58
Evidence: Confirmed present verbatim in source's own README/docs (REPO-012 audit,
Dimension E) — single source, moderate-confidence dimension verdict, does not meet
the STRONG CANDIDATE bar alone.

---

### PAT-014

Pattern Name: Sequence-aware tool-call chain evaluation (not just per-call)
Problem Solved: Catches a multi-step evasion where no single tool call looks
dangerous in isolation, but the sequence of calls together accomplishes something a
policy would have blocked if it saw the whole picture.
Observed In: REPO-012 (agentward — `PolicyEngine.evaluate_chaining(source_skill,
target_skill)`)
Mechanism: In addition to evaluating individual tool calls, the engine separately
evaluates transitions/sequences between calls, tracking call-sequence state
specifically for this purpose (not general agent memory).
Required Conditions: A policy engine that already has a per-call interception point
(PAT-010) to extend with sequence awareness; some notion of call-sequence state to track
against.
Strengths: A genuinely differentiated mechanism beyond simple per-call allow/deny —
confirmed by direct source read, not inferred from a feature list.
Weaknesses: Single-source finding. The audited source's maintenance signal is weak
(last commit 2026-04-28, ~4 months stale as of the audit — a material downgrade from
the original triage's "active" characterization) and its license is Business Source
License 1.1 (proprietary until 2028-04-24, not simply MIT as commercial reuse would
require before then) — both real adoption frictions independent of mechanism
quality.
Failure Modes: Sequence-tracking state itself becomes a new attack surface or
source of false positives if not carefully scoped (e.g. two legitimate, unrelated
tasks whose calls interleave and are misread as one evasive chain).
Complexity: Medium-High — requires session/state tracking beyond a stateless
per-call check, a real step up in implementation complexity from PAT-010 alone.
Token/Cost Implications: None direct (deterministic code).
Human-Control Implications: Indirect — strengthens the reliability of the policy
layer (PAT-010) that approval/permission decisions (PAT-011, PAT-012) ultimately depend on,
rather than being itself a human-facing control.
Hermes Relevance: DOM-08 — most relevant if Hermes' tool surface grows complex
enough that single-call policy checks stop being sufficient, which is not
established as a current need.
Alternative Patterns: PAT-010 (parent mechanism)
Recommendation: CANDIDATE
Confidence: 48
Evidence: Confirmed by direct source read (Dimension A verdict: Strong for the
mechanism itself), but single-source, stale maintenance signal, and a real license
restriction all weigh against a STRONG CANDIDATE rating despite sound code.

---

### PAT-015

Pattern Name: Confidence-threshold-to-handler escalation pipeline
Problem Solved: Turns "the model isn't confident about this output" into a concrete,
differentiated action (not just a flag) — different confidence failure types route
to different remediation handlers rather than one generic "ask a human" catch-all.
Observed In: REPO-013 (ashutoshrana/confidence-escalation — `score() -> evaluate() ->
dispatch() -> call()` pipeline driven by a `ThresholdPolicy`, four distinct
`EscalationHandler` subclasses: `HumanInLoopHandler`, `ModelUpgradeHandler`,
`ToolRestrictionHandler`, `ComplianceLoggingHandler`)
Mechanism: A `ConfidenceScorer` computes a 0.0-1.0 score from one or more scoring
methods (logprob, verbalized confidence, semantic consistency, tool-call risk, or a
composite); a middleware layer evaluates that score against a threshold policy and
dispatches to a specific handler type — escalating to a human is only one of four
possible responses, alongside upgrading to a stronger model, restricting available
tools, or just logging for compliance.
Required Conditions: The underlying model/runtime must be able to produce or
approximate a per-call confidence signal (logprob access, or a verbalized-confidence
prompt pattern) — not free in every deployment.
Strengths: The four-handler differentiation is more sophisticated than a binary
"escalate or don't" — routing low confidence to a model upgrade rather than always a
human pause is a genuinely useful degree of freedom. Real async-native implementation
(`AsyncConfidenceEscalationMiddleware`) and six framework adapters as separate real
files, not a single-framework demo.
Weaknesses: Every signal type this scorer computes is a MODEL-confidence signal (how
sure the model is about its own output) — none of them measure TASK ambiguity
(missing required field, conflicting user intent), which is DOM-09's actual research
question, not DOM-10's. Zero adoption signal (0 stars, 0 forks, solo author,
~3-month-stale commit as of audit) — sound code, no external validation.
Failure Modes: Poorly calibrated confidence signals (a known general LLM weakness)
can both under-trigger (false confidence skips needed escalation) and over-trigger
(constant escalation, defeating the purpose); routing to `ModelUpgradeHandler`
assumes a cost/quality model hierarchy is already available and configured.
Complexity: Medium — the pipeline itself is modest, but building a reliable,
calibrated confidence signal in the first place is a real, separate engineering
problem this pattern does not solve.
Token/Cost Implications: Direct — a `ModelUpgradeHandler` response by definition
increases per-call cost by escalating to a more expensive model; relevant to DOM-16
(cost/model routing) as a cross-cutting concern, not just DOM-10.
Human-Control Implications: Provides a graduated, non-binary alternative to "always
ask a human" — but only for model-confidence failures, not ambiguity failures (see
Weaknesses).
Hermes Relevance: DOM-10 (primary — closest real-code match found in Stage -2.3/-2.4
to a working confidence-threshold-to-escalation trigger). Secondary/cross-cluster:
DOM-16 (the ModelUpgradeHandler routing choice — see Cluster D's PAT-027).
Alternative Patterns: PAT-016 (the DOM-09 ambiguity-focused equivalent — deliberately
NOT the same mechanism, see Weaknesses)
Recommendation: CANDIDATE
Confidence: 55
Evidence: Confirmed by direct source read of all four handler classes and the
scorer/middleware pipeline (Dimension E verdict: Strong for DOM-10). Held at
CANDIDATE rather than STRONG despite sound, well-tested code because it is a
single source with zero external adoption signal — the mechanism-quality bar is met,
the "high confidence" bar for a lone source is judged not met given the total
absence of any outside validation.

---

### PAT-016

Pattern Name: Multi-factor risk/ambiguity gate with assess-before-generate ordering and rolling-history context
Problem Solved: Directly implements the raw idea's "under ambiguity, the system stops
and asks; it does not guess" principle as an enforceable architectural ordering
(assess first, act only after) rather than a soft prompt instruction, using more than
a single message in isolation to judge risk.
Observed In: SKL-012 (Human Gate Designer — DAG-workflow gate-placement decision
tree: irreversibility, cost threshold, confidence threshold, task ambiguity), SKL-027
(Crisis Detection Intervention AI — multi-signal detection -> tiered severity ->
mandatory human-flag), SKL-028 (Crisis Response Protocol — `assessCrisisLevel()` run
strictly BEFORE response generation, using current message + conversation history +
a 7-day check-in window, not the single message alone)
Mechanism: Two independently-original mechanisms converge on the same underlying
structure. SKL-012 evaluates a DAG node's output against named thresholds
(irreversibility, >$0.50 cost, <0.7 confidence, ambiguity) to decide whether to place
a gate at all, then presents contextual information (prior state, highlighted
decision, metrics) with three routing outcomes: approve / modify (re-execute with
injected feedback) / reject (at node/phase/full-abort granularity). SKL-027/028
(a tightly-coupled pair, treated as one source-family) run a similar risk assessment
but structurally *before* any response is generated at all — using a rolling history
window, not just the triggering message — and apply a hard rule ("never automate
past a positive detection") rather than a soft threshold. The composite pattern for
Hermes is: assess risk/ambiguity using more than the single current input, BEFORE
generating or acting, against named (not vague) thresholds, with a non-binary
response set (not just allow/deny).
Required Conditions: The runtime must support an assessment step that can run to
completion and be inspected before any generation/action step begins — a runtime
that generates and acts in one inseparable pass cannot easily adopt the
"assess-before-generate" half of this pattern.
Strengths: This is the best-evidenced convergent finding in the entire Stage
-2.2/-2.5 pass for DOM-09 — two genuinely independent original domains (generic
DAG-workflow tooling vs. mental-health crisis intervention) arrived at structurally
similar answers, which is real corroborating signal, not just one vendor's design
choice repeated (independently corroborated a third time by Cluster E's finding —
social-media-agent's "unknown human response routes back to the human node rather
than guessing" mechanism, PAT-033 — a third, structurally-unrelated domain reaching
the same "ask again on ambiguity" design). The non-binary response set
(approve/modify/reject-by-granularity from SKL-012; continue/check-in/resource-
display/protocol-response/emergency-escalate from SKL-028) avoids the "everything
either proceeds or fully blocks" failure mode of a naive gate.
Weaknesses: SKL-012's specific thresholds ($0.50, 0.7 confidence) are stated as
illustrative examples, not empirically validated constants — would need Hermes-
specific tuning. SKL-012 assumes the agent already emits calibrated per-action
confidence and cost estimates, which is itself a real, unverified dependency (see
PAT-015's identical calibration-risk note). SKL-027/028's clinical indicator taxonomy is
explicitly NOT reusable — only the structural ordering and hard-rule-vs-soft-
threshold distinction transfers; Hermes' own ambiguity categories (unclear brand fit,
controversial claim, wrong-page cross-post) would need original derivation.
Failure Modes: Poorly calibrated confidence/cost signals cause both under- and
over-triggering (identical risk to PAT-015, same root cause — LLM confidence
miscalibration is a cross-cutting weakness of every threshold-based gate found in
this research). Over-importing SKL-027/028's 5-tier granularity where a simpler
2-tier "ask or don't" would suffice for Hermes v1 (explicitly flagged as an open
right-sizing question, not resolved here).
**Explicit exclusion, carried forward from Stage -2.2 and re-confirmed here: do NOT
adapt SKL-027's 30-day auto-delete data-retention policy — it directly conflicts
with DOM-11's never-delete principle (see PAT-021). This exclusion applies to the composite
pattern's Required Conditions as much as to SKL-027 alone; nothing about combining
it with SKL-012 changes this.**
Complexity: Medium — the decision-tree/threshold logic itself is not complex; the
real cost is building trustworthy confidence/cost signals to feed it (shared
dependency with PAT-015) and, for the assess-before-generate half, potentially
restructuring the execution loop to support a hard pre-generation assessment step.
Token/Cost Implications: Low for the assessment step itself (a decision tree, not a
separate model call, in SKL-012's design); SKL-027/028's use of a rolling 7-day
history window implies a real context-retrieval cost if adapted literally, scalable
down for Hermes' actual needs.
Human-Control Implications: This pattern is a direct, structural implementation of
two of the raw idea's three named behavioral principles simultaneously — ambiguity
triggers a stop (DOM-09) and the gate itself is the irreversible-action confirmation
mechanism (DOM-07) — assessed with more context than a single message, before
anything is generated.
Hermes Relevance: DOM-09 (primary), DOM-07 (secondary — the gate-placement half
overlaps directly with PAT-011's approval-coordinator, this pattern determines *when*
that gate should trigger, PAT-011 is the code plumbing that a triggered gate runs
through).
Alternative Patterns: PAT-011 (approval-coordinator plumbing), PAT-015 (the DOM-10 sibling
pattern using the same threshold-gating concept for model-confidence rather than task
-ambiguity), PAT-017 (gate content/format design, complementary)
Recommendation: STRONG CANDIDATE
Confidence: 68
Evidence: Stage -2.2 completed full adversarial review and role-simulation notes for
all three skills individually (SKL-012 solo; SKL-027/028 jointly) — summarized and
extended here for the composite pattern. Two independently-original source domains
corroborate the same structural mechanism, satisfying the >=2-independent-source bar
for STRONG CANDIDATE even though no single source is a deep-audited repo (all
evidence is skill-catalog-level, Medium Evidence Quality per Stage -2.2, which caps
how high Confidence can reasonably be set here — held at 68, not higher, for that
reason).

Adversarial Review (Section 13) — synthesized from Stage -2.2's per-skill reviews,
re-verified as still applicable to the composite:
Q1 (assumptions): Calibrated confidence/cost signals (SKL-012) and a well-studied,
severity-classifiable signal space (SKL-027/028) — neither is automatically true for
Hermes; both would need original work, not just adoption of the decision structure.
Q2 (failure modes for Hermes): Same calibration-miscalibration risk as PAT-015; risk of
over-importing clinical tier-granularity or SKL-012's illustrative thresholds as if
they were validated constants.
Q3 (complexity introduced): Moderate to adapt the tiering/escalation structure;
building the actual ambiguity-signal detection underneath it is a separate, larger
Hermes-specific research/build problem this pattern does not solve.
Q4 (lock-in): None — pure decision-structure pattern, no framework or vendor
dependency.
Q5 (evidence missing): All three sources are single-vendor skill documentation
(SomeClaudeSkills), not independently deep-audited code — real-world crisis-protocol
practice outside the skill packaging is independently well-evidenced, which is
unusual corroboration for a skill-catalog-only source, but the skill's own
*packaging* has not been code-verified the way a repo audit would.
Q6 (simpler competing approach): A flat binary "ask or don't ask" rule, matching the
raw idea's literal simplicity, may be sufficient for Hermes v1 — the multi-tier
system is a refinement to evaluate for right-sizing, not an assumed requirement.
Q7 (marketing vs. engineering): Real, carefully-scoped engineering in both original
domains; the risk is over-import of unnecessary tier granularity, not hollow
marketing claims.

Role Notes (Section 14):
- Repository/Skill Auditor: Structurally the most rigorous escalation mechanism found across both Stage -2.2
  and -2.4 combined — explicit hard-rule plus graduated severity plus
  non-binary routing, all inspectable in the skills' documented method (not just
  named in a title). Verdict: Strong, with the auto-delete exclusion carried
  forward as a hard constraint on any adaptation.
- Reliability Reviewer: The assess-before-generate ordering constraint
  (from SKL-028) is the single most valuable, narrowly-scoped takeaway here —
  recommend it be treated as a standalone architectural requirement for Hermes'
  execution loop regardless of how the rest of the tiering system is right-sized.
- Skeptic: Attempted rejection: combining a DAG-workflow gate-design
  skill with a clinical crisis-intervention skill risks over-engineering DOM-09 with
  imported complexity the raw idea's simple "stop and ask" principle doesn't call
  for. Counter (same as Stage -2.2's original finding): the hard-rule-plus-
  assess-first *structure* is exactly what the raw idea demands; tier granularity is
  optional and can be simplified to 2 tiers without losing the structural property.
  Rejection attempt does not succeed against the composite pattern; the objection is
  preserved as a right-sizing note for Phase -1, not resolved here.

---

### PAT-017

Pattern Name: Gate format calibrated to task novelty (DO-CONFIRM vs. READ-DO) with bounded "killer-item" checklist content
Problem Solved: Answers not just *when* a human-control gate should trigger (PAT-016)
but *what it should actually check* once triggered, and how confident to be that a
gate's content is any good — using an externally-validated methodology rather than
an ad hoc "add a review step."
Observed In: SKL-030 (Checklist Discipline — DO-CONFIRM for experts/routine tasks vs.
READ-DO for novel/unfamiliar tasks; 5-9 "killer items" per pause point; iterative
real-user testing before trust is placed in a checklist), SKL-012 (Human Gate
Designer — pause-point placement at irreversibility/point-of-no-return, contextual
presentation design)
Mechanism: Rather than a single generic review-step format, the gate's format is
selected based on how familiar/routine the task is: a well-understood, frequently-
repeated action gets a lightweight DO-CONFIRM checklist (verify from memory/glance);
an unusual or first-of-its-kind action gets a full READ-DO walkthrough (step through
explicitly, don't rely on memory). Checklist content itself is capped at 5-9 items
specifically to avoid the checklist-bloat failure mode, and is not trusted until
iteratively refined against real usage (5-10 refinement cycles in the source
methodology).
Required Conditions: Some way to classify a given gated action as routine/familiar
vs. novel/unfamiliar to select the format; a feedback loop to actually iterate a
checklist's content against real outcomes rather than authoring it once and never
revisiting it.
Strengths: SKL-030 has the strongest Evidence Quality basis found in the entire
Stage -2.2 skill pass — grounded in independently-verifiable, externally-documented
real-world outcomes (WHO Safe Surgery Checklist trial results, the Boeing 299 origin
case, Pronovost's central-line infection protocol), not the skill vendor's own
unverified claims. The 5-9-item cap is a self-correcting design feature against
checklist bloat, not a risk to import blindly.
Weaknesses: SKL-030's original method assumes human-team dynamics (verbal
confirmation, physical "forcing functions") that don't directly apply to a
solo-owner-plus-agent system — the core mechanism (pause-point placement, killer-item
extraction, format selection) transfers; the team-coordination implementation
details need real reinterpretation, not a literal port. SKL-012's specific
thresholds carry the same "illustrative, not validated" caveat noted in PAT-016.
Failure Modes: A checklist authored once and never iterated against real outcomes
loses SKL-030's core evidentiary strength — the mechanism's value depends on the
refinement discipline being actually followed, not just the initial design.
Complexity: Low-Medium — this is primarily a design methodology, not new
infrastructure; the real cost is the iterative validation discipline, which is a
process commitment more than an engineering one.
Token/Cost Implications: None direct — this shapes what a human sees at a gate
already established by PAT-011/PAT-016, not a new model-driven step.
Human-Control Implications: Directly strengthens gate quality for whichever gates
Hermes adopts (PAT-011's plumbing, PAT-016's trigger logic) — this pattern is specifically
about making sure a gate, once triggered, actually catches what it's supposed to
catch, evidenced by real historical error-prevention outcomes outside the skill
vendor's own claims.
Hermes Relevance: DOM-07 (primary), DOM-15 (cross-cluster — pre-publish
quality-gate content design; see Cluster D's PAT-031).
Alternative Patterns: PAT-011 (plumbing), PAT-016 (trigger logic) — this pattern is
deliberately the third, complementary leg (content/format), not a competing
mechanism.
Recommendation: STRONG CANDIDATE
Confidence: 72
Evidence: SKL-030's real-world corroboration (external clinical/aviation trial
outcomes, independently documented outside the skill's own packaging) is unusually
strong for a skill-catalog source — satisfies the "high confidence" alternate bar
for STRONG CANDIDATE even without a second deep-audited repo source, per Stage
-2.2's own Evidence Quality: High rating for this skill specifically (the single
highest in that pass).

Adversarial Review (Section 13) — synthesized from Stage -2.2, re-verified:
Q1 (assumptions): Assumes team/verbal-confirmation dynamics designed for human
teams — needs deliberate reinterpretation for a solo-owner + AI-agent structure
(what replaces "state your name/role aloud" or a physical forcing function?).
Q2 (failure modes for Hermes): Checklist bloat if the 5-9-item discipline isn't
actually enforced; a checklist trusted without the source methodology's iterative
real-use validation loses its evidentiary basis entirely.
Q3 (complexity introduced): Moderate and real — the method insists on 5-10
refinement cycles with actual usage before trust is warranted; this is a genuine
process cost, not a one-shot copy-paste.
Q4 (lock-in): None — pure methodology, no framework dependency.
Q5 (evidence missing): None significant relative to other candidates in this
cluster — this is the best-evidenced single source found in the whole skill pass.
Q6 (simpler competing approach): An unstructured "have a human look at it" (Hermes'
implicit baseline) is simpler but has none of this method's demonstrated
error-catching rigor — this pattern strengthens what the baseline checks, it doesn't
replace a simpler alternative with a more complex one for no gain.
Q7 (marketing vs. engineering): Genuine, externally-grounded methodology.

Role Notes (Section 14):
- Repository/Skill Auditor: Real-world grounding is independently
  checkable (documented historical interventions, not the skill author's own
  assertions) — the strongest-evidenced single source in the cluster. Verdict:
  Strong.
- Reliability Reviewer: The DO-CONFIRM vs. READ-DO distinction is a
  genuinely useful reliability concept specifically for Hermes — routine publish
  actions (e.g. a recurring content type to an established page) could use
  DO-CONFIRM, while a first-of-kind action (first post to a brand-new page) should
  force READ-DO. Recommend this distinction be carried into any DOM-07 gate design
  explicitly, not left implicit.
- Skeptic: Attempted rejection: this may be over-engineered for a
  solo-owner system — checklists with verbal team confirmation assume multiple
  humans, which Hermes doesn't have. Counter: only the "forcing function"/verbal-
  confirmation implementation details need reinterpretation; the core mechanism
  (pause-point placement, killer-item extraction, format choice by novelty) doesn't
  require multiple humans and benefits a solo owner over an unstructured review.
  Rejection attempt does not succeed; candidate survives as STRONG with the noted
  reinterpretation required.

---

### PAT-018

Pattern Name: Urgency-tiered owner-notification escalation
Problem Solved: Gives a human owner cheap, calibrated visibility into agent activity
without either flooding them with routine updates or burying a genuinely urgent one
among routine noise — a precondition for the owner being willing to reduce
involvement over time (DOM-10) rather than a substitute for it.
Observed In: SKL-019 (Liaison — 4-tier urgency framework: Immediate [build failures,
security issues, blocking decisions] / Same-Day [milestones, opportunities] / Weekly
[trends, low-priority decisions] / Archive Only [routine/expected outcomes], paired
with 5 communication templates by message type)
Mechanism: Rather than a flat notification stream, every reportable event is
classified into one of four urgency tiers up front, and routed/timed accordingly —
an Immediate-tier event interrupts, a Weekly-tier one gets batched, an Archive-tier
one is recorded but not surfaced as a notification at all.
Required Conditions: A classification step that can reliably sort events into these
tiers — misclassification (treating something Immediate as Weekly, or vice versa)
defeats the entire point.
Strengths: A real, concrete tiering scheme rather than a vague "keep the owner
informed" statement — genuinely addresses the specific problem of making reduced
owner involvement (DOM-10) safe rather than reckless, by making sure the owner still
sees the things that matter, cheaply.
Weaknesses: Single-source finding, no independent corroboration. The original
information-gathering layer is entirely software-dev-specific (git/npm/build status)
and would need substantive retargeting to a content/social-ops context (post status,
publish queue, research findings) — not a drop-in mechanism. The 4-tier bucketing is
coarser than PAT-016's more granular, named-threshold approach to a related problem
(deciding when to gate an action, vs. this pattern's concern of deciding when to
notify about one) — see also Cluster C's PAT-025, a related human-facing digest
pattern with its own 6-stage weighted-index alternative.
Failure Modes: Miscalibrated tier assignment either causes owner fatigue (too much
in Immediate/Same-Day) or missed important events (too much folds into Weekly/
Archive) — the tiering logic itself needs the same calibration discipline as any
threshold-based mechanism in this cluster (shared risk with PAT-015/PAT-016).
Complexity: Low — a classification-and-routing scheme, not new infrastructure.
Token/Cost Implications: Minimal.
Human-Control Implications: This is a notification/visibility pattern, not an
approval gate — it does not block or require confirmation of anything by itself; it
is what makes trusting an agent with less real-time oversight (DOM-10) tenable,
complementary to but distinct from PAT-011/PAT-016's gating mechanisms.
Hermes Relevance: DOM-10 (primary), DOM-14 (cross-cluster — owner-visibility
infrastructure; see Cluster C's PAT-025).
Alternative Patterns: PAT-015, PAT-016 (related threshold/tiering concepts applied to
different decisions — escalating a low-confidence action vs. notifying about a
completed one)
Recommendation: CANDIDATE
Confidence: 50
Evidence: Confirmed present in the skill's documented method (Stage -2.2, Evidence
Quality: Medium, single source) — real and concrete, but no independent corroboration
and a real domain-retargeting gap, so held below the STRONG CANDIDATE bar.

---

## Cluster C — State, Memory & Reliability (DOM-11, 12, 13, 14)

Sources read: `jshiv-cronicle.md`, `getzep-graphiti.md`,
`nousresearch-hermes-agent.md` (REPO-001), `hermes-agent-capability-reference.md`,
plus skill-catalog.md records SKL-014, SKL-019, SKL-023, SKL-029; research-domains.md
DOM-11 through DOM-14 definitions.

### PAT-019 — Authoritative Event Log + Disposable Derived Projection

Pattern Name: Authoritative Event Log + Disposable Derived Projection
Problem Solved: Lets a system rebuild fast-queryable state cheaply while
keeping one clearly-designated store as the source of truth, so operators know
which store must never be lost and which can be wiped/rebuilt freely.
Observed In: REPO-016 (jshiv/cronicle) — Dimension A, FACT, code-verified.
Mechanism: cronicle writes an append-style JSONL event log
(`cronicle.jsonl`) documented in-code as authoritative, and separately
maintains a SQLite "state plane" whose own package doc states it is a
"retention-windowed... projection" that "rebuilds from event ingest" — i.e.
explicitly disposable. The separation is declared in code comments, not just
inferred from behavior.
Required Conditions: The team must actually treat the "authoritative" side
as inviolable in practice (see Weaknesses) — the pattern's value depends
entirely on that store never being subject to silent loss.
Strengths: Clean mental model (one store = truth, one store = cache);
lets the cache be freely dropped/rebuilt for performance or corruption
recovery without any data-loss risk, since it's reconstructable.
Weaknesses: The label "authoritative" is a design intent, not a structural
guarantee — see Failure Modes. Nothing in the pattern itself prevents the
"authoritative" store from also being subject to rotation/deletion, which is
exactly what was found in cronicle's own implementation (PAT-021).
Failure Modes: cronicle's own "authoritative" `cronicle.jsonl` is, by the
same codebase's design, subject to lumberjack rotation with `MaxAge: 28`
days — i.e., the thing the architecture calls authoritative is deleted after 28
days by default. This is the single clearest illustration in this cluster
that declaring a store "authoritative" in docs/comments does not make it
immutable; the retention policy on the authoritative side must be checked
independently, every time, per instance.
Complexity: Low — the split itself is a simple architectural convention,
not a new subsystem.
Token/Cost Implications: None directly; indirectly enables cheaper
queries against the derived projection instead of replaying the full log.
Human-Control Implications: An owner auditing "what happened" needs to
know which store they're looking at — if they inspect the disposable
projection after it's been rebuilt, they may see an incomplete picture with
no indication anything is missing.
Hermes Relevance: DOM-11 (directly — this is the shape a compliant
append-only history store would take) and DOM-13 (the projection-rebuild
mechanism is itself a lightweight recovery strategy).
Alternative Patterns: PAT-021 (names the specific way this pattern's
"authoritative" side can quietly fail); PAT-022 (a different mechanism —
non-destructive invalidation inside one store — for the same underlying
never-lose-history goal).
Recommendation: CANDIDATE — the architectural idea is sound and directly
relevant to DOM-11, but the one real-world instance found does not itself
satisfy Hermes' never-delete principle without modification (the
"authoritative" log must be made genuinely non-rotating/non-deleting, which
cronicle's own implementation is not). Not rated STRONG CANDIDATE because the
single available instance is also this pattern's own best cautionary example.
Confidence: 70 — mechanism is code-verified FACT; the caveat is equally
code-verified FACT, not speculation.
Evidence: `jshiv-cronicle.md` Dimensions A and D; `internal/cronicle/log.go:397-404`,
`internal/cronicle/state/store.go` package doc (both cited verbatim in the audit file).

---

### PAT-020 — Per-Subsystem Staged Write-Approval Gate (Foreground vs. Autonomous Origin)

Pattern Name: Per-Subsystem Staged Write-Approval Gate
Problem Solved: Lets a system distinguish writes made during an
interactive/foreground turn from writes an autonomous background process
decided to make on its own, and hold the latter for review before they take
effect.
Observed In: REPO-001 (NousResearch/hermes-agent), `tools/write_approval.py`
— FACT, code-verified.
Mechanism: Writes to memory/skills subsystems are staged as pending
records under `<HERMES_HOME>/pending/{memory,skills}/<id>.json` rather than
applied immediately; the gate explicitly distinguishes interactive
(foreground) writes from a `background_review` autonomous self-improvement
fork's writes. The module's own docstring names `background_review` as "the
source of the 'wrong assumptions' users complained about" — i.e. this gate
was built in direct response to a real observed failure mode, not
speculatively. (This is the same underlying mechanism Cluster A's PAT-004
references from the pause-and-resume angle — PAT-020 is its full extraction.)
Required Conditions: Needs an actual review/approval step downstream
(human or otherwise) that consumes the pending queue — the gate only creates
the checkpoint, it doesn't by itself guarantee anyone looks at it.
Strengths: Origin-aware (not just "gate everything" — distinguishes risk
by where the write came from); built from a named real incident, not
theoretical; per-subsystem scoping (memory vs. skills) rather than one
global gate.
Weaknesses: **Ships disabled by default** — "`false` (default) — write
freely (the pre-gate behaviour)." A stock deployment gets none of this
protection unless an operator explicitly turns it on.
Failure Modes: Because the gate is off by default, the exact incident it
was built to prevent (autonomous background writes based on wrong
assumptions) is the default behavior of an unconfigured instance — the fix
exists in the codebase but does not protect anyone who doesn't know to
enable it.
Complexity: Low-Medium — file-based staging queue, no new infrastructure
required.
Token/Cost Implications: Negligible.
Human-Control Implications: Directly implements a real approval-gate
primitive for DOM-07, but only if Hermes' deployment configuration
explicitly enables `write_approval` — this is an operational discipline
Hermes must enforce (via config template or a fork), not something the base
architecture guarantees on its own. This is the exact "ships mechanism,
defaults off" theme also found at PAT-021, PAT-046-050's REPO-001 findings,
and Cluster F's PAT-048/PAT-051.
Hermes Relevance: DOM-07 (approval gates, primary — directly complements
Cluster B's PAT-011/PAT-016/PAT-017) and DOM-11 (it gates memory *writes*
specifically, so it's a partial control point for history integrity, though
it does not address deletion at all).
Alternative Patterns: None found this pass with the same
origin-distinguishing property (foreground vs. autonomous-background).
Recommendation: CANDIDATE — real, well-motivated mechanism, but "adopt
this and turn it on" is a configuration decision Hermes must make and
enforce, not something inherited safely by default.
Confidence: 75 — directly code-verified, single high-confidence
deep-audited source.
Evidence: `nousresearch-hermes-agent.md` Dimension B; `tools/write_approval.py`.

---

### PAT-021 — Time-Gated Auto-Deletion of Session/Transcript/Log History

Pattern Name: Time-Gated Auto-Deletion of Session/Transcript/Log History
Problem Solved: Bounds unbounded disk growth from accumulating
session/transcript/log data by permanently removing data older than a
retention window.
Observed In: REPO-001 (NousResearch/hermes-agent) `hermes_state.py`,
`maybe_auto_prune_and_vacuum(retention_days=90)`; REPO-016 (jshiv/cronicle)
`internal/cronicle/log.go`, lumberjack `MaxAge: 28`. Two independent
deep-audited sources, both FACT, both code-verified.
Mechanism: A background/startup routine permanently deletes database
rows and/or on-disk log files older than a fixed retention window. In
REPO-001 this is `prune_sessions()` removing ended sessions plus their
`.json`/`.jsonl`/`request_dump_*` transcript files after 90 days of
inactivity; in cronicle it's lumberjack's `MaxAge`-based rotation deleting
`cronicle.jsonl` backups after 28 days.
Required Conditions: None — this is the default architectural instinct
for any system that logs continuously without an explicit retention
exemption.
Strengths: Solves a real, legitimate problem (disk growth) simply and
predictably.
Weaknesses: Directly and unconditionally destructive — there is no
soft-delete, archival, or export step; data is gone. In both observed
instances the deleted data is exactly the kind of history/audit-trail
content Hermes' never-delete principle is meant to protect (REPO-001:
session transcripts; cronicle: its own documented "authoritative" log, see
PAT-019).
Failure Modes: For Hermes specifically: this is a direct structural
conflict with the explicitly named behavioral principle "the system never on
its own deletes anything from memory/history." In REPO-001 the mechanism is
off by default (`auto_prune: false`), so a stock deployment does not violate
the principle today — but it is one config change away from doing so, with
no structural guardrail preventing that config change. In cronicle, the
rotation-delete is the default, unconditional behavior with no opt-out
found in this pass.
Complexity: Low — this is the simple/naive solution, which is exactly
why it recurs independently in two unrelated codebases.
Token/Cost Implications: None directly; this is a disk-management
mechanism, not a token-cost one.
Human-Control Implications: Maximal — this is a self-initiated deletion
mechanism operating without per-instance human confirmation. For Hermes,
this pattern must be either (a) never enabled and structurally prevented
from being enabled (config lock / fork — see Cluster F's PAT-048), or (b)
replaced entirely with a non-destructive alternative (archival, cold
storage, or the invalidation approach in PAT-022) before any component
resembling it is allowed near history data.
Hermes Relevance: DOM-11 — this is the single most concrete, precisely
named gap this cluster found for that domain. Confirms and sharpens the
Stage -2.2/-2.3 finding that no discovered source directly solves DOM-11;
this pattern instead documents the failure mode DOM-11 exists to prevent.
Alternative Patterns: PAT-022 (bi-temporal invalidation) is a genuine
non-destructive alternative for the "aging fact/state" problem, though not a
drop-in replacement for pruning raw transcript/log files specifically.
Recommendation: AVOID — as a default posture, this pattern must not be
inherited. Recording it is valuable specifically because it names, with two
independent code-verified instances, the exact shape of mechanism Hermes
must guard against inheriting from its fixed base architecture (REPO-001)
and must not reintroduce if building any custom log-rotation logic.
Confidence: 90 — two independent deep-audited FACT-level sources,
consistent mechanism, low ambiguity.
Evidence: `nousresearch-hermes-agent.md` Dimension C (`hermes_state.py`
line ~14375, `gateway/run.py` line ~7188); `jshiv-cronicle.md` Evidence
Section (`internal/cronicle/log.go:397-404`).

---

### PAT-022 — Bi-Temporal Fact Invalidation over Destructive Update

Pattern Name: Bi-Temporal Fact Invalidation over Destructive Update
Problem Solved: Lets a memory system represent "this fact was true, then
became false" without ever overwriting or deleting the original record —
preserving the full history of what the system believed and when, not just
its current belief state.
Observed In: REPO-017 (getzep/graphiti) — Dimension C, FACT, code-verified.
Mechanism: Edge (fact) records carry `expired_at`, `valid_at`,
`invalid_at` timestamp fields (`graphiti_core/edges.py:271-277`,
serialization confirmed at lines 352-354, 998-1000). A contradicted or
updated fact is marked invalid/expired via these fields rather than
overwritten or removed — both the old and new belief states remain queryable
against a point in time.
Required Conditions: A graph (or equivalent structured entity/edge)
data model; willingness to take on a graph-database dependency (Neo4j,
FalkorDB, Kuzu, or Neptune in Graphiti's case — 4 independent driver
implementations confirmed, so the dependency is at least backend-agnostic).
Strengths: Directly demonstrated, code-verified non-destructive handling
of contradictory information — a stronger, more precise mechanism than
"just never call delete" because it has an explicit answer for what happens
when new information contradicts old, which a pure append-only log doesn't
resolve on its own.
Weaknesses: The same codebase that implements this also exposes real,
first-class hard-delete methods: `EntityEdge.delete()`,
`delete_by_uuids()` (implemented across all 4 backends), and — most
significantly — `Graphiti.remove_episode()` as a public, documented,
top-level API method (`graphiti_core/graphiti.py:1765`), not an internal
test-cleanup utility. The non-destructive behavior is Graphiti's default for
*contradiction-handling*, not a structural guarantee that nothing can ever
be deleted.
Failure Modes: If adopted as a component or comparison baseline without
an explicit integration-boundary decision to disable/never-call the
hard-delete API surface, a caller (human or agent) could permanently remove
history through a fully supported, documented path. The safety property
lives at the call-site discipline, not in the library's structure.
Complexity: Medium — bi-temporal fields are a straightforward schema
addition, but a graph-database backend is real infrastructure to run and
maintain.
Token/Cost Implications: Query patterns over a temporal graph can be
more expensive than flat-log scans for some access patterns; not quantified
this pass.
Human-Control Implications: Strong for the specific problem of "what did
the system believe over time" (a genuine audit/trust asset for DOM-14
alongside DOM-11) — but only if the coexisting delete API is fenced off by
policy or wrapper, which is a Hermes-side integration decision, not
something Graphiti enforces.
Hermes Relevance: DOM-11 (non-destructive fact-update mechanism, primary)
and DOM-12 (a graph substrate is a plausible way to maintain narrative/entity
continuity across sessions beyond a single context window — the bi-temporal
fields let "what changed and when" be reconstructed for narrative
continuity, not just factual recall).
Alternative Patterns: PAT-019 (authoritative log split) is a simpler,
lower-infra alternative for the same underlying never-lose-history goal, at
the cost of not natively resolving contradictions.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes a graph database backend is acceptable
operational infrastructure; assumes facts decompose cleanly into
entity/edge triples rather than free-text or unstructured content.
Q2 (where it could fail for Hermes): If integrated naively, Hermes'
content- or research-agent could call `remove_episode()` or
`delete_by_uuids()` directly (they are ordinary public API methods) and
violate the never-delete principle without any structural block —
"non-destructive by default" is not "non-destructive by construction."
Q3 (complexity introduced): A graph-database dependency (deployment,
backup, query language, operational monitoring) is nontrivial
infrastructure for a system that does not yet have one.
Q4 (lock-in): Bi-temporal semantics and graph-query patterns create
conceptual lock-in; migrating to a different memory substrate later means
re-deriving equivalent temporal guarantees elsewhere.
Q5 (evidence missing): Test suite exists (`tests/`) but its size/coverage
was not assessed this pass (Dimension F: Unconfirmed); no production-scale
adoption evidence was gathered.
Q6 (simpler competing approach): PAT-019's flat authoritative-log split
achieves non-destructive history at far lower infrastructure cost, if
Hermes doesn't actually need graph-relationship queries over its history.
Q7 (marketing vs. engineering): The bi-temporal fields are verified
engineering, not marketing prose — but "graph memory" as a category is
frequently oversold industry-wide, and the fields alone do not
automatically deliver DOM-12's narrative-continuity goal, which is an
application-layer concern the schema merely makes possible, not automatic.

Role Notes (Section 14):
- Repository Auditor: The bi-temporal fields are directly read in source
  and match documentation exactly — high confidence this mechanism is real
  and not aspirational. The delete methods are equally real and present
  consistently across every backend, not a stray leftover.
- Reliability Reviewer: No retry/circuit-breaker layer was confirmed in
  `graphiti_core` itself this pass (Dimension D: Weak/Unconfirmed) — any
  durability guarantee for this pattern currently rests entirely on the
  chosen graph-driver's own reliability characteristics, which were not
  independently verified.
- Skeptic: The public `remove_episode()` API undercuts any framing of this
  mechanism as "safe by construction" for a never-delete requirement.
  Disagreement with the Repository Auditor's framing: the Auditor treats the
  invalidation mechanism as strong standalone evidence the *pattern* works;
  the Skeptic holds that the coexisting first-class delete API means this
  *specific implementation* cannot itself be trusted as a compliance
  boundary without an enforced wrapper — the reusable idea is sound, the
  library as-is is not a guarantee.

Recommendation: STRONG CANDIDATE — as a pattern (bi-temporal
invalidation as the answer to "how do you update a fact without destroying
history"), not as an endorsement of adopting Graphiti wholesale without a
delete-API fence.
Confidence: 72 — high confidence in the mechanism itself (code-verified,
single deep-audited source, Dimension C rated Strong); confidence tempered
below 80 by the Skeptic's unresolved objection about the coexisting
delete API and the unconfirmed reliability layer.
Evidence: `getzep-graphiti.md` Dimension C and Evidence Section;
`graphiti_core/edges.py:271-277,352-354,710,843,998-1000`;
`graphiti_core/graphiti.py:1765`.

---

### PAT-023 — DAG-Scheduled Task Execution with Wired Hard Budget-Abort

Pattern Name: DAG-Scheduled Task Execution with Wired Hard Budget-Abort
Problem Solved: Runs unattended, recurring, dependency-ordered work
reliably, while guaranteeing a runaway task cannot silently exceed its
assigned cost budget.
Observed In: REPO-016 (jshiv/cronicle) — Dimensions A and D, FACT,
code-traced end-to-end; REPO-001 (NousResearch/hermes-agent) — Dimension D,
FACT (crash-safety engineering), UNKNOWN (full cron contract doc unread this
pass). Two independent deep-audited sources.
Mechanism: cronicle: HCL-declared tasks with explicit `depends_on` DAG
edges (`internal/cronicle/dag.go`), cron- or listener-triggered
(`cron.go`/`listen.go`); automatic downstream-skip on upstream failure; a
per-task `BudgetUSD` traced end-to-end from config
(`config.go:151-153`) through execution (`exec.go:321`) to a hard abort in
the agent runner (`pkg/agent/agent.go:318-320`, `ErrBudgetExceeded` raised
when `currentCost > cfg.BudgetUSD`) — independently code-verified, not a
docs claim. REPO-001: an internal cron subsystem
(`cron/scheduler.py`, `jobs.py`, `executions.py`, `lifecycle_guard.py`,
`monitor.py`) plus unusually detailed SQLite crash-safety engineering in the
shared state layer (WAL checkpoint discipline, with inline comments citing a
specific past production incident — a `TRUNCATE` checkpoint strategy that
"caused B-tree corruption on large concurrent-access databases," since
replaced with `PASSIVE` — see PAT-024).
Required Conditions: Tasks must be expressible as a (mostly) static
dependency graph known ahead of execution; per-task cost must be meterable
in real time to compare against a budget.
Strengths: The budget-abort path is unusually well-evidenced — traced
through three separate files/layers, not just claimed in one place.
Crash-safety engineering in REPO-001 is grounded in a named real incident,
not aspirational hardening.
Weaknesses: cronicle's own claimed "distributed mode" (SQLite-durable
job queue) was explicitly NOT independently verified this pass — flagged
UNKNOWN, not confirmed. REPO-001's dedicated architecture doc for this
subsystem (`docs/chronos-managed-cron-contract.md`) was not read in full —
its actual crash-recovery *contract* (what's guaranteed vs. best-effort) is
still unknown.
Failure Modes: A genuinely dynamic/emergent task graph (an agent
deciding its next action based on live results, rather than a pre-declared
DAG) does not fit this model without translation — this pattern suits
scheduled/recurring work better than open-ended autonomous task chains.
Unverified "distributed mode" claims should not be relied upon without a
dedicated follow-up audit.
Complexity: Medium — a DAG scheduler plus budget wiring is a real
subsystem, not a one-file utility; REPO-001's SQLite crash-safety layer in
particular reflects nontrivial hard-won engineering.
Token/Cost Implications: This pattern's entire second half (BudgetUSD
abort) is directly a cost-control mechanism — one of the few in this
cluster's evidence with a fully traced enforcement path (contrast with
REPO-001's separate billing subsystem, Dimension G, which is UNKNOWN
whether it enforces or only reports — a Cluster D concern; see PAT-028 and
PAT-051, which independently confirm the same open question).
Human-Control Implications: A hard abort on budget overrun is a
legible, predictable safety rail an owner can trust without watching every
run. Crash-safety engineering reduces the odds of silent data corruption
requiring manual owner intervention.
Hermes Relevance: DOM-13 (primary — this is exactly the
scheduling/reliability substrate question DOM-13 asks about REPO-001) and
DOM-16 (the budget-abort half is directly a cost-control mechanism).
Alternative Patterns: SKL-029 (Background Job Orchestrator, skill
catalog) — a conventional queue+worker+dead-letter-queue pattern
(BullMQ/Celery/SQS) is a simpler-to-reason-about alternative for teams
already running that infra, at the cost of an extra infra dependency
cronicle's single-binary design avoids. Not rated as its own pattern record
here since it's a well-known standard pattern (per SKL-029's own Evidence
Quality: "standard/well-known, not novel") rather than a distinctive
mechanism worth a dedicated entry.

Adversarial Review (Section 13):
- Q1: Assumes tasks decompose into a mostly-static DAG known ahead of time,
  and that per-task cost is meterable in real time.
- Q2: REPO-001's own crash-recovery *contract* (what it actually guarantees)
  remains unread/UNKNOWN — treating Dimension D's "Strong" verdict as
  covering the full cron subsystem's reliability, rather than just the
  state-layer crash-safety evidence it's actually based on, would overstate
  confidence.
- Q3: REPO-001's cron subsystem complexity (5 separate modules) was not
  independently traced for correctness this pass, only confirmed to exist.
- Q4: cronicle's mechanism requires either a Go runtime or reimplementation
  to reuse directly; REPO-001 is already the fixed substrate so no
  additional lock-in there, but that also means Hermes cannot "choose" this
  half of the pattern independently of adopting REPO-001 as a whole.
- Q5: cronicle's "distributed mode" claim is explicitly unverified; do not
  cite it as evidence of durable multi-node execution.
- Q6: SKL-029's queue+worker+DLQ pattern is simpler and more familiar to
  teams already on conventional backend infra.
- Q7: The budget-abort claim is verified engineering (traced through three
  files); the "distributed mode" claim is closer to a docs/marketing claim
  not yet backed by independent verification.

Role Notes (Section 14):
- Repository Auditor: Budget-abort (cronicle) and WAL crash-safety
  engineering (REPO-001) are both FACT-level, code-confirmed — high
  confidence in the mechanisms as narrowly described.
- Reliability Reviewer: cronicle's distributed-mode claim and REPO-001's
  full cron crash-recovery contract are both open/unverified — this pattern
  should not be cited as proof of "durable execution across restarts" for
  either repo without a dedicated follow-up read of
  `docs/chronos-managed-cron-contract.md`.
- Skeptic: Combining two different repos with different scopes (cronicle:
  a general-purpose task scheduler; REPO-001: Hermes' actual fixed
  substrate) into one pattern record risks implying they are
  interchangeable. They are not — REPO-001's own crash-recovery contract is
  the operative one for Hermes; cronicle is a comparison/best-practice
  reference only, not something literally adopted, since the base
  architecture is already fixed.

Recommendation: STRONG CANDIDATE (as a comparison-baseline pattern for
evaluating REPO-001's actual cron subsystem, per the domain reframing — not
as a suggestion to adopt cronicle itself).
Confidence: 65 — tempered from higher due to the two flagged UNKNOWNs
(cronicle's distributed-mode claim; REPO-001's unread crash-recovery
contract doc) both bearing directly on this pattern's reliability claims.
Evidence: `jshiv-cronicle.md` Dimensions A, D; `nousresearch-hermes-agent.md`
Dimension D; `hermes-agent-capability-reference.md` "Scheduling / Cron" section.

---

### PAT-024 — WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed Agent State

Pattern Name: WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed
Agent State
Problem Solved: Prevents database corruption under concurrent
cron-triggered access to a single SQLite-backed state store.
Observed In: REPO-001 (NousResearch/hermes-agent), `hermes_state.py` —
Dimension D, FACT, code-verified, citing a named real production incident.
Mechanism: Explicit choice of `PRAGMA wal_checkpoint(PASSIVE)` over
`TRUNCATE`, with inline code comments documenting that a `TRUNCATE`
checkpoint strategy previously "caused B-tree corruption on large
concurrent-access databases" in production and was replaced; lock-contention
handling for concurrent cron-triggered connections; idempotent
throttled auto-maintenance (`min_interval_hours` gating on
`maybe_auto_prune_and_vacuum`, separate from that function's retention
concern — see PAT-021).
Required Conditions: Only applies to SQLite-backed state under
concurrent access — narrow and technology-specific.
Strengths: Grounded in a named, specific past incident rather than
generic best-practice — this is hard-won engineering knowledge, not
speculative hardening.
Weaknesses: Extremely narrow scope (one database engine's checkpoint
semantics); not a general pattern applicable regardless of what state
backend Hermes ends up using.
Failure Modes: If Hermes inherits REPO-001's SQLite state layer
(likely, since it's the fixed base architecture) without inheriting this
specific checkpoint discipline (e.g., during a future fork/patch of
`hermes_state.py` for the DOM-11 auto-prune concern in PAT-021), the same
corruption class could resurface.
Complexity: Low — a narrow, specific configuration/discipline choice,
not a new subsystem.
Token/Cost Implications: None.
Human-Control Implications: Prevents a class of silent data corruption
that would otherwise require manual owner intervention to diagnose and
recover from.
Hermes Relevance: DOM-13 (crash-recovery/reliability) — narrowly but
directly, since Hermes' state layer is inherited from REPO-001 as-is unless
explicitly changed.
Alternative Patterns: None found this pass at this level of
specificity.
Recommendation: CONTEXT-DEPENDENT — directly relevant only if/when
Hermes' actual technology choices are confirmed to retain REPO-001's
SQLite-backed state layer (likely, but not yet a Phase -2 decision to make).
If any future fork or patch touches `hermes_state.py`'s checkpoint logic
(e.g. to address PAT-021), this specific discipline must be preserved, not
just the retention-window number changed.
Confidence: 80 — narrow, code-verified, single high-confidence
deep-audited source; not downgraded for source count since the claim is
narrow enough that a single direct code read is sufficient evidence.
Evidence: `nousresearch-hermes-agent.md` Dimension D.

---

### PAT-025 — Urgency-Tiered Human-Facing Status Digest

Pattern Name: Urgency-Tiered Human-Facing Status Digest
Problem Solved: Gives a human owner cheap, non-intrusive visibility into
autonomous-agent activity without requiring them to watch every action —
the specific visibility mechanism that makes reduced owner involvement safe
rather than reckless.
Observed In: SKL-019 (Liaison), SKL-023 (Skill Logger) — both
skill-catalog records, Evidence Quality Medium (single source each, per
Stage -2.2 records), not independently deep-audited as code this pass.
SKL-014 (Logging & Observability) provides the infra-logging substrate
underneath but explicitly does NOT itself address the human-facing framing
(see Weaknesses). (SKL-019 also underlies Cluster B's PAT-018 — that record
covers its urgency-tiering mechanism from the DOM-10 trust-calibration
angle; this record covers the same skill plus SKL-023 from the DOM-14
observability angle. Not a duplicate: different mechanisms emphasized.)
Mechanism: SKL-019: 5 communication templates (Status Briefing, Decision
Request, Celebration Report, Concern Alert, Opportunity Summary) selected via
a 4-tier urgency-escalation framework (Immediate / Same-Day / Weekly /
Archive Only). SKL-023: a 6-stage pipeline (Capture, Analyze, Score,
Aggregate, Alert, Improve) with a 4-weighted-dimension quality index
(Completion 25% / Efficiency 20% / Output Quality 30% / Satisfaction 25%)
and threshold-based alerting (quality decline >20%, error-rate doubling,
usage drop >50%).
Required Conditions: Needs an underlying activity/event log to draw
from (see PAT-019, PAT-023) — this pattern is the human-facing digest layer on
top of raw logs, not a replacement for having logs.
Strengths: Both mechanisms are concrete and directly transferable in
structure (urgency tiers; weighted quality index) even though their source
domains (software-project status; skill-invocation analytics) differ from
Hermes' content/research-agent context.
Weaknesses: Both are software-project-specific in their current form
(SKL-019 gathers git/build/npm state; SKL-023 tracks skill invocations) and
would need real retargeting to content pieces, publish events, and research
findings. Neither has been deep-audited as running code — both are
Claude Skill definitions (prompt/instruction-level), Medium evidence
quality, single source each, unknown maintenance signal. SKL-019's 4-tier
urgency bucketing is coarser than some comparison mechanisms found
elsewhere in this research (e.g. SKL-012 Human Gate Designer's more
granular threshold gating — PAT-016).
Failure Modes: A digest layer this coarse could either under-alert
(genuinely concerning autonomous action classified as "Weekly" or "Archive
Only") or over-alert (routine action pushed to "Immediate," training the
owner to ignore alerts) if the urgency-classification logic isn't tuned
carefully to Hermes' actual risk profile.
Complexity: Low-Medium — template selection plus threshold logic, no
new infrastructure.
Token/Cost Implications: Digest generation adds periodic LLM calls
(or templated non-LLM formatting) proportional to activity volume, not
per-action.
Human-Control Implications: This is the core mechanism DOM-14 is about
— it directly operationalizes "give the owner cheap visibility without
requiring them in the loop for every action." Its quality is only as good
as the urgency classification underneath it, which here is a documented
starting point, not a finished mechanism (per SKL-019's own Stage -2.2
reasoning summary).
Hermes Relevance: DOM-14 (primary) and DOM-10 (trust-calibration —
enables reduced involvement over time by keeping the visibility cost low).
Alternative Patterns: SKL-014 provides the infra-logging layer this
pattern would sit on top of, but does not itself solve the human-facing
framing problem — it was explicitly scored ADAPT with the domain-specific
assumption flagged: "does NOT address DOM-14's specific reframed need."
Recommendation: CANDIDATE — real, concrete, directly on-target
mechanisms, but neither is deep-audited code, both need real retargeting
work, and the underlying urgency-classification logic is acknowledged even
in its own source record as a starting point rather than a finished
mechanism. Not STRONG CANDIDATE: two sources exist but both sit at Medium
evidence quality with unknown maintenance signal, which does not amount to
the "high confidence" bar the single-source path requires, and the
two-source path's sources are not independent enough in evidence strength
to compensate.
Confidence: 55 — reflects the Medium/Medium evidence quality of both
underlying sources, not the clarity of the mechanism itself.
Evidence: `skill-catalog.md` SKL-014, SKL-019, SKL-023.

---

## Known Gap, Confirmed Not Resolved (Cluster C)

**DOM-11** still has no repository or skill in this research's entire
discovery set that *directly solves* append-only/audit-log architecture as
its stated purpose — consistent with the identical finding at Stage -2.2 and
Stage -2.3. What this cluster's pass adds is sharper: two independent,
code-verified negative examples (PAT-021) naming exactly the failure mode DOM-11
guards against, plus two partial/adjacent mechanisms (PAT-019, PAT-022) that could
inform a Hermes-specific solution but do not themselves constitute one
off-the-shelf. This should be carried into Stage -2.6/-2.7 as a documented
gap requiring Hermes-specific design work, not resolved by any candidate
found in Phase -2.

---

## Cluster D — Evaluation, Cost & Security (DOM-15, 16, 17)

Sources read: repo-audits/{berriai-litellm, nvidia-nemo-guardrails,
the-pr-agent-pr-agent, nousresearch-hermes-agent, hermes-agent-capability-reference}.md;
skill-catalog.md SKL-015/016/017/025/030/031; deduplication-map.md Cluster 2;
research-domains.md DOM-15/16/17.

### PAT-026 — Pre-Call Blocking Budget Enforcement

Pattern Name: Pre-Call Blocking Budget Enforcement
Problem Solved: Preventing an LLM call from ever executing once a spend ceiling is
reached, rather than only detecting the overspend after the fact.
Observed In: REPO-022 (litellm — code-verified), SKL-015 (Cost Optimizer),
SKL-025 (Cost Accrual Tracker) — independent design convergence on the same
mechanism from a deep-audited repo and an unrelated skill-catalog source family.
Mechanism: A hook fires *before* the model call is dispatched (litellm:
`_PROXY_MaxBudgetLimiter.async_pre_call_hook`, `litellm/proxy/hooks/max_budget_limiter.py`,
raises `ProxyRateLimitError` and blocks — code-verified, not just documented). Budget
scope is layered (per-key/team/org/model/session — litellm has 4 distinct
budget-scope hook files) with periodic resets (`reset_budget_job.py`) for
rolling windows. SKL-015 generalizes this as a percentage-remaining waterfall
(>20% normal / 10-20% downgrade / <5% halt-unless-critical) — same "gate before
spend" shape, expressed as tiers instead of a binary block.
Required Conditions: A defined budget/spend ceiling per scope; a call path with a
single chokepoint where the hook can intercept before the provider request is sent.
Strengths: Enforcement is structural, not a policy the caller has to remember to
check — an agent literally cannot spend past the cap through this path. Layered
scopes (per-key/team/model/session) let a single deployment express nuanced
budget policy rather than one global number.
Weaknesses: Only as strong as the chokepoint's coverage — any call path that
bypasses the hook (a second provider integration, a raw HTTP fallback) escapes
enforcement entirely. Waterfall tiering (SKL-015) trades hard cutoffs for softer
degradation, which is friendlier but reintroduces a judgment call ("is this node
on the critical path?") that a pure block does not have.
Failure Modes: (1) New call path added later that doesn't route through the
budget hook — silent enforcement gap, not a crash, so it can go unnoticed. (2)
Budget-reset job failure/drift could either wrongly block a fresh period or
wrongly let a stale window's spend leak into the new one — litellm's dedicated
`reset_budget_job.py` exists specifically because this needs its own reliability
handling, not just the enforcement hook. (3) Tiered/waterfall degrade-instead-of-block
(SKL-015) can silently trade away output quality under budget pressure unless the
"critical path" exemption logic is itself audited — directly relevant to Hermes'
stated tension between the cost and quality constraints (DOM-16 research question).
Complexity: Medium — requires a real chokepoint architecture (all calls funnel
through one interceptable point), not just a counter.
Token/Cost Implications: This IS the cost-control mechanism; no meaningful
token overhead of its own (a synchronous pre-call check).
Human-Control Implications: A block/halt event should be visible to the owner
(not just silently dropped) — none of the sources reviewed specify how a human
is notified when the ceiling is hit; this is left to the deployment, and Hermes
would need to add it explicitly if this pattern is adopted, since "the agent
went silent because budget hit zero" is a bad default failure mode for a
solo-owner system with no team to notice.
Hermes Relevance: DOM-16 — this is the closest thing found to a *comparison
baseline* for hermes-agent's own cost mechanism. hermes-agent's own
`agent/billing_usage.py`/`billing_view.py`/`usage_pricing.py`/`aux_accounting.py`
were confirmed to exist (REPO-001 Dimension G) but whether they *enforce* (block/cap)
or only *track/report* is UNKNOWN pending a read of `docs/billing-lifecycle.md` —
this pattern is the concrete shape that "enforcement" would need to take if
hermes-agent's billing subsystem turns out to be report-only (see PAT-028 below,
and Cluster F's PAT-051, which independently confirms the same open question from
a different pair of repos).
Alternative Patterns: PAT-027 (routing as a softer cost-control lever), PAT-028
(hermes-agent's own unconfirmed mechanism), PAT-029 (composable pipeline framing).
Recommendation: STRONG CANDIDATE
Confidence: 85
Evidence: litellm code-verified (REPO-022, Dimension D, direct read of
`max_budget_limiter.py` lines 73/80 — `raise`/block confirmed, not inferred from
docs) + independently arrived-at same shape in SKL-015/025 (different source,
different original domain — DAG pipeline cost governance vs. LLM API gateway).
Two independent sources, one code-verified — satisfies Gate G5's STRONG CANDIDATE
citation requirement.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes a single, complete request chokepoint exists. Assumes
budget scope boundaries (key/team/session) map cleanly onto however Hermes
structures its own multi-page/multi-profile operation.
Q2 (failure modes for Hermes): If Hermes ever calls a model provider from more
than one code path (e.g., a fast-path shortcut that bypasses the normal agent
loop), the enforcement gap in Weaknesses above becomes real, not hypothetical.
Q3 (complexity introduced): Real but proportionate — this is infrastructure
Hermes needs regardless of source, since "cost control is a serious constraint,
not a secondary concern" is an explicit hard requirement from the raw idea.
Q4 (lock-in): None if adopted as a pattern (the mechanism, not litellm itself);
some lock-in if litellm-the-proxy is adopted wholesale as infrastructure.
Q5 (evidence missing): Whether litellm's budget-reset job (`reset_budget_job.py`)
has itself been stress-tested for the drift failure mode named above — not
traced this pass.
Q6 (simpler competing approach): A single global spend counter checked
manually before each batch of work is simpler but reintroduces exactly the
"policy the caller has to remember to check" weakness this pattern exists to
avoid — not a real substitute for a solo-owner system that wants to trust the
guardrail unattended.
Q7 (marketing vs. engineering): Engineering — verified via direct source-line
citation (litellm), not vendor copy. SKL-015's mechanism is well-specified
(concrete thresholds, function-level description) though its own evidence
quality is only Medium (single skill-catalog source, no independent
corroboration for the skill itself — the corroboration here is architectural
convergence with litellm, not a second citation of SKL-015 specifically).

Role Notes (Section 14, required for this Strong Candidate):
- Repository Auditor: litellm's enforcement claim is the strongest
  code-verified finding in this entire cluster — raises/blocks confirmed at
  specific line numbers, not inferred. Highest-confidence source in Cluster D.
- Reliability Reviewer: The budget-reset-job failure mode (Q5/failure
  mode 2) is the one piece of this pattern that has NOT been independently
  verified as reliable — flag as an open item if litellm-proxy itself (not just
  the pattern) is ever considered for adoption, not just the abstract pattern.
- Skeptic: Attempted rejection — is a hard block even desirable for
  Hermes, given the co-equal "quality over throughput" constraint? A hard halt
  mid-task could leave content generation stranded incomplete. Counter: the
  pattern as observed already supports graduated response (litellm's own
  layered scopes; SKL-015's waterfall) — a hard global halt is one *option*
  within the pattern, not the only shape it can take. Rejection does not
  succeed; candidate survives as STRONG CANDIDATE with the graduated-response
  nuance carried into Hermes Relevance.

---

### PAT-027 — Task-Classified, Multi-Strategy Cost-Aware Model Routing

Pattern Name: Task-Classified, Multi-Strategy Cost-Aware Model Routing
Problem Solved: Choosing which model tier handles a given task so that cheap
tasks don't pay premium-model prices, without a human manually assigning a
model per call.
Observed In: REPO-022 (litellm `router_strategy/`, code-verified — 10 distinct
strategy files: lowest_cost, lowest_latency, lowest_tpm_rpm[_v2], least_busy,
simple_shuffle, tag_based_routing, budget_limiter, plus adaptive_router/,
auto_router/, complexity_router/, quality_router/ subpackages), SKL-016 (LLM
Router — task-type classification into 3 tiers, 3 progressive strategies:
static / cascading-try-cheap-first / adaptive-after-~100-executions).
Mechanism: Two complementary approaches converge on the same goal by different
means. litellm: pluggable routing-strategy family selected per deployment,
driven by live signals (cost, latency, queue depth) rather than a single fixed
rule — `LowestCostLoggingHandler.async_get_available_deployments` selects a
deployment from logged spend data, a real algorithm not a config flag. SKL-016:
classifies the *task* first (classify/validate/write/reason/architect) into a
tier (Haiku/Sonnet/Opus-class), then picks provider by latency/compliance, with
a feedback loop that recalibrates after ~100 executions.
Required Conditions: Multiple model tiers/providers actually available to
route between; for SKL-016's adaptive strategy, enough execution volume (~100+)
to make the feedback loop meaningful — not useful at very low volume.
Strengths: litellm's multi-strategy plugin family means the routing policy
itself is swappable without redesigning the call path — a genuinely modular
mechanism, code-confirmed (Dimension A "Strong" verdict, 10 real strategy
files). SKL-016's task-first classification directly addresses Hermes'
specific tension (cost is a hard constraint, quality is co-equal) by trying to
match task difficulty to model cost rather than uniformly downgrading.
Weaknesses: SKL-016's specific "45-85% savings / 95%+ quality" figures are
self-asserted marketing claims, not independently verified (Section 12.1
discipline — noted, not relied on for this record's confidence). Task
classification is itself a judgment call that can misfire (an apparently
"simple" task that is actually nuanced gets routed to a weak model) — this is
the exact quality-vs-cost tension DOM-16's research question names, not solved
by this pattern, only structured by it.
Failure Modes: Misclassification silently degrades output quality without an
explicit error (a wrong-tier routing doesn't fail loudly, it just produces a
worse draft) — this interacts badly with Hermes' "quality over throughput" hard
constraint unless paired with a downstream quality gate (see PAT-031/Cluster B's
approval-gate patterns) that would catch a bad draft regardless of why it's bad.
Complexity: Medium (litellm's plugin approach) to Medium-High (SKL-016's
adaptive/feedback-loop strategy, which needs execution-history storage).
Token/Cost Implications: This is the direct cost-control mechanism; the
routing decision itself is cheap (a classification step), the savings come
from where the *actual* work then gets sent.
Human-Control Implications: Neither source exposes a human-visible "why was
this routed to the cheap tier" explanation by default — for a system with a
hard quality constraint, Hermes would likely want routing decisions to be
inspectable/loggable, not just effective, so a human can audit whether cost
pressure is silently eroding quality over time.
Hermes Relevance: DOM-16 — same comparison-baseline role as PAT-026. hermes-agent
itself was not confirmed (REPO-001, this cluster's audit) to have an
equivalent task-classification routing layer — `hermes model`/`hermes moa`/
`hermes fallback` CLI commands exist (capability-reference doc) for
manual/preset model selection and fallback-on-error, but no evidence was found
of task-difficulty-based automatic tiering analogous to litellm/SKL-016. This
is a candidate gap for Stage -2.6, not a resolved finding — the CLI commands
found describe user-configured presets and error-triggered fallback, not
automatic per-task cost/quality-aware routing.
Alternative Patterns: PAT-026 (blocking vs. routing as the lever), PAT-028
(hermes-agent's own unconfirmed mechanism).
Recommendation: STRONG CANDIDATE
Confidence: 75
Evidence: litellm code-verified (REPO-022, Dimension A, 10 real strategy files
confirmed via direct directory/file read) + SKL-016 (skill-catalog, Medium
evidence quality, marketing figures explicitly discounted per Section 12.1 but
underlying task-classification mechanism assessed as sound independent of
those figures). Two independent sources.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes task difficulty is classifiable ahead of the actual
work — true for well-understood task types, less true for genuinely novel
content requests.
Q2 (failure modes for Hermes): Misclassification-driven silent quality
degradation (see Failure Modes) is the primary risk, specifically because it's
silent rather than a hard error.
Q3 (complexity introduced): Real — a classification layer plus (for the
adaptive variant) execution-history storage and recalibration logic.
Q4 (lock-in): None as an abstract pattern; litellm-as-infrastructure would
introduce a proxy-layer dependency if adopted wholesale rather than as a
pattern to reimplement.
Q5 (evidence missing): SKL-016's savings/quality percentages, explicitly (already
discounted, not used in scoring — restated here per Section 13 discipline).
Whether litellm's adaptive/complexity_router subpackages (named but not opened
this pass) actually implement task-difficulty classification the way SKL-016
describes, or something narrower — flagged as an open follow-up, not assumed.
Q6 (simpler competing approach): A single fixed "always use the mid-tier
model" policy is simpler and avoids misclassification risk entirely, at the
cost of forgoing any savings on genuinely simple tasks — a real, simpler
alternative worth naming, not obviously inferior for a low-volume solo-owner
system where the adaptive strategy's ~100-execution warm-up may never be reached.
Q7 (marketing vs. engineering): Mixed — litellm's routing-strategy plurality is
engineering (code-verified); SKL-016's specific savings claims are marketing
and explicitly excluded from this record's confidence basis.

Role Notes (Section 14, required for this Strong Candidate):
- Repository Auditor: litellm's strategy plugin family is real and
  more extensive than Stage -2.3's docs-only triage suggested (10 files, not a
  vague "supports routing" claim) — upgraded confidence on direct read.
- Reliability Reviewer: The silent-misclassification failure mode
  is the material risk here, precisely because nothing in either source
  surfaces a routing decision for human review by default — recommend this be
  carried forward as an explicit requirement (routing decisions should be
  logged/inspectable) if Stage -2.6 advances this pattern.
- Skeptic: Attempted rejection — for a low-volume solo-owner
  content pipeline, is task-classified routing even worth the complexity over
  a single fixed model choice? Counter: the explicit co-equal cost/quality
  constraint from the raw idea specifically motivates this — the Owner named
  cost control as "a serious constraint, not a secondary concern," which a
  single-fixed-model policy does not address at all. Rejection does not
  succeed for Hermes' stated constraints, though the Skeptic's simpler
  alternative (Q6) is preserved as a legitimate lower-complexity fallback if
  volume never justifies the adaptive variant.

---

### PAT-028 — Reported-Only Cost Tracking (Confirmed Tracking, Unconfirmed Enforcement) — Gap Pattern

Pattern Name: Reported-Only Cost Tracking (Confirmed Tracking, Unconfirmed Enforcement)
Problem Solved: N/A — this is not a recommended mechanism but a named
anti-pattern/gap worth distinguishing from PAT-026, because "has cost tracking"
and "has cost enforcement" are frequently conflated and REPO-001 is the
concrete case where that conflation risk is live.
Observed In: REPO-001 (nousresearch-hermes-agent — `agent/billing_usage.py`,
`billing_view.py`, `usage_pricing.py`, `aux_accounting.py` confirmed to exist
by direct code presence; `docs/billing-lifecycle.md` confirmed to exist by
name but not read in full this pass).
Mechanism: A real, structured usage/cost-tracking subsystem exists (module
names and the `hermes insights` CLI command both point at tracking/analytics),
but no pre-call blocking hook or budget-ceiling enforcement code analogous to
PAT-026's litellm mechanism was found in the audit's targeted search. This is
UNKNOWN, not confirmed absent — the module names ("billing_usage", "usage_pricing",
"aux_accounting") read as tracking/accounting terminology rather than
enforcement terminology, which is the basis for treating this as a live risk
worth naming rather than a settled gap. (Cluster F independently found the
identical gap shape in REPO-041's Swarm Map budget-check mechanism — see
PAT-051 — two structurally unrelated repos exhibiting the same "computes
budget/exceeded but no confirmed enforcement call site" pattern.)
Required Conditions: N/A (this is a gap description).
Strengths: N/A.
Weaknesses: The core weakness this pattern names: a system can report
accurate cost data while still silently overspending, because reporting and
blocking are architecturally separate concerns (PAT-026 shows the mechanism that
closes this gap; nothing in REPO-001's audited code confirms that mechanism is
present).
Failure Modes: If Hermes is built on stock hermes-agent and assumes "there's a
billing subsystem" means "spend is capped," it could overspend against the
DOM-16 hard constraint without any code failure at all — the tracking would
faithfully report the overspend after it already happened.
Complexity: N/A.
Token/Cost Implications: Directly the subject of this gap — the open question
is whether hermes-agent's own cost mechanism actually controls token/cost
spend or only measures it after the fact.
Human-Control Implications: If enforcement is in fact absent, a human (the
Owner) is the only backstop against overspend on a stock deployment — same
"ships mechanism off/absent by default, relies on operator discipline" theme
already flagged as a cross-cutting REPO-001 finding (see PAT-020, PAT-021,
PAT-048).
Hermes Relevance: DOM-16, directly — this is the central open question for
whether hermes-agent's base architecture satisfies Hermes' cost-control hard
constraint out of the box, or whether Hermes needs to add an enforcement layer
akin to PAT-026/PAT-027 on top.
Alternative Patterns: PAT-026 (the enforcement mechanism this gap lacks, if the
gap is confirmed real).
Recommendation: INSUFFICIENT EVIDENCE
Confidence: 40
Evidence: REPO-001 Dimension G (Moderate-Weak, provisional verdict, explicitly
UNKNOWN pending a read of `docs/billing-lifecycle.md` and the billing modules'
actual logic) + REPO-001's own "Open Follow-Ups" list, item 2, names this
exact question as unresolved. Not resolved by this pattern-extraction pass
either — carried forward as an open question, not guessed at.

---

### PAT-029 — Composable Cost-Governance Pipeline (Capture -> Enforce -> Route -> Verify)

Pattern Name: Composable Cost-Governance Pipeline (Capture -> Enforce -> Route -> Verify)
Problem Solved: Building cost governance as separable stages that can be
adopted incrementally or swapped independently, rather than one monolithic
cost-control component.
Observed In: SKL-025 (Cost Accrual Tracker — capture stage), SKL-015 (Cost
Optimizer — enforce stage), SKL-016 (LLM Router — route stage, invoked by
Optimizer's downgrade action), SKL-031 (Cost Verification Auditor — verify
stage, closes the loop back onto Accrual Tracker's data). Architecturally
corroborated by REPO-022 (litellm), which independently keeps its own
budget-enforcement hooks (`max_budget_limiter.py` family) and routing
strategies (`router_strategy/`) as separate files/modules rather than one
combined component — the same separation-of-concerns shape, arrived at
independently in a real production codebase.
Mechanism: Four distinct responsibilities, each with a narrow function-level
API in the skill-catalog design: `recordUsage()`/`getCurrentCost()`/`finalize()`
(capture) feeds a percentage-remaining waterfall (enforce) that on "downgrade"
invokes task-classified routing (route), while a variance-check loop
(±20% threshold, 40% per-node tolerance) validates the capture layer's
estimates stay accurate over time (verify) — this is already documented in
`phase-m2/deduplication-map.md` Cluster 2 as an intentionally-not-collapsed
complementary pipeline, not competing implementations.
Required Conditions: A system with enough call volume/complexity that a single
combined cost-tracking function becomes unwieldy; less useful at very small scale.
Strengths: Each stage is independently testable/replaceable; a system could
adopt just the capture+enforce stages (PAT-026-equivalent) without the
routing/verify stages, or add stages incrementally.
Weaknesses: Four separate components is real integration surface — more moving
parts than a single combined tracker, with more places for the stages to drift
out of sync with each other if not deliberately kept coherent.
Failure Modes: The verify stage (SKL-031) existing as a separate, optional
component means a deployment could adopt capture+enforce+route without it and
have no mechanism to catch cost-estimate drift over time — the loop only
closes if all four stages are actually wired together.
Complexity: Medium — four components, but each individually simple; the
composability is the point.
Token/Cost Implications: Same as PAT-026/PAT-027 — this is the cost-control
mechanism itself, structured as a pipeline rather than one function.
Human-Control Implications: None of the four stages, as documented, surfaces a
human-facing summary/alert by default (parallels PAT-027's gap) — Hermes would
need to add reporting/visibility on top.
Hermes Relevance: DOM-16 — offers a structural template (how to decompose cost
governance into stages) rather than a single mechanism, useful if Stage -2.6
recommends building a cost layer on top of hermes-agent rather than relying on
its own billing subsystem (see PAT-028).
Alternative Patterns: PAT-026 (capture+enforce collapsed), PAT-027 (route in
isolation).
Recommendation: CANDIDATE
Confidence: 55
Evidence: Primary evidence is a single source family (4 skill-catalog records
from the same gallery, explicitly designed to reference each other — not
fully independent sources of each other). Architectural corroboration from
litellm's independent separation-of-concerns raises confidence above a bare
single-source rating, but not to STRONG CANDIDATE, since litellm corroborates
the *shape* (separate concerns) rather than this exact four-stage pipeline.

---

### PAT-030 — Dependency-Aggregation Guardrail Architecture (Flow-DSL Orchestration Over Specialized Detectors)

Pattern Name: Dependency-Aggregation Guardrail Architecture (Flow-DSL Orchestration Over Specialized Detectors)
Problem Solved: Providing broad content-safety/security coverage (jailbreak
detection, PII/sensitive-data detection, injection detection, topic safety,
fact-checking) without reimplementing each detection mechanism from scratch.
Observed In: REPO-024 (NVIDIA-NeMo/Guardrails — code-verified: ~28 independent
guardrail integration modules in `library/`, real Colang `.co` flow files
directly inspected, third-party integrations ActiveFence/CrowdStrike
AIDR/Llama Guard/Trend Micro/Patronus AI/Fiddler/Polygraf/Cleanlab/GLiNER
confirmed by directory structure).
Mechanism: A purpose-built DSL (Colang) describes conversation-level guardrail
flows rather than single-turn keyword filters; the actual detection work is
delegated to a plurality of specialized third-party/model-based detectors
plugged in through a common integration surface, with layered detection inside
at least one module (`jailbreak_detection/heuristics/` + `/model_based/` —
fast heuristic pass plus model-based fallback, a genuine two-tier design).
Required Conditions: Willingness to depend on and trust multiple third-party
detection vendors/models rather than a single homegrown check; a conversation
structure that Colang's flow model can wrap.
Strengths: Leverages best-in-class detectors per threat category instead of
one team reimplementing jailbreak detection, PII detection, and fact-checking
all from scratch — real architectural leverage, code-confirmed (Dimension A,
"Strong" verdict, actual `.co` files read).
Weaknesses: Trades implementation effort for integration-maintenance and
trust-in-third-parties overhead — every added integration is a new dependency
and a new thing to trust; this is a FACT about the tradeoff's existence
(confirmed via directory structure — 28+ integration modules is real surface
area), not a judgment on whether the tradeoff suits Hermes (Phase -2 does not
decide that).
Failure Modes: A detector vendor's own failure/downtime/API change could
silently degrade a guardrail flow that depends on it; the aggregation
architecture inherits whichever failure modes its component detectors have,
compounded by however many are wired into a given flow.
Complexity: Medium-High — Colang itself is a new DSL to learn (Dimension H,
"Moderate" verdict — clean conceptual separation but real learning-curve cost),
on top of configuring however many third-party integrations are adopted.
Token/Cost Implications: Not independently assessed this pass (each
model-based detector likely carries its own inference cost, additive to the
main agent's own calls — flagged as an open question, not measured).
Human-Control Implications: This is a content-safety guardrail layer, not a
human-approval mechanism (correctly distinguished from DOM-07 in the source
audit) — it operates automatically/pre-emptively rather than routing a
decision to a human, which is a different control philosophy than the
approval-gate patterns in Cluster B (PAT-011/PAT-016/PAT-017) and should not
be conflated with them when Stage -2.6 builds the capability matrix.
Hermes Relevance: DOM-17 (content-safety-guardrail half specifically — the
credential/secrets half of DOM-17 is separately covered by PAT-032 below). This
is the single most substantive DOM-17 content-safety candidate found across
Stages -2.3/-2.4 — no comparable guardrail-orchestration mechanism was found
elsewhere in this project's research.
Alternative Patterns: A from-scratch, single-provider guardrail implementation
(not separately catalogued — named here only as the architectural alternative
NeMo Guardrails itself was compared against in its own audit).
Recommendation: STRONG CANDIDATE
Confidence: 70
Evidence: Single deep-audited source (REPO-024), but high-confidence per the
audit's own dimension verdicts (A: Strong, I: Strong, J: Strong — Apache 2.0,
confirmed by direct file read) — satisfies Gate G5's alternative STRONG
CANDIDATE criterion ("one deep-audited source with high confidence") without
requiring a second independent source.

Adversarial Review (Section 13):
Q1 (assumptions): Assumes Hermes is willing to depend on multiple external
detection vendors/models rather than keep all safety logic in-house.
Q2 (failure modes for Hermes): Vendor-dependency failure modes named above;
also a real learning-curve cost (Colang) for a solo-owner-maintained system
with no dedicated team to absorb that cost.
Q3 (complexity introduced): Real and non-trivial — Medium-High per the
source audit's own Dimension H verdict, not minimized here.
Q4 (lock-in): Meaningful if Colang and the full integration surface are
adopted wholesale; much lower if only the *pattern* (aggregate specialized
detectors behind a common flow interface) is extracted and reimplemented
without Colang specifically.
Q5 (evidence missing): Token/cost overhead of the aggregated detectors,
not assessed this pass — a real gap for DOM-16/DOM-17 reconciliation.
Q6 (simpler competing approach): A single, narrower content-safety check
(e.g., one moderation API call before publish) is far simpler and avoids the
vendor-aggregation overhead entirely — plausibly sufficient if Hermes' actual
content-safety needs turn out to be narrower than the full breadth this
pattern is built for; this is a real, not strawman, competing approach given
Hermes' current solo-owner, moderate-scale framing.
Q7 (marketing vs. engineering): Engineering — the integration breadth and
Colang mechanism were confirmed via direct code/file inspection, not vendor
copy; the tradeoff cost (Weakness above) is stated as fact, not glossed over.

Role Notes (Section 14, required for this Strong Candidate):
- Repository Auditor: This is the strongest single-source
  candidate in Cluster D — every dimension touched came back Strong on direct
  inspection, no docs-vs-code disagreement found.
  Confidence in the *audit* is high; confidence in *fit for Hermes specifically*
  is more moderate (see Skeptic below), which is why this record's own
  Confidence field is 70, not 85+.
- Reliability Reviewer: Vendor-dependency failure modes (Q2) are
  the main reliability concern — an aggregation architecture is only as
  reliable as its weakest depended-on integration, and this was not
  stress-tested in the audit.
- Skeptic: Attempted rejection — for a single-owner, moderate-scale
  social content pipeline, is this much guardrail breadth (28+ integrations)
  proportionate, or over-built? Counter: the pattern itself is adoptable
  partially (a handful of integrations, or even the Colang flow-DSL concept
  alone without most integrations) — the architecture doesn't force
  all-or-nothing adoption. Rejection does not fully succeed, but the Skeptic's
  simpler-alternative (Q6) is preserved as a live, not dismissed, option for
  Stage -2.6 to weigh against this pattern's full breadth.

---

### PAT-031 — Advisory Critique-Before-Decision (Non-Blocking Structured Review)

Pattern Name: Advisory Critique-Before-Decision (Non-Blocking Structured Review)
Problem Solved: Surfacing structured, multi-dimensional critique of a draft
alongside a human's decision point, without itself controlling whether the
action proceeds.
Observed In: REPO-026 (the-pr-agent/pr-agent — code-verified: `auto_approve_logic()`
exists at line 630 but its invocation is commented out of the live `run()` path,
lines 150-152; the actual live path calls `publish_comment()`, posting a
structured review comment, not gating the merge).
Mechanism: A reviewer produces a structured, multi-facet assessment (configurable
dimensions: `require_score`, `require_tests`, `require_estimate_effort_to_review`,
`require_security_review`, `require_todo_scan` — confirmed in code, not a single
free-text critique) and posts it where the human will see it alongside the
artifact being judged (the PR diff), but does not block, require, or gate the
merge/publish action itself.
Required Conditions: A human decision point that already exists independently
(a merge button, a publish action) that the critique can sit alongside —this
pattern augments an existing human decision, it does not create one.
Strengths: Real, structured, multi-dimensional feedback (not a single
pass/fail) delivered at exactly the moment a human is about to decide;
incremental-review-state handling confirmed (avoids duplicate/stale comments
across revisions, Dimension D).
Weaknesses: **This is explicitly NOT an enforcement mechanism as observed** —
a correction to how this repo was characterized at Stage -2.3 (which described
it as "gating output before a human ever sees a draft"). Direct code reading
found the gate exists in source but is dead code on the live path. If Hermes
needs an actual pre-publish block (its raw idea names "explicit confirmation
for irreversible actions" as a recurring behavioral principle), this pattern
alone does not provide it — it must be paired with a real gate (Cluster B's
PAT-011/PAT-016/PAT-017).
Failure Modes: The most likely failure mode isn't in the mechanism itself but
in mischaracterizing it — treating "there's a review step" as equivalent to
"nothing gets published without approval" would be a real, load-bearing error
for a system with Hermes' stated irreversible-action-confirmation requirement.
Complexity: Low — a single reviewer class producing structured output and
posting a comment; no gating infrastructure required.
Token/Cost Implications: One structured-review LLM call per reviewed item;
cheap relative to a full gating pipeline since it doesn't need to hold up a
merge/publish queue.
Human-Control Implications: Directly instructive by negative example — this is
the "surface critique for human judgment" half of a human-control design,
explicitly not the "block until approved" half. DOM-15's research question
("how is content reviewed prior to the approval gate") is well-served by this
pattern as the review step; DOM-07's approval gate itself needs a separate
mechanism (PAT-011).
Hermes Relevance: DOM-15 directly (the review/critique step feeding into an
approval gate) — but must not be mistaken for DOM-07 (the gate itself). This
distinction is the single most reusable insight from this source, more than
the specific reviewer-config mechanism.
Alternative Patterns: Cluster B's PAT-011/PAT-016/PAT-017 (approval-gate
patterns) provide the actual blocking half this pattern lacks — together they
form a complete DOM-07/DOM-15 pipeline (surface critique, then gate on it).
Recommendation: CONTEXT-DEPENDENT
Confidence: 75
Evidence: Code-verified single source (REPO-026, Dimension E, exact line
numbers cited: `auto_approve_logic()` defined at line 630, invocation commented
out at lines 150-152) — high confidence in what the mechanism actually is;
CONTEXT-DEPENDENT rather than STRONG CANDIDATE because whether an
advisory-only critique is sufficient for Hermes depends entirely on whether
it's paired with a real gate elsewhere, which this source does not provide.

---

### PAT-032 — Entropy-Threshold Secret Detection

Pattern Name: Entropy-Threshold Secret Detection
Problem Solved: Catching accidentally-exposed platform API credentials/secrets
(the credential half of DOM-17) before they leak.
Observed In: SKL-017 (Security Auditor — skill-catalog only, not
cross-verified against a deep-audited repo this pass).
Mechanism: Pattern matching combined with entropy analysis (threshold >4.5 on
strings >20 characters) to flag likely secrets in source/config, as one stage
of a broader 4-stage scan (dependency CVE analysis, secret detection, OWASP
static analysis, dangerous-function detection).
Required Conditions: Access to the codebase/config files to scan; a defined
entropy threshold tuned to avoid excessive false positives on legitimately
high-entropy non-secret strings.
Strengths: Concrete, directly implementable technique (a specific threshold
and string-length cutoff, not a vague "scan for secrets" description).
Weaknesses: Single skill-catalog source, Medium evidence quality, not
independently corroborated; addresses only the credential/secrets half of
DOM-17 — explicitly does not address the content-safety-guardrail half (that's
PAT-030's territory), a documented gap in the source record itself. Note:
Cluster B's agentward `scan/` static pre-deployment dependency/toolchain
scanner (flagged in that cluster's Cross-Cluster Notes) was NOT independently
re-verified or extracted as its own pattern by this cluster's pass either —
carried forward below as an unresolved cross-cluster flag, not folded into
this record.
Failure Modes: Entropy-based detection can both miss low-entropy secrets
(e.g. a memorable but real password) and false-positive on high-entropy
non-secret strings (hashes, generated IDs) — a tuning problem, not resolved by
this record.
Complexity: Low — a scanning script/step, not an architectural change.
Token/Cost Implications: Minimal — a static scan, not an LLM-driven mechanism
by default (though could be paired with one for triage).
Human-Control Implications: Findings need a human review step regardless of
detection method — this pattern produces a report, not an autonomous
remediation.
Hermes Relevance: DOM-17, credential/secrets half only, directly relevant to
Hermes' multi-account social automation implying multiple real platform
credentials.
Alternative Patterns: None catalogued this pass for the credential half of
DOM-17.
Recommendation: CANDIDATE
Confidence: 55
Evidence: Single skill-catalog source (SKL-017), Medium evidence quality per
its own catalog record — insufficient sourcing for STRONG CANDIDATE under
Gate G5's two-independent-source-or-one-deep-audited-source rule (this is
neither).

---

## Cluster E — Social-Media Operations (DOM-03, 18, 19, 20, 21, 22)

Sources read in full: REPO-039 (langchain-ai/social-media-agent), REPO-036
(gitroomhq/postiz-app), REPO-033 (indranilbanerjee/digital-marketing-pro),
REPO-029 (GOAT-AI-lab/GOAT-Storytelling-Agent), REPO-030 (HKUDS/ViMax),
REPO-031 (ChrisChen667788/wind-comic), REPO-034 (ALwrity/ALwrity), REPO-037
(brightbeanxyz/brightbean-studio). Skill records cross-checked: SKL-002
through SKL-006, SKL-023.

### PAT-033 — Structured HITL Brief With Typed Multi-Action Response (Edit/Rewrite/Accept/Reject)

Pattern Name: Structured human-approval brief with typed multi-action response (Edit / Rewrite-via-feedback / Accept / Reject)
Problem Solved: Giving a human approver everything needed to make a real decision on generated content in one place, with a real rejection path (not just accept-or-timeout), and a defined behavior when the human's response can't be classified.
Observed In: REPO-039 (langchain-ai/social-media-agent) — deep-audited, high confidence.
Mechanism: LangGraph's official `interrupt()` primitive pauses the graph and constructs a Markdown brief containing: the generated post verbatim, source URLs, selectable image options with a marked default, an editable/priority-tiered schedule proposal, and the grounding research report. Four documented human actions: Edit (submit → schedule directly), Response (free text → routed to an LLM rewrite node, or interpreted as a reschedule), Accept (schedule as-is), Ignore (real reject — thread ends, nothing is scheduled). An unrecognized response routes back to the human node rather than being guessed.
Required Conditions: A framework or custom mechanism capable of pausing/resuming agent execution mid-graph (LangGraph interrupts here, but the shape generalizes to any durable-execution primitive); a UI or channel able to render a rich brief and capture structured actions, not just yes/no.
Strengths: Verified by direct code read, not README. Rejection is first-class, not an edge case. Ambiguous human input has an explicit, non-guessing fallback — an independent third corroboration of the "ask again on ambiguity" design already found twice in Cluster B (SKL-012's DAG gate-placement, SKL-027/028's crisis-response ordering — PAT-016).
Weaknesses: Coupled to LangGraph's interrupt semantics for the underlying pause/resume; a non-LangGraph implementation would have to build equivalent state-durability itself. The brief-construction and action-routing logic is bespoke per node — not a reusable library, a design to reimplement.
Failure Modes: If the durable-execution layer underneath the interrupt fails or the graph state is lost mid-approval, the human's pending decision context could be lost (not tested in this audit — UNKNOWN whether social-media-agent has recovery for this). A rewrite-via-LLM path on ambiguous "Response" input could itself misinterpret feedback — the audit did not verify how rewrite failures are surfaced back to the human.
Complexity: Medium.
Token/Cost Implications: One extra LLM call on the "Response → rewrite" path; otherwise no repeated generation cost — the brief itself is templated, not LLM-generated.
Human-Control Implications: This pattern *is* a human-control mechanism — it directly implements DOM-07's core need (approval gate with genuine reject path, complementary to Cluster B's PAT-011) and DOM-09's ambiguity-routing need (unknown input → ask again, don't guess, complementary to PAT-016).
Hermes Relevance: DOM-07 (primary, Cluster B), DOM-21 (publish-mechanics boundary — this gate sits before DOM-21's publish step, PAT-035), DOM-09 (ambiguity routing, PAT-016), DOM-19/20 (the brief format itself is a content-review UX worth reusing).
Alternative Patterns: PAT-040 (brightbean-studio's configurable multi-stage approval — more product/config-driven, less rich-brief-driven).
Recommendation: STRONG CANDIDATE.
Confidence: 85.
Evidence: `phase-m2/repo-audits/langchain-ai-social-media-agent.md`, Dimension E (verified via direct read of `human-node.ts`, 291 lines, up through interrupt construction). MIT license, 2,748 stars, pushed same-week as audit, 31 real test files.

Adversarial Review (Section 13):
- Q1 Assumptions: assumes a framework capable of durable pause/resume (LangGraph here); assumes a UI/channel that can render Markdown and capture 4 distinct actions, not a plain yes/no bot.
- Q2 Where could it fail for Hermes: Hermes' own agent runtime is `hermes-agent` (REPO-001), not LangGraph — the *pause/resume* mechanics would need to be rebuilt on REPO-001's own primitives; REPO-001's closest equivalent is `write_approval.py` (PAT-020), a staged file-based gate, not an in-process interrupt — a materially different mechanic that would need adaptation, not direct port.
- Q3 Complexity introduced: a typed action-routing layer (4 actions, one of which triggers a secondary LLM call) plus brief-construction logic — real but bounded complexity, not a new framework.
- Q4 Lock-in: conceptual pattern is framework-agnostic; the specific interrupt/resume code is LangGraph-specific and would not port directly.
- Q5 Evidence missing: no direct evidence on approval-context durability under a crash mid-interrupt; `memory-v2/` (possibly relevant) was explicitly not inspected this audit pass.
- Q6 Simpler competing approach: a plain accept/reject binary with a separate free-text comment box — simpler to build, but loses the structured priority-tier reschedule and the explicit non-guessing ambiguity fallback, both of which are real value-adds this pattern earns through its complexity.
- Q7 Marketing vs engineering: none found — Stage -2.4's audit explicitly checked the README's claim against the code and found the code *richer* than the README suggested, not thinner. No marketing inflation detected.

Role Notes (Section 14):
- Repository Auditor: mechanism confirmed via direct code read (not inferred), all four actions independently verified against the interrupt payload's own text. High confidence in what's documented above.
- Reliability Reviewer: the pattern is strong on the *decision* side but unverified on the *durability* side (Q5) — recommend Hermes not treat this as evidence that approval-state durability comes for free; that would need separate verification against whatever runtime Hermes actually uses.
- Skeptic: attempted rejection — the strongest objection is architectural mismatch (Q2): this is a LangGraph pattern and Hermes is REPO-001-based, so what's actually portable is the *brief content design and action taxonomy*, not the pause/resume code. Recommendation stands as STRONG CANDIDATE but the record should be read as "STRONG CANDIDATE for the brief/action-taxonomy design," not "STRONG CANDIDATE for the implementation."

---

### PAT-034 — Multi-Stage LangGraph Subgraph Pipeline With Per-Stage Fallback Routing

Pattern Name: Decomposed-subgraph content pipeline with explicit degrade-not-fail fallback
Problem Solved: Building a multi-stage content pipeline (research → draft → condense → illustrate → gate → publish) as separately testable/failable stages rather than one monolithic prompt chain, so a failure in one stage degrades gracefully instead of killing the whole run.
Observed In: REPO-039 (langchain-ai/social-media-agent) — deep-audited, high confidence. (Single source — see Recommendation.)
Mechanism: Separate LangGraph subgraphs per concern (`find-and-generate-images`, `verify-links`, `verify-tweet`, `curate-data`/`generate-posts-subgraph`, `ingest-data`, `repurposer`) coordinated by a `supervisor-graph`. Image generation is wrapped in try/catch that logs and falls back to text-only rather than failing the pipeline; the over-length condense step is capped at 3 retries.
Required Conditions: A graph/workflow engine (or hand-rolled state machine) that supports typed state passed between stages and conditional routing.
Strengths: Verified by direct reading of the graph definition, not inferred. Explicit bounded retry (condense) and explicit fallback (images) rather than unbounded retry or silent failure.
Weaknesses: This is a single-process LangGraph app, not a distributed durable-execution system (contrast PAT-035's Temporal-based approach) — a process crash mid-pipeline has different recovery properties than a durable-workflow engine.
Failure Modes: Not independently checked whether a supervisor-graph-level failure (not a subgraph failure) has its own fallback; the audit only confirmed subgraph-level fallback (images) and bounded retry (condense).
Complexity: Medium-High (7 named subgraphs plus a supervisor).
Token/Cost Implications: Bounded retry on condense (max 3x cost multiplier on that stage only); image fallback avoids paying for a failed image generation twice.
Human-Control Implications: Indirect — this is the pipeline that feeds into PAT-033's human gate; a fallback that silently degrades to text-only changes what the human reviews at the gate, which is itself worth surfacing to the approver (not confirmed whether it is).
Hermes Relevance: DOM-03 (chained/narrative decomposition), DOM-20 (multi-modal generation), and cross-cluster to DOM-01 (Cluster A — general orchestration-pattern comparison; Cluster A's own patterns, e.g. PAT-001, did not directly address orchestration-granularity choice, so this comparison remains open for Stage -2.6/-2.7 triangulation, not resolved here).
Alternative Patterns: PAT-042 (ViMax's finer-grained, schema-contracted per-module pipeline — a different decomposition philosophy, more modules, tighter per-module output contracts, worth comparing directly at synthesis).
Recommendation: CANDIDATE. (Single deep-audited source; real and well-evidenced, but this is a general orchestration-architecture pattern better triangulated against Cluster A's dedicated orchestration-framework audits before any STRONG rating — recommend Stage -2.6/-2.7 cross-check against Cluster A's LangGraph/ADK/OpenAI-Agents-Python findings rather than rating strength from this cluster's evidence alone.)
Confidence: 65.
Evidence: `phase-m2/repo-audits/langchain-ai-social-media-agent.md`, Dimensions A and D.

---

### PAT-035 — Reversibility-Differentiated Retry/No-Retry Publish Policy

Pattern Name: Classify-then-retry: safe-to-retry vs. irreversible-so-never-retry publish operations
Problem Solved: Preventing double-posting/duplicate side effects when a publish operation times out or partially fails, without abandoning retries for genuinely safe-to-repeat operations.
Observed In: REPO-036 (gitroomhq/postiz-app, Temporal-based) AND REPO-037 (brightbeanxyz/brightbean-studio, Django/DB-flag-based) — **two independent sources, structurally unrelated implementations converging on the same design.**
Mechanism: Both systems classify publish-adjacent operations into at least two buckets — safely-retryable (status checks, some media/comment operations, capped retries) and irreversible (the actual publish mutation) — and set the irreversible bucket to effectively zero retries, treating a timeout there as "outcome unknown" rather than retrying. postiz-app: four differentiated Temporal activity-proxy retry policies, `maximumAttempts: 1` on `postSocialPending`/`finalizePost`, explicit code comment reasoning about a retried-but-already-completed timeout risk. brightbean-studio: `RETRY_BACKOFF` schedule + `MAX_RETRIES` cap + `_fail_permanently()`, failures classified via `getattr(e, "retryable", True)`, a `PlatformPost`+`published_at` record kept once succeeded to prevent a later retry from double-posting — same "don't double-publish on retry" concern, arrived at independently via database state instead of a workflow engine's activity policy.
Required Conditions: The ability to distinguish, per operation, whether repeating it is safe (idempotent or side-effect-free) versus unsafe (mutates external state that can't be checked/undone); some form of persisted record of "did this already succeed" to check before allowing a retry.
Strengths: Two structurally unrelated systems (distributed workflow engine vs. single-process DB-flag) independently arrived at the same core design decision — this is a real convergent-evidence signal, not one project's idiosyncratic choice. Both are backed by direct code reading, not documentation claims.
Weaknesses: Neither implementation is a drop-in library; both require re-deriving the retryable/non-retryable classification for whatever platforms Hermes actually targets. postiz-app's variant has **zero automated test coverage** (confirmed: 0 `.spec.ts`/`.test.ts` files found) despite the code's sophistication — a real evidence-quality caveat on that specific source, though the design itself was verified by direct reading regardless. brightbean-studio's approval-workflow claims (90-day retention, tiered rate limits) were not independently re-verified this pass.
Failure Modes: A misclassification (marking something retryable that is actually irreversible, or vice versa) directly reintroduces the double-post risk this pattern exists to prevent — the pattern's safety depends entirely on getting that classification right per platform/operation, which is a Hermes-specific design task, not something inherited for free.
Complexity: Medium.
Token/Cost Implications: None directly (this is an operations/reliability pattern, not an LLM-cost pattern) — though a failed-and-retried LLM-generation step upstream of publish would have its own separate cost implications not covered by this pattern.
Human-Control Implications: Directly protects the irreversible-action principle from CLAUDE.md/Master Plan P-level guardrails (explicit confirmation before irreversible actions) at the *mechanics* layer — this is what makes "the human approved it, then publish either succeeds cleanly or fails cleanly (never silently duplicates)" actually true in practice.
Hermes Relevance: DOM-21 (primary), DOM-07 (the irreversible-action boundary DOM-07 cares about at the decision layer, this pattern implements at the mechanics layer).
Alternative Patterns: None found that solve the same problem differently in this source set — both audited publish-mechanics repos converge on this same design, which is itself the notable finding (no real "alternative" competing design was observed; see Adversarial Review Q6 for the simpler-but-worse alternative).
Recommendation: STRONG CANDIDATE.
Confidence: 88.
Evidence: `phase-m2/repo-audits/gitroomhq-postiz-app.md` Dimension D; `phase-m2/repo-audits/brightbeanxyz-brightbean-studio.md` Dimension D.

Adversarial Review (Section 13):
- Q1 Assumptions: assumes each publish-adjacent operation can be cleanly classified as idempotent-safe or not; assumes a persistence layer exists to record "already succeeded" before a retry decision is made.
- Q2 Where could it fail for Hermes: if Hermes publishes across many heterogeneous platform APIs with inconsistent idempotency guarantees (some platforms may not even expose a way to check "did my last post go through"), the classification itself becomes uncertain per-platform, which is exactly the failure mode named above.
- Q3 Complexity introduced: a per-operation-type retry-policy table plus a persisted success-record check before any retry — real but bounded; not a new framework.
- Q4 Lock-in: **both source repos are AGPL-3.0.** The *pattern* (concept) is freely usable; the *code* is not — any direct reuse of either repo's retry-policy code would trigger AGPL's network-use disclosure requirement. This is a real, confirmed constraint, not a hypothetical one.
- Q5 Evidence missing: postiz-app's variant has zero test coverage despite being the more architecturally sophisticated of the two — the design was verified by reading, not by evidence that it behaves correctly under real concurrent-failure conditions. Neither audit traced what happens if the persisted "already succeeded" check itself fails or is unavailable (a database outage at exactly the wrong moment).
- Q6 Simpler competing approach: unconditional retry-with-idempotency-key (let the platform API's own idempotency key, where offered, prevent duplicates) — simpler to implement, but only works where the target platform actually supports idempotency keys, which is not guaranteed across arbitrary social platforms; this is why both source projects built their own classification layer instead of relying on that.
- Q7 Marketing vs engineering: none found — this is code-comment-documented engineering reasoning in both sources ("heartbeat reporting proved unreliable in production," "must never retry" past the accepted boundary), not README marketing language.

Role Notes (Section 14):
- Repository Auditor: both mechanisms independently confirmed via direct code reading (retry-policy configuration in postiz-app; `_schedule_retry`/`_fail_permanently` in brightbean-studio). High confidence in what's documented.
- Reliability Reviewer: this is one of the strongest-evidenced patterns in this cluster precisely because of the independent convergence — two unrelated engineering teams solving the same problem the same way is a meaningfully stronger signal than one team's design choice. The postiz-app zero-test-coverage gap is real but doesn't undermine the *design's* validity, since the design was verified by direct reading, not by trusting the test suite.
- Skeptic: attempted rejection — the AGPL exposure (Q4) is a real practical constraint worth weighing at Stage -2.6/-2.7 if any code-level reuse (not just pattern-level) is ever considered; and the "convergent evidence" framing should not be overstated — both are still web/social-platform publishing tools, a fairly narrow domain, so two data points from that domain is meaningful but not overwhelming corroboration. Recommendation stands as STRONG CANDIDATE on the strength of the two-source, independently-confirmed convergence, with the AGPL caveat carried forward explicitly rather than buried.

---

### PAT-036 — Real Fetch-Then-Structure Competitive-Research Synthesis Pipeline

Pattern Name: Fetch-then-tag competitive/audience research (source+date+confidence discipline, brand-isolated storage)
Problem Solved: Producing competitive/audience research that is actual synthesis over real fetched data (not an LLM improvising from a static or absent dataset), with each claim traceable to a source, date, and confidence level.
Observed In: REPO-033 (indranilbanerjee/digital-marketing-pro) — deep-audited, high confidence. Comparison baselines (weaker evidence, single-source Skill records, not code-verified): SKL-003 (Research Analyst — 5-phase pipeline with source-credibility discipline) and SKL-004 (Competitive Cartographer — positioning-map method).
Mechanism: `agents/competitive-intel.md` defines an agent contract with explicit `mode` (snapshot vs. monitoring, with inference fallback if unspecified) and 10 numbered, checkable Behavior Rules (public-data-only sourcing; mandatory source+date+confidence tagging per claim; confirmed-vs-inferred labeling discipline; brand-isolated storage; baseline/change-detection with explicit default alert thresholds, e.g. "pricing change (any), ad-creative volume spike (>30% week-over-week)"). Backed by real Python: `competitor-scraper.py` does actual HTTP fetch + HTML parsing (requests + BeautifulSoup4, rotating user-agents, rate limiting) and **fails transparently** — a structured JSON error with an explicit fallback recommendation, not silent degradation, when dependencies are missing. `competitor-tracker.py` (537 lines) and `narrative-mapper.py` (759 lines) confirmed as substantial real files, not stubs.
Required Conditions: Actual web-fetch capability (not just an LLM asked to "research" from training knowledge); a storage convention for baselines to diff future scans against (change-detection needs a "before" state).
Strengths: This is the rare case in this audit round where a candidate's own test suite exceeded its catalog claim (402 real test functions found vs. 209 claimed) rather than falling short — a genuine positive-direction evidence correction. Honest-failure design (structured error + fallback advice, not silent pretend-success) is a strong reliability signal in its own right.
Weaknesses: The 10 Behavior Rules are enforced at the prompt level (LLM self-compliance), not structurally in code — no code-level gate confirmed to prevent the agent from ignoring a rule (e.g., rule 6, "never mix data across brands") was found. See PAT-039 for this as its own named risk pattern.
Failure Modes: If the LLM agent simply doesn't follow a behavior rule (since nothing structurally enforces it), the failure is silent from the system's perspective — no test or gate would catch a cross-brand data leak at the agent-compliance layer, only at the storage-path layer (which IS structurally enforced, see PAT-037).
Complexity: Medium (real scraping infra + tiered agent-contract design, but no orchestration layer beyond a single well-specified agent).
Token/Cost Implications: Fetch/parse cost is non-LLM (Python scraping); LLM cost is bounded to synthesis over already-structured fetched data, not open-ended "research the web" prompting — likely cheaper and more predictable than an LLM-only research approach.
Human-Control Implications: Source+date+confidence tagging on every claim gives a human reviewer (or downstream agent) the ability to judge trust per-claim rather than trusting an opaque summary — directly useful for Hermes' quality-over-throughput and epistemic-honesty principles (P5).
Hermes Relevance: DOM-18 (primary — this finding resolves Stage -2.3's "thin coverage" flag on DOM-18), DOM-19 (secondary, the snapshot/monitoring dual-mode design — see PAT-038), DOM-05/DOM-07 (the prompt-vs-structural-enforcement gap, see PAT-039).
Alternative Patterns: None deep-audited in this cluster; SKL-003/SKL-004 are lighter-weight comparison baselines (general market/positioning research, not social-platform-specific, not code-verified) rather than true alternatives.
Recommendation: STRONG CANDIDATE.
Confidence: 82.
Evidence: `phase-m2/repo-audits/indranilbanerjee-digital-marketing-pro.md`, Dimensions B, C, D, F. Skill records SKL-003, SKL-004 in `phase-m2/skill-catalog.md`.

Adversarial Review (Section 13):
- Q1 Assumptions: assumes target competitor data is publicly scrapable (no login-walled or heavily bot-protected sources) and that `robots.txt` compliance (claimed but not fully traced to its implementation line) is actually adequate for whatever jurisdictions/platforms Hermes operates in.
- Q2 Where could it fail for Hermes: social-platform competitive signals (post performance, hashtag trends) are a different scraping target than the general competitor/marketing-page scraping this repo demonstrates — the mechanism (fetch-then-tag-then-synthesize) transfers, but the specific scraper code would need substantial rework for social-platform APIs/rate limits, which is a different, harder problem (platform ToS and anti-bot measures are typically stricter for social platforms than for a competitor's marketing site).
- Q3 Complexity introduced: real scraping infrastructure (dependency management, rate limiting, user-agent rotation) plus a tiered agent-contract with numbered rules — non-trivial but bounded and well-organized.
- Q4 Lock-in: coupled to the Claude Code plugin/skill format (`SKILL.md`, `plugin.json`) for the agent-contract layer; the scraping scripts themselves are plain Python, portable.
- Q5 Evidence missing: the append-only-vs-overwrite behavior of the actual persistence path (`campaign-tracker.py --action save-insight`) was not independently verified — relevant to whether this pattern is compatible with Hermes' never-delete memory principle (DOM-11) if adopted as-is.
- Q6 Simpler competing approach: an LLM-only "research this competitor" prompt with web-search tool access and no dedicated scraping layer — much simpler to stand up, but loses the structured source/date/confidence tagging discipline and the change-detection/baseline mechanism, both of which are the actual differentiators this pattern earns through its extra complexity.
- Q7 Marketing vs engineering: none found — Stage -2.4's audit specifically re-verified the strongest claim (real vs. static-data-wrapper synthesis) against the code and confirmed it; the test-count claim also under- rather than over-stated reality.

Role Notes (Section 14):
- Repository Auditor: confirmed via direct reading of `competitive-intel.md` in full plus partial reads of the three backing scripts (sizes/structure verified via `wc -l`, not fully line-read) — high confidence on the mechanism shape, moderate confidence on exact scraper implementation details not fully read.
- Reliability Reviewer: the honest-failure design (structured error on missing deps, not silent fake success) is a specifically good reliability signal worth calling out — many research/scraping tools silently degrade to hallucinated output when scraping fails, and this one explicitly does not.
- Skeptic: attempted rejection — the prompt-level-only enforcement of the Behavior Rules (Q1/Weaknesses) is a real gap for anything Hermes would treat as safety-critical (e.g. brand isolation is currently trust-based, not code-enforced, despite the storage-path layer being separately structurally enforced — see PAT-037). Recommendation stands as STRONG CANDIDATE for the fetch-then-tag research mechanism specifically; the behavior-rule-enforcement question is carried forward as its own separate, lower-rated pattern (PAT-039) rather than dragging this rating down.

---

### PAT-037 — Brand-Isolated Storage Path Convention

Pattern Name: Path-based per-tenant storage isolation (`~/.claude-marketing/brands/{slug}/...`)
Problem Solved: Preventing one brand/page's data from being read or written under another's context, via a structural (filesystem-path) mechanism rather than an application-logic check.
Observed In: REPO-033 (indranilbanerjee/digital-marketing-pro) — deep-audited, high confidence. Single source.
Mechanism: `scripts/_common.py` implements real path-resolution logic (`~/.claude-marketing/brands/{slug}/...` with a documented override-then-fallback chain); confirmed independently referenced by `audience-simulator.py` and `auto-save-insight.py`, indicating consistent application across scripts, not an isolated one-off.
Required Conditions: A filesystem (or equivalent namespaced storage) where path-scoping can be structurally enforced at the I/O layer, not just checked in application logic.
Strengths: Structural (path-based), not merely a documented convention — every script inspected independently uses the same scheme, and it's simple enough to audit at a glance.
Weaknesses: Filesystem-path isolation is coarser and weaker than a real multi-tenant access-control layer — it prevents accidental cross-brand writes by well-behaved code, but does not prevent a bug (or a compromised/misbehaving process) with filesystem access from reading across brand directories; there is no enforced permission boundary, just a naming convention consistently followed.
Failure Modes: A single script that constructs a path incorrectly (typo, wrong variable) could write outside its brand's directory with nothing to catch it — no observed test (`test_skill_script_contracts.py` covers skill/script *contracts*, not specifically cross-brand path isolation; not independently confirmed to cover this case).
Complexity: Low.
Token/Cost Implications: None (storage-layer mechanism, not LLM-cost-related).
Human-Control Implications: Reduces (but does not eliminate) the risk of one page/brand's content or research leaking into another's context — relevant to trust if Hermes runs multiple pages concurrently.
Hermes Relevance: DOM-24 (primary — cross-cluster to Cluster F), DOM-19 (secondary — per-page/brand isolation is a precondition for per-page strategy).
Alternative Patterns: REPO-001's (`hermes-agent`) profile-routing/multiplexing mechanism (Cluster F, PAT-046/PAT-047) is a substantially heavier-weight, more structurally-enforced alternative for the same underlying need — Stage -2.5 synthesis should compare the two directly: this pattern is simpler and lower-effort to adopt but weaker-enforced; REPO-001's is opt-in/config-heavy but (per the Cluster F/REPO-001 audit) offers real per-profile isolated memory/sessions when enabled.
Recommendation: CANDIDATE.
Confidence: 60.
Evidence: `phase-m2/repo-audits/indranilbanerjee-digital-marketing-pro.md`, Dimension G.

---

### PAT-038 — Snapshot-vs-Monitoring Dual-Mode Research Agent

Pattern Name: Explicit mode input with inference fallback (snapshot vs. ongoing-monitoring)
Problem Solved: Letting one agent contract serve both a one-time "tell me the current state" research request and an ongoing "watch for changes and alert me" monitoring request, without needing two separate agents.
Observed In: REPO-033 (indranilbanerjee/digital-marketing-pro) — deep-audited, high confidence. Single source.
Mechanism: `agents/competitive-intel.md` accepts an explicit `mode` input (`snapshot` vs `monitoring`) with a documented fallback inference rule when the caller doesn't specify one; monitoring mode layers baseline/change-detection with explicit named alert thresholds (e.g. pricing change, ad-creative volume spike >30% week-over-week) on top of the same underlying fetch-then-tag mechanism as PAT-036.
Required Conditions: A persisted baseline to diff against for monitoring mode; a caller (human or orchestrating agent) that can supply or omit the mode input.
Strengths: Avoids duplicating the fetch/synthesis logic across two separate agents; the mode-inference fallback means the contract degrades gracefully when the caller doesn't specify intent explicitly.
Weaknesses: Only one source observed; the specific inference-fallback logic (what it defaults to and why) was described in the audit but not quoted verbatim — moderate rather than full confidence in the exact decision rule.
Failure Modes: If the inference fallback guesses "snapshot" when the caller actually wanted ongoing monitoring (or vice versa), the caller may not get the alerting behavior they expected with no explicit error — an ambiguity-handling gap worth comparing against DOM-09's "ask, don't guess" principle (this repo's agent silently infers rather than asking).
Complexity: Low-Medium.
Token/Cost Implications: Monitoring mode implies repeated scans over time (recurring cost); snapshot mode is one-shot.
Human-Control Implications: None structurally — this is a research-agent input-mode design, not an approval mechanism.
Hermes Relevance: DOM-18, DOM-19.
Alternative Patterns: None observed in this source set.
Recommendation: CANDIDATE.
Confidence: 55.
Evidence: `phase-m2/repo-audits/indranilbanerjee-digital-marketing-pro.md`, Dimension B.

---

### PAT-039 — Prompt-Level-Only Behavior Rules Without Structural Enforcement (Risk Pattern)

Pattern Name: Numbered/checkable behavior rules enforced only at the prompt level
Problem Solved: N/A — this is recorded as a **named risk pattern**, not a solution: a well-specified but weakly-enforced control mechanism worth flagging so it isn't mistaken for a structural guarantee.
Observed In: REPO-033 (indranilbanerjee/digital-marketing-pro) — deep-audited, high confidence. Cross-referenced (by the Stage -2.4 audit itself) against `microsoft/agent-governance-toolkit` (REPO-010, Cluster B), which the audit describes as raising this same general prompt-vs-structural-enforcement risk class — Cluster B's PAT-010 (structural pre-execution policy gate, the govern()/proxy interception mechanism) is precisely the structural-enforcement answer to the risk this record names; the two records should be read together at Stage -2.6.
Mechanism: 10 numbered "Behavior Rules" in an agent's system-prompt contract (e.g. "never mix data across brands," mandatory source+date+confidence tagging) are well-specified and individually checkable in principle, but enforcement is entirely the LLM's own prompt-compliance — no code-level gate was found that would catch or block the agent violating one of these rules.
Required Conditions: N/A (risk pattern).
Strengths: The rules themselves are a genuinely good format (specific, checkable, not vague prose) — worth reusing as a *writing style* for agent contracts even while treating the *enforcement* gap as a separate problem to solve.
Weaknesses: No structural backstop confirmed for the most safety-relevant rules (cross-brand data isolation) beyond the separately-enforced storage-path convention (PAT-037), which is itself only a naming convention.
Failure Modes: An LLM agent under sufficiently unusual or adversarial input could violate a Behavior Rule with nothing in the code path to detect or prevent it — this is a known general class of LLM-agent risk, not specific to this repo, but concretely observed here.
Complexity: N/A.
Token/Cost Implications: None directly.
Human-Control Implications: Directly relevant — if Hermes relies on prompt-level rules alone for anything safety-critical (e.g. never-delete, brand isolation, publish gating), this pattern is the cautionary example for why that's insufficient on its own.
Hermes Relevance: DOM-05, DOM-07 (cross-cluster to Cluster B's PAT-010 — read together, not independently).
Alternative Patterns: PAT-037 (structural path-based isolation) is a partial structural backstop for the specific cross-brand-mixing rule, though it only covers storage location, not all 10 rules; Cluster B's PAT-010 is the fuller structural answer.
Recommendation: CONTEXT-DEPENDENT — good as a contract-writing style; AVOID relying on it alone for anything Hermes treats as safety-critical without a structural backstop.
Confidence: 65.
Evidence: `phase-m2/repo-audits/indranilbanerjee-digital-marketing-pro.md`, Dimension E.

---

### PAT-040 — Configurable Multi-Stage Human-Approval Workflow

Pattern Name: Test-covered, config-driven N-stage approval workflow
Problem Solved: Supporting more than one approval step (e.g. draft review then final publish review) as a configurable product feature rather than a hardcoded single gate.
Observed In: REPO-037 (brightbeanxyz/brightbean-studio) — deep-audited, moderate confidence (full configuration surface not traced).
Mechanism: `apps/approvals/test_workflow.py` contains a `TwoStageFlowTests` test class confirming a real, test-covered multi-stage approval flow exists; the audit did not trace how many stages are configurable or who can be assigned to each stage.
Required Conditions: A data model for approval-stage configuration (who approves, how many stages) and a state machine tracking where a given piece of content is in that sequence.
Strengths: Test-covered, not just claimed — the `TwoStageFlowTests` class is direct evidence the mechanism is exercised by automated tests, not just documented.
Weaknesses: Shallow audit coverage — the actual configuration surface (max stages, assignment rules, what happens if a stage's approver is unavailable) was not traced this pass.
Failure Modes: UNKNOWN — insufficiently audited to state specific failure modes with confidence; flagged as a gap rather than guessed.
Complexity: Medium (implied by "configurable," not independently verified).
Token/Cost Implications: None (product-workflow mechanism, not LLM-related).
Human-Control Implications: Directly relevant to DOM-07 as an alternative shape to PAT-033's single rich-brief gate — a config-driven multi-stage model rather than a single interrupt-based gate.
Hermes Relevance: DOM-07, DOM-21.
Alternative Patterns: PAT-033 (richer single-gate brief, LangGraph-specific mechanics).
Recommendation: CANDIDATE. (Explicitly not STRONG — evidence quality is capped by the audit's own acknowledged shallow coverage of this specific dimension, consistent with Section 10.4 rule 2.)
Confidence: 45.
Evidence: `phase-m2/repo-audits/brightbeanxyz-brightbean-studio.md`, Dimension E.

---

### PAT-041 — Static/Dynamic Character-Feature Separation for Cross-Scene Consistency

Pattern Name: Static-vs-dynamic trait extraction for visual character continuity
Problem Solved: Keeping a character visually recognizable across many independently-generated images/scenes despite normal narrative variation (changing clothes, props, expressions).
Observed In: REPO-030 (HKUDS/ViMax) — deep-audited, high confidence. Single source.
Mechanism: `character_extractor.py`'s system prompt explicitly separates "static features" (physical appearance/physique — relatively unchanging) from "dynamic features" (attire, accessories, carried items — easily changeable), instructing the model to group all name-references to the same entity under one character record. Output is schema-enforced via a Pydantic `ExtractCharactersResponse` model, using a custom `TrailingCommaTolerantPydanticOutputParser` built specifically to tolerate a known, specific LLM JSON-formatting failure mode.
Required Conditions: A schema-enforcement layer for LLM output (Pydantic or equivalent, directly analogous to Cluster A's PAT-003) and a per-character persisted record that later generation steps can reference.
Strengths: Concrete, specific prompt-design technique (not a generic "extract characters" call) directly targeting the actual failure mode (visual drift on changeable features being mistaken for identity change). Backed by a real, targeted regression-test suite (`test_crash_regressions.py`, `test_hang_guards.py`, `test_wrong_output_guards.py`, `test_hygiene_guards.py` — 25 test files total) specifically aimed at failure modes, not just happy-path features.
Weaknesses: Single source; LangChain-coupled implementation (schema/parser code, not the prompt-design idea itself, is framework-specific).
Failure Modes: The static/dynamic classification itself is a judgment call embedded in the prompt — an LLM misclassifying a normally-static feature as dynamic (or vice versa) would reintroduce the consistency problem this pattern exists to solve; not independently stress-tested by this audit beyond confirming the mechanism's existence and the regression-test suite's existence.
Complexity: Medium.
Token/Cost Implications: One extraction call per character-appearing scene; retry via `tenacity` adds bounded extra cost on transient failures.
Human-Control Implications: None structurally — a generation-quality mechanism, not an approval mechanism.
Hermes Relevance: DOM-20 (primary).
Alternative Patterns: PAT-043 (wind-comic's dual-threshold vision-LLM style-consistency audit — a *verification-after-generation* approach, versus this pattern's *consistency-by-construction-at-extraction* approach; genuinely different points in the pipeline, worth citing together as complementary rather than competing).
Recommendation: STRONG CANDIDATE.
Confidence: 78.
Evidence: `phase-m2/repo-audits/hkuds-vimax.md`, Dimensions B, C, D.

Adversarial Review (Section 13):
- Q1 Assumptions: assumes character identity can be meaningfully decomposed into a static/dynamic feature split for the specific visual style Hermes would generate (illustrated/stylized content may have different consistency needs than photorealistic).
- Q2 Where could it fail for Hermes: if Hermes' content is primarily text (not multi-modal/visual), this pattern is not applicable at all — its relevance is conditional on DOM-20 actually needing image/video generation, which per the raw idea's "احتمالاً ویدیو" (probably video) is stated as likely but not certain.
- Q3 Complexity introduced: a dedicated extraction step with its own schema, parser, and retry logic — a real additional pipeline stage, not a prompt tweak.
- Q4 Lock-in: LangChain-coupled for the schema/parser plumbing specifically; the static/dynamic prompt-design idea itself is framework-agnostic.
- Q5 Evidence missing: no direct evidence on how well the classification holds up across a genuinely long series (the audit confirmed the mechanism exists and is tested for crash/hang/malformed-output robustness, not for long-run consistency-drift specifically).
- Q6 Simpler competing approach: a single reference image passed to every generation call ("use this character sheet") — simpler, but doesn't handle the case where the character needs to be *described* to a text-only step or where no single reference image is available yet.
- Q7 Marketing vs engineering: the audit specifically corrected the README's "4-agent" framing as a marketing simplification of a real ~13-module pipeline (see PAT-042) — this particular mechanism (character extraction) was not itself found to be oversold, but the audit's general caution about this repo's marketing-vs-code framing gap is worth carrying forward.

Role Notes (Section 14):
- Repository Auditor: confirmed via direct reading of `character_extractor.py`'s system prompt and Pydantic schema; the custom trailing-comma-tolerant parser is a specific, verifiable hardening detail, not a generic claim.
- Reliability Reviewer: the named regression-test files (crash/hang/wrong-output/hygiene guards) are a genuinely strong reliability signal for the surrounding pipeline, though they test robustness of extraction, not correctness of the static/dynamic classification judgment itself — those are different properties and shouldn't be conflated.
- Skeptic: attempted rejection — the pattern's applicability is conditional on Hermes actually doing visual generation (Q2), which is a real "maybe" in the raw idea, not a confirmed requirement; also single-sourced, so "STRONG" here rests on this one source's evidence depth rather than corroboration. Recommendation stands as STRONG CANDIDATE on the strength of that one source's evidence depth (schema-enforced + targeted regression tests + specific, non-generic technique), consistent with the Stage -2.5 exit criterion's "one deep-audited high-confidence source" allowance — but the conditional-applicability caveat should travel with this record into Stage -2.6.

---

### PAT-042 — Fine-Grained Specialized Pipeline With Per-Module Schema Contracts

Pattern Name: Narrow single-purpose LLM modules with individual Pydantic contracts (vs. monolithic multi-role agent)
Problem Solved: Decomposing a complex multi-modal generation pipeline (idea → script → storyboard → character/style consistency → images → video) into small, independently testable/retryable units, each with its own typed output contract, rather than a small number of broad "role" agents.
Observed In: REPO-030 (HKUDS/ViMax) — deep-audited, high confidence. Single source (in this cluster; cross-cluster comparison recommended, see below).
Mechanism: 13 specialized single-purpose modules under `agents/` (novel_compressor, character_extractor, event_extractor, scene_extractor, screenwriter, script_planner, script_enhancer, storyboard_artist, character_portraits_generator, camera_image_generator, best_image_selector, reference_image_selector, global_information_planner), each with its own system prompt, Pydantic response schema, and per-module `tenacity` retry decorator, plus a separate general-purpose `agent_runtime/` layer (loop, tool executor, session index, context compactor) distinct from the pipeline-specific modules.
Required Conditions: Willingness to build/maintain many small typed contracts rather than fewer broad ones; a schema-enforcement library.
Strengths: Each module is individually testable and independently retryable (a failure in `character_extractor` doesn't require re-running `screenwriter`). Schema-first output (not free-text parsing) is a real reliability improvement over regex-based approaches (contrast PAT-044/GOAT-Storytelling-Agent).
Weaknesses: 13+ modules is real coordination overhead — more moving parts to maintain, version, and keep contract-compatible with each other than a smaller number of broader agents.
Failure Modes: Not independently traced whether the `agent_runtime/` layer's failure handling (crash recovery, partial-pipeline resume) covers cross-module state, or only per-module retry — the audit confirmed per-module retry decorators but did not trace end-to-end pipeline-level recovery.
Complexity: High.
Token/Cost Implications: Many small calls rather than fewer large ones — likely more total LLM calls (higher fixed per-call overhead) in exchange for smaller, more reliably-parseable individual outputs and cheaper targeted retries (only the failed module reruns, not the whole pipeline).
Human-Control Implications: None structurally — an architecture/decomposition pattern, not an approval mechanism.
Hermes Relevance: DOM-20 (primary), DOM-03 (decomposition philosophy), cross-cluster to DOM-01 (Cluster A — recommend direct comparison against Cluster A's dedicated multi-agent-orchestration-framework findings before any final judgment on whether this granularity is right for Hermes; not resolved by Cluster A's own patterns, see PAT-034's identical note).
Alternative Patterns: PAT-034 (social-media-agent's coarser subgraph decomposition — 7 subgraphs vs. this pattern's 13 narrow modules — a genuinely different point on the granularity spectrum, worth comparing directly at synthesis, not silently merging).
Recommendation: CANDIDATE. (Real and well-evidenced, but — like PAT-034 — this is fundamentally an orchestration-granularity choice that Cluster A's dedicated framework audits are better positioned to adjudicate; recommend Stage -2.6/-2.7 triangulate rather than rating strength from this cluster alone.)
Confidence: 68.
Evidence: `phase-m2/repo-audits/hkuds-vimax.md`, Dimensions A, B.

---

### PAT-043 — Dual-Threshold Vision-LLM Consistency Audit

Pattern Name: Score-against-reference visual consistency gate (hard-regen / soft-warn thresholds, fail-open)
Problem Solved: Catching visual style drift (a generated shot not matching the established reference style) automatically, before it reaches a human or gets published, with a graceful behavior when the audit itself can't run.
Observed In: REPO-031 (ChrisChen667788/wind-comic) — deep-audited, high confidence. Single source.
Mechanism: `lib/style-audit.ts` uses a vision-LLM call to score a generated shot against a reference `styleBible` frame across 4 named dimensions (palette, lighting, colorTemperature, texture, each 0-100), takes the overall score as the minimum of the four (a deliberately conservative aggregation — one bad dimension fails the whole shot), and enforces two thresholds: a hard `regenThreshold` (default 70 — triggers automatic regeneration) and a softer `passThreshold` (default 85 — passes with a warning between 70-85). Explicit, documented skip conditions (no reference image → skip; mock/data-URI images → skip, vision can't read them) and fail-open behavior (any thrown error in the audit returns `null`, treated as "no audit data," not a crash). The code's own header comment documents the specific prior bug this mechanism was built to fix (style drift from an earlier version that fed the reference as an image-gen hint but never verified compliance).
Required Conditions: A vision-capable LLM; an established reference frame/style-bible to score against; a pipeline stage positioned after generation and before either human review or publish.
Strengths: Genuinely engineered, not aspirational — the header comment documents a real prior failure and why this specific fix addresses it. Conservative aggregation (min of 4 dimensions, not average) avoids one dimension's high score masking another's failure. Explicit, sensible failure/skip handling rather than crashing or silently passing everything when the audit can't run.
Weaknesses: Single source; the specific threshold values (70/85) are this repo's tuning, not a universal constant — would need Hermes-specific calibration. Vision-LLM scoring is itself an LLM call with its own failure/inconsistency risk (not independently stress-tested for scoring reliability/repeatability across repeated runs of the same image).
Failure Modes: A vision-LLM that scores inconsistently across repeated calls on the same image (temperature/sampling variance) could cause flaky regen-vs-pass decisions; not tested by this audit. The fail-open-to-null behavior means a systematic audit failure (e.g. the vision API is down) silently stops catching drift rather than blocking the pipeline — a deliberate design choice (favors availability over strictness) worth flagging explicitly as a tradeoff, not a flaw.
Complexity: Medium.
Token/Cost Implications: One additional vision-LLM call per generated shot being audited — a real, per-shot recurring cost, though cheaper than a failed/discarded generation reaching a human reviewer.
Human-Control Implications: This is a pre-human quality gate (DOM-15-adjacent, complementary to Cluster D's PAT-031), not a replacement for human approval — reduces how often a human sees an obviously-off-style shot, doesn't replace the human decision.
Hermes Relevance: DOM-20 (primary).
Alternative Patterns: PAT-041 (ViMax's static/dynamic extraction-time consistency approach — complementary, not competing: PAT-041 aims for consistency *at generation time*, this pattern *verifies after the fact*).
Recommendation: STRONG CANDIDATE.
Confidence: 80.
Evidence: `phase-m2/repo-audits/chrischen667788-wind-comic.md`, Dimension D (full file read, 190 lines).

Adversarial Review (Section 13):
- Q1 Assumptions: assumes a stable, pre-established reference frame/style-bible exists before generation begins; assumes the vision-LLM used for scoring is itself reliable and reasonably consistent run-to-run.
- Q2 Where could it fail for Hermes: if Hermes' content style is meant to evolve/vary intentionally over a series (not stay fixed to one reference), a drift-detection-against-a-fixed-reference mechanism would need rework — it assumes "drift from reference = bad," which may not hold for content designed to evolve.
- Q3 Complexity introduced: one additional vision-LLM-calling pipeline stage with threshold logic and explicit skip/fail-open handling — bounded complexity, cleanly isolatable as a single stage.
- Q4 Lock-in: the pattern (score-against-reference, dual-threshold, fail-open) is fully framework-agnostic; the specific TypeScript implementation is coupled to this app's Next.js/API-route structure.
- Q5 Evidence missing: scoring-consistency/repeatability of the vision-LLM call across repeated runs on identical input was not tested; the "8-dimension character-DNA" figure from the original catalog record was explicitly NOT verified by this audit (a different, 4-dimension *style* mechanism was read instead) — do not conflate the two.
- Q6 Simpler competing approach: skip automated verification entirely and rely on the human approval gate (PAT-033/PAT-040) to catch style drift — simpler, but pushes the catch-rate burden entirely onto a human who may not have the same shot immediately before them for comparison, and costs human attention on every generation rather than only flagged ones.
- Q7 Marketing vs engineering: none found for the audited mechanism — the header comment's own documented bug-and-fix narrative is engineering documentation, not marketing copy; the unverified "8-dimension character-DNA" figure is a separate, unaudited claim, correctly left as UNKNOWN rather than assumed to match.

Role Notes (Section 14):
- Repository Auditor: confirmed via full read of `style-audit.ts` (190 lines) — high confidence in the mechanism as documented; the "8-dimension character-DNA" claim is a distinct, unverified mechanism in the same repo and should not be cited under this pattern record.
- Reliability Reviewer: the explicit skip conditions and fail-to-null-not-crash behavior are exactly the kind of reliability thinking Section 10.1.6 rewards — genuinely one of the better-engineered reliability mechanisms found in this cluster. The one open reliability question (Q5, scoring repeatability) is worth a real follow-up if Hermes adopts this pattern, not just a footnote.
- Skeptic: attempted rejection — single-sourced, and the fail-open design (Q5/Weaknesses) is a real tradeoff that a stricter system might reject in favor of fail-closed (block publish if the audit can't run) — Hermes' own risk tolerance should decide which direction is right, this pattern's specific choice (favor availability) is not automatically the correct one for Hermes. Recommendation stands as STRONG CANDIDATE for the mechanism's engineering quality and evidence depth; the fail-open-vs-fail-closed choice is flagged as a design decision Hermes would need to make deliberately, not inherit by default.

---

### PAT-044 — Fixed-Window Literal-Text Scene-Carryover Baseline

Pattern Name: Naive scene-to-scene continuity via truncated prior-text injection
Problem Solved: Basic narrative continuity between sequentially-generated scenes, without building a structured narrative-state model.
Observed In: REPO-029 (GOAT-AI-lab/GOAT-Storytelling-Agent) — deep-audited, high confidence on the mechanism itself; low confidence on current project health (last pushed 2025-11-12, 9+ months stale as of audit date — maintenance-signal correction from Stage -2.3's "active" characterization).
Mechanism: `generate_scene(..., previous_scene=None)` accepts the prior scene's text, truncates it to the last N words via a utility function, and injects it into the next generation prompt. The main loop passes the last generated scene forward as `previous_scene` for the next call — a real, working, chained generation loop, but continuity is literal-text-window carryover, not a structured character/plot-state model.
Required Conditions: None beyond basic sequential prompting — this is closer to a starting baseline than an engineered system.
Strengths: Simple, verifiably working, trivially cheap to implement — the lowest-effort real answer to "does the next generation step see what came before."
Weaknesses: No world-state/character-state tracking beyond the initial act/chapter plan; a fixed word-count truncation can cut off mid-thought or drop earlier-but-still-relevant plot threads. Structured-output parsing (`Plan.parse_text_plan`) uses regex with silent empty-list failure on total parse failure — not schema-enforced (contrast PAT-041's Pydantic-schema approach).
Failure Modes: No checkpointing — a crash mid-generation loses all in-memory progress. The regex-parse failure path was not confirmed to be checked by callers (UNKNOWN whether a silent empty-plan failure propagates visibly or just produces a broken story silently).
Complexity: Low.
Token/Cost Implications: Cheapest option in this cluster — no extra extraction/audit calls, just the base generation calls themselves.
Human-Control Implications: None — fully autonomous generate-to-completion script, no approval gates found anywhere in the code.
Hermes Relevance: DOM-03 (as the simple end of a spectrum, not a recommended default).
Alternative Patterns: PAT-041 (ViMax's schema-enforced, static/dynamic-feature-aware extraction — a substantially more engineered answer to a related continuity problem).
Recommendation: CONTEXT-DEPENDENT. (Useful only as a lower-bound baseline or for a genuinely low-stakes/low-budget context; not recommended as Hermes' primary continuity mechanism given the no-checkpointing and silent-failure gaps, and given DOM-03's research question explicitly anticipates more than this.)
Confidence: 70.
Evidence: `phase-m2/repo-audits/goat-ai-lab-goat-storytelling-agent.md`, Dimensions C, D.

---

### PAT-045 — Skill-Invocation Quality Index Retargeted Toward Content-Performance Feedback (Documented Gap, Not a Resolved Pattern)

Pattern Name: Weighted quality-index + threshold alerting, as a *candidate direction* for DOM-22
Problem Solved: N/A as a working DOM-22 mechanism — recorded to make the DOM-22 gap explicit and show what the closest available comparison actually is (and isn't).
Observed In: SKL-023 (Skill Logger, SomeClaudeSkills) — single source, Medium evidence quality (single-source Skill record, not code-verified against a real repo).
Mechanism: A 6-stage pipeline (Capture, Analyze, Score, Aggregate, Alert, Improve) with a 4-weighted-dimension quality index (Completion 25%, Efficiency 20%, Output Quality 30%, Satisfaction 25%) and threshold-based alerting (e.g. quality decline >20%). Designed to track *skill invocations*, not content performance — would need full retargeting to track published-content performance instead. (Same source underlies Cluster C's PAT-025, which covers it from the DOM-14 owner-visibility angle — this record is scoped narrowly to the DOM-22 gap-documentation purpose.)
Required Conditions: N/A — not a verified working mechanism in this domain, a structurally-similar mechanism from an adjacent domain.
Strengths: The weighted-index-plus-threshold-alert *shape* is a reasonable starting structure to adapt from, if Hermes needs one.
Weaknesses: Not evidence for DOM-22 as actually solved — this is the closest available comparison point, and it is a significant retargeting exercise away from what DOM-22 actually needs (external platform-analytics ingestion feeding back into content/research strategy), not a small adaptation.
Failure Modes: N/A (not a working mechanism to fail).
Complexity: N/A.
Token/Cost Implications: N/A.
Human-Control Implications: N/A.
Hermes Relevance: DOM-22.
Alternative Patterns: None found — this is the gap itself.
Recommendation: INSUFFICIENT EVIDENCE.
Confidence: 30.
Evidence: `phase-m2/skill-catalog.md` SKL-023.

**Explicit gap statement:** Consistent with Stage -2.3's finding, **DOM-22 (analytics & experimentation feedback loops) has no real, inspectable implementation anywhere in this cluster's 8 deep-audited repos or the cross-checked skill records.** SKL-023 is the closest available mechanism and it is from an entirely different domain (skill-usage analytics, not social-content performance analytics), requiring substantial retargeting rather than adaptation. This gap is carried forward into Stage -2.6 (as a documented no-candidate finding, not silently dropped) and Stage -2.7's Knowledge Gaps section.

---

## Cluster E Unresolved Cross-References (carried into Stage -2.6)

- **wind-comic's Director-agent coordination role** (`services/hybrid-orchestrator.ts` / `types/agents.ts`) was flagged at Stage -2.4 as also relevant to DOM-01 (Cluster A orchestration). Cluster A's own pass (PAT-001—PAT-009) did not independently extract an equivalent finding — `types/agents.ts` (608 lines) was not read in full by either the Stage -2.4 audit or Cluster A's Stage -2.5 pass. **Unresolved**: a dedicated follow-up read is needed before Stage -2.6 if this mechanism is to be scored.
- **E-02/PAT-034 (social-media-agent's 7-subgraph decomposition) and E-10/PAT-042 (ViMax's 13-module decomposition)** are both, at bottom, orchestration-granularity choices better adjudicated by Cluster A's dedicated framework audits (LangGraph, ADK, OpenAI Agents SDK, REPO-001 itself). Cluster A's own patterns (PAT-001—PAT-009) do not directly address the granularity-choice question either. **Unresolved**: recommend Stage -2.6/-2.7 explicitly triangulate this three-way comparison (PAT-001's narrow-waist philosophy vs. PAT-034's 7-subgraph split vs. PAT-042's 13-module split) rather than leaving each cluster's framing to stand alone.

---

## Cluster F — Scaling & Self-Maintenance (DOM-24, 25)

Sources: the REPO-001/040/041 audit trio (`nousresearch-hermes-agent.md`,
`hermes-agent-capability-reference.md`, `nimblecoai-hermes-agent.md`,
`nimblecoai-hermes-swarm-map.md`). `skill-catalog.md` confirmed to have zero
skill coverage for either DOM-24 or DOM-25.

### PAT-046 — Profile-Based Tenant Isolation (Whole-Instance Boundary)

Pattern Name: Profile-Based Tenant Isolation
Problem Solved: Running multiple independent agent identities (e.g. separate
social pages) from one shared codebase without a from-scratch project per
instance.
Observed In: REPO-001 (`gateway/profile_routing.py`, `docs/profile-routing.md`,
`gateway/run.py` `_profile_runtime_scope`)
Mechanism: `config.yaml`'s `profile_routes` maps platform + `guild_id`/
`chat_id`/`thread_id` combinations to named profiles; each profile gets a
fully separate `HERMES_HOME` (separate `MEMORY.md`, `USER.md`, `SOUL.md`,
sessions, tools). Requires `gateway.multiplex_profiles: true`; off by default,
`profile_routes` ignored entirely if unset.
Required Conditions: Operator explicitly enables `multiplex_profiles` and
maintains `profile_routes` config per new tenant/page.
Strengths: Real, mainline (merged 2026-08-10/11, not long-standing but
current), documented with a precise doc-to-code match, actively hardened
(`docs/ADR.md` 2026-07-13 entry fixing a real cross-profile plugin-manager
state leak).
Weaknesses: Heavyweight — one full profile (separate memory/skills/session
state) per isolation boundary, not a cheap per-context flag. Does not by
itself achieve the raw idea's "add a page without a from-scratch project" goal
cheaply if isolation boundaries are numerous/fine-grained (e.g. per-DM, not
just per-page).
Failure Modes: Misconfigured or omitted `profile_routes` silently serves the
wrong profile's data to a new context. The ADR-documented plugin-manager leak
is a confirmed real instance of this failure class already occurring in
production before being fixed — not hypothetical.
Complexity: Medium
Token/Cost Implications: Each profile carries its own memory/session state —
cost scales roughly linearly with tenant count, no shared-context savings
across tenants.
Human-Control Implications: None directly, but a misrouted profile is exactly
the kind of silent cross-tenant leak DOM-08 (access boundaries) cares about —
same class of concern as Cluster E's PAT-037 (brand-isolated storage path), a
much lighter-weight alternative for a related need.
Hermes Relevance: DOM-24 (core need) — this is REPO-001's native, current
answer, but framed per the reframing rule as "how does hermes-agent's
mechanism satisfy this need, what's the gap": it satisfies whole-page-level
isolation natively; it does not satisfy finer-grained (thread/DM-level)
isolation without provisioning a full profile per boundary.
Alternative Patterns: PAT-047 (lighter-weight alternative/complement); PAT-037
(Cluster E's much lighter path-based isolation for a related but distinct
per-brand need).
Recommendation: CANDIDATE
Confidence: 85 — single deep-audited source, but high-confidence: doc and
code cross-checked and agree, feature verified as mainline via `gh api` commit
history.
Evidence: `nousresearch-hermes-agent.md` Dimension A/C/H;
`hermes-agent-capability-reference.md` "Multi-Instance / Multi-Tenancy"
section.

---

### PAT-047 — Automatic Per-Context Memory Scoping (`context_id` Routing)

Pattern Name: Automatic Per-Context Memory Scoping
Problem Solved: Isolating memory *writes* automatically within a single agent
profile so a fact learned in one thread/channel/DM does not leak into
another, without provisioning a whole new profile per context.
Observed In: REPO-040 (`tools/memory_tool.py` — `_global_path_for()`,
`_scoped_path_for()`, `_path_for()`, wired via `_context_id_for_source` in
`gateway/run.py`; tested by `tests/tools/test_memory_scoping.py`,
`test_memory_scoping_legacy.py`, `tests/gateway/test_context_id_derivation.py`),
REPO-001 (PR #47552, "feat(memory): add opt-in `context_id` scoping...",
named by the issue thread itself as "the core fix," open/unmerged as of
2026-08-24) — 2 independent sources: a tested production implementation and
the corroborating upstream community consensus that this is the right fix.
Mechanism: Routes memory reads/writes through a per-context path derived from
thread/channel/DM identity, rather than a per-profile path — isolation
happens automatically at write-time within one profile instead of requiring a
separate profile per isolation boundary.
Required Conditions: Requires wiring `_context_id_for_source` at every
`AIAgent()` construction call site; requires the platform adapter to expose a
stable context identifier (thread/channel/DM id).
Strengths: Tested, not just claimed. Actively hardened post-initial-ship —
recent commits (`f3bf7e1` "scope DMs and stop persisting the merged view into
scoped files," `d3078fb` "pool a thread's memory into its parent channel")
show real production edge cases were found and fixed, not a one-shot patch
left unmaintained. Lighter-weight than PAT-046 for fine-grained isolation.
Weaknesses: Not yet merged into REPO-001 mainline — consuming it today means
either depending on the `cyborg-garden` fork directly or waiting on upstream
review. Adds a second isolation axis alongside PAT-046's profile routing if both
are ever used together.
Failure Modes: Context-derivation edge cases (exactly the two classes already
found and fixed: DM-vs-channel pooling, merged-view persistence) recur if a
new platform adapter introduces a context shape the scoping logic doesn't yet
handle — this is an ongoing engineering surface, not a "solved once and done"
guarantee.
Complexity: Medium
Token/Cost Implications: Negligible — a routing/path-selection mechanism, not
a compute-heavy one.
Human-Control Implications: None directly; a scoping bug is a silent-leak
risk relevant to DOM-08, same class as PAT-046's failure mode but at finer
grain.
Hermes Relevance: DOM-24 — this is the closer structural analog to the raw
idea's "add a page without a from-scratch project" goal (cheap per-context
isolation vs. PAT-046's whole-profile-per-boundary weight).
Alternative Patterns: PAT-046
Recommendation: STRONG CANDIDATE
Confidence: 80
Evidence: `nimblecoai-hermes-agent.md` Dimension B/C (full); cross-referenced
against `nousresearch-hermes-agent.md` Dimension C (PR #47552 sourcing, `gh
pr view` verified).

Adversarial Review (Section 13, Q1-Q7):
- Q1 (assumptions): Assumes hermes-agent's `AIAgent()` construction call
  sites can be intercepted to inject a context-id resolver; assumes platform
  context boundaries (thread/channel/DM) map cleanly onto memory-scoping
  needs; assumes the fork stays rebasable against a fast-moving upstream.
- Q2 (where could it fail for Hermes): A new platform adapter introducing an
  unhandled context shape could reproduce the same class of leak bugs already
  twice-patched. Fails structurally if PR #47552 is rejected or redesigned
  upstream, leaving consumers permanently diverged from mainline.
- Q3 (complexity introduced): A second isolation axis on top of PAT-046's
  profile routing — Hermes would need to decide whether it needs one or both,
  which is itself a design decision this research does not make.
- Q4 (lock-in): Real external dependency — availability depends on either an
  unmerged upstream PR's review timeline or ongoing reliance on the
  `cyborg-garden` fork's maintenance.
- Q5 (evidence missing): No independent third-party validation under load or
  production incident postmortem beyond the fork's own commit messages and
  test suite.
- Q6 (simpler competing approach): PAT-046 is operationally simpler (no new
  scoping logic, reuses existing profile machinery) at the cost of heavier
  per-tenant resource/config overhead — a real trade-off Stage -2.6 should
  weigh explicitly rather than default to the "cooler" mechanism.
- Q7 (marketing vs. engineering): None found — code, tests, and dated commit
  history throughout, no promotional framing.

Role Notes (Section 14):
- Repository Auditor: Confirms dedicated, real tests exist across three
  files; this is verified engineering, not a documentation-only claim.
- Reliability Reviewer: The two post-ship bugfix commits are evidence this is
  *not* a one-time-solved mechanism — flags it as "proven but still-hardening"
  and recommends treating adoption as requiring ongoing monitoring, not a
  drop-in guarantee.
- Skeptic: The mechanism's practical availability to Hermes hinges entirely
  on an external, unmerged PR and an external org's fork that Hermes does not
  control. Committing to this pattern before upstream status resolves means
  either inheriting `cyborg-garden`'s maintenance burden by consuming their
  fork, or redoing already-verified engineering work independently. Argues
  for treating Confidence as provisional and revisiting once PR #47552's fate
  is known, rather than as a settled recommendation now. **Disagreement
  preserved, not resolved:** recommendation stays STRONG CANDIDATE (the
  mechanism itself is sound and proven) but Confidence is capped at 80 rather
  than higher, specifically because of this dependency risk.

---

### PAT-048 — Three-Layer Deployment Separation (Image / Scaffolding / Artefact)

Pattern Name: Three-Layer Deployment Separation (Image / Scaffolding /
Artefact)
Problem Solved: Making safety/security mechanisms structurally
non-overridable at deploy time, rather than leaving them as config toggles
that can be silently left off or turned off later.
Observed In: REPO-041 (`docs/architecture/image-vs-hsm-boundary.md`, read in
full)
Mechanism: Formally separates three layers: (1) the immutable Docker image
(hermes-agent runtime) — this project's own "Decision Framework" explicitly
classifies "Approval system, path security... dangerous-command detection" as
things that "must be immutable, can't be optional, can't be overridden by
config" and belong here; (2) per-deployment "HSM scaffolding" (config,
plugins, hooks installed at agent-creation time); (3) opt-in git-sourced
"artefact" packages from a separate registry.
Required Conditions: Requires the deploying party to own/control its own
container build pipeline, and discipline to keep security-relevant logic out
of the scaffolding/config layer entirely.
Strengths: Directly, independently corroborates the cross-cutting gap already
found in REPO-001's own audit (safety mechanisms — write-approval (PAT-020),
auto-prune guard (PAT-021) — ship real but off-by-default/config-overridable).
This repo's contributors arrived at the same underlying problem from a
different angle and designed an explicit structural answer to it — a second,
independent source pointing at the same real gap, which is what makes this
pattern evidence-worthy despite coming from a single repo.
Weaknesses: This is Swarm Map's own architecture, not something Hermes
inherits for free merely by using REPO-001 as its base — REPO-001 itself is
typically run as a bare process/gateway, not container-per-agent. Adopting
this shape is a real architectural commitment (container-per-agent
deployment), not a small config change.
Failure Modes: If adopted loosely — e.g. a security toggle left in the
scaffolding layer "for now" instead of baked into the image — the entire
benefit of the separation is lost while the appearance of safety remains.
This pass did not verify whether the boundary is tooling-enforced (e.g. a CI
check rejecting scaffolding that tries to override image-level security) or
merely a documented convention — flagged UNKNOWN, not confirmed either way.
Complexity: Medium-High (requires a real container build/deploy pipeline
investment)
Token/Cost Implications: None directly (deployment-architecture pattern, not
a runtime mechanism).
Human-Control Implications: High relevance — this is a mechanism for making
approval-gate and never-delete guarantees durable and non-silently-disablable,
directly addressing DOM-05/DOM-07/DOM-11's need (see PAT-020, PAT-021) for
guarantees stronger than "the default happens to be off."
Hermes Relevance: DOM-24 primarily (deployment architecture); cross-cutting
to DOM-05/07/11.
Alternative Patterns: none observed in this cluster; a lighter-weight
alternative would be a documented, audited config-discipline policy without
an image/scaffolding split — see Skeptic note below.
Recommendation: STRONG CANDIDATE
Confidence: 75 — single deep-audited source; downgraded from what PAT-047's
2-source bar would allow because the enforcement-tooling question (is the
boundary actually enforced, or just conventional?) remains open.
Evidence: `nimblecoai-hermes-swarm-map.md` Dimension A/C/H; cross-referenced
against `nousresearch-hermes-agent.md`'s own Cross-Cutting Observation
(independent second source for the underlying problem, not for this specific
solution).

Adversarial Review (Section 13, Q1-Q7):
- Q1 (assumptions): Assumes Hermes owns/controls its own container build
  pipeline — untrue if Hermes runs the "default" hermes-agent way (bare
  process, not containerized per-agent).
- Q2 (where could it fail for Hermes): If Hermes is not deployed
  container-per-agent, this three-layer separation has no natural
  attachment point — it is Swarm Map's architecture, not hermes-agent's.
- Q3 (complexity introduced): Requires standing up an entire image build/
  deploy pipeline — real engineering investment a single-operator, private,
  VPS-hosted Hermes (per Owner decision OD-001) may not need at all.
- Q4 (lock-in): Adopting this shape commits Hermes to container-per-agent
  deployment as an architectural choice, not a reversible config setting.
- Q5 (evidence missing): No evidence this separation has been stress-tested
  against an actual attempted safety-bypass; it is a documented design
  philosophy plus code structure, not a demonstrated defense under attack.
- Q6 (simpler competing approach): For a private single-operator context, a
  documented and manually-audited config discipline ("never set `auto_prune`/
  `write_approval` to unsafe values," checked at deploy time) could achieve
  similar practical safety at far lower engineering cost than a full
  image/scaffolding/artefact pipeline.
- Q7 (marketing vs. engineering): The source doc reads as genuine internal
  engineering rationale, not marketing — but it is aspirational design
  philosophy; this pass did not verify the boundary is actually
  tooling-enforced rather than just followed by convention (see Failure
  Modes).

Role Notes (Section 14):
- Repository Auditor: Confirms the doc exists and states the philosophy
  explicitly; did not verify whether any CI/build-time check actually
  prevents scaffolding config from overriding image-baked security settings.
- Reliability Reviewer: The pattern's real value is closing exactly the
  "opt-in-off by default" gap already found in REPO-001 — but only if the
  boundary is structurally enforced, not merely documented intent.
- Skeptic: Questions whether this is even proportionate for Hermes given
  OD-001 (private, single-user, single-operator system) — the operational
  overhead of a full image/scaffolding/artefact split may not be justified
  unless Hermes grows into a genuinely multi-tenant, multi-operator system.
  Recommends Stage -2.6 treat this as PATTERN_ONLY / architecture-reference
  rather than something to directly build at current scale. **Disagreement
  preserved:** recommendation stays STRONG CANDIDATE for the pattern's
  soundness and relevance to DOM-24/05/07/11, but the Skeptic's
  scale-appropriateness objection is carried forward explicitly rather than
  resolved here — a real open question for Stage -2.6/-2.7, not this record.

---

### PAT-049 — Hardened-Fork-as-Default-Deployment-Target

Pattern Name: Default-Image Override to a Hardened Fork
Problem Solved: Making every newly-deployed agent inherit a safer baseline
(the `context_id` memory-scoping fix) without touching the base framework's
own code or requiring per-deployment operator judgment.
Observed In: REPO-041 (`lib/services/harness.ts` `DEFAULT_IMAGE_REPO =
'cyborg-garden/hermes-agent-mt'`; `lib/services/config.ts` `defaultImage:
'ghcr.io/cyborg-garden/hermes-agent-mt:latest'`; test assertions in
`lib/services/__tests__/local-build.test.ts` explicitly confirming compose
output does NOT reference `nousresearch/hermes-agent`) — a single repo, but
the claim is code+test verified, not README-only.
Mechanism: The orchestration layer's default deployment target points at the
hardened/patched fork (PAT-047's mechanism) rather than plain upstream REPO-001
— one config point of leverage upgrades every newly-deployed agent's safety
posture without modifying the base framework.
Required Conditions: An orchestration/deployment layer that centralizes image
selection (as REPO-041 does); the hardened fork must itself remain
available and current.
Strengths: Verified by test assertion, not just claim — a deliberate, tested
choice. Single point of control; doesn't require forking or patching the
orchestrator's own core logic.
Weaknesses: Creates a soft dependency on the hardened fork's continued
maintenance and availability. Safety only propagates as far as this one
config value is respected everywhere agents get deployed.
Failure Modes: This is exactly the class of risk the GHCR-staleness trap
(documented in REPO-040's own audit — `ghcr.io/nimblecoai/*` images frozen at
their last pre-rename build, pulling successfully but silently serving stale
code) already demonstrated in this same trio. If image references are pinned
by tag (`:latest`) rather than digest, or if the org/image path changes again
without the deployment config being updated, newly-deployed agents could
silently regress to an unpatched baseline.
Complexity: Low to implement (a single config value); Medium ongoing risk to
sustain correctly.
Token/Cost Implications: None directly.
Human-Control Implications: Indirect but real — ensures new tenants/pages
inherit the safer default without a human needing to remember to configure
it per-deployment, reducing reliance on operator diligence at each
onboarding step.
Hermes Relevance: DOM-24 — a low-engineering-cost way to make "safe by
default" durable at fleet scale, complementary to PAT-047.
Alternative Patterns: PAT-047 (the underlying mechanism this pattern defaults
to)
Recommendation: CANDIDATE
Confidence: 70 — real and verified, but its safety value depends entirely on
an external fork's ongoing maintenance, a dependency risk demonstrated (not
hypothetical) elsewhere in this same trio.
Evidence: `nimblecoai-hermes-swarm-map.md` Dimension C/G.

---

### PAT-050 — Thin-Fork, Weekly-Automated-Rebase Maintenance Discipline

Pattern Name: Thin-Fork Maintenance Discipline
Problem Solved: Keeping a downstream fork/patch set against a fast-moving
upstream (REPO-001) low-risk and mergeable, if Hermes ever needs to consume
or maintain a patched version before an upstream PR lands.
Observed In: REPO-040 (`docs/rebase-journal.md`, read in full — 27 fork
commits sit atop 410 absorbed upstream commits; weekly automated rebase via
CI; only 3 conflicts across the entire history, each dated and documented
with resolution approach)
Mechanism: Keep the fork's own delta minimal and rebase against upstream
frequently (automated, weekly) rather than diverging; maintain a running,
dated, quantified journal of each rebase's conflict count and resolution.
Required Conditions: CI infrastructure capable of automated rebase; the
fork's own patch set must be kept genuinely small.
Strengths: Demonstrably low-conflict (3 conflicts / 410 commits) — a
quantified evidence trail, not a marketing claim. The journal itself is a
reusable evidence-quality pattern (dated, quantified operational log) worth
noting independent of the memory-scoping content it happens to document.
Weaknesses: Requires upfront CI/automation investment; the approach degrades
if the fork's own delta grows large, at which point weekly rebases become
increasingly conflict-prone.
Failure Modes: If the rebase automation itself breaks silently, drift from
upstream could accumulate unnoticed unless the journal is actively checked —
the journal is a record, not an alerting mechanism.
Complexity: Medium (CI/automation investment upfront; low ongoing burden once
built)
Token/Cost Implications: None directly (an engineering-process pattern, not a
runtime mechanism).
Human-Control Implications: None directly.
Hermes Relevance: DOM-24 primarily, but general: this is precisely the
discipline Hermes would need if it ever forks/patches REPO-001 rather than
waiting for PR #47552 to merge — a live decision surface for Stage -2.6.
Alternative Patterns: none observed in this cluster.
Recommendation: CANDIDATE
Confidence: 70 — single source; a well-evidenced process pattern (not a
runtime mechanism), so "strong candidate for adoption" is a less natural fit
than for PAT-046/PAT-047 — recorded as a "worth doing if Hermes ever forks
anything" note rather than a system component to build.
Evidence: `nimblecoai-hermes-agent.md` Dimension D/H/I.

---

### PAT-051 — Cost-Tracking-Without-Confirmed-Enforcement (Documented Gap, Not a Pattern to Adopt)

Pattern Name: Cost-Tracking Infrastructure Without Verified Budget
Enforcement
Problem Solved: N/A — this record documents a recurring *gap*, not a
mechanism to adopt, flagged because it directly bears on whether DOM-16
(cost-aware model routing / hard budget caps) can be considered satisfied by
anything in this cluster's source material.
Observed In: REPO-001 (`agent/billing_usage.py`, `agent/billing_view.py`,
`agent/usage_pricing.py`, `agent/aux_accounting.py` — enforcement UNKNOWN per
that audit's own Dimension G), REPO-041 (`app/api/harnesses/[id]/policy/
route.ts` computes `{budget, exceeded}` correctly, but no automatic
enforcement call site — pause/stop on `exceeded: true` — was found in a
targeted search of `app/` and `lib/`) — 2 independent sources exhibiting the
identical gap pattern. (Cluster D independently found the same gap shape for
REPO-001 alone — see PAT-028; this record additionally corroborates it with
REPO-041 as a second, structurally unrelated instance.)
Mechanism: Both systems compute and expose real spend/usage figures against a
budget, but in neither case could this pass confirm that exceeding the
budget automatically triggers any restrictive action (pausing an agent,
blocking a request). The computation surface is real; the enforcement hook is
either absent or was not found within this pass's search depth.
Required Conditions: N/A.
Strengths: N/A (not a pattern being recommended).
Weaknesses: The core weakness this record exists to flag: "cost tracking
exists" is not the same claim as "cost is capped," and treating the former as
satisfying the latter would be a real, specific error for Stage -2.6 to avoid
making, given DOM-16's need is explicitly for enforcement, not just
visibility.
Failure Modes: If Hermes's own cost-control design assumes one of these
subsystems already caps spend (because a `budget`/`exceeded` field exists),
actual spend could run past any intended ceiling with no automatic backstop,
since no enforcement call site was confirmed in either repo.
Complexity: N/A
Token/Cost Implications: This is precisely the point of the record — neither
audited mechanism was confirmed to bound cost automatically.
Human-Control Implications: If Hermes relies on a human periodically checking
a dashboard/CLI (`hermes insights`, Swarm Map's dashboard) rather than an
automatic hard stop, budget control becomes a human-diligence dependency, not
a structural guarantee — directly relevant to the same "guarantee vs.
default/discipline" theme as PAT-048.
Hermes Relevance: DOM-16 (cost control) — a documented gap, not a satisfied
need; directly corroborates Cluster D's PAT-028.
Alternative Patterns: PAT-026 (Cluster D's pre-call blocking enforcement
mechanism — the concrete shape enforcement would need to take, if Hermes
builds it rather than relying on either gap-exhibiting subsystem).
Recommendation: INSUFFICIENT EVIDENCE
Confidence: N/A — deliberately not scored, since this record documents an
open question (does either mechanism enforce?) rather than a candidate
mechanism with a confidence-bearing recommendation.
Evidence: `nousresearch-hermes-agent.md` Dimension G;
`nimblecoai-hermes-swarm-map.md` Dimension E/G — both explicitly label this
UNKNOWN, not confirmed-absent, in their own audits; this record's purpose is
to make sure that shared UNKNOWN doesn't get silently resolved to "satisfied"
by omission at Stage -2.6.

---

## DOM-25 — Explicit Gap (No Pattern Record Forced)

No mechanism resembling genuine autonomous external-technology-scouting with
recommendation synthesis (DOM-25's actual research question) was found
anywhere in this cluster's source material. The closest surface-level analog
is REPO-001's `hermes curator` CLI command ("Background skill maintenance —
status, run, pause, pin") and `hermes journey` ("Timeline of learned skills +
memories over time") — but neither's actual mechanism was inspected beyond a
one-line CLI reference table entry this pass (docs page not fetched, code not
read), so this cannot even be confirmed as a partial answer, let alone scored
as a pattern. `skill-catalog.md` independently confirms zero skill coverage
for DOM-25 (and DOM-24) at Stage -2.2.

**Status: documented gap, carried forward to Stage -2.6/-2.7 as a real,
unfilled research need.** If this gap persists through Stage -2.6, it is
itself a notable finding: Hermes' own Phase -2 research process may be the
closest existing model for what DOM-25 actually needs, since no external
precedent was found.

---

# Cross-Cluster Reconciliation

Each of the six extraction forks flagged mechanisms it noticed that belonged
primarily to another cluster's domain scope, so the coordinator could route
them rather than have them silently dropped (per the Stage -2.5 fork
instructions). This section closes the loop: which flags landed in a real
pattern record, and which remain open.

## Resolved (flag -> landing pattern)

| Flag raised by | Mechanism | Landed in |
|---|---|---|
| Cluster A | REPO-001 write-approval/tool-confirmation trigger logic (DOM-07/09) | PAT-020 (Cluster C), PAT-016 (Cluster B) |
| Cluster A | REPO-001 `hermes_state.py` hard-deletion / auto-prune (DOM-11) | PAT-021 |
| Cluster A | REPO-001 billing subsystem enforcement-unknown (DOM-16) | PAT-028, PAT-051 |
| Cluster A | REPO-001 profile-routing/tenant isolation (DOM-24) | PAT-046, PAT-047 |
| Cluster A | REPO-001 cron/ + WAL crash-safety (DOM-13) | PAT-023, PAT-024 |
| Cluster B | REPO-013's `ModelUpgradeHandler` / cost-routing (DOM-16) | Cross-referenced at PAT-015 <-> PAT-027 (not duplicated) |
| Cluster B | SKL-019/SKL-014 overlap (DOM-14) | PAT-025 |
| Cluster C | REPO-001 write-approval relevant to Cluster B's DOM-07 | Cross-referenced at PAT-020 <-> PAT-011/PAT-016 (not duplicated) |
| Cluster C | REPO-001 billing subsystem relevant to Cluster D | PAT-028 (Cluster D's own independent finding; PAT-023 also notes it) |
| Cluster D | D-06 (pr-agent advisory review) needs Cluster B's gate patterns | PAT-031 <-> PAT-011/PAT-016/PAT-017, explicitly paired |
| Cluster D | SKL-030/SKL-007 already Cluster B's (not re-extracted) | Correctly avoided — PAT-017, PAT-008 are the canonical records |
| Cluster E | E-05 brand-isolated storage vs. REPO-001 profile-routing (DOM-24) | PAT-037 <-> PAT-046/PAT-047, explicitly compared in both records |
| Cluster E | E-07 prompt-only enforcement vs. governance-toolkit (DOM-05/07) | PAT-039 <-> PAT-010, explicitly paired |
| Cluster E | E-01 ambiguity-routing corroborates Cluster B's DOM-09 finding | Folded into PAT-016's Strengths field as a third corroborating source |
| Cluster F | F-03 "ships mechanism, defaults off" theme relevant to Clusters B/C | Cross-referenced at PAT-048 <-> PAT-020/PAT-021 |
| Cluster F | F-06 cost-tracking-without-enforcement relevant to Cluster D | PAT-051 <-> PAT-028, explicitly corroborated as convergent finding |

## Unresolved — genuine open items for Stage -2.6/-2.7

These were flagged by one cluster's pass but never independently verified or
extracted as a pattern by the cluster they were routed to. They are real
research gaps, not oversights to silently paper over:

1. **Agentward's `scan/` static pre-deployment dependency/toolchain risk
   scanner** (flagged by Cluster B, relevant to DOM-17) was never
   independently read or extracted as a pattern by Cluster D — DOM-17's
   catalog coverage (PAT-030, PAT-032) does not include a pre-deployment
   dependency-scanning mechanism. Real gap.
2. **cronicle's `SKILL.md`-based skill-loading capability** (flagged by
   Cluster C as relevant to DOM-04/06) was not picked up as a distinct
   pattern by Cluster A — PAT-005 covers REPO-001's own SKILL.md
   compatibility but not cronicle's independent implementation of the same
   idea, which would have been a second corroborating source.
3. **wind-comic's Director-agent coordination role** (`types/agents.ts`,
   flagged by Cluster E as relevant to DOM-01) — neither the original
   Stage -2.4 audit nor Cluster A's Stage -2.5 pass read this file in full.
   Unread, unscored.
4. **REPO-001 Dimension E's publish-specific approval-gating, explicitly
   UNKNOWN (not confirmed absent)** (flagged by Cluster F as relevant to
   Cluster B's DOM-07) — Cluster B's sources (governance-toolkit, humanlayer,
   agentward, confidence-escalation) do not touch REPO-001 directly, so this
   specific UNKNOWN was never independently investigated. Still open.
5. **Cross-cluster orchestration-granularity triangulation**: PAT-001
   (narrow-waist philosophy), PAT-034 (7-subgraph decomposition), and
   PAT-042 (13-module decomposition) represent three different points on an
   orchestration-granularity spectrum that no single cluster's evidence is
   positioned to rank against Hermes' actual needs. Recommend a dedicated
   Stage -2.6/-2.7 comparison pass rather than resolving from any one
   cluster's framing.
6. **`hermes security audit` CLI's dependency-CVE stage** (capability-
   reference doc only; flagged by Cluster D relevant to PAT-032's DOM-17
   credential-scanning gap) — the underlying implementation was not read,
   only the CLI reference-table entry.

---

# Documented Gaps (Stage -2.5)

Per Section P2/P5 discipline, a missing candidate is recorded as an explicit
gap, not silently omitted or filled with a forced weak pattern:

- **DOM-11** (append-only memory/audit-log architecture): no direct
  off-the-shelf solution found across all of Phase -2's discovery. PAT-021
  names the failure mode to avoid (AVOID); PAT-019/PAT-022 are partial,
  adjacent mechanisms informative for a Hermes-specific design, not
  themselves a solution. Consistent finding across Stage -2.2, -2.3, and now
  -2.5.
- **DOM-16 enforcement** (does hermes-agent's own billing subsystem actually
  cap spend, or only report it?): unresolved — PAT-028 and PAT-051
  independently confirm the same UNKNOWN from two structurally unrelated
  repos (REPO-001, REPO-041). `docs/billing-lifecycle.md` remains unread.
- **DOM-22** (analytics & experimentation feedback loops): zero inspectable
  implementation found anywhere in Phase -2's 26 deep-audited repos or 32
  skill records. PAT-045 documents the closest (inadequate) comparison
  point.
- **DOM-25** (self-updating ecosystem-intelligence agent): zero mechanism
  found. Notable finding: Phase -2's own research process may be the closest
  existing model, since no external precedent exists.
- **DOM-23** (community/audience-engagement automation): remains BLOCKED per
  OQ-01, not researched this stage per Owner instruction — not a Stage -2.5
  gap, a standing scope exclusion.

---

# Gate G5 Self-Check (Stage -2.5 Exit Criteria, Master Plan Section 17)

- [x] **Patterns cite sources.** All 51 records have an `Observed In` and
  `Evidence` field citing REPO-/SKL- IDs and specific files/line numbers
  where available.
- [x] **Strong patterns cite >=2 independent sources OR one deep-audited
  high-confidence source.** Verified per-record above; every one of the 19
  STRONG CANDIDATE records states explicitly in its Recommendation/Evidence
  reasoning which branch of this rule it satisfies.
- [x] **Failure modes present.** All 51 records have a populated Failure
  Modes field (the 3 pure gap-documentation records — PAT-028, PAT-045,
  PAT-051 — use it to describe the risk of *mistaking the gap for a solved
  problem*, consistent with their nature as negative/gap findings rather than
  positive mechanisms).
- [x] **Human-control implications present.** All 51 records have this field
  populated, including explicit "None structurally" / "N/A" statements where
  genuinely inapplicable (e.g. PAT-006, PAT-009, PAT-041, PAT-042 — pure
  generation/integration mechanisms with no approval-gate relevance) rather
  than left blank.
- [x] **Every STRONG CANDIDATE has completed Adversarial Review (Section 13)
  and Role Notes with disagreement preserved (Section 14).** Verified: all
  21 STRONG CANDIDATE records (PAT-001, 003, 004, 005, 006, 010, 011, 016,
  017, 022, 023, 026, 027, 030, 033, 035, 036, 041, 043, 047, 048) carry both
  sections with at least Repository/Skill Auditor + Reliability Reviewer +
  Skeptic notes, and every Skeptic section preserves a real, unresolved
  objection rather than a rubber-stamped agreement. Note: PAT-020 and
  PAT-046 are deliberately rated CANDIDATE, not STRONG, despite strong
  individual source evidence — both are off-by-default/config-dependent
  mechanisms per their own Weaknesses fields, and the forks judged that
  dependency severe enough to withhold a STRONG rating even though the
  evidence-quality bar alone would have supported one.

**Stage -2.5 exit criteria met.** Every active (non-BLOCKED) domain has
either >=1 pattern record or an explicit documented gap (see table below).

---

# Domain Coverage Summary (Stage -2.5, cross-check for Stage -2.6)

| Domain | Patterns |
|---|---|
| DOM-01 (orchestration) | PAT-001, 002, 003, 004, 034, 042 |
| DOM-02 (agent contracts) | PAT-002, 003, 004, 007, 008 |
| DOM-03 (narrative/multi-modal gen) | PAT-034, 042, 044 |
| DOM-04 (skill design) | PAT-001, 005 |
| DOM-05 (prompt-reliability) | PAT-010, 039, 048 |
| DOM-06 (tool-use/MCP) | PAT-001, 005, 006, 009 |
| DOM-07 (approval gates) | PAT-004, 011, 016, 017, 020, 033, 035, 036, 040, 048 |
| DOM-08 (least-privilege) | PAT-010, 012, 013, 014, 046, 047 |
| DOM-09 (ambiguity) | PAT-004, 016, 033 |
| DOM-10 (progressive autonomy) | PAT-015, 016, 018, 025 |
| DOM-11 (append-only memory) | **GAP** — PAT-019, 020, 021 (AVOID), 022, 048 are adjacent/negative evidence only, not a solution |
| DOM-12 (narrative continuity) | PAT-022 |
| DOM-13 (scheduling reliability) | PAT-019, 023, 024 |
| DOM-14 (observability/trust) | PAT-018, 022, 025 |
| DOM-15 (pre-publish review) | PAT-008, 017, 031 |
| DOM-16 (cost control) | PAT-002, 003, 015, 023, 026, 027, 028, 029, 051 |
| DOM-17 (security/guardrails) | PAT-030, 032 |
| DOM-18 (competitive research) | PAT-036, 038 |
| DOM-19 (audience/brand strategy) | PAT-033, 036, 037, 038 |
| DOM-20 (multi-modal generation) | PAT-033, 034, 041, 042, 043 |
| DOM-21 (publish mechanics) | PAT-033, 035, 040 |
| DOM-22 (analytics feedback) | **GAP** — PAT-045 is a documented non-solution |
| DOM-23 (community management) | BLOCKED (OQ-01) — not in scope this stage |
| DOM-24 (multi-tenant onboarding) | PAT-037, 046, 047, 048, 049, 050 |
| DOM-25 (self-updating research agent) | **GAP** — no pattern found |

23 of 24 active domains (all except DOM-23, which is BLOCKED) have >=1
pattern record; 3 of those 23 (DOM-11, DOM-22, DOM-25) have only
gap-documentation, not a positive candidate — carried forward explicitly,
not silently dropped, per Section 8's Stage -2.5 exit criteria and Gate G5.

---

