# Hermes Phase -2 Skill Catalog

Stage -2.2 (Skill Discovery) | Revision: 1 | Updated: 2026-08-23
Schema: Master Plan Section 9.1 | Scoring: Section 10 | Negative research: Section 13

Primary source: Campaign SCS (Section 15.1), `https://someclaudeskills.com/skills`
(181 skills total, catalog fetched 2026-08-23). 32 skills inspected beyond title/
description: the 18 Section 15.1 suggested leads in full, plus 14 additional skills
selected via Hidden Pattern Mining against Hermes' behavioral principles and the
domain registry. Skills not inspected were screened out by title/category as clearly
outside all 25 domains (e.g. Windows-95-aesthetic web design, pet memorial creators,
knot theory) — per Section 15.1/Stage -2.2 rules, Claude does not complete the list
for its own sake and does not rate by title.

**Evidence Quality note (applies to all records below):** every record's evidence is
single-source (the rendered someclaudeskills.com documentation page for that skill),
not cross-verified against the underlying `erichowens/some_claude_skills` GitHub
repo's actual script/code contents. This caps Evidence Quality at Medium for the
whole catalog (Section 12 evidence hierarchy places docs below source code). No score
below reflects code-level verification. Scores are therefore conservative relative to
what a Section 9.3-style deep audit would produce; none of these are being proposed
for REUSE (direct adoption) — the ceiling classification used throughout is ADAPT.

**License note (applies to all records below):** no individual skill in this gallery
states an explicit per-skill license; the site carries a general "© 2026 Curiositech"
notice. Treat licensing as unclear pending direct repository inspection — this alone
would cap Licensing Clarity (Section 10.1.8, max 5) low for every record.

---

## SKL-001 — Orchestrator
```
Skill ID: SKL-001
Name: Orchestrator
Source: SomeClaudeSkills
Repository: erichowens/some_claude_skills (unverified — not cloned)
URL: https://someclaudeskills.com/docs/skills/orchestrator/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Master coordinator that delegates to specialist skills, synthesizes outputs, and creates new skills on-the-fly when capability gaps emerge.
Original Domain: General multi-skill software/product work (web design, research, docs).

Core Method: Five-phase process — Understanding, Decomposition, Delegation, Coordination, Synthesis. Decision logic for engaging multiple specialists vs. keeping work simple; invokes skill-coach on capability gaps rather than working around them.
Primary Workflow: Complex request -> phase 1-5 -> integrated deliverable.
Inputs: Complex multi-domain requests.
Outputs: Integrated deliverables, implementation roadmaps, unified documentation.
Dependencies: A pool of specialist skills to delegate to; skill-coach for gap-filling.
Activation Conditions: "orchestrate," "coordinate," "multi-skill," "complex task," "decompose," "synthesize," "delegate," "missing skill."

Generalizable Components: The 5-phase coordinate/delegate/synthesize loop and the explicit "don't work around a capability gap, name it and fill it" rule are portable to any small fixed-role agent system.
Project-Specific Assumptions: Assumes a large, growable pool of named specialist skills to delegate across — built for a many-skill ecosystem, not a fixed 2-role system.
Domain-Specific Assumptions: Software/product-development framing throughout examples.

Hermes Research Domains Covered: DOM-01

Overlap With: SKL-019 (Liaison, shares coordination-visibility concern), SKL-020 (Team Builder, shares gap-filling logic)
Potential Conflicts: None identified.

Evidence Quality: Medium — single doc source, no code inspected
Maintenance Signal: Unknown (no commit/activity data in fetched content)
Documentation Quality: High — clearly structured, explicit decision logic

Reuse Classification: ADAPT
Confidence: 65
Score: 72
Reasoning Summary: Clean 5-phase coordination loop with an explicit, inspectable delegation/synthesis mechanism (Relevance ~20/25, Generalizability ~11/15 — needs real adaptation for Hermes' fixed 2-role case rather than a large specialist pool). Useful as a comparison baseline for DOM-01's reframed question against hermes-agent's own orchestration mechanism, not a direct fit as-is.
```

## SKL-002 — Systems Thinking
```
Skill ID: SKL-002
Name: Systems Thinking
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/systems_thinking/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Diagnose why systems perpetuate problematic behavior via stocks/flows/feedback-loop analysis; select structural interventions over symptomatic fixes.
Original Domain: General systems analysis (based on Meadows' "Thinking in Systems").

Core Method: Three decision trees (Systems Analysis, Stock-Flow Analysis, Trap Escape) plus a leverage-point hierarchy ranking intervention types from parameter tweaks (lowest leverage) to paradigm shifts (highest).
Primary Workflow: Map behavior over time -> identify stocks/flows -> spot feedback loops/traps -> pick highest-leverage intervention.
Inputs: A persistent or recurring problem description.
Outputs: Structural diagnosis + ranked intervention recommendation.
Dependencies: None technical — an analytical framework, not a tool.
Activation Conditions: Recurring problems, policy resistance, exponential/oscillating/eroding performance patterns.

Generalizable Components: The leverage-point ranking is a genuinely reusable prioritization lens (e.g., for judging whether a Hermes fix should be a parameter tweak or a structural redesign).
Project-Specific Assumptions: None strong — it's domain-agnostic by design.
Domain-Specific Assumptions: Examples drawn from organizational/policy contexts, not software agents specifically.

Hermes Research Domains Covered: DOM-19 (loosely — as a strategy-decision lens, not a content mechanism)

Overlap With: None significant.
Potential Conflicts: None.

Evidence Quality: Medium — grounded in an external, well-regarded book (Meadows 2008), but the skill's own application to software/agent contexts is unverified.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 50
Score: 55
Reasoning Summary: Intellectually solid and well-sourced, but it's an analytical lens, not an inspectable agent mechanism — no direct research-domain need consumes it as a component. Kept as REFERENCE for Phase -1 strategic thinking, not scored higher since Relevance to the 25-domain registry is indirect at best.
```

## SKL-003 — Research Analyst
```
Skill ID: SKL-003
Name: Research Analyst
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/research_analyst/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Systematic landscape/competitive research producing evidence-based recommendations across market, technology, and methodology domains.
Original Domain: General market/technology research.

Core Method: 5-phase process (Scope Definition, Information Gathering, Analysis & Synthesis, Insight Generation, Findings Presentation) with explicit source-prioritization rules (recency preference, multi-source corroboration).
Primary Workflow: Research question -> multi-source gathering with credibility checks -> synthesis -> recommendations with citations.
Inputs: Research questions, stakeholder context, constraints.
Outputs: Executive summaries, detailed reports, competitive matrices, landscape maps.
Dependencies: Read, Grep, Glob, WebSearch, WebFetch tools; pairs with Orchestrator, Competitive Cartographer, Design Archivist.
Activation Conditions: "market research," "competitive analysis," "landscape research," "best practices," "trend analysis."

Generalizable Components: The 5-phase pipeline and source-credibility discipline (recency + multi-source corroboration) map cleanly onto Hermes' research-agent role (b) — content/competitive research per page.
Project-Specific Assumptions: Assumes generic web-search/fetch tool access, which any Hermes research agent would also need — low friction to adapt.
Domain-Specific Assumptions: Framed for market/tech research broadly, not social-media-specific competitive research — would need retargeting to platform-specific signals (post performance, hashtag trends, etc.).

Hermes Research Domains Covered: DOM-18

Overlap With: SKL-004 (Competitive Cartographer — narrower, positioning-focused variant)
Potential Conflicts: None.

Evidence Quality: Medium — single source, mechanism well-specified.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 74
Reasoning Summary: Directly matches DOM-18's need for a competitive/audience-research pipeline with real source-credibility discipline (not just "search the web"). Retargeting from generic market research to social-platform-specific signals is the main adaptation cost — this is exactly the comparison-baseline role DOM-18 was scoped for.
```

## SKL-004 — Competitive Cartographer
```
Skill ID: SKL-004
Name: Competitive Cartographer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/competitive_cartographer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Maps competitive landscapes onto 2D positioning axes to reveal defensible "white space" and differentiation strategy.
Original Domain: Product/brand positioning strategy.

Core Method: 6-step process (Define Space, Identify Players, Analyze Positioning, Create Map, Find White Space, Recommend Strategy); prioritizes user authenticity over trend-chasing; treats constraints as potential advantages.
Primary Workflow: Domain + offer -> map direct/adjacent/aspirational competitors -> plot on 2D axes -> find gaps -> recommend positioning headline.
Inputs: User's background, offerings, market context.
Outputs: Spatial competitive maps, white-space recommendations, positioning strategy.
Dependencies: Read, Write, WebSearch, WebFetch; pairs with Career Biographer, Research Analyst.
Activation Conditions: Competitive analysis, market positioning, differentiation, repositioning requests.

Generalizable Components: The "map competitors on 2D axes, then find defensible white space" mechanism is a concrete, executable method (not just "do competitive research") directly useful for each social page's positioning within its niche.
Project-Specific Assumptions: Assumes a single coherent "offer" to position — Hermes would run this once per page, not once for the whole system.
Domain-Specific Assumptions: General product/brand framing, not social-content-specific, but the mechanism transfers cleanly.

Hermes Research Domains Covered: DOM-18, DOM-19

Overlap With: SKL-003 (Research Analyst — broader; this is the narrower positioning-specific method)
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 73
Reasoning Summary: Concrete, well-specified positioning method with genuine decision logic (white-space-finding, anti-"me-too" discipline) rather than generic research advice. Strong comparison-baseline candidate for DOM-18's per-page competitive-research need.
```

## SKL-005 — Product Appeal Analyzer
```
Skill ID: SKL-005
Name: Product Appeal Analyzer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/product_appeal_analyzer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Evaluates product/content desirability via a three-part "Desirability Triangle" (Identity Fit, Problem Urgency, Trust Signals) and a weighted-impact prioritization formula.
Original Domain: Landing-page/product-marketing conversion analysis.

Core Method: 4-step process scoring 9 dimensions (1-10) across the triangle; objection mapping by type; prioritization via (Users Affected x Severity) / Fix Difficulty.
Primary Workflow: Landing/product page -> persona identification -> triangle scoring -> objection mapping -> prioritized fix list.
Inputs: Landing pages, positioning documents, messaging frameworks.
Outputs: Desirability scores, 5-second comprehension test results, top objections with mitigations, prioritized recommendations.
Dependencies: Read, Write, Edit, WebFetch; pairs with UX Friction Analyzer, Competitive Cartographer.
Activation Conditions: Market positioning, desirability, value-prop clarity, messaging strategy.

Generalizable Components: The weighted-impact formula (Users x Severity / Difficulty) is a clean, reusable prioritization mechanism transferable to any "which fix matters most" decision, including content-strategy prioritization (DOM-19) and quality-gate triage (DOM-15).
Project-Specific Assumptions: Assumes a single static artifact (a landing page) to evaluate — would need adaptation to evaluate a content series' overall appeal rather than one static page.
Domain-Specific Assumptions: Conversion/marketing framing, not narrative-content framing.

Hermes Research Domains Covered: DOM-19

Overlap With: None significant among inspected skills.
Potential Conflicts: None.

Evidence Quality: Medium — single source, internally consistent formula.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 71
Reasoning Summary: The Desirability Triangle and impact-prioritization formula are genuinely reusable decision mechanisms for DOM-19's brand/strategy layer, though built for static marketing pages rather than an evolving content series — real but moderate adaptation cost.
```

