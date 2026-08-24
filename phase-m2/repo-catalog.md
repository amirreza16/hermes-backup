# Hermes Phase -2 Repository Catalog

Continuously maintained (Section 6.1). Schema: Master Plan Section 9.2.
First populated at Stage -2.3 (Open Repository / Project Discovery), 2026-08-24.

REPO-001 (`NousResearch/hermes-agent`) is the Owner-disclosed known base
architecture, formally reserved in `research-domains.md` under
`## Known Base Architecture` — not repeated here as a full record since it did
not come through the normal Stage -2.3 discovery funnel (Section 9.2's schema
still applies to it at Stage -2.4). All records below (REPO-002 onward) are
genuine Stage -2.3 discoveries, found via broad category search seeds per
Section 15.2 with no assumed relevance, and are candidate **comparison
baselines** for the domains reframed around REPO-001, or **primary
green-field candidates** for domains not governed by the known base
architecture. Six parallel discovery passes were run, one per domain cluster;
duplicate finds across passes (e.g. `langchain-ai/langgraph` found by both the
core-architecture and memory/reliability passes) were merged into a single
record citing every relevant DOM ID.

Two records (REPO-040, REPO-041) were independently verified and added by the
primary Phase -2 session (not a discovery-pass fork) after a fork surfaced a
GitHub issue on REPO-001 itself describing them — see the note at REPO-040 and
the corresponding entry in `research-domains.md`.

Depth at this stage is triage-level (README + structure + light source skim),
per Section 15.2 — README-only evaluation is insufficient for high confidence,
but a full Section 9.3 A-J deep audit is Stage -2.4 scope, not this catalog's.
No numeric scores are assigned here (Section 10 scoring applies at deep-audit
/ pattern stage, not repo triage).

---

## Cluster A — Core Agent Architecture (DOM-01, 02, 04, 06)

```
Repo: langchain-ai/langgraph
URL: https://github.com/langchain-ai/langgraph
Category: Multi-agent orchestration framework / durable execution
Stars: 40.4k
Forks: 6.8k
Recent Activity: Active, 7,045 commits, 473 open issues
License: MIT
Primary Language: Python
Maturity: Mature/production (v1+ ecosystem)
Claimed Purpose: Low-level stateful-agent orchestration; graph-based workflows, durable execution/checkpointing, HITL checkpoints, short/long-term memory.
Potential Hermes Relevance: DOM-01 (orchestration/handoff comparison baseline for hermes-agent), DOM-02 (state-schema-as-contract angle), DOM-13 (checkpoint-based durable-execution pattern — "journal-replay" model, comparison baseline for hermes-agent's scheduling/reliability substrate).
Triage Decision: DEEP AUDIT
Decision Rationale: Widely-adopted, code-inspectable, explicit HITL + durable-execution primitives directly comparable to Hermes' approval-gated 2-role need. Found independently by two discovery passes (core architecture and memory/reliability), confirming cross-domain relevance rather than being merged only for convenience.
Date Triaged: 2026-08-24
```

```
Repo: openai/openai-agents-python
URL: https://github.com/openai/openai-agents-python
Category: Multi-agent orchestration framework (lightweight, handoff-based)
Stars: 28.9k
Recent Activity: Active, 2,175 commits, voice/realtime support recently added
License: MIT
Primary Language: Python
Maturity: Production-ready; official successor to OpenAI's earlier "Swarm"
Claimed Purpose: Handoff-based agent delegation ("agents as tools"), Pydantic-enforced structured outputs, tracing, session management.
Potential Hermes Relevance: DOM-01 (handoff pattern closer to Hermes' 2-fixed-role scale than large-swarm frameworks), DOM-02 (schema-typed handoff contracts).
Triage Decision: DEEP AUDIT
Decision Rationale: Purpose-built handoff mechanism architecturally the closest fit found to a small, fixed-role pipeline; officially maintained by the model vendor.
Date Triaged: 2026-08-24
```

```
Repo: pydantic/pydantic-ai
URL: https://github.com/pydantic/pydantic-ai
Category: Agent contract / structured-output framework
Stars: 19.5k
Recent Activity: Active, 2,803 commits
License: MIT
Primary Language: Python
Maturity: Production-ready
Claimed Purpose: Output contract as first-class typed citizen (`output_type` validated every run, not just suggested); sub-agent composition via "capabilities."
Potential Hermes Relevance: DOM-02 — directly matches the domain's research question (is the mechanism expressive/enforced or merely suggested at role boundaries).
Triage Decision: DEEP AUDIT
Decision Rationale: Best direct hit found for DOM-02's exact question; code-inspectable design philosophy ("enforced-or-fails"), not just docs claims.
Date Triaged: 2026-08-24
```

```
Repo: google/adk-python
URL: https://github.com/google/adk-python
Category: Multi-agent orchestration framework (Google-backed)
Stars: 21.3k
Forks: 3.9k
Recent Activity: Active, 3,877 commits, 306 open issues, bi-weekly releases
License: Apache 2.0
Primary Language: Python
Maturity: Stable (v2.0)
Claimed Purpose: Graph-based workflow runtime (routing/fan-out/fan-in/loops/retry), Agent+Workflow class split, tool-confirmation HITL gates, MCP tool integration, output_schema enforcement.
Potential Hermes Relevance: DOM-01 (orchestration), DOM-02 (output_schema/Task API contracts), DOM-06 (native MCP integration + built-in retry). Cross-relevant to DOM-07 (tool-confirmation gate structurally analogous to Hermes' irreversible-action approval requirement) though DOM-07 was not this pass's slice.
Triage Decision: DEEP AUDIT
Decision Rationale: Covers three domains at once with real, mature, org-backed code.
Date Triaged: 2026-08-24
```

```
Repo: modelcontextprotocol/servers
URL: https://github.com/modelcontextprotocol/servers
Category: MCP reference implementation
Stars: 89.8k
Recent Activity: Active, 4,161 commits
License: Apache 2.0 (new servers) / MIT (existing)
Primary Language: TypeScript, Python
Maturity: Official reference — explicitly self-described as "educational examples," not production-hardened
Claimed Purpose: Canonical reference servers (filesystem, git, memory, fetch, sequential-thinking, time, everything).
Potential Hermes Relevance: DOM-06 — primary/highest-trust source for what MCP actually is, per Section 12.2 evidence order (official protocol stewards).
Triage Decision: DEEP AUDIT
Decision Rationale: Highest evidence tier available (source from the protocol's own stewards); necessary baseline before judging any third-party MCP claim.
Date Triaged: 2026-08-24
```

```
Repo: mabualzait/MicroMCP
URL: https://github.com/mabualzait/MicroMCP
Category: MCP gateway / security-isolation pattern
Stars: 3
Recent Activity: 4 commits, single author, 2025
License: MIT
Primary Language: JavaScript/Node.js
Maturity: Experimental MVP
Claimed Purpose: Composes many single-purpose MCP servers behind a policy/audit gateway for blast-radius containment and least-privilege per-service credentials.
Potential Hermes Relevance: DOM-06 — directly addresses the "blast-radius containment on failure" half of the domain's research question.
Triage Decision: REFERENCE ONLY
Decision Rationale: Too thin (3 stars, MVP, one author) for full audit weight, but the gateway-isolation pattern is worth citing at Stage -2.5.
Date Triaged: 2026-08-24
```

