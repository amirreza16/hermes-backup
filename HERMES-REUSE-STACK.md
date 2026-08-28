# Hermes Reuse Stack
Revision: 1 | Updated: 2026-08-29 | Phase -2 Stage -2.7 Decision File

This file is the concise, decision-oriented companion to
`phase-m2/capability-matrix.md` (full need-by-need mapping) and
`phase-m2/pattern-catalog.md` (full pattern records with adversarial review
and role notes). It mirrors the capability matrix's candidate set, organized
by Reuse Class instead of by Hermes research need. Every entry cites record
IDs; every REUSE entry lists compatibility conditions; every UNKNOWN lists
the specific missing evidence — per Section 16.3's rules.

**Per Master Plan Section 19.3, stated here as the receiver rule for Phase
-1:** Phase -1 MUST NOT assume any entry below is automatically appropriate.
Phase -1 owns which knowledge fits, what adapts or is rejected, what gaps
remain, and the best evidence-based specification path. Nothing below
constrains that choice beyond the Build Readiness North Star (Section 2.4).

A final negative-research pass (Section 13) was run across this whole stack
at synthesis time — see "Synthesis-Level Skeptic Pass" at the end of this
file — in addition to the per-pattern adversarial review already completed
for every STRONG CANDIDATE during Stage -2.5.

---

## REUSE

- **PAT-001 — Narrow-Waist Core + Plugin/Skill Edges**
  - Why: This is not a choice — it is the actual, deep-audited shape of
    REPO-001, Hermes' fixed base architecture. A small, stable core with all
    new capability arriving as CLI+skill / service-gated tool / plugin.
  - Evidence: REPO-001, `AGENTS.md` design philosophy + ~40 single-purpose
    `agent/` modules + 8-backend `plugins/memory/` tree (PAT-001).
  - Conditions: The three-way extension boundary is a documented convention,
    not a compiler-enforced one — nothing prevents Hermes-specific work from
    accidentally growing the core instead of using an extension surface.
    Reuse is conditional on actively defending that boundary in review, not
    automatic.

- **PAT-005 — Progressive-Disclosure Skill Packaging (SKILL.md + Validation Gate)**
  - Why: REPO-001's native `skills/` tree already uses the same SKILL.md
    progressive-disclosure shape as the Claude Skills convention — a real,
    positive compatibility finding, not assumed.
  - Evidence: REPO-001 Dimension H (`skills/creative/ascii-video/SKILL.md`
    etc.); SKL-009 for the optional validation/shibboleths discipline layered
    on top.
  - Conditions: File-shape compatibility is confirmed; behavioral/activation
    compatibility (does REPO-001's skill-matching logic behave the way
    Claude's does) is NOT independently verified — a real open item before
    treating this as fully proven, not just structurally plausible.

- **PAT-024 — WAL-Checkpoint Crash-Safety Discipline for SQLite-Backed Agent State**
  - Why: Already present in REPO-001's `hermes_state.py`, grounded in a
    named real production incident (a prior `TRUNCATE` checkpoint strategy
    that caused B-tree corruption, since replaced with `PASSIVE`).
  - Evidence: REPO-001 Dimension D, `hermes_state.py` inline comments citing
    the incident directly.
  - Conditions: Only reusable as-is if Hermes retains REPO-001's SQLite
    state layer unmodified; any future fork/patch to `hermes_state.py` (e.g.
    to address the PAT-021 auto-prune concern below) must preserve this
    specific checkpoint discipline, not just change the retention number.

---

## ADAPT

- **PAT-003 — Schema-Enforced Output With Retry-Until-Valid Loop**
  - What to preserve: The "validate immediately, typed-retry on failure, up
    to a configurable limit" shape — confirmed independently by three
    frameworks (openai-agents-python, adk-python, pydantic-ai).
  - What must change: REPO-001 has no equivalent — this is new build work on
    Hermes' substrate, not a port. Retry-exhaustion behavior (crash?
    escalate? drop the turn?) must be explicitly decided, not inherited
    silently from whichever pattern is copied.
  - Estimated adaptation level: HEAVY.

