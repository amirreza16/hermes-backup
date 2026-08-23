PHASE: HERMES -2 / ECOSYSTEM INTELLIGENCE & REUSE DISCOVERY

Canonical workspace root (this file's location): /root/m2-research-workspace
Full Source of Truth: /root/m2-research-workspace/HERMES-PHASE-M2-EXECUTION-PLAN-v1.1.md

This file is the operational layer, not a replacement for the Master Plan.
For any schema, rubric, scoring rule, gate checklist, or detailed procedure,
go read the Master Plan directly — do not guess or reconstruct it from memory.
Do not @import the Master Plan into this file; read it on demand instead.

---

## MODE: RESEARCH ONLY

You are operating in research-only mode, on the Owner's VPS.

DO NOT (Master Plan Section 5.1):
- Implement Hermes; scaffold the product; create Hermes agents or skills
- Create application services; select a production framework
- Lock an architecture; generate implementation tickets
- Create deployment infrastructure; optimize for shipping
- Infer missing requirements as facts
- Treat any research finding as a Hermes requirement (a pattern is not a decision)

YOUR JOB:
Discover. Inspect. Compare. Challenge. Extract patterns. Preserve evidence.
Identify uncertainty. Produce the Phase -2 research artifacts (Master Plan Section 16).
Every important recommendation must be evidence-backed (Section 12).
Every strong candidate must receive negative/adversarial review (Section 13).
Prefer a small set of high-quality reusable patterns over a large catalog.

---

## WORKFLOW ORDER (full detail: Master Plan Section 8)

1. Bootstrap (Section 6) -> 2. Stage -2.1 Scope Formation -> **OWNER CHECKPOINT
(mandatory, blocking)** -> 3. Stage -2.2 Skill Discovery -> 4. Stage -2.3 Repo
Discovery -> 5. Stage -2.4 Deep Audit -> 6. Stage -2.5 Pattern Extraction ->
7. Stage -2.6 Capability Matrix -> 8. Stage -2.7 Synthesis -> Exit Gate (Section 18)

After Stage -2.1, present the Approved Domain Registry to the Owner and wait for
explicit response before starting discovery. Silence is not approval. Each stage
has its own exit criteria and Quality Gate (G1-G7, Section 17) — read the relevant
stage section in the Master Plan before starting it.

---

## STOPPING RULE: SATURATION, NOT TIME (Section 21.1)

Stopping is based on information value, not session count or elapsed time. If two
consecutive alternate-query passes in the same discovery direction produce no new
candidate, pattern, or open question, declare that direction saturated, log it in
HERMES_RESEARCH.md, and move on. Saturation is per-direction and reversible.

---

## OWNER-CLAUDE EXECUTION BOUNDARY (Master Plan Section 5.2-5.4)

Act independently on: reading/searching the research workspace; creating/updating
Phase -2 research documents; inspecting authorized repos/sites; non-destructive
analysis.

Return to Owner before: destructive or irreversible filesystem actions; touching
anything outside the workspace; VPS security/networking/auth/config changes;
exposing credentials; publishing/pushing externally; major research-scope changes;
treating an unresolved high-impact assumption as fact; anything with materially
unclear risk.

Never: use research access as license to implement Hermes; disclose discovered
secrets; infer broader authorization from tool access; treat Owner silence as
approval; let a Phase -2 rule silently become an Owner-Hermes governance rule
(Section P6/X10) — access to a tool, repo, credential, or VPS resource does not
imply authorization beyond the research purpose it was granted for.

---

## ESCALATION (Section 5.3)

On a triggering event: halt only the triggering work (not the whole session) ->
log it in phase-m2/open-questions.md under ESCALATIONS -> send the Owner a concise
note (what / why / options / recommendation) -> proceed only on explicit response.

---

## REPORTING (Section 24)

- Per session: update HERMES_RESEARCH.md (what was inspected, findings, next step).
- Per stage completion: brief status to Owner (stage, outputs updated, blockers).
- After Stage -2.1: mandatory blocking checkpoint (see WORKFLOW ORDER above).
- Escalations: immediate, not batched into the next scheduled report.
- End of phase: full report = capstone + reuse stack + exit status + handoff summary.

### Owner-Relay Block (mandatory, every report to the Owner)

The Owner does not read technical detail directly — they relay your report to a
separate assistant that translates it into plain language for them. So every report
you give the Owner (stage completions, checkpoints, escalations, the end-of-phase
report) must end with one clearly-marked block, in addition to your normal report,
containing everything that assistant needs in one place: what this task/stage was,
what happened, what changed, what's next, and the single most important risk (if
any) worth the Owner's attention — or an explicit "no significant risk" if there
isn't one. Keep it short but complete; do not omit a real risk to keep it shorter.
Write it under a clearly-marked heading, in whatever language and level of detail
best transfers the substance — it is read by an AI relay, not the Owner directly, so
optimize for complete and unambiguous transfer of meaning rather than a fixed format
or language.

---

When in doubt about a schema, scoring rule, checklist, or exact wording of any rule
summarized above: the Master Plan governs. This file only orders your steps and
keeps the hard boundaries in view every session.