```
Repo: InfinitiBit/graphbit
URL: https://github.com/InfinitiBit/graphbit
Category: Multi-agent orchestration engine (reliability-focused)
Stars: 580
Recent Activity: 471 commits, active governance docs (CONTRIBUTING/SECURITY/CODE_OF_CONDUCT)
License: Apache 2.0
Primary Language: Rust (core), Python bindings
Maturity: Active, claims real production adoption (Grant Thornton Germany — unverified, README claim)
Claimed Purpose: Per-agent circuit breakers, retry with exponential backoff/jitter, retryable-vs-non-retryable error classification, LLM-based tool selection.
Potential Hermes Relevance: DOM-06 (concrete answer to error-handling/blast-radius robustness), secondarily DOM-01.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real reliability mechanisms with a named (unverified) production adopter, but general orchestration engine, not centrally MCP-specific — reliability-pattern comparison, not a DOM-06 primary.
Date Triaged: 2026-08-24
```

```
Repo: authzed/mcp-server-reference
URL: https://github.com/authzed/mcp-server-reference
Category: MCP authorization pattern reference
Stars: 1
Recent Activity: 4 commits, appears newly initialized
License: Apache 2.0
Primary Language: TypeScript
Maturity: Early-stage/thin
Claimed Purpose: Zanzibar-style fine-grained authorization (SpiceDB) + OAuth 2.0 gating on MCP tool invocations.
Potential Hermes Relevance: DOM-06/DOM-08 boundary — illustrates a real (if minimal) permission-scoping-per-tool-call pattern.
Triage Decision: REFERENCE ONLY (low confidence — per Section 10.4 rule 2, evidence too thin to score even if scoring applied here)
Decision Rationale: Too little code/activity to audit meaningfully; concept (Zanzibar-for-MCP) worth citing if DOM-06/DOM-08 gap analysis needs a concrete example.
Date Triaged: 2026-08-24
```

---

## Cluster B — Human Control, Safety & Trust (DOM-05, 07, 08, 09, 10)

```
Repo: microsoft/agent-governance-toolkit
URL: https://github.com/microsoft/agent-governance-toolkit
Category: Agent runtime governance / policy enforcement
Stars: 6.1k
Forks: 1.1k
Recent Activity: Active — 2,456 commits, 102 open issues, 118 open PRs
License: MIT
Primary Language: Python (+ TS/.NET/Go/Rust SDKs)
Maturity: "Production-quality public preview" (not GA)
Claimed Purpose: Structural (not prompt-level) enforcement of agent policy — `govern()` decorator blocks tool calls via YAML policy engine; zero-trust identity (SPIFFE/DID) with trust scoring; 4-level privilege rings; SRE-style reliability (SLOs, circuit breakers, chaos testing). Explicitly frames itself against "please follow the rules" prompt-level safety.
Potential Hermes Relevance: DOM-05 (structural constraint enforcement vs. prompt drift), DOM-07 (`require_approval` policy action), DOM-08 (privilege rings + per-agent credential scoping maps directly to Hermes' multi-page isolated-credential need).
Triage Decision: DEEP AUDIT
Decision Rationale: Real code across multiple language SDKs, MIT license, no doc/code mismatch found on inspection at this depth — though claims like "10/10 OWASP coverage" need Stage -2.4 verification, not face-value acceptance (Section 12.1). Strongest single candidate found this stage — cross-cuts three domains.
Date Triaged: 2026-08-24
```

```
Repo: humanlayer/humanlayer
URL: https://github.com/humanlayer/humanlayer
Category: Human-in-the-loop approval SDK
Stars: 11.3k
Forks: 940
Recent Activity: Repo's own README states it is deprecated ("the code here is pretty much all deprecated"), redirecting to humanlayer.com for an active rebuild — 2,098 historical commits, but this specific repo is winding down.
License: present, exact terms unconfirmed at this pass
Primary Language: TypeScript (+ Go client)
Maturity: Formerly active, self-declared transition/deprecation
Claimed Purpose: Wraps tool calls with approval gates routed via Slack/email, audit trails, escalation paths.
Potential Hermes Relevance: DOM-07 — most directly on-target artifact found for approval-gate mechanics, but deprecation status is a real maintenance-signal risk (Section 10.1.7) to weigh at audit, not gloss over. Popularity (11.3k stars) is not proof of current suitability (Section 12.1).
Triage Decision: DEEP AUDIT
Decision Rationale: Despite deprecation, highest-profile purpose-built approval-gate SDK found, with real code across `/hld`, `/hlyr`, `/packages`. Audit the mechanism as a pattern; treat "is this project still viable to adopt" as a separate, likely-negative question — record both findings distinctly, don't let pattern quality launder project maintenance risk.
Date Triaged: 2026-08-24
```

```
Repo: agentward-ai/agentward
URL: https://github.com/agentward-ai/agentward
Category: Agent tool-call permission/policy control plane
Stars: 19
Forks: 5
Recent Activity: 118 commits, v0.4.0, maintainers transparently document own test-coverage gaps
License: Business Source License 1.1 (proprietary until 2028-04-24, converts to Apache 2.0 after — restricts code reuse now, concepts remain studiable)
Primary Language: Python (+ npm bindings)
Maturity: Early-stage, functional (3,466 passing tests), explicitly "not battle-tested end-to-end" per maintainers
Claimed Purpose: Intercepts tool calls; policy-based allow/block/require-approval/redact; path/domain/CIDR/argument-shape constraints; session-level evasion detection (fragmentation, privilege escalation, exfiltration sequencing); explicitly agent-specific, contrasted against generic OAuth/IAM.
Potential Hermes Relevance: DOM-08 — matches the domain's exclusion criterion (must be agent-specific, not generic IAM) better than any other candidate found; evasion-detection layer also relevant to DOM-17.
Triage Decision: DEEP AUDIT
Decision Rationale: Small/early but unusually well-documented about its own limits (positive evidence-quality signal — self-reported gaps beat unverified confidence, per Section 12.1). License restriction noted for Dimension J.
Date Triaged: 2026-08-24
```