## SKL-006 — Task Decomposer
```
Skill ID: SKL-006
Name: Task Decomposer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/task_decomposer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Breaks natural-language problems into DAG-suitable sub-tasks as the foundational step before DAG construction/execution.
Original Domain: General software/research/design/business/ML project decomposition.

Core Method: 5-step process — Domain Detection, Phase Identification, Sub-Task Specification, Dependency Mapping, Structured Output. Concrete/vague classification per phase ("can specify now" vs. "unclear until later").
Primary Workflow: Problem description -> domain classification -> phase-pattern application -> sub-task list with dependencies and cost estimate.
Inputs: Natural-language problem description.
Outputs: Structured decomposition (phases, sub-tasks, dependency map, execution waves, cost range).
Dependencies: Domain meta-skill patterns; downstream dag-planner/dag-runtime/dag-skills-matcher tools.
Activation Conditions: Breaking a vague problem into concrete sub-tasks; identifying phases/dependencies/parallelization.

Generalizable Components: The concrete-vs-vague sub-task classification and dependency-mapping logic are reusable for breaking a content series into schedulable steps.
Project-Specific Assumptions: Assumes a DAG execution runtime exists downstream (dag-planner etc.) — Hermes would need its own equivalent.
Domain-Specific Assumptions: None of the five listed domain patterns (software/research/design/business/ML) is "serialized narrative content" — this is a real, documented gap: the mechanism decomposes tasks but has no explicit concept of cross-step narrative-state carryover (tone, plot/thread continuity), which is the specific requirement DOM-03 was scoped around.

Hermes Research Domains Covered: DOM-03

Overlap With: None significant.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 55
Score: 68
Reasoning Summary: Solid generic decomposition mechanism, but DOM-03's core need — preserving narrative continuity across chained sub-tasks — is not addressed by this skill at all; it would need to be paired with a separate continuity-tracking mechanism (see DOM-12) to actually fit Hermes' "chained/narrative, not independent pieces" requirement. Score capped below 70 because a core piece of the domain's need is an unaddressed gap, not because the mechanism itself is weak.
```

## SKL-007 — Recursive Synthesis
```
Skill ID: SKL-007
Name: Recursive Synthesis
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/recursive_synthesis/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Orchestrates multi-agent document creation via adversarial review and synthesis, producing authoritative founding documents (constitutions, charters, architecture records).
Original Domain: Organizational governance-document drafting.

Core Method: 6-phase process — Setup (select 10 cognitively diverse agents), Divergence (parallel independent position papers), Synthesis (ranked-choice principle hierarchy), Commentary (mandatory steel-manned adversarial review), Reality Check (fresh practitioner audit for implementability), Final Merge (Constitution + Practitioner's Guide + Editorial Notes + Dissenting Appendix).
Primary Workflow: Problem definition -> 10 parallel position papers -> synthesis -> adversarial commentary -> implementability audit -> final merge.
Inputs: Problem definition, agent roster.
Outputs: Constitution (authoritative), Practitioner's Guide, Editorial Notes, Dissenting Appendix.
Dependencies: Opus-tier model for philosophical reasoning, Sonnet-tier for technical agents; DAG-based parallelization; no cross-agent communication during divergence/synthesis phases.
Activation Conditions: Constitutional/governance documents, contested architecture decisions, founding documents where correctness outweighs speed.

Generalizable Components: The structured-adversarial-synthesis pattern (diverge -> synthesize -> steel-manned critique -> reality-check -> merge) is a genuinely strong mechanism for high-stakes, rare decisions — notably, it mirrors this very Master Plan's own Section 13/14 negative-research and role-simulation protocol.
Project-Specific Assumptions: Assumes ~10 parallel agent invocations per use, each substantial (position paper + later commentary) — a materially expensive pattern.
Domain-Specific Assumptions: Built for one-time governance documents, not repeated content decisions.

Hermes Research Domains Covered: DOM-02, DOM-15 (as a candidate mechanism for rare, high-stakes decisions only — not routine per-post review)

Overlap With: None directly redundant; conceptually related to SKL-012 Human Gate Designer and SKL-030 Checklist Discipline (all three are quality-assurance mechanisms at different granularities).
Potential Conflicts: None.

Evidence Quality: Medium — single source, no field-adoption evidence shown.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT (narrow scope — see Adversarial Review)
Confidence: 65
Score: 76

Adversarial Review (Section 13):
Q1 (assumptions): Assumes ~10 genuinely diverse, capable agent perspectives and a governance-document-scale task; assumes distinct "diversity" is achievable across agents likely drawn from the same underlying model family (illusory-diversity risk).
Q2 (failure modes for Hermes): If applied to routine per-post content review instead of rare governance decisions, this pattern would blow the cost budget and destroy throughput — a direct conflict with Hermes' co-equal cost and quality constraints (DOM-16).
Q3 (complexity introduced): High — 10-agent parallel run, multi-phase synthesis, steel-manning discipline, final multi-document merge.
Q4 (lock-in): Low — pure prompt/orchestration pattern, no infrastructure lock-in.
Q5 (evidence missing): No field metrics on how often the Reality Check phase actually catches real errors; single-source documentation only.
Q6 (simpler competing approach): A standard single- or dual-reviewer critique loop (the baseline already implied by DOM-15) handles routine per-post review at far lower cost; Recursive Synthesis only earns its cost for genuinely rare, high-stakes Hermes decisions (e.g., defining a page's brand constitution once, or Hermes' own top-level behavioral charter).
Q7 (marketing vs. engineering): Genuine, well-specified engineering technique grounded in real deliberation/ensemble-review practice, not marketing fluff — the risk is scope-misapplication, not that the mechanism is hollow.
Reasoning Summary: Adversarial review surfaced a real and material scope-fit risk — this mechanism would violate Hermes' cost constraint if misapplied to routine content review — which is exactly why it is classified ADAPT with a narrow recommended scope (one-time governance/constitution-style documents only) rather than a broader REUSE-leaning recommendation, and why the score stays under the Strong Candidate band despite a high-quality mechanism.
```

## SKL-008 — Agent Creator
```
Skill ID: SKL-008
Name: Agent Creator
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/agent_creator/
License: References @modelcontextprotocol SDK licensing for its technical dependency; skill itself unlicensed
Last Verified: 2026-08-23

Original Purpose: Meta-agent for creating new custom agents, skills, and MCP integrations via structured design methodology.
Original Domain: General agent/tooling meta-development.

Core Method: 7-step rapid-prototyping process (Requirement Analysis, Persona Development, Knowledge Mapping, Structural Organization, Example Creation, Documentation, Validation), ~45 min total; 3 template categories (Technical Expert, Creative/Design, Orchestrator); progressive disclosure to avoid knowledge-dump anti-patterns.
Primary Workflow: Domain requirement -> template selection -> persona/knowledge/structure -> validated agent spec.
Inputs: Domain requirements, capability gaps.
Outputs: Complete agent specification (persona, knowledge encoding, MCP integrations, docs, validation artifacts).
Dependencies: Skill Coach (quality review), Skill Documentarian; MCP SDK packages.
Activation Conditions: "create agent," "new skill," "MCP server," "custom tool," "agent design."

Generalizable Components: The template-category framework (Technical Expert / Creative / Orchestrator) is a useful comparison point when deciding how to characterize Hermes' content-generation vs. research agents.
Project-Specific Assumptions: Assumes the Claude Skills/MCP tooling ecosystem specifically.
Domain-Specific Assumptions: Generic agent-authoring; not social-media-specific.

Hermes Research Domains Covered: DOM-04

Overlap With: SKL-009 (Skill Architect), SKL-010 (Skill Creator), SKL-022 (Skill Coach) — all meta-tools for authoring Claude-ecosystem building blocks; see Deduplication Cluster 1.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 74
Reasoning Summary: Solid, concrete agent-authoring methodology usable as a comparison baseline for DOM-04's reframed question (how hermes-agent's own capability-authoring mechanism compares). Not selected as the dedup-cluster canonical (see SKL-009) since Skill Architect's validation tooling is more complete.
```

## SKL-009 — Skill Architect
```
Skill ID: SKL-009
Name: Skill Architect
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skill_architect/
Repository: erichowens/some_claude_skills
License: Not explicitly stated
Last Verified: 2026-08-23

Original Purpose: Unified authority for creating expert-level Claude Skills, combining workflow methodology with domain-expertise encoding.
Original Domain: Claude Skills authoring.

Core Method: 6-step process (Understand with Examples, Plan Reusable Contents, Initialize, Edit, Validate & Package, Iterate); progressive disclosure (metadata -> SKILL.md -> on-demand resources); "shibboleths" concept (encode expert judgment, not generic facts); explicit decision-tree-over-template guidance; mandatory "NOT for" exclusion clauses.
Primary Workflow: Gather examples -> plan resources -> init script -> build tools before docs -> validate (errors -> warnings -> suggestions) -> iterate on real usage.
Inputs: Domain expertise, usage examples, anti-patterns, temporal knowledge.
Outputs: Skill directory (SKILL.md <500 lines, /scripts, /references, /assets).
Dependencies: `validate_skill.py`, `check_self_contained.py`; required frontmatter fields (name, description, allowed-tools).
Activation Conditions: Creating/auditing skills, improving activation rates, debugging skill failures.

Generalizable Components: Progressive disclosure, the "shibboleths" concept (differentiating real expert judgment from generic filler), and validation-script-backed quality gating are all portable ideas for however Hermes structures its own capability units.
Project-Specific Assumptions: Assumes the SKILL.md / progressive-disclosure packaging convention specifically — a real, unresolved dependency, since whether `hermes-agent`'s native capability mechanism is compatible with (or bridgeable to) this convention is exactly DOM-04's reframed open question, not yet answered.
Domain-Specific Assumptions: Claude-ecosystem-specific tooling (the two named validation scripts).

Hermes Research Domains Covered: DOM-04

Overlap With: SKL-008 (Agent Creator), SKL-010 (Skill Creator), SKL-022 (Skill Coach) — Deduplication Cluster 1; this is the canonical selection (see deduplication-map.md).
Potential Conflicts: None.

Evidence Quality: Medium — single source; script names given but scripts not inspected.
Maintenance Signal: Unknown
Documentation Quality: High — most complete of the four skill-authoring variants (only one with named validation tooling and explicit anti-pattern clauses)

Reuse Classification: ADAPT
Confidence: 60
Score: 79
Reasoning Summary: The most architecturally complete of the four skill-authoring-methodology skills found (validation scripts, shibboleth concept, mandatory exclusion clauses raise Architectural Quality and Evidence Quality above its siblings). Held just under the Strong Candidate band because a material, unresolved dependency remains: whether this packaging convention is compatible with `hermes-agent`'s actual native capability mechanism is unknown until Stage -2.4 — flagging it explicitly rather than assuming compatibility.
```