- **PAT-010 — Structural Pre-Execution Policy Gate (govern()/proxy interception)**
  - What to preserve: Enforcement moved out of the prompt into code — a
    wrapper/proxy that intercepts every tool call before execution against a
    declarative policy, surviving prompt drift by construction.
  - What must change: Requires a single funnel point for all of REPO-001's
    tool calls, not yet confirmed to exist; adopting either audited source's
    full policy-DSL/monorepo may be disproportionate for Hermes' current
    single-owner, small-known-tool-surface scale (Skeptic objection
    preserved in PAT-010's own record) — a lighter hardcoded interception
    point implementing the same concept is a live alternative.
  - Estimated adaptation level: MEDIUM.

- **PAT-011 — Approval-Coordinator as First-Class Execution Parameter (maker-checker gate)**
  - What to preserve: An action-execution call that takes an approval
    dependency as a parameter — blocks structurally on a persisted,
    externally-resolvable approval object, not a prompt-level pause.
  - What must change: REPO-001's execution model does not confirmed support
    suspend/resume the way this pattern needs; a simpler synchronous
    "block-and-wait-in-process" design may fully satisfy Hermes' actual
    single-owner need without either audited source's persistence/API
    infrastructure.
  - Estimated adaptation level: MEDIUM.

- **PAT-016 — Multi-Factor Risk/Ambiguity Gate, Assess-Before-Generate + Rolling-History**
  - What to preserve: Assess risk/ambiguity using more than the single
    triggering message, BEFORE generating or acting, against named
    thresholds, with a non-binary response set — the single best-corroborated
    DOM-09 finding (3 independently-original source domains converge,
    including a third corroboration from Cluster E's social-media-agent).
  - What must change: All illustrative thresholds ($0.50, 0.7 confidence)
    need Hermes-specific calibration; clinical tier-granularity from the
    crisis-response half must not be over-imported; explicitly exclude
    SKL-027's 30-day auto-delete policy (conflicts with the DOM-11
    never-delete principle).
  - Estimated adaptation level: MEDIUM.

- **PAT-017 — Gate Format Calibrated to Task Novelty (DO-CONFIRM/READ-DO)**
  - What to preserve: DO-CONFIRM for routine/familiar gated actions,
    READ-DO for novel ones; 5-9 item "killer checklists," refined
    iteratively against real outcomes — the strongest-evidenced single
    skill-catalog source in the whole project (externally-documented
    real-world outcomes, not vendor claims).
  - What must change: The source methodology assumes human-team dynamics
    (verbal confirmation, physical forcing functions) that need genuine
    reinterpretation for a solo-owner-plus-agent system.
  - Estimated adaptation level: LIGHT.

- **PAT-020 — Per-Subsystem Staged Write-Approval Gate**
  - What to preserve: REPO-001's real `write_approval.py` mechanism —
    origin-aware (foreground vs. autonomous-background writes), built in
    direct response to a named real incident.
  - What must change: **Ships disabled by default.** Adopting this means
    explicitly enabling it and verifying it, not assuming a stock deployment
    already has this protection.
  - Estimated adaptation level: LIGHT (a config flip plus verification, not
    a build — but not zero-cost, per this file's stated rule that an
    off-by-default mechanism is not free REUSE).

- **PAT-026 — Pre-Call Blocking Budget Enforcement**
  - What to preserve: A hook that fires before the model call is dispatched
    and can block outright — enforcement is structural, not a policy the
    caller has to remember to check. Two independent sources converge
    (litellm, code-verified; SKL-015, an unrelated skill family).
  - What must change: Whether REPO-001's own billing subsystem already does
    this is UNKNOWN (see PAT-028 below) — this pattern is likely necessary
    *new* build work, not an upgrade to an existing REPO-001 mechanism.
    Requires a single request chokepoint to exist.
  - Estimated adaptation level: HEAVY.

- **PAT-027 — Task-Classified Multi-Strategy Cost-Aware Model Routing**
  - What to preserve: Classify the task first, then route to a model tier —
    directly addresses Hermes' explicit co-equal cost/quality tension rather
    than uniformly downgrading everything.
  - What must change: No equivalent found in REPO-001 (its CLI commands are
    manual presets and error-triggered fallback, not automatic
    difficulty-based tiering); misclassification silently degrades quality
    without a loud error — needs pairing with a downstream quality gate.
  - Estimated adaptation level: MEDIUM.

- **PAT-032 — Entropy-Threshold Secret Detection**
  - What to preserve: A specific, concrete technique (entropy >4.5 on
    strings >20 chars) for catching exposed platform credentials.
  - What must change: Single skill-catalog source, no independent
    corroboration; addresses only the credential half of DOM-17, not the
    content-safety-guardrail half.
  - Estimated adaptation level: LIGHT.

- **PAT-035 — Reversibility-Differentiated Retry/No-Retry Publish Policy**
  - What to preserve: Classify publish-adjacent operations as safely-
    retryable vs. irreversible, and treat an irreversible-bucket timeout as
    "outcome unknown," never retried — the strongest convergent-evidence
    finding in the entire social-media-operations domain (two structurally
    unrelated implementations independently reach the same design).
  - What must change: Both source repos are AGPL-3.0 — the pattern is
    freely reusable, the code is not. The retryable/non-retryable
    classification must be re-derived per actual target platform; neither
    source traced what happens if the "already succeeded" persistence check
    itself fails.
  - Estimated adaptation level: MEDIUM.

- **PAT-036 — Fetch-Then-Tag Competitive/Audience Research Synthesis**
  - What to preserve: Real HTTP fetch + structured synthesis with mandatory
    source+date+confidence tagging per claim, honest-failure design
    (structured error, not silent hallucinated fallback) — the best-
    evidenced DOM-18/19 finding this phase.
  - What must change: Behavior rules are prompt-level-only, not structurally
    enforced (see PAT-039 below); social-platform scraping targets differ
    materially from this repo's general-marketing-page scraping and would
    need substantial rework.
  - Estimated adaptation level: MEDIUM.

- **PAT-037 — Brand-Isolated Storage Path Convention**
  - What to preserve: Simple, structural (filesystem-path), consistently-
    applied per-brand isolation — low cost to adopt.
  - What must change: Weaker-enforced than REPO-001's own profile-routing
    (PAT-046) — a real lightweight-vs-heavyweight tradeoff Phase -1 should
    weigh explicitly, not one this phase resolves.
  - Estimated adaptation level: LIGHT.

- **PAT-041 — Static/Dynamic Character-Feature Separation**
  - What to preserve: Separates unchanging physical traits from changeable
    attire/props at extraction time, schema-enforced, backed by a targeted
    regression-test suite.
  - What must change: Conditional entirely on Hermes actually needing visual
    generation (raw idea says "probably video," not confirmed); schema/
    parser plumbing is LangChain-specific, the prompt-design idea is not.
  - Estimated adaptation level: MEDIUM.

- **PAT-043 — Dual-Threshold Vision-LLM Consistency Audit**
  - What to preserve: Score-against-reference with conservative aggregation
    (minimum of 4 dimensions), dual thresholds (hard-regen/soft-warn), and
    explicit fail-open handling grounded in a documented real prior bug.
  - What must change: Threshold values (70/85) are this repo's tuning, not a
    universal constant; the fail-open-vs-fail-closed choice is a deliberate
    Hermes risk-tolerance decision, not something to inherit by default.
  - Estimated adaptation level: MEDIUM.

- **PAT-046 — Profile-Based Tenant Isolation (whole-instance boundary)**
  - What to preserve: REPO-001-native, mainline, real per-profile
    isolated memory/sessions when enabled.
  - What must change: Off by default; heavyweight per-boundary (a full
    profile per isolation need) — satisfies whole-page isolation, not
    fine-grained thread/DM-level isolation without provisioning a full
    profile per boundary.
  - Estimated adaptation level: LIGHT (enable + config), though real
    per-tenant resource cost scales linearly.

- **PAT-047 — Automatic Per-Context Memory Scoping (`context_id` routing)**
  - What to preserve: Cheap per-context isolation within one profile —
    the closer structural analog to the raw idea's "add a page without a
    from-scratch project" goal than PAT-046. Tested, actively hardened
    post-ship (two real production edge-case bugfixes already merged).
  - What must change: Not yet merged into REPO-001 mainline (PR #47552,
    open as of last access) — adopting today means depending on the
    `cyborg-garden` fork's ongoing maintenance, or reimplementing the fix
    independently while waiting on upstream review.
  - Estimated adaptation level: MEDIUM.

---

## REFERENCE

- **PAT-002 — Handoff-vs-Agents-as-Tools Composition With History Compression**
  - Pattern worth studying: Explicit two-primitive distinction (control-
    transfer vs. bounded call) with optional history compression to control
    token growth across repeated agent-to-agent calls.
  - Why not reuse directly: No equivalent in REPO-001; framework-specific
    machinery (`Handoff` class) that would need building from scratch, not
    porting.

- **PAT-006 — Session-Lifecycle-Aware MCP Client Wrapper**
  - Pattern worth studying: A dedicated session-manager component
    separating connection-lifecycle handling from tool-calling logic itself.
  - Why not reuse directly: REPO-001's own `optional-mcps/` depth was not
    independently traced this phase — this is a comparison baseline for a
    future deeper audit, not confirmed to be a gap REPO-001 actually has.

- **PAT-007 — Explicit 4-Section Agent Contract Prompt + Typed I/O + Test Checklist**
  - Pattern worth studying: A design-time contract-authoring discipline
    (role/scope/typed-I/O/test-checklist) including an explicit
    out-of-scope-refusal test case.
  - Why not reuse directly: Doc-only, single-vendor, no code or
    field-adoption evidence; a written contract with no runtime enforcement
    behind it (pair with PAT-003 if pursued).

- **PAT-009 — When-to-Use-MCP Decision Tree + Security-Hardening Sequence**
  - Pattern worth studying: A concrete decision tree for whether an
    integration warrants an MCP server at all, plus a fixed
    security-hardening order.
  - Why not reuse directly: Doc-only, single source, Node/TypeScript stack
    assumptions may not match REPO-001's actual MCP implementation language.

- **PAT-015 — Confidence-Threshold-to-Handler Escalation Pipeline**
  - Pattern worth studying: Four differentiated escalation handlers (human,
    model-upgrade, tool-restriction, compliance-logging) instead of one
    generic "ask a human" catch-all.
  - Why not reuse directly: Single source, zero external adoption signal;
    measures model-confidence, not task-ambiguity — a materially different
    question than DOM-09 actually asks.

- **PAT-018 — Urgency-Tiered Owner-Notification Escalation**
  - Pattern worth studying: 4-tier urgency classification (Immediate/
    Same-Day/Weekly/Archive-Only) that makes reduced owner oversight safe
    rather than reckless.
  - Why not reuse directly: Entirely software-dev-specific in its current
    form (git/build/npm status); needs full retargeting to content/social-
    ops events.

- **PAT-022 — Bi-Temporal Fact Invalidation over Destructive Update**
  - Pattern worth studying: Mark contradicted facts invalid/expired via
    timestamp fields rather than overwriting or deleting — a precise answer
    to "how do you update a fact without destroying history."
  - Why not reuse directly: The same library also exposes first-class
    hard-delete methods (`remove_episode()`) as ordinary public API — the
    non-destructive property lives at call-site discipline, not library
    structure. A graph-database dependency is real new infrastructure.

- **PAT-023 — DAG-Scheduled Task Execution with Wired Hard Budget-Abort**
  - Pattern worth studying: A per-task budget traced end-to-end from config
    through execution to a hard runtime abort — one of the few cleanly
    traced enforcement paths found in this research.
  - Why not reuse directly: REPO-001's own cron subsystem's full
    crash-recovery contract (`docs/chronos-managed-cron-contract.md`) was
    not read this phase; comparison baseline for a future deeper audit.

- **PAT-025 — Urgency-Tiered Human-Facing Status Digest**
  - Pattern worth studying: A weighted quality index plus threshold-based
    alerting as an owner-visibility layer sitting atop raw activity logs.
  - Why not reuse directly: Neither source is deep-audited code; both are
    software-dev/skill-invocation-specific and need real retargeting.

- **PAT-030 — Dependency-Aggregation Guardrail Architecture (Flow-DSL over Specialized Detectors)**
  - Pattern worth studying: A purpose-built DSL orchestrating a plurality of
    specialized third-party detectors instead of one team reimplementing
    every safety check from scratch.
  - Why not reuse directly: 28+ third-party integration surface is likely
    disproportionate for Hermes' current solo-owner scale; real
    learning-curve cost (Colang) with no dedicated team to absorb it.

- **PAT-031 — Advisory Critique-Before-Decision (Non-Blocking Structured Review)**
  - Pattern worth studying: Structured, multi-dimensional critique surfaced
    alongside a human decision point, without itself gating anything.
  - Why not reuse directly: Explicitly not an enforcement mechanism —
    correcting an earlier mischaracterization; must pair with a real gate
    (PAT-011/PAT-016/PAT-017) to satisfy Hermes' irreversible-action
    principle.

- **PAT-033 — Structured HITL Brief With Typed Multi-Action Response**
  - Pattern worth studying: The single best-evidenced approval-brief/
    action-taxonomy design found in this research (Edit/Rewrite/Accept/
    Reject, explicit non-guessing fallback on ambiguous input).
  - Why not reuse directly: LangGraph-`interrupt()`-specific pause/resume
    mechanics — REPO-001 has no equivalent primitive. Reusable as design,
    not as code.

- **PAT-034 — Decomposed-Subgraph Content Pipeline With Degrade-Not-Fail Fallback**
  - Pattern worth studying: Per-concern subgraphs with explicit bounded
    retry and fallback-not-failure on image generation.
  - Why not reuse directly: An orchestration-granularity choice this
    research did not adjudicate against PAT-001's narrow-waist philosophy or
    PAT-042's finer-grained alternative — flagged for Stage-1 triangulation,
    not resolved here.

- **PAT-048 — Three-Layer Deployment Separation (Image/Scaffolding/Artefact)**
  - Pattern worth studying: Makes safety mechanisms structurally
    non-overridable at deploy time by baking them into an immutable image
    layer, closing the "ships mechanism, defaults off" gap found repeatedly
    elsewhere in REPO-001.
  - Why not reuse directly: Commits to container-per-agent deployment — real
    architectural weight that may be disproportionate for a private,
    single-operator, VPS-hosted system (OD-001). Recommended as architecture
    reference, not a build target, at current scale.

---

## REJECT

- **PAT-021 — Time-Gated Auto-Deletion of Session/Transcript/Log History**
  - Reason: Directly, unconditionally destructive — no soft-delete,
    archival, or export step. Confirmed present (though off by default) in
    REPO-001 itself and unconditionally by default in a comparison repo
    (cronicle). Directly conflicts with Hermes' explicit never-delete
    behavioral principle. Recorded specifically so Hermes never re-inherits
    or reintroduces this shape, not because deletion logic in general is
    disallowed.

- **PAT-039 — Prompt-Level-Only Behavior Rules Without Structural Enforcement**
  - Reason: A well-specified but weakly-enforced control mechanism — good as
    a contract-writing style, unsafe as the sole safeguard for anything
    Hermes treats as safety-critical (e.g. brand isolation, never-delete,
    publish gating). Pairs with PAT-010 as the structural fix, not a
    standalone REJECT of the writing style itself.

- **PAT-044 — Fixed-Window Literal-Text Scene-Carryover Baseline**
  - Reason: No world-state tracking beyond an initial plan, no
    checkpointing, silent regex-parse failure path. Useful only as a
    documented lower bound, not as Hermes' primary narrative-continuity
    mechanism — DOM-03's research question explicitly anticipates more than
    this.

---

## UNKNOWN

- **DOM-11 (append-only memory & audit-log architecture) — no candidate**
  - Missing evidence: No repository or skill anywhere in this research's
    entire discovery set directly solves this. PAT-019/PAT-022 are partial,
    adjacent mechanisms; PAT-021 names the failure mode to avoid, not a
    solution.
  - Required follow-up: This is genuine Hermes-specific design work for
    Phase -1, not a research gap Phase -2 can close by searching further —
    consistent finding across Stage -2.2, -2.3, and -2.5.

- **PAT-028 / PAT-051 — REPO-001 & REPO-041 cost-tracking-without-confirmed-enforcement**
  - Missing evidence: Whether either subsystem's computed budget/exceeded
    figures actually trigger a restrictive action, or only report — two
    independent, structurally unrelated repos exhibit the identical
    unresolved gap.
  - Required follow-up: Read `docs/billing-lifecycle.md` (REPO-001) in
    full and re-search REPO-041's `app/`/`lib/` for an enforcement call site
    before Stage 1 treats either subsystem as satisfying DOM-16's
    enforcement need.

- **DOM-22 (analytics & experimentation feedback loops) — no candidate**
  - Missing evidence: Zero inspectable implementation anywhere in this
    research's 26 deep-audited repos or 32 skill records. PAT-045 is the
    closest comparison (skill-usage analytics, not content-performance
    analytics).
  - Required follow-up: A dedicated discovery pass scoped specifically to
    platform-analytics-ingestion tooling, not attempted this phase — flagged
    as a real, not exhaustively-searched, gap.

- **DOM-25 (self-updating ecosystem-intelligence agent design) — no candidate**
  - Missing evidence: No mechanism resembling autonomous external-
    technology-scouting-with-recommendation-synthesis found anywhere.
    REPO-001's `hermes curator`/`hermes journey` CLI commands are
    surface-level analogs, not inspected beyond a reference-table entry.
  - Required follow-up: Read the underlying `hermes curator`/`hermes
    journey` implementation before concluding this is a true external gap
    rather than an under-inspected internal candidate. Notable: this
    phase's own research process may be the closest existing model for what
    DOM-25 actually needs.

---

## Synthesis-Level Skeptic Pass (Section 13, run across the whole stack)

Beyond the per-pattern adversarial review already completed for all 21
STRONG CANDIDATE patterns during Stage -2.5, this pass asks: does the
**combination** of everything above introduce a risk no single pattern's
own review would surface?

1. **Cumulative "ships mechanism, defaults off" exposure.** PAT-020
   (write-approval), PAT-021 (auto-prune — REJECT), PAT-046/PAT-047
   (tenant isolation), and PAT-028/PAT-051 (cost enforcement) are five
   separate instances of the same underlying posture in REPO-001 and its
   derivatives: real protective mechanisms that do nothing unless an
   operator explicitly configures them on. Taken individually, each is a
   LIGHT-to-MEDIUM adaptation. Taken together, they imply Hermes cannot
   trust REPO-001's *defaults* for any of its three named behavioral
   principles (irreversible-action confirmation, cost control, never-delete)
   — it needs one deliberate, audited configuration profile (or a fork)
   that turns all of them on at once, not five independent opt-ins assumed
   safe in isolation. This is the single highest-leverage finding for
   Phase -1 to act on early, before any other adaptation work.
2. **AGPL exposure clusters, not just PAT-035.** Both of PAT-035's source
   repos (postiz-app, brightbean-studio) are AGPL-3.0; PAT-014's source
   (agentward) is Business Source License 1.1 until 2028. If Phase -1 ever
   considers *code*-level reuse (not pattern-level) from more than one of
   these, licensing review should happen once, up front, not per-candidate
   as each comes up.
3. **Orchestration-granularity question is asked three times, answered
   zero.** PAT-001 (narrow-waist), PAT-034 (7-subgraph), and PAT-042
   (13-module) each represent a real granularity choice, and no cluster's
   evidence in this phase is positioned to rank them against Hermes' actual
   needs — this was flagged individually at each pattern but is worth
   surfacing once, here, as a single open design question rather than three
   separate loose threads.
4. **Skeptic's overall verdict:** none of the above invalidates any REUSE/
   ADAPT entry — every objection was already weighed into that entry's own
   Confidence score and Adaptation Level. The value of this pass is
   surfacing three *cross-cutting* items (config-profile need, licensing
   review timing, granularity triangulation) that no single pattern record
   could see on its own, for explicit Phase -1 attention.