```
Repo: ashutoshrana/confidence-escalation
URL: https://github.com/ashutoshrana/confidence-escalation
Category: Confidence-gated escalation middleware
Stars: 0
Forks: 0
Recent Activity: 35 commits, CI badge present, 0 open issues/1 PR
License: MIT
Primary Language: Python, framework-agnostic (LangChain/CrewAI/AutoGen/Google ADK adapters)
Maturity: Early but functionally complete for its scope — real tests, real code
Claimed Purpose: Multi-signal confidence scoring (logprob + verbalized + tool-risk) feeding threshold policies (single/dual/composite-chain) routing to `HumanInLoopHandler`, `ModelUpgradeHandler` (haiku→sonnet→opus), `ToolRestrictionHandler`, or `ComplianceLoggingHandler`; explicitly targets OWASP Agentic AI ASI-09 "Human-Agent Trust Exploitation."
Potential Hermes Relevance: DOM-10 (this is the trigger-logic mechanism DOM-10's research question actually asks for — confidence threshold → escalation, not just "the agent can ask"); secondarily DOM-09, though framed as model-confidence rather than task-ambiguity — a related but distinct signal, do not conflate at Stage -2.5.
Triage Decision: DEEP AUDIT
Decision Rationale: Closest match found anywhere in Stage -2.3 to DOM-10's actual research question. Zero stars is a genuine maturity/adoption gap to record honestly, not a disqualifier — Section 12.1 forbids treating a recent/unpopular repo as useless solely for being new.
Date Triaged: 2026-08-24
```

```
Repo: FareedKhan-dev/agentic-guardrails
URL: https://github.com/FareedKhan-dev/agentic-guardrails
Category: Guardrail-design tutorial
Stars: 46
Recent Activity: 2 commits — essentially a single publish
License: MIT
Primary Language: Jupyter Notebook
Maturity: Experimental/pedagogical
Claimed Purpose: Walks through a 3-layer guardrail architecture (input validation, action planning, output verification) with mocked API responses — explicitly a teaching narrative, not a deployable library.
Potential Hermes Relevance: DOM-05 — conceptually relevant layered-defense framing.
Triage Decision: REFERENCE ONLY
Decision Rationale: Confirmed pedagogical/conceptual on inspection (mocked responses, incomplete production code) — fails the DEEP AUDIT bar but has comparison value.
Date Triaged: 2026-08-24
```

```
Repo: systempromptio/awesome-ai-agent-governance
URL: https://github.com/systempromptio/awesome-ai-agent-governance
Category: Curated index (no code)
Stars: 28
Forks: 43
Recent Activity: Actively maintained, 54 commits
License: N/A (list, not software)
Maturity: N/A
Claimed Purpose: Index of agent-governance projects (names Cedar, OPA, Casbin, Penholder, CoreBase, ThumbGate, systemprompt-core, SteerPlane, LiteLLM, Portkey as leads).
Potential Hermes Relevance: DOM-08 — none of the named leads independently verified this pass; useful only as a discovery index for a future pass.
Triage Decision: REFERENCE ONLY
Decision Rationale: Not an inspectable implementation itself.
Date Triaged: 2026-08-24
```

---

## Cluster C — State, Memory & Reliability (DOM-11, 12, 13, 14)

```
Repo: jshiv/cronicle
URL: https://github.com/jshiv/cronicle
Category: Agent scheduling / durable execution (cron + DAG workflow runtime)
Stars: 23
Recent Activity: 431 commits on main, actively maintained
License: MIT
Primary Language: Go
Maturity: Early-to-mid; "production-ready fundamentals," niche adoption
Claimed Purpose: Unifies shell tasks and AI-agent tasks under one cron-scheduled, DAG-dependency, HCL-declared runtime with git versioning; native cron triggers, dependency-gated DAG with automatic downstream-skip on failure, distributed mode with SQLite-durable job queue, cancel/retry/resume.
Potential Hermes Relevance: DOM-13 (primary comparison baseline for hermes-agent's scheduling/reliability substrate). DOM-11 (secondary) — structured JSONL event log + per-run transcript files + SQLite state projection as an append-style audit trail, BUT its log rotation policy (500MB × 3 files × 28-day gzip retention) eventually discards old logs, a direct point of tension with Hermes' never-delete principle — flag explicitly for DOM-11 gap analysis at Stage -2.4, do not silently adopt this rotation behavior. DOM-16 (secondary) — native `budget_usd` per-run cost ceiling with abort-on-exceed and USD-cost reporting. DOM-06 (secondary) — MCP server subprocess support + Anthropic Agent Skills loading via `load_skill`.
Triage Decision: DEEP AUDIT
Decision Rationale: Small/low-star but unusually dense multi-domain fit (four separate Hermes domains) with real, inspectable Go source, not just marketing copy — exactly the kind of small-but-architecturally-relevant candidate Section 12 favors over popularity.
Date Triaged: 2026-08-24
```

```
Repo: getzep/graphiti
URL: https://github.com/getzep/graphiti
Category: Agent memory (temporal knowledge graph)
Stars: reported ~20k+ in secondary sources, not directly confirmed this pass — verify at audit
License: unconfirmed this pass — verify at audit
Primary Language: Python
Maturity: Active, backs Zep's commercial memory product
Claimed Purpose: Builds/queries a temporally-aware knowledge graph — bi-temporal model (t_valid/t_invalid per edge), fact invalidation instead of overwrite, provenance tracking to source data.
Potential Hermes Relevance: DOM-12 (primary) — purpose-built for continuity across sessions too long for one context window, not generic RAG. DOM-11 (secondary) — the "fact invalidation, not deletion" model is directly comparable to the never-delete principle and could double as a comparison baseline there.
Triage Decision: DEEP AUDIT
Decision Rationale: Purpose-built (not generic RAG) with a documented, code-level mechanism, not just a claim.
Date Triaged: 2026-08-24
```

```
Repo: mem0ai/mem0
URL: https://github.com/mem0ai/mem0
Category: Agent memory (hybrid vector + graph + KV)
Stars: reported 47k-60k across sources (wide variance — do not trust the number alone per Section 12.1, verify at audit)
License: Apache 2.0
Primary Language: Python
Maturity: Active, high community adoption signal
Claimed Purpose: "Universal memory layer for AI Agents" — fact/preference extraction on each `add()`, stored across vector DB + graph DB (Neo4j, Pro tier) + KV cache, multi-signal retrieval (semantic + BM25 + entity).
Potential Hermes Relevance: DOM-12 — comparison baseline against Graphiti; different architecture (fact-extraction + multi-store vs. temporal-graph-native).
Triage Decision: REFERENCE ONLY
Decision Rationale: Well-evidenced and real, but graph-memory tier is Pro/paywalled and its continuity model is less purpose-built for narrative/voice continuity than Graphiti's — useful documented comparison, not worth a full audit given Graphiti covers the same ground more directly.
Date Triaged: 2026-08-24
```

```
Repo: eugene-khyst/postgresql-event-sourcing
URL: https://github.com/eugene-khyst/postgresql-event-sourcing
Category: Event-sourcing / append-only store reference architecture
License: unconfirmed
Primary Language: Java (Spring Boot)
Maturity: Reference/template repo, not a live product
Claimed Purpose: Reference implementation of an event-sourced system on Postgres as event store.
Potential Hermes Relevance: DOM-11 comparison baseline — generic append-only/event-store mechanics (not agent-specific).
Triage Decision: REFERENCE ONLY
Decision Rationale: Not agent-specific and a different stack than Hermes will plausibly use, but a clean, citable textbook pattern for the DOM-11 pattern write-up.
Date Triaged: 2026-08-24
```