## SKL-010 — Skill Creator
```
Skill ID: SKL-010
Name: Skill Creator
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skill_creator/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Guides creation of modular skill packages extending Claude's capabilities.
Original Domain: Claude Skills authoring (packaging/distribution emphasis).

Core Method: 6-step process near-identical to Skill Architect's (Understanding, Planning, Initializing via `init_skill.py`, Editing, Packaging via `package_skill.py` into a distributable .zip, Iteration); resource taxonomy (Scripts=deterministic code, References=contextual docs with grep-pattern guidance for >10k-word files, Assets=output-only templates).
Primary Workflow: Same as Skill Architect but with distribution/packaging as its distinguishing emphasis (zip output).
Inputs/Outputs: Same category as SKL-009, output specifically a distributable .zip.
Dependencies: `init_skill.py`, `package_skill.py`.
Activation Conditions: Creating or updating a skill.

Generalizable Components: The Scripts/References/Assets resource taxonomy is a clean, reusable organizing principle.
Project-Specific Assumptions: Same Claude Skills packaging convention as SKL-009.
Domain-Specific Assumptions: Same as SKL-009.

Hermes Research Domains Covered: DOM-04

Overlap With: SKL-008, SKL-009, SKL-022 — Deduplication Cluster 1 (secondary reference; canonical is SKL-009 Skill Architect, which has more complete validation tooling and explicit anti-pattern guidance).
Potential Conflicts: None — genuinely near-duplicate, not conflicting.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 55
Score: 62
Reasoning Summary: Near-duplicate of Skill Architect with a packaging/distribution emphasis; kept as a secondary reference for the Scripts/References/Assets taxonomy specifically, not scored independently high since it's redundant with the cluster's canonical pick on every other dimension.
```

## SKL-011 — Skill Grader
```
Skill ID: SKL-011
Name: Skill Grader
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skill_grader/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Mechanical 10-axis rubric for grading Claude Skill quality (A+ to F), producing prioritized improvement recommendations.
Original Domain: Claude Skills quality auditing.

Core Method: Read full skill folder -> score 10 axes (0-100) -> convert to letter grades -> weighted overall (Description Quality and Scope Discipline at 2x weight, others 1x; formula (2xAxis1 + 2xAxis2 + Axes3-10)/12) -> write 1-3 improvements per below-B+ axis.
Primary Workflow: Skill folder -> per-axis scoring -> weighted grade -> improvement report.
Inputs: Skill folder contents (SKILL.md, references, CHANGELOG, README).
Outputs: Grading report (axis table, top 3 improvements, detailed feedback).
Dependencies: None technical — self-contained rubric.
Activation Conditions: Auditing/comparing skill quality, prioritizing improvement roadmaps.

Generalizable Components: The weighted-rubric-with-calibrated-axes design pattern is directly analogous to (and could inform) how Hermes might design its own DOM-15 pre-publish quality-gate rubric — a rubric-design pattern, not a content-review rubric itself.
Project-Specific Assumptions: Grades *skills specifically*, not general content.
Domain-Specific Assumptions: Claude Skills format-specific axes (frontmatter, progressive disclosure, etc.) don't transfer directly to grading social content.

Hermes Research Domains Covered: DOM-04, DOM-15 (as a rubric-design analog, not directly executable)

Overlap With: None directly redundant.
Potential Conflicts: None.

Evidence Quality: Medium — single source, formula fully specified.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 55
Score: 65
Reasoning Summary: Not directly applicable (it grades skills, not social content), but the weighted-axis rubric-design pattern is a legitimate reference point for constructing Hermes' own pre-publish quality rubric under DOM-15.
```

## SKL-012 — Human Gate Designer
```
Skill ID: SKL-012
Name: Human Gate Designer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/human_gate_designer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Designs human-in-the-loop review checkpoints for DAG workflows — what information humans see, how they give feedback, how decisions route back into execution.
Original Domain: General DAG-based agent workflow design.

Core Method: Gate-placement decision tree evaluating irreversibility, user-facing-output status, cost threshold (>$0.50 example), confidence threshold (<0.7 example), and task ambiguity. Presentation design surfaces prior DAG state, highlighted decisions, confidence/cost metrics, and a modification field — never raw output alone. Three feedback pathways: Approve (continue), Modify (re-execute with feedback injected into prompt), Reject (node/phase/full-abort granularity).
Primary Workflow: DAG node output + metadata -> decision tree -> gate placed or skipped -> human sees contextual presentation -> routes via approve/modify/reject.
Inputs: DAG node outputs, confidence scores, cost data, task context.
Outputs: Gate placement specifications, presentation templates, feedback-injection prompts, routing logic.
Dependencies: Task Decomposer (identifies gate-needing nodes), Output Contract Enforcer (validates gate schemas).
Activation Conditions: "human review," "approval gate," "human-in-the-loop," "approval workflow."

Generalizable Components: This is the single most directly-matching mechanism found in this pass for Hermes' two explicit behavioral principles — irreversible-action confirmation (DOM-07) and ambiguity-triggered stopping (DOM-09) — expressed as an actual multi-factor decision tree with named thresholds and a non-binary (approve/modify/reject-at-granularity) feedback model, not just "add a human review step."
Project-Specific Assumptions: Assumes agents already emit calibrated confidence scores and cost estimates per action — this is itself a real dependency (verbalized LLM confidence is often poorly calibrated), not a given.
Domain-Specific Assumptions: DAG-node framing; the specific $0.50/0.7 thresholds are illustrative defaults, not empirically validated — would need Hermes-specific tuning.

Hermes Research Domains Covered: DOM-07, DOM-09

Overlap With: SKL-013 (Output Contract Enforcer — complementary, validates what a gate passes through rather than deciding when to gate).
Potential Conflicts: None.

Evidence Quality: Medium — single source; thresholds are stated as examples, not validated constants.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 70
Score: 82

Adversarial Review (Section 13):
Q1 (assumptions): Requires agents to already produce calibrated per-action confidence and cost estimates for the decision tree to function — a real prerequisite, not automatically true of any agent runtime (including `hermes-agent`, unverified until Stage -2.4).
Q2 (failure modes for Hermes): If confidence scores are poorly calibrated (a known general LLM weakness), the <0.7 threshold could both under-trigger (false confidence skips a needed gate) and over-trigger (excessive gating causes approval fatigue) — this needs its own evaluation, not blind trust in the threshold.
Q3 (complexity introduced): Moderate — building reliable per-action confidence/cost instrumentation is nontrivial engineering, separate from the gate-decision logic itself.
Q4 (lock-in): Low — pure decision-logic pattern, portable regardless of underlying framework.
Q5 (evidence missing): Single-source documentation; no field validation of the specific thresholds shown.
Q6 (simpler competing approach): A blanket "always confirm before publish" rule (which the raw idea already requires for publish specifically) is simpler and already mandatory regardless of this skill; this mechanism's real contribution is the *general* gate-placement decision framework for non-publish situations, plus the modify/reject-granularity routing, which is more sophisticated than a binary approve/reject.
Q7 (marketing vs. engineering): Genuine engineering — concrete decision logic and routing states, even though the numeric thresholds are illustrative rather than empirically tuned.

Role Notes (Section 14, required for this Strong Candidate):
- Auditor (2026-08-23): Mechanism is fully inspectable — decision tree, presentation contract, and 3-way routing are all explicit, not hand-wavy. Verdict: Strong — genuine architectural substance.
- Reliability Reviewer (2026-08-23): The single biggest reliability risk is upstream — confidence-score calibration. This skill assumes good confidence signals exist; it does not itself solve producing them. Recommend treating "build calibrated confidence scoring" as a prerequisite research item (linked to DOM-15/DOM-16 evaluation work), not bundled for free with this pattern.
- Skeptic (2026-08-23): Attempted rejection: could argue Hermes doesn't need this at all since the raw idea already mandates human approval before every publish unconditionally, making a *selective* gate-placement decision tree unnecessary for v1. Counter: the raw idea's principle is about ambiguity and irreversibility broadly, not publish alone (e.g., should a research agent's speculative competitive claim also gate?) — the selective mechanism has value beyond the publish case. Rejection attempt does not succeed; candidate survives as ADAPT, not REUSE (thresholds unvalidated, confidence-calibration dependency unresolved).

Reasoning Summary: Best single skill found for DOM-07/DOM-09 — a genuine multi-factor decision tree, not a restatement of "add human review." Held to ADAPT rather than REUSE because it depends on confidence-calibration infrastructure that is not itself provided and is unverified for `hermes-agent`.
```

