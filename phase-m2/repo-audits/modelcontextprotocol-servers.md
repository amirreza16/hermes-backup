# Deep Audit: modelcontextprotocol/servers

Stage -2.4 (Deep Repository Audit). Schema: Master Plan Section 9.3 (Dimensions A-J).
Repo-catalog record: REPO-006. Relevant DOM ID: DOM-06 (primary source for "what MCP
actually is," per Section 12.2 evidence order — official protocol steward).

Source: `git clone --depth 1 https://github.com/modelcontextprotocol/servers.git`, inspected
2026-08-24. Dual/transitional license (see Dimension J).

## A — Architecture
Seven reference server implementations confirmed present under `src/`: `everything`, `fetch`,
`filesystem`, `git`, `memory`, `sequentialthinking`, `time`. Each is a standalone MCP server
demonstrating one capability area — this is a collection of worked examples, not a single
unified framework. TypeScript and Python both represented (per Stage -2.3 triage; not
independently re-verified language-split this pass, but confirmed via `package.json` +
`tsconfig.json` at the root that a Node/TS toolchain governs at least part of the repo).
Verdict: Strong for "reference implementations exist and are real, inspectable code" — this
is the correct read of what this repo is; Not Applicable for "is there one architecture" —
by design, there are seven independent small architectures, one per server.

## B — Agent design
Not applicable — this repo provides MCP *servers* (tool-providing endpoints), not agents.
Agent-side design questions (DOM-01/DOM-02) are out of this repo's scope by construction.
Verdict: Not Applicable.

## C — Context & memory
The `memory` server specifically is directly relevant if Hermes ever wants a reference
implementation of an MCP-exposed memory store — not deeply inspected this pass beyond
confirming the directory exists (UNKNOWN on its internal storage mechanism).
Verdict: Not assessed beyond confirming existence.

## D — Reliability
Confirmed, directly from the repo's own README (self-reported, high-confidence since it is
the maintainers' own explicit disclaimer, not a marketing claim to be skeptical of): these are
described as **reference/educational examples**, explicitly **not production-ready** —
"Developers should evaluate their own security requirements and implement appropriate
safeguards based on their specific threat model." This is an important, load-bearing finding
for DOM-06: this repo cannot be treated as evidence of a production-grade error-handling/
blast-radius-containment pattern — that question is better answered by REPO-008
(`InfinitiBit/graphbit`) or REPO-007 (`MicroMCP`), both already triaged as REFERENCE ONLY for
exactly this reason.
Verdict: Weak by design (self-disclosed) — not a criticism of code quality, but a scope fact:
do not cite this repo for DOM-06's reliability/robustness sub-question.

## E — Human control
Not applicable/not found — servers expose tools, they don't implement approval-gate logic
themselves (that would be the calling agent's responsibility).
Verdict: Not Applicable.

## F — Evaluation
Not found — out of scope for a reference-server collection.
Verdict: Not Applicable.

## G — Operations
Not the focus — no cost/routing logic (these are tool servers, not agents/routers).
Verdict: Not Applicable.

## H — Reusability
Each server is small and self-contained by design (the explicit purpose is "here's how you'd
build your own MCP server for X capability") — high reusability as *reference material to
read and adapt*, low reusability as *production infrastructure to import wholesale* (per
Dimension D's finding).
Verdict: Strong as reference material; Weak as drop-in production infrastructure — both
verdicts follow directly from the same, single, self-disclosed fact.

## I — Evidence
Docs vs. code: no disagreement found — the README's own "not production-ready, educational
examples" framing accurately describes what was found in the code (small, focused, clearly
didactic implementations). This is a case where the source is unusually honest about its own
limitations, which the Stage -2.3 triage record already flagged ("official reference —
explicitly not production-hardened") — this audit confirms that self-assessment was accurate,
not overstated caution or false modesty.
Verdict: Strong — docs and code agree, and agree honestly.

## J — License
Confirmed from `LICENSE` file text directly (FACT): the repository is **mid-transition** from
MIT to Apache-2.0. New code and specification contributions are Apache-2.0; documentation
(excluding specs) is CC-BY-4.0; contributions from authors who have not yet consented to
relicensing remain MIT. This means **different files in this repo may carry different
licenses** depending on contribution history — a real nuance a README-only pass would likely
miss or oversimplify as "just Apache 2.0" or "just MIT."
Verdict: Moderate — permissive either way (MIT and Apache-2.0 are both permissive), but the
per-file license provenance requires actual checking before reusing any specific file
verbatim, not a blanket assumption.

---

## Evidence Summary (Stage -2.4 exit criterion)
No docs-vs-code contradiction found — this repo's own self-disclosure (not production-ready,
educational) matches what real inspection found (small, clean, clearly didactic
implementations). The one genuinely non-obvious finding from actual file inspection (as
opposed to a README skim) is the split MIT/Apache-2.0/CC-BY-4.0 licensing depending on
contribution date and consent status (Dimension J) — a README-only pass would very likely
have missed or flattened this nuance, which is exactly the kind of gap Section 8 requires this
stage to surface.

## Stage -2.3 Triage Reassessment
No change — DEEP AUDIT was correctly scoped as "necessary baseline before judging any
third-party MCP claim," and this pass confirms that framing was accurate: this repo is best
used as ground-truth reference material and a licensing-provenance check, not as a
reliability-pattern source (that role correctly belongs to the REFERENCE ONLY candidates
already identified at Stage -2.3).