```
Repo: langfuse/langfuse
URL: https://github.com/langfuse/langfuse
Category: LLM/agent observability platform
License: open-source, self-hostable — exact license unconfirmed this pass
Maturity: Active, YC-backed, broad integration ecosystem (OpenTelemetry, LangChain, OpenAI SDK, LiteLLM)
Claimed Purpose: Traces, evals, prompt management, playground, datasets for LLM apps/agents; async batched trace ingestion.
Potential Hermes Relevance: DOM-14 (primary) — structured trace capture of LLM calls/tool invocations/control-flow decisions, framework-agnostic.
Triage Decision: REFERENCE ONLY
Decision Rationale: Strong and real, but a third-party tool to integrate, not an architectural pattern to build from scratch — relevant as "what a human-auditor-facing observability layer looks like," and a candidate for actual adoption later (Phase -1 concern), not something needing a Section 9.3 A-J audit here.
Date Triaged: 2026-08-24
```

```
Repo: Arize-ai/phoenix
URL: https://github.com/Arize-ai/phoenix
Category: LLM/agent observability platform
License: Elastic License 2.0
Stars: reported 10k+ (secondary source)
Maturity: Active
Claimed Purpose: Self-hostable LLM/agent/RAG observability — OpenTelemetry-standard traces of prompt/response/tool-call/retrieval/agent-decision steps, zero-cloud-dependency local mode.
Potential Hermes Relevance: DOM-14 — second strong reference alongside Langfuse; license terms differ (Elastic 2.0 vs. Langfuse's), relevant if either is ever actually adopted.
Triage Decision: REFERENCE ONLY
Decision Rationale: Same reasoning as Langfuse — real, well-evidenced tool-integration candidate rather than an architecture-pattern candidate for this research phase.
Date Triaged: 2026-08-24
```

---

## Cluster D — Evaluation, Cost & Security (DOM-15, 16, 17)

```
Repo: BerriAI/litellm
URL: https://github.com/BerriAI/litellm
Category: LLM gateway / cost & routing infrastructure
Stars: ~57.2k
Forks: ~10.9k
Recent Activity: Very high (44k+ commits, active CI/CD)
License: CONFIRMED at Stage -2.4 (2026-08-24) — dual: MIT for the core, with a separately-licensed `enterprise/` carve-out (not plain MIT as previously guessed). See `phase-m2/repo-audits/berriai-litellm.md` Dimension J for detail.
Primary Language: Python + Rust core
Maturity: Mature, production-proven at scale
Claimed Purpose: Unified proxy/SDK for 100+ LLM providers with budget caps (per key/team/org/model, daily/monthly), auto-routing (cheap-first escalation), retry/fallback.
Potential Hermes Relevance: DOM-16 — mature, widely-adopted implementation of exactly the mechanisms Hermes needs to compare hermes-agent's routing/budget system against.
Triage Decision: DEEP AUDIT
Decision Rationale: Highest evidence ceiling available for this domain; docs describe a concrete budget/routing config surface, but architectural detail wasn't visible from a single-page fetch — needs real Stage -2.4 code inspection before claims are trusted (Section 12.2 — docs untested against code at this depth).
Date Triaged: 2026-08-24
```

```
Repo: AgentBudget/agentbudget
URL: https://github.com/AgentBudget/agentbudget
Category: Per-session LLM cost circuit-breaker (SDK)
Stars: 108
Forks: 26
Recent Activity: Active (166 commits, recent v0.4.0, LangChain/LangGraph integration)
License: Apache 2.0
Primary Language: Python (+ Go/TS SDKs)
Maturity: Early-active, small but real, versioned releases
Claimed Purpose: "ulimit for AI agents" — process-wide patching of OpenAI/Anthropic SDKs, per-session dollar budget, `BudgetExhausted` hard-stop, loop detection, soft/hard limits.
Potential Hermes Relevance: DOM-16 — smaller, more inspectable comparison than LiteLLM; session-isolation mechanism directly analogous to Hermes' per-page-instance need.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real, working, tested mechanism, but narrower/single-purpose vs. LiteLLM's fuller routing story — comparison point, not primary audit target given limited Stage -2.4 bandwidth.
Date Triaged: 2026-08-24
```

```
Repo: NVIDIA-NeMo/Guardrails
URL: https://github.com/NVIDIA-NeMo/Guardrails
Category: LLM output/conversation safety guardrail toolkit
Recent Activity: Active (v0.22.0, May 2025 per docs)
License: Apache 2.0
Primary Language: Python (+ Colang DSL)
Maturity: Mature, vendor-backed
Claimed Purpose: Programmable guardrails intercepting LLM input/output — self-check moderation, fact-checking/hallucination detection, jailbreak/injection detection; models the entire conversation flow, not just a single-turn filter.
Potential Hermes Relevance: DOM-17 — most evidenced content-safety-guardrail candidate found; directly answers "guardrails against generating/publishing harmful content" independent of the approval gate (DOM-07).
Triage Decision: DEEP AUDIT
Decision Rationale: Mature, vendor-maintained, architecturally distinct (flow-based, not keyword filter) — highest-value comparison baseline found in this cluster.
Date Triaged: 2026-08-24
```

```
Repo: SoCloseSociety/MiloAgent
URL: https://github.com/SoCloseSociety/MiloAgent
Category: Multi-account social automation agent (Reddit/Twitter/Telegram)
Stars: 33
Forks: 6
Recent Activity: Active (62 commits)
License: MIT
Primary Language: Python (FastAPI, APScheduler, SQLite)
Maturity: Early-active, single real end-to-end system
Claimed Purpose: Autonomous multi-account engagement bot with pre-post checks (spam/duplicate/banned-phrase filtering), rate limiting, shadowban detection, circuit breaker, karma-tiered account rotation.
Potential Hermes Relevance: DOM-17 — negative example: credentials are only gitignored YAML files, no real vaulting/encryption/rotation. Informative as a "what not to do" comparison baseline. (Incidentally touches DOM-23/community engagement, but DOM-23 remains BLOCKED — noted only for awareness, not triaged as in-scope.)
Triage Decision: REFERENCE ONLY
Decision Rationale: Useful negative example of weak credential handling in a real multi-account bot, not strong enough as a positive pattern source for a full audit.
Date Triaged: 2026-08-24
```

```
Repo: The-PR-Agent/pr-agent
URL: https://github.com/The-PR-Agent/pr-agent
Category: LLM reviewer/critic agent (code review, generalizable pattern)
Maturity: Mature, production-proven, widely adopted
License: open-source — exact license unconfirmed this pass
Primary Language: Python
Claimed Purpose: Automated reviewer agent producing structured feedback before human merge — generator/reviewer separation, single LLM call review (~30s), low cost, handles any PR size.
Potential Hermes Relevance: DOM-15 — most evidenced real-world "reviewer agent gates output before human sees it" mechanism found; domain is code not content, but the review-then-gate mechanism reads as domain-agnostic (Section 10.1.2 generalizability).
Triage Decision: DEEP AUDIT
Decision Rationale: Best available concrete implementation of the evaluator/critic-before-human-approval pattern DOM-15 needs; most other DOM-15 hits were papers/articles, not inspectable code.
Date Triaged: 2026-08-24
```