## SKL-013 — Output Contract Enforcer
```
Skill ID: SKL-013
Name: Output Contract Enforcer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/output_contract_enforcer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Validates DAG node outputs against declared JSON schemas so downstream nodes receive predictable, compatible input.
Original Domain: DAG-based agent workflow reliability.

Core Method: Sequential fail-fast validation gate — JSON-parseable? -> required fields present? -> correct types? -> constraints satisfied? — each failure stops validation and reports the specific breach.
Primary Workflow: Node output -> parse -> schema check -> pass/warn/fail with specific violation detail.
Inputs: Node output (any format), target JSON schema.
Outputs: Validation result (status + summary + specific failure reasons).
Dependencies: A standard base schema (status/summary/artifacts/data/risks); upstream node must declare its output schema explicitly.
Activation Conditions: Validating node output, generating schemas from descriptions, debugging downstream rejection.

Generalizable Components: The sequential fail-fast schema-validation gate, with specific (not generic) violation reporting, is directly reusable at any agent-to-agent handoff boundary — exactly DOM-02's need for a content-agent/research-agent/approver contract enforcement point.
Project-Specific Assumptions: Assumes explicit upstream schema declaration — a discipline Hermes would need to adopt deliberately, not automatic.
Domain-Specific Assumptions: DAG-node framing, otherwise generic.

Hermes Research Domains Covered: DOM-02

Overlap With: SKL-012 (Human Gate Designer — complementary: this validates *what* passes through a boundary; Gate Designer decides *when* a boundary needs a human).
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 75
Reasoning Summary: Solid, narrow, clean fail-fast validation mechanism for DOM-02. Standard JSON-schema-validation engineering rather than a novel architectural contribution — useful and low-risk to adapt, not a Strong Candidate because the mechanism itself is fairly conventional.
```

## SKL-014 — Logging & Observability
```
Skill ID: SKL-014
Name: Logging & Observability
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/logging_observability/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Structured logging, distributed tracing, and metrics guidance for production systems.
Original Domain: General software-service observability (SRE).

Core Method: 5-question log-level decision tree (system failure? recoverable? unexpected? business event? debug-needed?); mandatory structured JSON logging (no string interpolation); correlation-ID propagation via AsyncLocalStorage + W3C traceparent header; OTel SDK bootstrap before app code loads.
Primary Workflow: Instrument code -> structured logs + correlation IDs + OTel traces -> dashboards/alerts.
Inputs: Application code, request/response patterns, error chains.
Outputs: Logger config with redaction rules, OTel bootstrap, correlation middleware, Prometheus metrics module, Grafana dashboard JSON, Alertmanager rules.
Dependencies: Pino/Winston/structlog, OpenTelemetry SDK, log aggregation platform, Grafana+Prometheus.
Activation Conditions: "structured logging," "distributed tracing," "OpenTelemetry," "correlation ID."

Generalizable Components: Structured-logging discipline, correlation-ID propagation, and the redact-at-source (not ad-hoc-filter) anti-pattern are all sound, portable practices for any Hermes infra logging layer.
Project-Specific Assumptions: Assumes a conventional web-service infra stack (OTel, Prometheus, Grafana).
Domain-Specific Assumptions: This is infra-level service observability (uptime, latency, errors) — it does NOT address DOM-14's specific reframed need: a human-readable *decision trace* for a non-technical owner auditing agent behavior, as distinct from an on-call engineer's dashboards. That is a real, documented gap.

Hermes Research Domains Covered: DOM-14

Overlap With: SKL-019 (Liaison — closer fit for the human-facing side of DOM-14; this skill covers the infra layer beneath it).
Potential Conflicts: None.

Evidence Quality: Medium — single source, technically detailed.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 70
Reasoning Summary: A solid, conventional infra-observability layer Hermes will likely need regardless, but it does not by itself satisfy DOM-14's actual reframed need (human-owner decision-trace visibility, not engineer-facing dashboards) — must be paired with something like SKL-019 Liaison's communication layer on top.
```

## SKL-015 — Cost Optimizer
```
Skill ID: SKL-015
Name: Cost Optimizer
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/cost_optimizer/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Monitors cumulative LLM spend during DAG execution, enforcing budget constraints via dynamic model selection and node management.
Original Domain: LLM-pipeline cost governance.

Core Method: Tiered waterfall enforcement — >20% budget remaining: execute normally; 10-20%: downgrade Tier-2+ nodes to cheapest model; <5%: halt unless critical path; optional nodes skipped when budget critical.
Primary Workflow: Pre-execution cost estimate (historical token averages) -> compare to remaining budget -> apply tier action.
Inputs: Budget allocation, DAG execution state, node costs, historical performance data.
Outputs: Cost breakdown report (spent, skipped/downgraded nodes, tier distribution, recommendations).
Dependencies: Cost Accrual Tracker (real-time data), LLM Router (executes downgrades), Cost Verification Auditor (validates effectiveness).
Activation Conditions: "cost budget," "too expensive," "reduce cost," "budget exceeded."

Generalizable Components: The percentage-remaining-triggered waterfall (normal -> downgrade -> skip -> halt) is a concrete, directly implementable budget-enforcement mechanism — a strong comparison baseline for DOM-16's reframed question about `hermes-agent`'s own cost governance.
Project-Specific Assumptions: Assumes a DAG execution model with per-node cost estimation.
Domain-Specific Assumptions: None strongly limiting — the waterfall logic is domain-agnostic.

Hermes Research Domains Covered: DOM-16

Overlap With: SKL-016 (LLM Router), SKL-025 (Cost Accrual Tracker), SKL-031 (Cost Verification Auditor) — complementary pipeline, not redundant; see Deduplication Cluster 2.
Potential Conflicts: None.

Evidence Quality: Medium — single source; internally coherent with its named dependency skills.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 76
Reasoning Summary: Concrete, well-specified budget-enforcement waterfall that composes coherently with three sibling skills into a real cost-governance sub-system — directly useful as a comparison baseline for evaluating whether `hermes-agent`'s own cost control needs this level of explicit tiering.
```

## SKL-016 — LLM Router
```
Skill ID: SKL-016
Name: LLM Router
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/llm_router/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Selects the most appropriate LLM tier per task to optimize cost while maintaining quality, claiming "45-85% savings while maintaining 95%+ quality."
Original Domain: Multi-agent LLM-pipeline cost/quality optimization.

Core Method: Classify task type (classify/validate/write/reason/architect) -> assign to tier (Tier 1 Haiku-class, Tier 2 Sonnet-class, Tier 3 Opus-class) -> select provider by latency/compliance -> execute with quality feedback loop. Three progressive strategies: static tier assignment, cascading/try-cheap-first, adaptive learning (after ~100 executions).
Primary Workflow: Task description -> tier classification -> model/provider selection -> execution -> feedback-informed recalibration.
Inputs: Task description, quality requirements, execution constraints.
Outputs: Recommended model, provider, cost projection.
Dependencies: Multiple LLM providers; quality-assessment mechanism; historical performance tracking.
Activation Conditions: Model-assignment decisions for DAG nodes/multi-task workflows.

Generalizable Components: The task-type-to-tier classification and the three-strategy progression (static -> cascading -> adaptive) form a genuinely reusable model-routing decision framework — directly relevant to DOM-16's reconciliation of "cost is a hard constraint" with "quality over throughput."
Project-Specific Assumptions: The specific 45-85% savings and "95%+ quality" figures are asserted, not independently verified in the fetched content — flagged per Section 12 (marketing-flavored claims are lowest-trust evidence tier) even though the underlying mechanism is sound.
Domain-Specific Assumptions: Multi-provider assumption (Anthropic/OpenAI/Bedrock/Vertex/Ollama) — Hermes' actual provider set is undetermined.

Hermes Research Domains Covered: DOM-16

Overlap With: SKL-015 (Cost Optimizer), SKL-025 (Cost Accrual Tracker), SKL-031 (Cost Verification Auditor) — Deduplication Cluster 2, complementary.
Potential Conflicts: None.

Evidence Quality: Medium — single source; specific savings percentages are self-asserted, not corroborated (per Section 12.1, forbidden to trust marketing claims alone — noted, not relied upon for scoring).
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 77
Reasoning Summary: Good, concrete tiering/routing mechanism; score reflects the mechanism's quality, not the unverified savings percentages (Section 12.1 discipline applied — those numbers are noted as a claim, not treated as evidence).
```

## SKL-017 — Security Auditor
```
Skill ID: SKL-017
Name: Security Auditor
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/security_auditor/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Identifies vulnerabilities via dependency, secret, and static-code scanning against OWASP standards.
Original Domain: General application security auditing.

Core Method: 4-stage scan — dependency CVE analysis (npm audit/pip-audit/cargo audit), secret detection (pattern matching + entropy analysis, threshold >4.5 on strings >20 chars), OWASP Top 10 static analysis, language-specific dangerous-function detection (eval, pickle.loads, shell=True). Triage hierarchy: critical blocks deployment, high requires sprint fix, medium/low tracked.
Primary Workflow: Project directory -> 4-stage scan -> structured JSON report with severity/location/remediation.
Inputs: Project directory, package manifests, source files.
Outputs: Structured vulnerability report with triage priorities.
Dependencies: npm audit/pip-audit/cargo audit, grep/find, OWASP Top 10 2021 reference.
Activation Conditions: "security audit," "vulnerability scan," "OWASP," "secret detection."

Generalizable Components: The secret-detection entropy-threshold mechanism (>4.5 on strings >20 chars) is a concrete, usable technique for the credential-isolation half of DOM-17 — catching accidentally-committed platform API tokens.
Project-Specific Assumptions: Assumes a conventional codebase to scan; doesn't address the content-safety/guardrail half of DOM-17 (what gets published) at all — a documented gap.
Domain-Specific Assumptions: Generic application security, not social-automation-specific.

Hermes Research Domains Covered: DOM-17 (credential/secrets half only)

Overlap With: None significant.
Potential Conflicts: None.

Evidence Quality: Medium — single source, technically concrete.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 73
Reasoning Summary: Useful, concrete secret-detection mechanism for the credential-isolation half of DOM-17; does not address the content-safety-guardrail half at all, which remains an open gap for that domain regardless of this skill's adoption.
```

## SKL-018 — Launch Readiness Auditor
```
Skill ID: SKL-018
Name: Launch Readiness Auditor
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/launch_readiness_auditor/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Evaluates software projects for production readiness — shippable features, blocking issues, path to launch.
Original Domain: General SDLC / release-readiness auditing.

Core Method: 3-phase process (Discovery, Analysis scoring 8 health dimensions, Planning); triage matrix (Ship It/Sprint It/Defer It/Cut It) by completeness percentage; blocker severity classification.
Primary Workflow: Codebase -> feature/health scoring -> triage matrix -> sprint roadmap.
Inputs: Codebase access, feature docs, test results.
Outputs: Health scorecard, feature triage matrix, blocker inventory, sprint plan.
Dependencies: Pairs with security-auditor, test-automation-expert, site-reliability-engineer.
Activation Conditions: Assessing launch viability, sprint planning toward deployment.

Generalizable Components: None that map to a Hermes runtime capability — this evaluates whether *a codebase* is ready to ship, not any of Hermes' 25 research domains (agent architecture, memory, content generation, etc.).

Hermes Research Domains Covered: None

Evidence Quality: Medium — single source, well-specified but off-target.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REJECT
Confidence: 60
Score: 35
Reasoning Summary: Well-constructed skill on its own terms, but it audits build-readiness of a software project, not a Hermes runtime capability — same category of out-of-scope as the "Architecture documentation" / "Spec-driven development" seeds dropped at Stage -2.1 (Section 2.4's "North Star" build-readiness test is a downstream Phase -1/specification concern, not a Phase -2 research domain). See rejected-candidates.md REJ-001. Included in the Section 15.1 suggested-leads list, but the list is explicitly non-binding and Claude is required to challenge it — this is a direct example of that discipline in practice.
```

