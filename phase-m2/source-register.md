# Hermes Phase -2 Source Register

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.6.
First populated at Stage -2.2 (Skill Discovery), 2026-08-23.

Individual skill pages already carry their own URL/access-date in
`skill-catalog.md` per the Section 9.1 schema; this register exists for
sources whose claims materially inform decisions or are cited across multiple
records — not a duplicate of every skill URL.

---

```
Source ID: SRC-001
Title: Some Claude Skills — Skills Gallery
Type: website
URL: https://someclaudeskills.com/skills
Repository: erichowens/some_claude_skills (referenced, not cloned/inspected)
Author/Organization: Erich Owens, Curiositech
Date Accessed: 2026-08-23
License: Site carries "© 2026 Curiositech" notice; no explicit per-skill license found
Research Domains: DOM-01, DOM-02, DOM-03, DOM-04, DOM-06, DOM-07, DOM-09, DOM-10, DOM-13, DOM-14, DOM-15, DOM-16, DOM-17, DOM-18, DOM-19, DOM-22
Claims Used: Full 181-skill gallery listing (names/descriptions/categories); primary discovery index for Stage -2.2 Campaign SCS
Files Inspected: Gallery index page only at this URL; individual skill pages registered separately in skill-catalog.md (32 of 181 inspected beyond title/description)
Confidence: 70 — direct fetch of the live gallery page, but not cross-verified against the underlying GitHub repo's actual file contents
Notes: Named research input per Master Plan Section 15.1 (Campaign SCS) — not an authority, not a mandatory checklist. 181 total skills confirmed present at access time; no pagination (all shown on one page).
```

```
Source ID: SRC-002
Title: The Checklist Manifesto (Atul Gawande, 2009) — as cited within the Checklist Discipline skill
Type: discussion (secondary citation, not independently fetched)
URL: N/A — cited within https://someclaudeskills.com/docs/skills/checklist_discipline/, not independently accessed
Repository: N/A
Author/Organization: Atul Gawande
Date Accessed: 2026-08-23 (via citing skill page, not the primary work itself)
License: N/A (book, not inspected directly)
Research Domains: DOM-15, DOM-07
Claims Used: Grounding basis for SKL-030 Checklist Discipline's DO-CONFIRM/READ-DO format distinction, "killer items" concept, and forcing-function design; independently-verifiable real-world outcomes referenced (WHO Safe Surgery Checklist trial, Boeing 299 1935 incident, Pronovost central-line protocol)
Files Inspected: None — citation only, not independently verified against the primary source
Confidence: 40 — this is a second-hand citation via the skill's documentation, not a direct read of the primary work; flagged as the reason SKL-030's Evidence Quality is rated High-for-a-skill-source rather than fully independently corroborated. If SKL-030 advances toward Stage -2.5 pattern extraction, independently verifying at least the WHO/Pronovost outcome claims is recommended before treating them as FACT rather than INTERPRETATION (Section P5).
Notes: Registered because this is the single highest-evidence-quality basis found in the whole Stage -2.2 pass (see skill-catalog.md SKL-030) and because Section 12.2's evidence hierarchy places independent technical/historical corroboration above a vendor's own documentation — worth flagging its second-hand status honestly rather than letting the higher confidence bleed into an unverified primary claim.
```

```
Source ID: SRC-003
Title: erichowens/some_claude_skills (GitHub repository)
Type: repository
URL: https://github.com/erichowens/some_claude_skills
Repository: erichowens/some_claude_skills
Author/Organization: Erich Owens, Curiositech
Date Accessed: 2026-08-23 (URL surfaced via WebFetch/WebSearch results citing it; the repository itself was NOT cloned or inspected)
License: Unknown — not inspected
Research Domains: DOM-04 (all Stage -2.2 skill records generally)
Claims Used: None yet — registered as a known, not-yet-inspected candidate for Stage -2.3 (Open Repository Discovery), since every skill in skill-catalog.md traces back to this repo and the evidence-quality note on all 32 records depends on it remaining un-triaged.
Files Inspected: None
Confidence: 0 — placeholder registration only, no claims drawn from it
Notes: This is the actual underlying source code/script layer for everything in skill-catalog.md (the `.py` validation scripts, `init_skill.py`, `package_skill.py`, etc. referenced across multiple skill records were never opened). Per Section 12.2's evidence hierarchy (source code ranks above docs), triaging and, if warranted, deep-auditing this repo at Stage -2.3/-2.4 would materially raise the Evidence Quality ceiling on the entire skill-catalog.md set — currently capped at Medium precisely because this gap exists. Flagging explicitly for Stage -2.3 rather than silently leaving it implicit.
```