```
Repo: strands-agents/evals
URL: https://github.com/strands-agents/evals
Category: Agent evaluation framework
Stars: 182
Recent Activity: Active (210+ commits, 57 open issues, 24 open PRs)
License: Apache 2.0
Primary Language: Python 3.10+
Maturity: Active, real test suites, OpenTelemetry integration
Claimed Purpose: Rubric-based LLM-as-judge scoring, trajectory/session-level evaluators, CLI schema validation for CI/CD.
Potential Hermes Relevance: DOM-15 — post-hoc evaluation infrastructure, not a pre-publish gate; no native self-critique/reviewer loop.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real, well-evidenced framework, but mechanism doesn't match DOM-15's specific need (gate before human sees draft) as directly as pr-agent's live review-then-block pattern — useful for the rubric-scoring building block, not the core pattern.
Date Triaged: 2026-08-24
```

```
Repo: alexey-tyurin/ai-agent-mcp
URL: https://github.com/alexey-tyurin/ai-agent-mcp
Category: Content moderation via MCP + OpenAI moderation API
Stars: 4
Recent Activity: Low (25 commits, single contributor)
License: MIT
Primary Language: Python
Maturity: Functional proof-of-concept, explicitly not production-hardened (README admits missing auth/containerization/monitoring)
Claimed Purpose: Routes content through OpenAI's moderation API before LLM response, via Google ADK + MCP (SSE and STDIO transports).
Potential Hermes Relevance: DOM-17 — concrete working MCP-integration pattern for pre-publish moderation, small enough to be genuinely inspectable end-to-end.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real, testable code (a plus per Section 12.1) but explicitly proof-of-concept scale — minimal-worked-example reference, not a deep-audit target given NeMo Guardrails covers the same need with more maturity.
Date Triaged: 2026-08-24
```

---

## Cluster E — Social-Media Operations (DOM-03, 18, 19, 20, 21, 22)

```
Repo: GOAT-AI-lab/GOAT-Storytelling-Agent
URL: https://github.com/GOAT-AI-lab/GOAT-Storytelling-Agent
Category: Narrative/story generation agent
Stars: 158
Forks: 22
Recent Activity: 43 commits, active release blogpost + HF dataset
License: MIT
Primary Language: Python
Maturity: Active, small/focused
Claimed Purpose: Hierarchical multi-stage story generation (book spec -> chapter outline -> scene) preserving continuity via explicit "previous_scene" state passing.
Potential Hermes Relevance: DOM-03 — real inspectable Plan class + hierarchical continuity mechanism, directly analogous to narrative content-series decomposition.
Triage Decision: DEEP AUDIT
Decision Rationale: Small, real architectural separation (planning/init/enhance/generate stages), genuine state-carryover mechanism, not just a demo script.
Date Triaged: 2026-08-24
```

```
Repo: HKUDS/ViMax
URL: https://github.com/HKUDS/ViMax
Category: Agentic video generation / narrative adaptation ("Novel2Video")
Stars: 12.1k
Recent Activity: v1.2.0 released 2026-07-20, active
License: MIT
Primary Language: Python
Maturity: Mature, popular
Claimed Purpose: Adapts long-form fiction into episodic video via narrative compression, character tracking, scene planning; 4-agent roles (Director/Screenwriter/Producer/Video Generator).
Potential Hermes Relevance: DOM-03 (episodic decomposition with continuity) and DOM-20 (multi-modal, character-consistent generation).
Triage Decision: DEEP AUDIT
Decision Rationale: Most mature/popular candidate directly matching both domains' exclusion criteria (real continuity mechanism, not a single-shot demo); real multi-agent role separation.
Date Triaged: 2026-08-24
```

```
Repo: ChrisChen667788/wind-comic
URL: https://github.com/ChrisChen667788/wind-comic
Category: Multi-agent short-form drama/video pipeline
Stars: 451
Forks: 42
Recent Activity: 956 commits, v12.338, active roadmap
License: MIT (three bundled binaries carry copyleft: FFmpeg GPL-3.0, lightningcss MPL-2.0, sharp-libvips LGPL-3.0 — CI-enforced boundary)
Primary Language: TypeScript (strict), Next.js/React
Maturity: Mature, actively engineered (4,346 unit tests)
Claimed Purpose: text -> script -> storyboard -> character-consistent video -> voiceover -> export; 8-agent sequential pipeline with "strict consistency contracts" and an 8-dimension character-DNA + style-bible-frame consistency mechanism.
Potential Hermes Relevance: DOM-20 — best-evidenced multi-modal narrative-continuity candidate found this stage. Also touches DOM-01 (its Director-agent coordination role is directly relevant to multi-agent orchestration — cross-domain note).
Triage Decision: DEEP AUDIT
Decision Rationale: Highest evidence quality found in this pass — real tests, documented consistency-contract handoff mechanism, provider-agnostic design, explicit license-boundary enforcement (good governance signal).
Date Triaged: 2026-08-24
```

```
Repo: Absirkhan/ComicCrafter
URL: https://github.com/Absirkhan/ComicCrafter
Category: Multi-agent comic generation
Stars: 3
Recent Activity: not deeply verified, appears early
License: MIT
Primary Language: Python (FastAPI, ChromaDB, LangChain)
Maturity: Early/niche but functional
Claimed Purpose: 3-agent pipeline (Story/Prompt/Layout) with RAG-based (ChromaDB embeddings) character-consistency memory.
Potential Hermes Relevance: DOM-20 — architecturally distinct consistency mechanism (embedding retrieval vs. wind-comic's DNA-extraction) worth as a comparison pattern.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real working code with a genuinely different consistency mechanism worth comparing, but thin community/maintenance signal and redundant coverage vs. wind-comic/ViMax as primary audit targets.
Date Triaged: 2026-08-24
```

```
Repo: indranilbanerjee/digital-marketing-pro
URL: https://github.com/indranilbanerjee/digital-marketing-pro
Category: Multi-brand marketing/content operating system
Stars: 767
Forks: 129
Recent Activity: v3.31.1 (2026-08-17), monthly iteration cadence, issues actively fixed with regression guards
License: MIT, no telemetry
Primary Language: Python + YAML/JSON + Markdown skill defs (Claude Code plugin architecture)
Maturity: Mature, actively maintained
Claimed Purpose: 163 skills / 24 agents; per-brand state isolation (~/.claude-marketing/<brand-slug>/); 12-Part Engagement Flow (strategy -> competitive analysis -> client validation gate -> channel fan-out -> continuous improvement); multi-stage human-approval gates (typed-approval, voice-match scoring, humanize gate, disk-artifact audit re-derivation).
Potential Hermes Relevance: DOM-19 (primary — strongest content-strategy/multi-brand candidate found this stage); cross-relevant to DOM-18 (embedded competitive-analysis subsystem — currently the best available evidence for DOM-18, see gap note below) and DOM-07 (approval-gate design).
Triage Decision: DEEP AUDIT
Decision Rationale: Best-evidenced candidate in the entire social-media-ops pass — 209 real unit tests, real HTTP connectors, atomic writes, exit-code discipline, an audit layer that catches false "ready" claims. Not a spec collection.
Date Triaged: 2026-08-24
```