## SKL-019 — Liaison
```
Skill ID: SKL-019
Name: Liaison
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/liaison/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Human-interface agent translating multi-agent ecosystem activity into clear, actionable communication so humans don't feel lost in their own complex systems.
Original Domain: Software-project status communication.

Core Method: 5 communication templates (Status Briefing, Decision Request, Celebration Report, Concern Alert, Opportunity Summary); escalation-urgency framework — Immediate (build failures, security issues, blocking decisions), Same-Day (milestones, opportunities), Weekly (trends, low-priority decisions), Archive Only (routine/expected outcomes).
Primary Workflow: Gather system state (bash: build status, skill counts, git history) -> classify urgency -> select template -> produce human-facing brief.
Inputs: User queries, filesystem/git/build data.
Outputs: Formatted briefings, decision matrices, alerts, achievement reports.
Dependencies: Read, Bash, Grep, Glob; requires `.claude/` directories, git, npm build system access.
Activation Conditions: "status," "update me," "brief me," "summarize," "report."

Generalizable Components: The urgency-tiered escalation framework (Immediate/Same-Day/Weekly/Archive) and the template-per-communication-type structure directly address DOM-14's reframed need — giving the Owner cheap, non-intrusive visibility that makes reduced involvement (DOM-10) safe rather than reckless.
Project-Specific Assumptions: Info-gathering is software-dev-specific (git, npm, build status) — would need real retargeting to a content/social-ops environment (post status, publish queue, research findings) rather than a codebase.
Domain-Specific Assumptions: The 4-tier urgency bucketing is fairly coarse compared to, e.g., SKL-012's more granular threshold-based gating — a reasonable starting point, not a finished mechanism.

Hermes Research Domains Covered: DOM-14, DOM-10

Overlap With: SKL-014 (Logging & Observability — infra layer beneath this human-facing layer).
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 78
Reasoning Summary: Directly matches DOM-14's human-owner-visibility need and DOM-10's trust-calibration goal with a real (if coarse) escalation-urgency mechanism. Held just under the Strong Candidate band because its information-gathering layer is entirely software-dev-specific and needs substantive retargeting to a content/social-ops context, and the 4-tier bucketing is less granular than SKL-012's comparable mechanism.
```

## SKL-020 — Team Builder
```
Skill ID: SKL-020
Name: Team Builder
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/team_builder/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Designs high-performing team structures using organizational psychology; creates missing skills on-the-fly when team expertise gaps emerge.
Original Domain: Team/organizational design.

Core Method: 6-step process; sizing via Dunbar's Number (2-3 to 50+ people); composition via Belbin role balancing; health assessment (psychological safety vs. groupthink/role-confusion/burnout signals).
Primary Workflow: Team purpose -> role/skill/personality mapping -> complementary structure design -> norms -> psychological-safety practices.
Inputs: Team context, purpose, member profiles.
Outputs: Team compositions, collaboration rituals, newly-created skills for gaps.
Dependencies: Orchestrator, Research Analyst, Skill Coach, Agent Creator.
Activation Conditions: "team building," "team composition," "personality types," "missing skill."

Generalizable Components: The "identify a capability gap, fill it immediately rather than working around it" discipline (shared with SKL-001 Orchestrator) is a reusable principle.
Project-Specific Assumptions: Built for scaling teams of 2-3 up to 50+ people — Hermes has a fixed 2-role design by definition (Section 2.3 forbids deciding otherwise), so the core sizing/composition mechanism (Dunbar's Number, Belbin roles) has essentially no applicable surface here.
Domain-Specific Assumptions: Human-organizational-psychology framing throughout.

Hermes Research Domains Covered: DOM-01, DOM-02 (weakly)

Overlap With: SKL-001 (Orchestrator — shares gap-filling logic).
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 55
Score: 42
Reasoning Summary: The skill's core mechanism (team sizing/composition theory) targets a scaling problem Hermes does not have — a fixed 2-role design, not a growable team. Kept as REFERENCE only for the shared gap-filling principle; scored low because the primary mechanism doesn't apply.
```

## SKL-021 — Skillful Subagent Creator
```
Skill ID: SKL-021
Name: Skillful Subagent Creator
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skillful_subagent_creator/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Structured methodology for designing Claude subagents as specialists equipped with curated skills as standard operating procedures.
Original Domain: Claude subagent design.

Core Method: 6-step process — Define Role (testable in one sentence), Select Skills (2-5, "needed for >50% of tasks" criterion), Write 4-Section Prompt (Identity / Skill Usage Rules / Task-Handling Loop / Constraints), Define Contracts (explicit JSON input/output schemas), Wire DAG (orchestration pattern choice), Test (happy path, edge cases, out-of-scope refusal, skill adherence, contract validation).
Primary Workflow: Domain need -> role definition -> skill selection -> structured prompt -> explicit contracts -> orchestration wiring -> systematic test pass.
Inputs: Task description, file paths, context, constraints.
Outputs: Status, artifacts, summary, skills-used trace, risks, metadata (duration, tokens).
Dependencies: Pre-existing skills (created via skill-architect); an orchestrator system; DAG infrastructure.
Activation Conditions: Designing specialist subagents, selecting core skills, wiring DAG orchestration.

Generalizable Components: The 4-section prompt template and, especially, the explicit input/output JSON contract requirement plus the systematic test checklist (including "out-of-scope refusal") are directly reusable for defining Hermes' content-agent/research-agent boundaries with real rigor — exactly DOM-02's need.
Project-Specific Assumptions: Assumes a skill-preloading tier system (Preloaded/Catalog/None) that depends on the same Claude-Skills packaging convention flagged as an open dependency in SKL-009/SKL-008 (compatibility with `hermes-agent`'s native mechanism unverified until Stage -2.4).
Domain-Specific Assumptions: None beyond the packaging-convention dependency above.

Hermes Research Domains Covered: DOM-02

Overlap With: SKL-013 (Output Contract Enforcer — complementary: this defines the contract at design time, Enforcer validates it at runtime).
Potential Conflicts: None.

Evidence Quality: Medium — single source; the test checklist is unusually concrete for this source type.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 80

Adversarial Review (Section 13):
Q1 (assumptions): Assumes a pre-existing skill catalog and a skill-loading-tier runtime — dependent on the same open Claude-Skills-compatibility question as SKL-009.
Q2 (failure modes for Hermes): If `hermes-agent` doesn't support "preload 2-5 skills as SOPs," the specific loading-tier mechanism won't transfer directly, though the prompt-template and contract-definition discipline would still transfer independent of the loading mechanism.
Q3 (complexity introduced): Low-moderate — a structured prompt/contract-design methodology, not new infrastructure.
Q4 (lock-in): Low — mostly a documentation/design convention.
Q5 (evidence missing): Single source; no adoption evidence beyond the site's own use.
Q6 (simpler competing approach): Writing prompts ad hoc without the 4-section discipline is simpler but forfeits the explicit contract-testing rigor, which is exactly the valuable part given Hermes' need for crisp agent boundaries (ties to the ambiguity/irreversibility principles).
Q7 (marketing vs. engineering): Genuine engineering — concrete templates and a real test checklist, not marketing language.

Role Notes (Section 14, required for this Strong Candidate):
- Auditor (2026-08-23): The explicit JSON input/output contract requirement plus the "out-of-scope refusal" test case are genuinely strong, inspectable engineering discipline — directly verifiable, not just asserted. Verdict: Strong.
- Reliability Reviewer (2026-08-23): The test checklist (happy path/edge case/out-of-scope/skill-adherence/contract-validation) is the standout reliability contribution here — it's a genuine pre-deployment test discipline for agent boundaries, rare among the skills inspected in this pass. Verdict: Strong on reliability thinking specifically.
- Skeptic (2026-08-23): Attempted rejection: the skill-loading-tier mechanism may simply not transfer to `hermes-agent` at all, making roughly half the skill's content inapplicable. Counter: even discounting the loading-tier mechanism entirely, the 4-section prompt template + explicit contracts + test checklist remain fully usable independent of it. Rejection attempt does not succeed for the whole skill, but narrows what should actually be adapted — noted in Reasoning Summary.

Reasoning Summary: Genuinely strong contract-design and testing discipline for DOM-02, with the caveat that its skill-loading-tier component (not its prompt/contract/testing components) depends on unverified `hermes-agent` compatibility. Recommend adapting the prompt-template/contract/testing portions regardless of that finding; treat the loading-tier portion as conditional on Stage -2.4 results.
```

## SKL-022 — Skill Coach
```
Skill ID: SKL-022
Name: Skill Coach
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skill_coach/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Guides creation of high-quality Agent Skills via domain-expertise encoding, anti-pattern detection, and progressive disclosure.
Original Domain: Claude Skills authoring (quality-review emphasis).

Core Method: Same 6-step process family as SKL-009/SKL-010 with a 3-phase progressive-disclosure token budget (Phase 1 ~100 tokens metadata, Phase 2 <5k tokens core instructions, Phase 3 on-demand references); necessity decision tree (expertise spans 3+ projects -> skill; single task -> execute directly; external APIs -> MCP; multi-step orchestration -> subagents).
Primary Workflow: Same authoring loop as siblings, with explicit anti-pattern detection as its distinguishing emphasis.
Inputs/Outputs: Same category as SKL-009/010.
Dependencies: Valid frontmatter keys (name/description/allowed-tools/license/metadata); validation scripts.
Activation Conditions: "create skill," "review skill," "skill anti-patterns," "skill audit."

Generalizable Components: The "when should this even be a skill" necessity decision tree (3+ projects / single task / external API / multi-step) is a genuinely useful, distinct contribution not present in the other three cluster members — worth keeping even though the rest of the process is redundant.
Project-Specific Assumptions: Same Claude-Skills packaging dependency as siblings.
Domain-Specific Assumptions: Same as siblings.

Hermes Research Domains Covered: DOM-04

Overlap With: SKL-008, SKL-009, SKL-010 — Deduplication Cluster 1 (secondary reference; canonical is SKL-009).
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 55
Score: 60
Reasoning Summary: Largely redundant with SKL-009 (canonical), kept as secondary reference specifically for its necessity-decision-tree contribution (whether a capability should be a skill vs. an MCP server vs. a subagent), which the other three cluster members don't offer.
```