---

**Stage -2.3 additions (2026-08-24)** — non-repo sources surfaced by the six
parallel discovery passes; the repos themselves are recorded in
`repo-catalog.md` per Section 9.1's own URL/date fields, not duplicated here.

```
Source ID: SRC-004
Title: Model Context Protocol — Architecture Overview
Type: docs
URL: https://modelcontextprotocol.io/docs/2026-07-28/learn/architecture
Repository: N/A (spec docs, corresponds to modelcontextprotocol/servers)
Author/Organization: Anthropic (MCP steering group)
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-06
Claims Used: Primary-source architecture description of MCP, highest evidence tier per Section 12.2
Files Inspected: This page only
Confidence: 90 — official protocol steward documentation
Notes: Companion source to REPO-006 (modelcontextprotocol/servers).
```

```
Source ID: SRC-005
Title: OpenAI Agents SDK — Handoffs
Type: docs
URL: https://openai.github.io/openai-agents-python/handoffs/
Repository: N/A (docs, corresponds to openai/openai-agents-python, REPO-003)
Author/Organization: OpenAI
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-01, DOM-02
Claims Used: Maintainer-documented handoff-contract mechanism
Files Inspected: This page only
Confidence: 85
Notes: Companion source to REPO-003.
```

```
Source ID: SRC-006
Title: AutoGen — Handoffs Design Pattern
Type: docs
URL: https://microsoft.github.io/autogen/stable//user-guide/core-user-guide/design-patterns/handoffs.html
Repository: N/A
Author/Organization: Microsoft
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-01
Claims Used: Comparison baseline for handoff-pattern design vocabulary; AutoGen itself was deferred, not deep-audited, this stage
Files Inspected: This page only
Confidence: 70
Notes: N/A
```

```
Source ID: SRC-007
Title: AI Agent Error Handling: Retries, Circuit Breakers, and Fallback Chains
Type: discussion (independent technical writeup)
URL: https://www.openlegion.ai/en/learn/ai-agent-error-handling
Repository: N/A
Author/Organization: OpenLegion
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-06
Claims Used: Layered retry/fallback/circuit-breaker taxonomy used as comparison framing for DOM-06 gap analysis
Files Inspected: This page only
Confidence: 55 — independent vendor blog, not a primary implementation source
Notes: N/A
```

```
Source ID: SRC-008
Title: Agent Handoff Patterns: Routing Work Between AI Agents
Type: discussion (independent technical writeup)
URL: https://www.openlegion.ai/en/learn/agent-handoff-patterns
Repository: N/A
Author/Organization: OpenLegion
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-01
Claims Used: Secondary framing reference for handoff-pattern vocabulary
Files Inspected: This page only
Confidence: 55
Notes: N/A
```

```
Source ID: SRC-009
Title: Constraint Drift in LLM-Based Multi-Agent Systems
Type: paper (arXiv 2605.10481)
URL: https://arxiv.org/html/2605.10481v1
Repository: N/A
Author/Organization: Academic (authors not individually recorded this pass)
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-05
Claims Used: Names "Constraint State Governance" as a paradigm; explains the attention-based-instruction-decay mechanism behind why DOM-05's problem exists
Files Inspected: HTML version of paper
Confidence: 60 — academic source, no linked inspectable implementation
Notes: Explanatory/framing evidence, not an implementation candidate.
```

```
Source ID: SRC-010
Title: Dynamic Capability Scoping for Enterprise AI Agents
Type: paper (arXiv 2607.22445)
URL: https://arxiv.org/abs/2607.22445
Repository: N/A
Author/Organization: Academic
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-08
Claims Used: Three-source permission architecture (role ceiling + task-context classifier + policy prohibitions) as a comparison baseline
Files Inspected: Abstract/HTML
Confidence: 55 — academic source, no linked inspectable implementation
Notes: N/A
```

```
Source ID: SRC-011
Title: Trust Calibration in AI — UX Patterns
Type: docs (design-pattern guide)
URL: https://www.aiuxdesign.guide/patterns/trust-calibration
Repository: N/A
Author/Organization: AI Design Patterns
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-10
Claims Used: "Trust = (Competence x Consistency x Recoverability) / Consequence" framing used as comparison vocabulary for autonomy-graduation criteria
Files Inspected: This page only
Confidence: 45 — vendor/independent design guide, conceptual only
Notes: N/A
```