```
Repo: ALwrity/ALwrity
URL: https://github.com/ALwrity/ALwrity
Category: Content OS / marketing platform
Stars: 1.1k
Forks: 323
Recent Activity: 1,228 commits, 77 open issues/30 PRs — active but WIP
License: CORRECTED at Stage -2.4 (2026-08-24) — Stage -2.3 record incorrectly stated MIT; direct verification (file search + `gh repo view`, licenseInfo: null) found no LICENSE file exists in the repo at all. Treat as unlicensed/all-rights-reserved until the maintainers add one.
Primary Language: Python (FastAPI/SQLAlchemy backend), TypeScript/React frontend
Maturity: Active WIP, production-security features present (JWT/OAuth2, rate limiting)
Claimed Purpose: "Brand brain" built from website/competitor/channel ingestion; covers strategy, multi-modal generation (blog/YouTube/podcast/LinkedIn), SEO, publishing, analytics.
Potential Hermes Relevance: DOM-19 (secondary/comparison source to digital-marketing-pro — materially different architecture, full web app vs. skill-based CLI plugin); also touches DOM-20/21/22.
Triage Decision: DEEP AUDIT
Decision Rationale: Independent second source for DOM-19 needed to satisfy Stage -2.5's ">=2 independent sources" bar for any strong pattern extracted from this cluster.
Date Triaged: 2026-08-24
```

```
Repo: cofoundy/brand-skills
URL: https://github.com/cofoundy/brand-skills
Category: Brand identity generation skills
License: MIT (stated)
Maturity: unknown — not inspected beyond description snippet
Claimed Purpose: Turns an idea into name/identity/voice/brand-book via agent skills.
Potential Hermes Relevance: DOM-19 — scope is one-time brand definition, not ongoing strategy/planning.
Triage Decision: REFERENCE ONLY
Decision Rationale: Narrower scope than the domain's core need; Evidence Quality capped Low — description-level only, not fetched.
Date Triaged: 2026-08-24
```

```
Repo: gitroomhq/postiz-app
URL: https://github.com/gitroomhq/postiz-app
Category: Social media scheduling/publishing platform
Stars: 35.1k
Forks: 6.6k
Recent Activity: 2,838 commits, active, CI/CD present
License: AGPL-3.0
Primary Language: TypeScript (Next.js frontend, NestJS backend), Temporal for job processing
Maturity: Mature, largest-scale publishing candidate found
Claimed Purpose: Multi-platform scheduling/publishing with OAuth-only credential handling (no key storage/proxying).
Potential Hermes Relevance: DOM-21 (primary — largest, most production-proven candidate).
Triage Decision: DEEP AUDIT
Decision Rationale: Use of Temporal strongly implies durable-execution/retry semantics by construction, but a README-level fetch could NOT confirm specific retry/rollback/partial-failure code paths — per Section 12.1, must be verified at code level in Stage -2.4, flagged explicitly as an open evidence gap, not assumed.
Date Triaged: 2026-08-24
```

```
Repo: brightbeanxyz/brightbean-studio
URL: https://github.com/brightbeanxyz/brightbean-studio
Category: Self-hostable social media management platform
Stars: 2.2k
Forks: 453
Recent Activity: 529 commits, 18 open issues/8 PRs, moderate ongoing maintenance
License: AGPL-3.0
Primary Language: Python/Django, PostgreSQL, django-background-tasks (no Redis dependency)
Maturity: Production-ready per own docs (multiple deploy targets, RBAC, pre-commit + pytest/coverage)
Claimed Purpose: 11-platform publishing with automatic retries, per-account rate-limit tracking, 90-day publish audit log, tiered REST API rate limits with Retry-After headers, configurable multi-stage approval workflows.
Potential Hermes Relevance: DOM-21 — arguably stronger direct evidence than Postiz specifically on the reliability/rollback dimension named in the domain's exclusion criteria.
Triage Decision: DEEP AUDIT
Decision Rationale: Concrete, specific reliability features stated (not just implied by tech choice); smaller/more auditable codebase than Postiz; good complementary second source.
Date Triaged: 2026-08-24
```

```
Repo: msitarzewski/agency-agents
URL: https://github.com/msitarzewski/agency-agents
Category: Agent-persona/prompt collection (230+ personas)
Stars: 148k
Forks: 23.9k
Recent Activity: 395 commits, 61 open issues/89 PRs
License: MIT
Primary Language: Markdown (prompt/persona defs) + shell installers
Maturity: Mature, huge community, but NOT code — persona/prompt definitions only
Claimed Purpose: Includes an "X/Twitter Intelligence Analyst" persona for social listening/competitor tracking/audience intelligence.
Potential Hermes Relevance: DOM-18/DOM-19 — role-definition and process framing, not an executable pipeline.
Triage Decision: REFERENCE ONLY
Decision Rationale: No inspectable pipeline logic/code — pure prompt definitions. High popularity is a signal, explicitly not proof of architectural quality (Section 12.1). Useful only for framing how to define a competitive-intelligence agent's role/deliverables.
Date Triaged: 2026-08-24
```

```
Repo: langchain-ai/social-media-agent
URL: https://github.com/langchain-ai/social-media-agent
Category: HITL social-post sourcing/curation/scheduling agent
License: not captured this pass — verify at audit
Primary Language: TypeScript/Python (LangGraph)
Maturity: Active, official LangChain project
Claimed Purpose: Takes a URL, generates a Twitter/LinkedIn post from its content, uses a human-in-the-loop flow to handle platform authentication and let the user edit/accept/reject the generated post before it goes out.
Potential Hermes Relevance: DOM-07 (approval-gate mechanics for the exact generate-then-approve-then-publish shape Hermes needs), DOM-21 (publishing mechanics), DOM-19/DOM-20 (content-generation-from-source-material framing) — an unusually close structural analog to Hermes' entire content pipeline (source material -> draft -> human approval -> publish).
Triage Decision: DEEP AUDIT
Decision Rationale: Surfaced by the Cluster D discovery pass as out-of-slice but clearly relevant; independently verified to exist via direct repo check (not taken on the discovering fork's description alone, per Section 12.1). Official LangChain project, real HITL flow — closest single-repo analog to Hermes' full content-generation-agent shape found across all six discovery passes.
Date Triaged: 2026-08-24
```

---