## SKL-023 — Skill Logger
```
Skill ID: SKL-023
Name: Skill Logger
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/skill_logger/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Tracks skill-invocation quality via metrics and user signals to enable continuous improvement.
Original Domain: Claude Skill usage analytics.

Core Method: 6-stage pipeline (Capture, Analyze, Score, Aggregate, Alert, Improve); 4-weighted-dimension quality index — Completion 25%, Efficiency 20%, Output Quality 30%, Satisfaction 25%; alert thresholds (quality decline >20%, error-rate doubling, usage drop >50%).
Primary Workflow: Invocation -> capture metadata -> score 4 dimensions -> aggregate trends -> alert on threshold breach -> feed improvement recommendations.
Inputs: User queries, tool calls, execution metrics, feedback signals.
Outputs: Invocation logs, quality scorecards, trend reports, improvement recommendations.
Dependencies: Pairs with Skill Coach, Agent Creator, Automatic Stateful Prompt Improver.
Activation Conditions: "skill logging," "skill analytics," "track skill usage," "skill performance."

Generalizable Components: The weighted-quality-index formula and threshold-based alerting are directly transferable to two Hermes needs: ongoing (not just pre-publish) quality monitoring of the content-generation agent (DOM-15) and the analytics-feedback-loop question of DOM-22.
Project-Specific Assumptions: Tracks *skill* invocations specifically; would need retargeting to track *content pieces* or *research findings* instead.
Domain-Specific Assumptions: None strongly limiting beyond the retargeting above.

Hermes Research Domains Covered: DOM-14, DOM-15, DOM-22

Overlap With: None directly redundant.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 71
Reasoning Summary: A solid, concrete continuous-quality-monitoring mechanism (distinct from one-time pre-publish gating) that bridges DOM-15's evaluation need and DOM-22's feedback-loop need; needs retargeting from "skill invocations" to "content pieces/research outputs."
```

## SKL-024 — MCP Creator
```
Skill ID: SKL-024
Name: MCP Creator
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/mcp_creator/
License: References Anthropic's Model Context Protocol spec for its technical dependency; skill itself unlicensed
Last Verified: 2026-08-23

Original Purpose: Expert guidance for building production-ready MCP servers with security, error handling, and performance discipline.
Original Domain: MCP server development.

Core Method: 7-step sequence — Architecture Assessment (decision tree: external API+auth? persistent state? rate limiting? shared credentials? security boundaries? -> if any yes, use MCP), Server Scaffolding, Tool Design, Security Hardening (input validation, secret management, rate limiting, auth boundaries), Error Handling (structured responses, graceful degradation), Performance Tuning (connection pooling, caching), Testing (MCP Inspector + unit tests).
Primary Workflow: Assess need -> scaffold -> design tools -> harden -> handle errors -> tune -> test.
Inputs: Tool specifications, external service details, auth credentials, performance constraints.
Outputs: Production-ready MCP server code, tool definitions, security patterns, test suites.
Dependencies: `@modelcontextprotocol/sdk`, `zod`, database drivers, secret management, vitest.
Activation Conditions: "create MCP," "MCP server," "build MCP," "Model Context Protocol."

Generalizable Components: The when-to-use-MCP decision tree and the explicit security-hardening step sequence (validation -> secrets -> rate limiting -> auth boundaries) are directly useful as a comparison baseline for evaluating `hermes-agent`'s own MCP/tool-use robustness (DOM-06's reframed question).
Project-Specific Assumptions: Node/TypeScript-oriented dependency stack (`zod`, `@modelcontextprotocol/sdk`) — may or may not match `hermes-agent`'s actual language/stack (unverified until Stage -2.4).
Domain-Specific Assumptions: None beyond the stack assumption above.

Hermes Research Domains Covered: DOM-06

Overlap With: None directly redundant.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 74
Reasoning Summary: Concrete, security-conscious MCP-server-building methodology — good comparison baseline for DOM-06's reframed audit question, with the caveat that its dependency stack may not match `hermes-agent`'s actual implementation language.
```

## SKL-025 — Cost Accrual Tracker
```
Skill ID: SKL-025
Name: Cost Accrual Tracker
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/cost_accrual_tracker/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Real-time API cost monitoring during LLM execution, capturing partial costs on abort, with budget threshold controls.
Original Domain: LLM-pipeline cost tracking.

Core Method: `recordUsage()` accumulates token counts/expense after each API response; `getCurrentCost()` exposes running total; `finalize()` produces a CostReport with completion reason (completed/aborted/failed). Separate pricing for standard vs. cached tokens (90% discount on cached).
Primary Workflow: Per-API-call usage recording -> running cost exposure -> finalized report at end of execution or abort.
Inputs: TokenUsage objects (input/output tokens, cache metrics), model identifier.
Outputs: CostReport (aggregate tokens, total USD cost, completion reason, timestamp).
Dependencies: MODEL_PRICING lookup table; ExecutionManager for DAG-level aggregation; feeds Cost Optimizer and Cost Verification Auditor.
Activation Conditions: "cost tracking," "token usage," "API costs," "budget monitoring."

Generalizable Components: The three-function API surface (record/getCurrent/finalize) with explicit partial-cost capture on abort is a genuinely implementation-level, directly portable mechanism — unusually concrete (function signatures, not just prose) among the skills inspected.
Project-Specific Assumptions: DAG-execution framing for aggregation.
Domain-Specific Assumptions: None strongly limiting.

Hermes Research Domains Covered: DOM-16

Overlap With: SKL-015, SKL-016, SKL-031 — Deduplication Cluster 2, complementary.
Potential Conflicts: None.

Evidence Quality: Medium-High — single source, but implementation-level API detail (function signatures) rather than prose description raises confidence in what's actually being proposed.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 75
Reasoning Summary: The most implementation-concrete of the four cost-cluster skills (actual function signatures, not just workflow prose); directly useful as a comparison baseline for whatever cost-instrumentation `hermes-agent` provides natively.
```

## SKL-026 — Wisdom Accountability Coach
```
Skill ID: SKL-026
Name: Wisdom Accountability Coach
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/wisdom_accountability_coach/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Longitudinal memory coaching system tracking personal growth and accountability with compassion, teaching philosophy (Stoicism/Buddhism) through lived experience.
Original Domain: Personal coaching/therapy-adjacent (explicitly not therapy or crisis intervention).

Core Method: Longitudinal memory of commitments/life-areas/behavioral patterns across time; "Curious Mirror" compassionate-confrontation technique (asking "what happened?" rather than accusing); pattern-over-incident prioritization; support-vs-rescue distinction.
Primary Workflow: Track commitments over time -> detect patterns -> reflect via curious questioning -> apply relevant wisdom-tradition framing.
Inputs: User commitments, past conversations, life updates.
Outputs: Pattern reports, accountability check-ins, philosophical guidance.
Dependencies: Pairs with several other Lifestyle & Personal skills.
Activation Conditions: "accountability," "philosophy," "personal growth," "commitment tracking."

Generalizable Components: The pattern-over-incident framing and "Curious Mirror" non-accusatory reflection technique are conceptually interesting for how a Liaison-style report (SKL-019) might eventually narrate a trust/autonomy change to the Owner without being preachy or alarmist — but this is a soft communication idea, not an engineering mechanism.
Project-Specific Assumptions: Deeply human-relational framing (therapy-adjacent coaching) — most of the mechanism doesn't transfer to an agent-to-owner reporting context at all.
Domain-Specific Assumptions: Explicitly out of scope for crisis/clinical use, which also limits its relevance ceiling here.

Hermes Research Domains Covered: DOM-10 (weak/tangential)

Overlap With: None significant.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REFERENCE
Confidence: 50
Score: 38
Reasoning Summary: An interesting communication-framing idea for trust-calibration narration, but not an engineering mechanism — honestly scored low (Weak Fit band) given its relevance to any of the 25 domains is soft and indirect, despite being conceptually well-crafted in its own domain.
```