```
Source ID: SRC-012
Title: [FEATURE] Trust Calibration and Progressive Autonomy Model
Type: discussion (GitHub issue)
URL: https://github.com/anthropics/claude-code/issues/47183
Repository: anthropics/claude-code
Author/Organization: Anthropic / community
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-10
Claims Used: Negative evidence — even a leading agent CLI has progressive autonomy/trust calibration as an open feature request, not a shipped mechanism, corroborating DOM-10's "insufficient evidence in the wild" trajectory found across the whole cluster
Files Inspected: Issue text
Confidence: 75 — direct primary-source GitHub issue
Notes: Not independently re-verified via `gh` by the primary session (unlike the DOM-24 finding below); flag for verification if this becomes load-bearing for a strong pattern claim.
```

```
Source ID: SRC-013
Title: Human-in-the-Loop Tool Calling: Approval Gates for AI Agents
Type: discussion (vendor blog)
URL: https://www.scalekit.com/blog/human-in-the-loop-tool-calling
Repository: N/A
Author/Organization: Scalekit
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-07
Claims Used: Design principle — "the approval requirement should live in the workflow, not in the prompt," corroborating agent-governance-toolkit's own framing
Files Inspected: This page only
Confidence: 50 — vendor blog
Notes: N/A
```

```
Source ID: SRC-014
Title: Access Control for Multi-Tenant AI Agents
Type: discussion (vendor blog)
URL: https://www.scalekit.com/blog/access-control-multi-tenant-ai-agents
Repository: N/A
Author/Organization: Scalekit
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-08
Claims Used: Multi-tenant isolation failure-mode taxonomy (cache leakage, token reuse across tenants, stale in-memory mappings)
Files Inspected: This page only
Confidence: 50 — vendor blog
Notes: N/A
```

```
Source ID: SRC-015
Title: Long-Running AI Agent Runtime in 2026
Type: discussion (technical blog/survey)
URL: https://slavadubrov.github.io (exact post path not preserved by discovery pass — reverify path before citing as FACT)
Repository: N/A
Author/Organization: Slava Dubrov (independent)
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-13
Claims Used: Landscape survey naming two dominant checkpointing patterns (journal-replay vs. DB-checkpoint) and naming Temporal/Restate/Inngest/Hatchet/DBOS/LangGraph/AutoGen/CrewAI as the current field
Files Inspected: This page only
Confidence: 40 — independent blog, landscape survey only, exact URL path unconfirmed
Notes: Cite as a landscape-survey source only, not for any single technical claim, until the exact URL is re-confirmed.
```

```
Source ID: SRC-016
Title: Governance Decay: How Context Compaction Silently Erases Safety Constraints in Long-Horizon LLM Agents
Type: paper (arXiv 2606.22528)
URL: https://arxiv.org/abs/2606.22528
Repository: N/A
Author/Organization: Academic
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-12, DOM-05
Claims Used: Names a specific risk — context compaction can silently drop encoded behavioral constraints over long sessions — directly relevant to the DOM-12/DOM-05 intersection
Files Inspected: Abstract/HTML
Confidence: 60 — academic source
Notes: Worth citing prominently in Stage -2.5 pattern extraction as a named failure mode, not just a general concern.
```

```
Source ID: SRC-017
Title: Graphiti — Temporal Knowledge Graph (bi-temporal model docs)
Type: docs
URL: https://www.getzep.com/ai-agents/temporal-knowledge-graph
Repository: getzep/graphiti (REPO-017)
Author/Organization: Zep
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-12, DOM-11
Claims Used: t_valid/t_invalid bi-temporal mechanism detail, companion to REPO-017
Files Inspected: This page only
Confidence: 65 — maintainer docs, code-level verification still pending Stage -2.4
Notes: N/A
```

```
Source ID: SRC-018
Title: TsinghuaC3I/Awesome-Memory-for-Agents
Type: repository (curated list, not software)
URL: https://github.com/TsinghuaC3I/Awesome-Memory-for-Agents
Repository: TsinghuaC3I/Awesome-Memory-for-Agents
Author/Organization: Tsinghua C3I lab
Date Accessed: 2026-08-24
License: N/A (list)
Research Domains: DOM-12
Claims Used: None yet — discovery index only, registered for a possible future DOM-12 follow-up pass
Files Inspected: None
Confidence: 0 — placeholder registration
Notes: N/A
```