## Cluster F — Scaling & Self-Maintenance (DOM-24, 25)

```
Repo: NimbleCoAI/hermes-agent (fork, "hermes-agent-mt")
URL: https://github.com/NimbleCoAI/hermes-agent
Category: Multi-tenant fork of REPO-001
Recent Activity: active — "automated weekly upstream sync," recently rebased against ~410 upstream commits
License: inherits hermes-agent's (MIT, per REPO-001's own README) — unconfirmed whether the fork's own patches carry a different license, verify at audit
Primary Language: same as hermes-agent (Python)
Maturity: active, production-claimed (8 multi-tenant agents running for months across Signal/Mattermost adapters, per the fork's associated issue — see SRC entry)
Claimed Purpose: Adds `context_id`-based memory scoping, a `memory:scope` hook, admin-gated approval commands, and denial-feedback-with-pattern-context on top of stock hermes-agent, specifically to solve multi-tenant isolation.
Potential Hermes Relevance: DOM-24 (primary — a real production fork solving DOM-24's exact research question directly on REPO-001 itself), DOM-11 (touches memory write paths), DOM-08 (admin-gating of destructive commands).
Triage Decision: DEEP AUDIT
Decision Rationale: This is not a generic comparison pattern — it is a real third-party fork solving DOM-24's exact research question on the known base architecture itself, giving directly falsifiable, code-level evidence of what hermes-agent lacks natively and one concrete way to fix it. IMPORTANT: independently verified to exist via `gh repo view` by the primary Phase -2 session (2026-08-24) after a discovery-pass fork surfaced it — confirmed real, not a hallucinated finding, given this project's prior burn history with fabricated hermes-agent claims (see `research-domains.md` Known Base Architecture section). Auditing this fork meaningfully requires first auditing upstream REPO-001 — sequence Stage -2.4 accordingly (REPO-001 first, this second).
Date Triaged: 2026-08-24
```

```
Repo: NimbleCoAI/hermes-swarm-map
URL: https://github.com/NimbleCoAI/hermes-swarm-map
Category: Multi-tenant orchestration/admin control plane for agent runtimes
Maturity: active, "commons, public goods project" per its own README
License: not confirmed this pass — verify at audit
Primary Language: not confirmed this pass
Claimed Purpose: "Multiplayer admin and orchestrator platform for heterogeneous agent runtimes" — one dashboard for Hermes agents (container-per-agent) and Letta agents (memory-first, shared server); multi-tenant security, group approval, and audit from one control plane. Self-described as not yet symmetrical across runtimes (Hermes support is the mature path).
Potential Hermes Relevance: DOM-24 — this is the actual "commons product" referenced in the GitHub issue that first surfaced this whole cluster of findings (see SRC entry for NousResearch/hermes-agent#34352); a real, purpose-built control-plane answer to multi-tenant Hermes deployment, built by operators who hit the exact gap DOM-24 is researching.
Triage Decision: DEEP AUDIT
Decision Rationale: Independently discovered and verified directly by the primary Phase -2 session (2026-08-24), not the discovery-pass fork (which had conflated this project's name with the hermes-agent fork above) — confirmed real via direct repo fetch. Directly load-bearing for DOM-24 given its origin (built specifically to solve the gap documented in REPO-001's own issue tracker).
Date Triaged: 2026-08-24
```

```
Repo: tee-labs/hermes-multi-tenant
URL: https://github.com/tee-labs/hermes-multi-tenant
Category: Multi-tenant orchestration/deployment CLI (companion tool, not a fork of core)
Stars: 2
Forks: 0
Recent Activity: 35 commits on main
License: MIT
Primary Language: TypeScript
Maturity: Early-stage but structured (PRD/DESIGN/AGENTS docs, "104+ tests across 9 modules" per own claim)
Claimed Purpose: Kubernetes-based lifecycle management (create/delete/list/infra/templates) for deploying multiple Hermes Agent instances, with an NFS-backed persistent storage manager and SQLite tenant-state store.
Potential Hermes Relevance: DOM-24 (primary — literally "add a new page without a from-scratch project" as ops tooling), DOM-13 (deployment/reliability adjacency).
Triage Decision: REFERENCE ONLY
Decision Rationale: Real inspectable code, but solves the deployment/ops layer of multi-tenancy (K8s provisioning), not the in-agent isolation problem the NimbleCoAI fork addresses — complementary, lower adoption signal than the fork itself. Independently verified to exist via `gh repo view`.
Date Triaged: 2026-08-24
```

```
Repo: yerdaulet-damir/langgraph-sales-agent
URL: https://github.com/yerdaulet-damir/langgraph-sales-agent
Category: Multi-tenant agent framework (config-driven, LangGraph-based)
Stars: 29
Forks: 5
Recent Activity: 6 total commits, early-stage
License: MIT
Primary Language: Python
Maturity: Experimental
Claimed Purpose: "Drop a YAML, get a bot" — each tenant lives in /tenants/{name}/ with config.yaml (personality, LLM provider/model, rules) + products.json; new tenant = config-only, no code change.
Potential Hermes Relevance: DOM-24 (primary) — direct comparison baseline for "templated config, no per-instance project" pattern, independent of the hermes-agent codebase.
Triage Decision: REFERENCE ONLY
Decision Rationale: Clean, inspectable config-only-tenanting pattern, but the repo's own docs flag in-memory-only conversation state as production-unsafe, and tenant data isolation is claimed but not visibly enforced in code — a README-level claim not to take at face value (Section 12.1). Useful as a pattern reference, not strong enough alone for deep audit.
Date Triaged: 2026-08-24
```

```
Repo: unicodeveloper/tech-scouting-agent
URL: https://github.com/unicodeveloper/tech-scouting-agent
Category: Autonomous technology-scouting agent
Recent Activity: 1 commit — newly created
License: MIT
Primary Language: TypeScript
Maturity: Experimental/nascent
Claimed Purpose: Tracks patent-filing velocity, academic-citation acceleration, and government grant flow as three converging signals in a chosen tech domain, synthesizing a cited "momentum dossier" via the Valyu DeepResearch API; exposes real methods (patentVelocity(), citationAcceleration(), grantFlow()), not just prose.
Potential Hermes Relevance: DOM-25 (primary) — closest direct structural match found: multi-signal external monitoring -> synthesized, cited recommendation output, passing DOM-25's "not just a feed reader" exclusion bar.
Triage Decision: REFERENCE ONLY
Decision Rationale: Real, inspectable, non-trivial mechanism, but single-commit maturity, third-party paid API dependency (Valyu), no track record — good pattern reference for the "signal triangulation -> dossier" mechanism, not mature enough for deep audit.
Date Triaged: 2026-08-24
```

---

## Rejected Candidates (Triage Decision: REJECT)