## SKL-027 — Crisis Detection Intervention AI
```
Skill ID: SKL-027
Name: Crisis Detection Intervention AI
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/crisis_detection_intervention_ai/
License: "Licensed for mental health platforms, recovery communities, support networks — explicitly not for replacing professional care or general sentiment analysis" (per fetched content)
Last Verified: 2026-08-23

Original Purpose: Identifies mental health crises in user content via NLP/sentiment analysis, flagging concerning material for human review while surfacing professional resources.
Original Domain: Mental-health/recovery-platform crisis detection.

Core Method: Multi-signal detection (NLP models + keyword matching + contextual sentiment) -> severity classification (none/low/medium/high/immediate) -> mandatory human-counselor flagging for any positive detection ("never automate responses") -> immediate resource display -> severity-scaled escalation notification. Structured output: `{is_crisis, severity, signals, confidence, resources_shown}`. Data handling: encrypted at rest, access-logged, auto-deleted after 30 days.
Primary Workflow: User text -> multi-signal detection -> severity classification -> human flag + resource display -> escalation per severity.
Inputs: User text/journal entries.
Outputs: Structured crisis-assessment object.
Dependencies: Mental-health NLP models, on-call counselor notification system, encryption infra, crisis hotline integration.
Activation Conditions: "crisis detection," "suicide prevention," "mental health NLP," "intervention protocol."

Generalizable Components: This is a hidden-pattern-mining find (Section 15.1) — a mature, real-world-informed severity-classification + mandatory-human-escalation mechanism directly analogous to Hermes' "stop and ask, don't guess" principle (DOM-09), well beyond what any generic agent-framework doc in this pass offered. The mechanism to extract is the *structure* (multi-signal detection -> tiered severity -> hard human-flag rule -> scaled escalation), explicitly NOT the clinical indicator taxonomy itself (per Section 15.1: "extract the mechanism, not the original product assumptions").
Project-Specific Assumptions: Assumes clinically-grounded, well-studied indicator categories — Hermes' own "ambiguity/risk" categories (e.g., unclear brand fit, potentially controversial claim, wrong-page cross-post) would need to be independently derived, not borrowed.
Domain-Specific Assumptions: The specific NLP models (MentalBERT etc.) are entirely domain-specific and not reusable. **Notable tension, flagged explicitly rather than silently carried forward**: this skill's data-handling policy auto-deletes flagged content after 30 days — this is the OPPOSITE of Hermes' third behavioral principle (never self-delete from memory/history, DOM-11). This specific sub-mechanism must NOT be adapted into Hermes; noted here so it is not accidentally copied during pattern extraction (Stage -2.5).

Hermes Research Domains Covered: DOM-09

Overlap With: SKL-028 (Crisis Response Protocol — tightly coupled pair; detection feeds response).
Potential Conflicts: None between the two skills; internal conflict noted above between this skill's auto-delete policy and Hermes' DOM-11 principle.

Evidence Quality: Medium — single source; but the *general pattern* (not this specific implementation) is indirectly well-evidenced by the maturity of real-world clinical crisis-protocol practice the docs reference (988 Lifeline, clinical literature).
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 80

Adversarial Review (Section 13) — covers SKL-027 and SKL-028 jointly, given their tight coupling:
Q1 (assumptions): Assumes a severity-classifiable signal space with well-studied indicator taxonomies (true in clinical crisis intervention after decades of practice; NOT true out-of-the-box for Hermes' "ambiguity" — those categories would need original derivation).
Q2 (failure modes for Hermes): Risk of over-fitting to the specific "5 tiers" number or borrowing clinical categories too literally instead of re-deriving Hermes-appropriate tiers; separately, blindly importing the 30-day auto-delete policy would directly violate DOM-11's never-delete principle (see note above).
Q3 (complexity introduced): Low-moderate to adapt the tiering/escalation *structure*; the original ML detection models are entirely non-reusable, so "detection" itself must be rebuilt for Hermes' actual signal space (ambiguous requests, low-confidence generations, high-risk publish targets).
Q4 (lock-in): None — pure decision-structure pattern.
Q5 (evidence missing): Single-source skill documentation; however the underlying real-world practice (crisis-line protocols, clinical escalation research) is independently well-evidenced outside this specific skill packaging, which is unusual and a point in its favor.
Q6 (simpler competing approach): A flat binary "ask or don't ask" rule (matching the raw idea's literal simplicity) may be sufficient for Hermes v1; the 5-tier system is a refinement to evaluate for right-sizing, not an assumed requirement.
Q7 (marketing vs. engineering): Real, carefully-scoped engineering appropriate to its original high-stakes domain — the risk here is over-import, not hollow marketing.

Role Notes (Section 14, required for this Strong Candidate — shared with SKL-028):
- Auditor (2026-08-23): Structurally the most rigorous escalation mechanism found in this pass — explicit hard-rule ("never automate responses") plus graduated severity plus scaled notification. Verdict: Strong, with the explicit caveat that the data-retention sub-mechanism must be excluded, not adapted.
- Reliability Reviewer (2026-08-23): The "assess before generating response" ordering (in SKL-028) is a genuinely important reliability property — prevents an agent from committing to an action before its own risk-assessment step completes. Recommend this ordering constraint specifically be carried into Hermes' pattern extraction (Stage -2.5) as its own named mechanism.
- Skeptic (2026-08-23): Attempted rejection: this is scope creep — importing a clinical-crisis pattern into a social-media agent risks over-engineering DOM-09 with unnecessary tiering complexity the raw idea's simple "stop and ask" principle doesn't call for. Counter: the *hard-rule* half (never auto-act past a certain risk threshold) is exactly what the raw idea demands, and severity-tiering is optional refinement, not mandatory baggage — the pattern is extractable at whatever tier-count Hermes actually needs, including a simplified 2-tier version. Rejection attempt partially succeeds: recommend extracting the hard-rule + assess-before-act structure at minimum, treating the specific 5-tier granularity as optional, not mandatory.

Reasoning Summary: Strongest hidden-pattern-mining find of this pass for DOM-09 — real, mature escalation-design thinking transplanted from a domain that has already solved "detect risk, don't act, escalate to human" rigorously. Extract the structure only; explicitly do not carry forward the clinical indicator taxonomy or the 30-day auto-delete policy (direct conflict with DOM-11).
```

## SKL-028 — Crisis Response Protocol
```
Skill ID: SKL-028
Name: Crisis Response Protocol
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/crisis_response_protocol/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Implements safe crisis-intervention response features for AI coaching systems — detecting and responding to acute situations while maintaining human escalation pathways.
Original Domain: Mental-health/recovery AI coaching.

Core Method: Primary/secondary/tertiary indicator hierarchy (primary = immediate escalation triggers; secondary = elevated monitoring; tertiary = check-in triggers); 5-tier response system (No Crisis -> Low -> Medium -> High -> Critical) with escalating actions (continue -> gentle check-in -> resource display -> "Crisis Protocol Response" with human-support encouragement -> emergency escalation with human flag + contact notification). Assessment via `assessCrisisLevel()` runs BEFORE response generation, analyzing current message + conversation history + 7-day check-in window.
Primary Workflow: Message + history + check-in pattern -> pre-generation risk assessment -> tiered response selection -> calibrated action.
Inputs: Message content, conversation history, 7-day check-in data.
Outputs: Crisis assessment object (severity, indicators, recommended action, timestamp).
Dependencies: SKL-027 (detection feeds this response layer); Recovery Community Moderator; HIPAA compliance for health data.
Activation Conditions: Detected primary/secondary/tertiary indicators per the hierarchy above.

Generalizable Components: The **assess-before-generate ordering** — running risk assessment strictly before producing any response/action, using both the current input AND a rolling history window (not just the single message) — is the standout mechanism here, directly reusable as a hard architectural constraint for any Hermes agent action (not just publish): assess risk/ambiguity first, generate/act only after.
Project-Specific Assumptions: Same clinical-taxonomy dependency as SKL-027 — extract structure, not categories.
Domain-Specific Assumptions: HIPAA/mental-health-specific compliance dependency, not applicable to Hermes.

Hermes Research Domains Covered: DOM-09

Overlap With: SKL-027 (tightly coupled pair — see joint adversarial review and role notes under SKL-027).
Potential Conflicts: None between the pair.

Evidence Quality: Medium — single source; assess-before-generate ordering is a clean, independently-verifiable architectural claim regardless of the clinical content around it.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 65
Score: 81

Adversarial Review: See SKL-027 (joint review covers both skills).
Role Notes: See SKL-027 (joint role notes cover both skills).

Reasoning Summary: The assess-before-generate ordering constraint, combined with using a rolling history window rather than single-message judgment, is a genuinely valuable architectural pattern for enforcing Hermes' "stop and ask under ambiguity" principle reliably rather than as a soft suggestion. Paired with SKL-027 as one extractable pattern with two parts (detect, then respond).
```

## SKL-029 — Background Job Orchestrator
```
Skill ID: SKL-029
Name: Background Job Orchestrator
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/background_job_orchestrator/
License: "Educational content ... presented under educational fair use principles" (per fetched content)
Last Verified: 2026-08-23

Original Purpose: Guides production-grade background job systems for long-running async tasks without blocking API responses.
Original Domain: General backend job-queue architecture.

Core Method: Queue-and-worker architecture — API endpoint queues job and returns ID immediately; separate worker processes pull from queue asynchronously; failed jobs enter a dead-letter queue for inspection/recovery; client polls job-status endpoint. Technology selection guidance by stack (BullMQ for TS+Redis, Celery for Python/Django, SQS/Cloud Tasks for serverless).
Primary Workflow: Queue job -> worker processes -> dead-letter queue on failure -> status polling.
Inputs: Job data, configuration (retry attempts, timeout, priority).
Outputs: Job ID, job state, progress, final result/error.
Dependencies: Redis/RabbitMQ, BullMQ/Celery, worker process management, monitoring dashboard.
Activation Conditions: Long operations (>5s), batch operations with retry needs, scheduled/recurring work, rate-limited API calls.

Generalizable Components: The dead-letter-queue pattern for failed-job inspection/recovery is directly useful as a comparison baseline for DOM-13's reframed question about `hermes-agent`'s own scheduling/reliability substrate — a standard, well-understood pattern for "what happens when a scheduled agent run fails."
Project-Specific Assumptions: Assumes conventional backend infra (Redis, worker processes) — may or may not resemble how `hermes-agent`'s actual cron/scheduling mechanism is built.
Domain-Specific Assumptions: None beyond the infra assumption above.

Hermes Research Domains Covered: DOM-13

Overlap With: None significant.
Potential Conflicts: None.

Evidence Quality: Medium — single source, standard/well-known pattern (not novel).
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 68
Reasoning Summary: Solid, conventional job-queue architecture — useful as a reliability-pattern comparison baseline for DOM-13, though it's a well-known standard pattern rather than a novel architectural contribution, and its infra assumptions may not match `hermes-agent`'s actual scheduling implementation.
```