```
Source ID: SRC-019
Title: TeleAI-UAGI/Awesome-Agent-Memory
Type: repository (curated list, not software)
URL: https://github.com/TeleAI-UAGI/Awesome-Agent-Memory
Repository: TeleAI-UAGI/Awesome-Agent-Memory
Author/Organization: TeleAI-UAGI
Date Accessed: 2026-08-24
License: N/A (list)
Research Domains: DOM-12
Claims Used: None yet — discovery index only
Files Inspected: None
Confidence: 0 — placeholder registration
Notes: N/A
```

```
Source ID: SRC-020
Title: LiteLLM — Provider Budget Routing docs
Type: docs
URL: https://docs.litellm.ai/docs/proxy/provider_budget_routing
Repository: BerriAI/litellm (REPO-022)
Author/Organization: BerriAI
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-16
Claims Used: Primary-source config schema for budget/routing — needed to verify README-vs-code claims at Stage -2.4 audit
Files Inspected: This page only
Confidence: 70 — maintainer docs, code-level verification still pending
Notes: N/A
```

```
Source ID: SRC-021
Title: How Adversarial Judge Pipelines Make AI Agents Trustworthy
Type: discussion (independent technical writeup)
URL: https://dev.to/varun_pratapbhardwaj_b13/
Repository: N/A
Author/Organization: independent (dev.to)
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-15
Claims Used: Describes a concrete 2-round adversarial-judge / multi-model-consensus quality-gate architecture (approve/revise/reject) as a DOM-15 pattern reference, even without a linked repo
Files Inspected: This page only
Confidence: 40 — independent blog, no linked implementation
Notes: URL truncated by discovering pass — reverify full path before citing as FACT.
```

```
Source ID: SRC-022
Title: Content-Agent: Building an AI System That Researches, Fact-Checks, and Publishes
Type: discussion (independent writeup/case study)
URL: https://themachinist.org/content-agent
Repository: N/A
Author/Organization: independent (The Machinist)
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-07, DOM-15
Claims Used: Real-world LangGraph pipeline explicitly designed so "the agent never publishes on its own" — directly analogous to Hermes' approval-gate + quality-gate combination
Files Inspected: This page only
Confidence: 55 — independent case study, self-reported
Notes: N/A
```

```
Source ID: SRC-023
Title: awesome-mllm-guardrails
Type: repository (curated list, not software)
URL: https://github.com/ant-research/awesome-mllm-guardrails
Repository: ant-research/awesome-mllm-guardrails
Author/Organization: Ant Research
Date Accessed: 2026-08-24
License: N/A (list)
Research Domains: DOM-17
Claims Used: None yet — discovery index for guardrail repos/benchmarks/guard models, registered for a possible follow-up pass
Files Inspected: None
Confidence: 0 — placeholder registration
Notes: N/A
```

```
Source ID: SRC-024
Title: CANVAS — Continuity-Aware Narratives via Visual Agentic Storyboarding
Type: paper (arXiv 2604.13452)
URL: https://arxiv.org/pdf/2604.13452
Repository: N/A
Author/Organization: Academic
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-03, DOM-20
Claims Used: Explicit world-state model for narrative consistency — methodological comparison baseline, independent of any specific repo
Files Inspected: PDF (via fetch)
Confidence: 55 — academic source, no linked inspectable implementation
Notes: N/A
```

```
Source ID: SRC-025
Title: StoryState — Agent-Based State Control for Consistent and Editable Storybooks
Type: paper (arXiv 2602.01305)
URL: https://arxiv.org/pdf/2602.01305
Repository: N/A
Author/Organization: Academic
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-03
Claims Used: Explicit editable-state-as-first-class-object pattern, comparison baseline
Files Inspected: PDF (via fetch)
Confidence: 55 — academic source
Notes: N/A
```

```
Source ID: SRC-026
Title: Agentic Analytics: Closing the Loop from Insight to Action with AI Agents
Type: discussion (vendor blog)
URL: https://www.tredence.com/blog/agentic-analytics
Repository: N/A
Author/Organization: Tredence
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-22
Claims Used: Defines the "closed-loop analytics" concept DOM-22 is researching; marketing-tier evidence only, no inspectable implementation — explains why DOM-22 remained a confirmed coverage gap this stage (the concept is discussed everywhere, implemented nowhere inspectable this pass could find)
Files Inspected: This page only
Confidence: 30 — vendor marketing content, lowest evidence tier per Section 12.2
Notes: N/A
```