Full Section 9.7 records for the substantively-inspected rejections below live in
`rejected-candidates.md` (REJ-003 through REJ-008). Repos excluded purely by a
domain's own Exclusion Criteria without individual inspection (e.g. generic IAM
tools for DOM-08, large-scale workflow engines for DOM-13, academic-only papers
with no inspectable implementation) are not given individual records here —
see each domain's `research-domains.md` Exclusion Criteria and the discovery
forks' "deferred, not rejected" notes for that list.

```
Repo: Mattbusel/llm-budget
URL: https://github.com/Mattbusel/llm-budget
Category: LLM cost governance primitives (Rust crate)
Stars: 3
Recent Activity: Minimal (5 commits, solo author, no releases)
License: MIT
Primary Language: Rust
Maturity: Early prototype
Claimed Purpose: Hard budget enforcement (BudgetLedger, FleetGovernor, CostEvent) across agent fleets.
Potential Hermes Relevance: DOM-16 — real code exists, but evidence too thin for reliance.
Triage Decision: REJECT
Decision Rationale: Section 10.4 discipline — insufficient evidence maturity (3 stars, single contributor, no production signal); Section 12.1 forbids treating a recent/thin repo as production-proven. Concept (fleet-wide ledger) already better evidenced by AgentBudget/LiteLLM.
Date Triaged: 2026-08-24
```

```
Repo: anomalyco/opencode (Issue #13952 — proposal only, not shipped)
URL: https://github.com/anomalyco/opencode/issues/13952
Category: Agent audit-log design proposal
Claimed Purpose: Hash-chained (H(n)=SHA256(Action_n+H(n-1))) append-only agent-action log, runtime-appends-only/tools-cannot-modify, verify-audit integrity command.
Potential Hermes Relevance: DOM-11 — directly on-point mechanism (agent-action-specific, tamper-evident, append-only), but status is proposal-only, closed, not merged/implemented anywhere inspectable.
Triage Decision: REJECT (as a repo candidate — no shipped code exists to audit)
Decision Rationale: Section 12.2 evidence order — an unmerged proposal ranks below even docs/examples. The design idea (hash-chained append-only log) is preserved for Stage -2.5 pattern extraction with this issue cited as origin; the repo itself gets no further triage.
Date Triaged: 2026-08-24
```

```
Repo: dakshjain-1616/Agent-Memory-Compressor
URL: https://github.com/dakshjain-1616/Agent-Memory-Compressor
Category: Context compaction for long-running agents
Recent Activity: not confirmed — small/individual repo, no strong maintenance signal found
Claimed Purpose: Summarization + embedding-retrieval compaction with tunable ratios, importance-scoring, forgetting-curve trigger.
Potential Hermes Relevance: DOM-12 — directly on-topic mechanism.
Triage Decision: REJECT
Decision Rationale: Section 12.1 — no evidence of maintenance/adoption/testing beyond its own README; single-author repo, no corroborating signal. Graphiti covers the same need with materially stronger evidence.
Date Triaged: 2026-08-24
```

```
Repo: handrew/agentic_gpt
URL: https://github.com/handrew/agentic_gpt
Category: Toy agent library
Claimed Purpose: Thin ask_user_fn callback hook with no visible trigger logic for when to invoke it.
Potential Hermes Relevance: DOM-09 — name-match only.
Triage Decision: REJECT
Decision Rationale: No trigger logic for the actual DOM-09 research question (when to ask) — just an escape hatch, not a clarification mechanism. Dated, minimal activity.
Date Triaged: 2026-08-24
```

```
Repo: open-gitagent/gitagent
URL: https://github.com/open-gitagent/gitagent
Category: Git-native agent config framework
Stars: 658
Forks: 123
Recent Activity: active, real src/, rust/, examples, tests
License: MIT
Primary Language: TypeScript
Claimed Purpose: Version-controlled agent identity/rules/memory/tools as files in a git repo; MCP client with auto tool-discovery; plugin system.
Potential Hermes Relevance: DOM-24 — evaluated specifically for multi-tenancy comparison value.
Triage Decision: REJECT (for DOM-24 purposes only)
Decision Rationale: Repo's own FAQ explicitly states "no multi-tenant support" — direct disqualification for DOM-24. Its MCP auto-discovery/plugin-manifest pattern may be worth revisiting later for DOM-04/DOM-06, out of scope for this record.
Date Triaged: 2026-08-24
```

```
Repo: younis-ali/market-research-agent
URL: https://github.com/younis-ali/market-research-agent
Category: Competitor analysis app
Stars: 5
Recent Activity: 5 commits total — minimal
License: MIT
Primary Language: Python/FastAPI
Maturity: Early-stage / proof-of-concept
Claimed Purpose: LLM-generates competitor suggestions from a static, pre-populated PostgreSQL sector/address table.
Potential Hermes Relevance: DOM-18.
Triage Decision: REJECT
Decision Rationale: "Synthesis" is generation from a static seed table, not real market/competitive data gathering — fails DOM-18's exclusion criteria in substance despite superficially having a synthesis step. Minimal commit history, no real evidence of working research capability.
Date Triaged: 2026-08-24
```

---

## Coverage Gaps Confirmed This Stage

Per the saturation rule (CLAUDE.md / Section 21.1), the following are logged as
genuine, confirmed coverage gaps rather than silently left unaddressed:

- **DOM-09** (ambiguity detection & clarification-seeking behavior) — no dedicated
  repo found in three query passes; only academic papers and one rejected thin
  callback-hook (`handrew/agentic_gpt`). `ashutoshrana/confidence-escalation`
  (REPO — Cluster B) is the closest partial fit but is framed around model
  confidence, not task ambiguity — a related, not identical, signal. Consistent
  with Stage -2.2's finding of zero skill-gallery coverage for the same need.
- **DOM-22** (analytics & experimentation feedback loops) — two full alternate-query
  passes found zero materially relevant inspectable-code candidates; only vendor
  blogs and academic RL/recsys papers with no social-content linkage. The concept
  ("closed-loop analytics") is discussed everywhere, implemented nowhere
  inspectable that this pass could find.
- **DOM-18** (competitive & audience research automation) — **RESOLVED at Stage
  -2.4, no longer a gap.** Stage -2.3 flagged this as thin (only an
  embedded-subsystem candidate, unverified). Stage -2.4's deep audit of
  `indranilbanerjee/digital-marketing-pro` directly read its `competitive-intel`
  agent code (`competitor-scraper.py`/`competitor-tracker.py`/`narrative-mapper.py`
  — 222/537/759 lines, real, non-trivial) and confirmed genuine HTTP fetch+parse
  research-synthesis (robots.txt-respecting, source/date/confidence-tagged
  output), not a static-data wrapper — see
  `phase-m2/repo-audits/indranilbanerjee-digital-marketing-pro.md` for detail.
  DOM-18 now has real, code-verified coverage.

## Cross-Cluster Note

`ChrisChen667788/wind-comic`'s Director-agent coordination role (Cluster E) is
directly relevant to DOM-01 (Cluster A) — flagged by the discovering fork in case
the Cluster A pass had not surfaced an equivalent independently; recorded here for
visibility, not yet reconciled into a single cross-referenced finding.