## SKL-030 — Checklist Discipline
```
Skill ID: SKL-030
Name: Checklist Discipline
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/checklist_discipline/
License: Content grounded in "The Checklist Manifesto" (Atul Gawande, 2009); skill packaging itself unlicensed
Last Verified: 2026-08-23

Original Purpose: Transforms expertise into systematic excellence by catching predictable cognitive-attention failures in high-complexity, high-stakes coordination.
Original Domain: High-stakes human-team coordination (surgery, aviation, construction) — general, not software-specific.

Core Method: Checklist-design decision tree — diagnose root cause (ignorance vs. ineptitude) -> identify pause points (before critical commitment / point-of-no-return / after high-risk phases) -> select format (DO-CONFIRM for experts/routine tasks vs. READ-DO for novices/unfamiliar work) -> extract 5-9 "killer items" per pause point -> draft (60-90s max execution, one page) -> test iteratively with real users (5-10 refinement cycles expected) -> implement with verbal team confirmation and physical/procedural "forcing functions."
Primary Workflow: Diagnose failure mode -> place pause points -> pick format -> extract killer items -> draft, test, refine -> implement with forcing functions.
Inputs: Process documentation, expert knowledge, observed failure points.
Outputs: A 5-9-item checklist per pause point, team communication protocol, forcing functions.
Dependencies: None technical — a methodology, not a tool.
Activation Conditions: >100-step processes, high-stakes domains, cross-disciplinary coordination.

Generalizable Components: This is the second strong hidden-pattern-mining find of this pass (Section 15.1) — directly strengthens DOM-15's pre-publish quality-gate design with genuinely evidence-grounded discipline (not "add a reviewer step," but a specific, tested methodology for what such a gate should contain and how it should be validated before trust is placed in it). The pause-point-before-point-of-no-return concept also reinforces DOM-07's irreversible-action-gate placement logic.
Project-Specific Assumptions: Designed for human teams with verbal confirmation dynamics (e.g., OR staff stating name/role aloud) — a solo-owner-plus-AI-agent system needs a reinterpreted equivalent of the "team conversation" and "forcing function" elements (e.g., what physically/procedurally blocks a premature publish the way a "metal tent" blocks an OR departure?).
Domain-Specific Assumptions: None strongly limiting beyond the human-team-dynamics translation above — the core method is domain-agnostic by design (its own examples span surgery, aviation, and construction already).

Hermes Research Domains Covered: DOM-15, DOM-07

Overlap With: SKL-012 (Human Gate Designer — complementary: Gate Designer decides *when/where* to place a gate; Checklist Discipline defines *what the gate should actually check* and how to validate that it works).
Potential Conflicts: None.

Evidence Quality: High for a skill-catalog source — the *strongest* Evidence Quality basis of any skill in this pass, since it's grounded in independently-verifiable, well-documented real-world outcomes (WHO Safe Surgery Checklist trial results, Boeing 299's 1935 incident, Pronovost's central-line infection protocol), not just the skill vendor's own assertion.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 70
Score: 84

Adversarial Review (Section 13):
Q1 (assumptions): Assumes team/verbal-confirmation dynamics designed for human teams — needs deliberate reinterpretation for a solo-owner + AI-agent structure.
Q2 (failure modes for Hermes): If applied without discipline, could produce checklist bloat — though the mechanism itself explicitly guards against this via the 5-9 "killer items" cap, which is a self-correcting feature, not a risk to import blindly.
Q3 (complexity introduced): Moderate and real — the method itself insists on 5-10 iterative refinement cycles with actual users before a checklist is trustworthy; this is a genuine adoption cost, not a one-shot copy-paste.
Q4 (lock-in): None — pure methodology.
Q5 (evidence missing): None significant relative to other candidates in this pass — this is the strongest-evidenced skill inspected, given independent real-world corroboration.
Q6 (simpler competing approach): An unstructured "have a human look at it before publishing" (Hermes' baseline design already) is simpler but has none of this method's demonstrated error-catching rigor; this mechanism strengthens *what* the gate checks, complementing rather than replacing the baseline.
Q7 (marketing vs. engineering): Genuine, externally-grounded methodology, not marketing.

Role Notes (Section 14, required for this Strong Candidate):
- Auditor (2026-08-23): Mechanism is fully inspectable and its real-world grounding is independently checkable (these are documented historical interventions, not the skill author's own claims). Verdict: Strong — the best-evidenced candidate in this catalog.
- Reliability Reviewer (2026-08-23): The DO-CONFIRM vs. READ-DO distinction is a genuinely useful reliability concept for Hermes: routine, well-understood publish actions could use DO-CONFIRM (owner verifies from memory/glance), while unusual or first-of-kind actions (e.g., first post to a brand-new page) should use READ-DO (step through explicitly). Recommend this distinction be carried into DOM-07's pattern extraction.
- Skeptic (2026-08-23): Attempted rejection: this may be over-engineered for a solo-owner system — checklists with verbal team confirmation assume multiple humans, which Hermes doesn't have. Counter: the core mechanism (pause-point placement, killer-item extraction, DO-CONFIRM/READ-DO format choice) does not actually require multiple humans — only the "forcing function" and "verbal confirmation" implementation details need reinterpretation for a single owner, and even a solo owner benefits from a well-designed checklist over an unstructured review. Rejection attempt does not succeed; candidate survives as ADAPT with the noted reinterpretation needed.

Reasoning Summary: Best-evidenced skill found in this entire pass, and a genuine strengthening of DOM-15's pre-publish gate design beyond generic "add a review step" — recommend prioritizing this for Stage -2.5 pattern extraction alongside SKL-012 and the SKL-027/028 pair, all three of which converge on the same underlying Hermes need (calibrated, evidence-grounded human-control gating) from three independent original domains.
```

## SKL-031 — Cost Verification Auditor
```
Skill ID: SKL-031
Name: Cost Verification Auditor
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/cost_verification_auditor/
License: Not specified
Last Verified: 2026-08-23

Original Purpose: Validates that token-cost estimates align with actual API usage, within a ±20% variance threshold.
Original Domain: LLM-pipeline cost-estimation accuracy.

Core Method: Verify/build estimator -> define 3+ test cases (simple/medium/complex) -> generate pre-execution estimates -> execute against live API -> calculate variance ((actual-estimated)/estimated) -> pass if both input and output stay within ±20% -> apply calibration fixes if exceeded. Per-node variance tolerance up to 40% (normal LLM non-determinism); aggregate accuracy enforced more strictly. Uses CHARS_PER_TOKEN ratios (4.0 prose, 3.0-3.5 code, 3.0 JSON) for estimation.
Primary Workflow: Build/verify estimator -> test against live execution -> measure variance -> calibrate if needed.
Inputs: Prompt text, model selection, test case definitions.
Outputs: Variance analysis, pass/fail, calibration recommendations.
Dependencies: Cost Accrual Tracker, Cost Optimizer, Logging Observability; raw token-usage logs.
Activation Conditions: "cost verification," "token estimate accuracy," "API cost audit."

Generalizable Components: The explicit variance-threshold-with-calibration-loop closes the loop on DOM-16's cost mechanism — without this, a cost-estimation system can silently drift inaccurate over time; a small but genuinely useful completeness piece for the cost cluster.
Project-Specific Assumptions: None strongly limiting.
Domain-Specific Assumptions: The specific CHARS_PER_TOKEN ratios are for particular tokenizers/content types and may not transfer to Hermes' actual model choices without re-calibration.

Hermes Research Domains Covered: DOM-16

Overlap With: SKL-015, SKL-016, SKL-025 — Deduplication Cluster 2, complementary.
Potential Conflicts: None.

Evidence Quality: Medium — single source.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: ADAPT
Confidence: 60
Score: 69
Reasoning Summary: A useful but narrow utility-tool-level mechanism completing the cost-governance cluster; solid engineering, not architecturally novel, hence below the Useful-Candidate ceiling of its sibling skills.
```

## SKL-032 — Modern Auth 2026
```
Skill ID: SKL-032
Name: Modern Auth 2026
Source: SomeClaudeSkills
URL: https://someclaudeskills.com/docs/skills/modern_auth_2026/
License: OSS libraries referenced (SimpleWebAuthn, Supabase SDKs) follow their own licenses; skill itself unlicensed
Last Verified: 2026-08-23

Original Purpose: Passwordless-first end-user authentication (passkeys/WebAuthn, OAuth social login, magic links) for web/mobile applications.
Original Domain: Consumer-facing application authentication.

Core Method: WebAuthn passkey registration/authentication flows; OAuth redirect flows (Google/Apple); magic-link time-limited tokens; authentication-method priority ladder (passkeys > social OAuth > magic links > email OTP > SMS OTP) and a matching account-recovery hierarchy.
Primary Workflow: End-user registers/authenticates via passkey, OAuth, or magic link -> session established.
Inputs: User email/identifier, device capabilities, OAuth credentials.
Outputs: WebAuthn credential objects, OAuth sessions, Supabase auth sessions.
Dependencies: `@simplewebauthn/*`, `next-passkey-webauthn`, Supabase Auth, Google/Apple developer consoles.

Hermes Research Domains Covered: None — see reasoning.

Evidence Quality: Medium — single source, technically detailed for its actual (mismatched) purpose.
Maintenance Signal: Unknown
Documentation Quality: High

Reuse Classification: REJECT
Confidence: 65
Score: 22
Reasoning Summary: A clear example of "don't rate by title" discipline (Section 15.1/Stage -2.2 rule): "auth" sounds adjacent to DOM-08 (Permissions & least-privilege scoping), but the actual mechanism is end-user consumer login (passkeys/OAuth/magic links for people signing into an app) — completely different from DOM-08's real need, which is machine-to-machine credential isolation between an agent instance and a social platform's API per page. Zero component of this mechanism transfers. See rejected-candidates.md REJ-002.
```

---

## Summary

32 skills inspected (18 Section 15.1 suggested leads in full + 14 hidden-pattern-mining
additions). Classification breakdown: **ADAPT** 24, **REFERENCE** 6, **REJECT** 2,
**REUSE** 0 (none reached direct-adoption confidence — expected, given single-source
evidence throughout, per the Evidence Quality note above), **UNKNOWN** 0.

**Strong Candidates (score >= 80, full Section 13/14 review completed):**
SKL-012 Human Gate Designer (82), SKL-021 Skillful Subagent Creator (80), SKL-027
Crisis Detection Intervention AI (80) + SKL-028 Crisis Response Protocol (81, reviewed
jointly), SKL-030 Checklist Discipline (84).

**Domains with real coverage from this stage:** DOM-01, DOM-02, DOM-03 (partial —
documented gap), DOM-04, DOM-06, DOM-07, DOM-09, DOM-10, DOM-13, DOM-14, DOM-15,
DOM-16, DOM-17 (partial — credential half only), DOM-18, DOM-19, DOM-22.

**Domains with no coverage from this stage (carried forward to Stage -2.3/-2.4):**
DOM-05, DOM-08 (screened one candidate, rejected as mismatched), DOM-11 (see gap note
below), DOM-12, DOM-20, DOM-21, DOM-23 (BLOCKED, not researched), DOM-24, DOM-25.

**Documented gaps (honest per P5, not papered over):**
- **DOM-11** (append-only memory/audit-log architecture): no skill in the 181-title
  gallery addresses immutable/audit-log storage design at all — expected, since this
  gallery skews toward general app-development skills, not systems/data-infra
  patterns. Carried forward to Stage -2.3/-2.4 as a real, unfilled gap.
- **DOM-03/DOM-20** (narrative/chained multi-modal content generation): no skill in
  the gallery addresses serialized/narrative content generation or multi-modal
  (text+image+video) pipelines — also expected, since this is a general-purpose
  dev-skills catalog, not a creator-economy one. SKL-006 Task Decomposer partially
  covers the decomposition half only.
- **DOM-08** (permissions/credential isolation): one candidate screened
  (Modern Auth 2026) and rejected as a mechanism mismatch (end-user login, not
  machine-to-machine platform-API credential isolation) — still an open gap.

Saturation calls, dedup results, and rejected candidates are detailed in
`deduplication-map.md` and `rejected-candidates.md`.