```
Source ID: SRC-027
Title: Build an AI Competitor Intelligence Agent Team
Type: discussion (tutorial/walkthrough)
URL: https://www.theunwindai.com/p/build-an-ai-competitor-intelligence-agent-team
Repository: N/A (no independently verified repo link this pass)
Author/Organization: The Unwind AI
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-18
Claims Used: None yet — walkthrough-tier lead, flagged for possible follow-up if DOM-18's confirmed thin coverage needs a second pass
Files Inspected: This page only
Confidence: 20 — tutorial-tier, unverified
Notes: N/A
```

```
Source ID: SRC-028
Title: NousResearch/hermes-agent — Issue #34352, "Solving the Multi-Tenant Hermes Problem"
Type: discussion (GitHub issue, primary source on REPO-001 itself)
URL: https://github.com/NousResearch/hermes-agent/issues/34352
Repository: NousResearch/hermes-agent (REPO-001)
Author/Organization: NimbleCoAI (opened by NimbleCo AI), 24 comments from various operators
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-24 (primary), DOM-11, DOM-08
Claims Used: FACT (independently verified by the primary Phase -2 session via `gh issue view 34352 --repo NousResearch/hermes-agent` on 2026-08-24, not taken on the discovering fork's summary alone): the issue is real, open, has 24 comments, and states that stock hermes-agent has no tenant isolation — "one agent = one tenant. Memory is global, sessions don't scope by tenant" — with 12+ related open issues clustered into four sub-problems (gateway adapter multi-instance, profile routing, memory/context isolation, session key correctness). One commenter (jingchang0623-crypto, on issue #9514, translated from Chinese) self-reports a production incident: a content agent read competitor-monitoring memory and wrote it into a public article, risking legal consequences for the operator. This specific incident report is a third-party testimonial WITHIN a verified-real issue — the issue's existence and content are FACT; the incident itself is a REPORTED/CLAIMED event, not independently verified beyond the comment existing. No PRs addressing any of the 12+ issues have been merged or are open as of access date.
Files Inspected: Full issue text via `gh issue view`
Confidence: 90 for the issue's existence/content; 50 for the specific incident claim within it (self-reported, unverified beyond the comment existing)
Notes: This is the highest-value primary-source finding of Stage -2.3 — a documented, source-level fact about the known base architecture (REPO-001) itself, not a hypothesis. It directly informs DOM-24 and should be handed to whoever runs REPO-001's Stage -2.4 Dimension C/H audit rather than re-discovered. It also led directly to the discovery and independent verification of REPO-040 (NimbleCoAI/hermes-agent fork) and REPO-041 (NimbleCoAI/hermes-swarm-map). See the corresponding note added to `research-domains.md`'s Known Base Architecture section.
```

```
Source ID: SRC-029
Title: AWS Prescriptive Guidance — Agent Deployment Models (multi-tenancy)
Type: docs
URL: https://docs.aws.amazon.com/prescriptive-guidance/latest/agentic-ai-multitenant/agent-deployment-models.html
Repository: N/A
Author/Organization: AWS
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-24
Claims Used: Names the siloed/pooled/hybrid multi-tenancy taxonomy in vendor-neutral, architecture-level terms — classification framework for writing up DOM-24 findings, not evidence of any specific implementation
Files Inspected: This page only
Confidence: 60 — official vendor docs, architecture-level not implementation-level
Notes: N/A
```

```
Source ID: SRC-030
Title: Building Multi-Tenant Agents with Amazon Bedrock AgentCore
Type: discussion (official vendor blog)
URL: https://aws.amazon.com/blogs/machine-learning/building-multi-tenant-agents-with-amazon-bedrock-agentcore/
Repository: N/A
Author/Organization: AWS
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-24
Claims Used: Concrete namespace/composite-identifier isolation pattern (tenant_123:user_456) — specific, inspectable mechanism description, not just marketing, worth citing for DOM-24 pattern extraction at Stage -2.5
Files Inspected: This page only
Confidence: 55 — vendor blog, but describes a specific mechanism rather than pure marketing
Notes: N/A
```

```
Source ID: SRC-031
Title: Thoughtworks Technology Radar
Type: website (methodology reference)
URL: https://www.thoughtworks.com/radar
Repository: N/A
Author/Organization: Thoughtworks
Date Accessed: 2026-08-24
License: N/A
Research Domains: DOM-25
Claims Used: Not agentic/automated (human-curated), but the canonical "continuous external scouting -> rated, published recommendation" structure DOM-25 is trying to automate — a target-shape reference for what a good DOM-25 output artifact should look like, not an implementation source
Files Inspected: Site overview only
Confidence: 50 — reference/methodology, not an implementation
Notes: N/A
```
