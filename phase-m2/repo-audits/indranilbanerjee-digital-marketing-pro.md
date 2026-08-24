# Deep Audit: indranilbanerjee/digital-marketing-pro

Schema: Master Plan Section 9.3 (Dimensions A-J). Stage -2.4.
Repo-catalog record: REPO-033 (Cluster E). Relevant domains: DOM-19 (primary),
DOM-18 (secondary — this audit's primary assignment was to resolve whether the
Stage -2.3 "thin coverage" flag on DOM-18 is accurate), DOM-04 (skill-
architecture structure).
Audited: 2026-08-24. Method: `git clone --depth 1`, full read of
`agents/competitive-intel.md` (131 lines), direct inspection of
`scripts/competitor-scraper.py` (222 lines, partial read), `scripts/competitor-
tracker.py` and `scripts/narrative-mapper.py` (existence/size confirmed, not
fully read), `scripts/_common.py` (brand-isolation path verification), test
count verification, `gh repo view`.

## A — Architecture
Claude Code plugin architecture (`plugin.json`, `plugin.yaml`, `hooks/`,
`commands/`), not a standalone application — 24 agent definitions
(`agents/*.md`, YAML-frontmatter + system-prompt format) plus 163 SKILL.md
files (`find . -iname SKILL.md` = 163, confirming the catalog's count exactly)
under `skills/`, each a scoped capability invoked by the agents. Real backing
Python scripts under `scripts/` (confirmed to exist, non-trivial size — see
Dimension D) — this is not a "prompts-only" plugin; agents call real scripts
for scraping, storage, and computation.
Verdict: Strong — a real, substantial multi-agent plugin architecture with a
verified count of skills and confirmed backing implementation code, not just
prompt files.

## B — Agent design
`agents/competitive-intel.md`, read in full, is a genuinely sophisticated
agent contract: explicit `mode` input (`snapshot` vs `monitoring`, with
fallback inference logic if unspecified), 10 numbered "Behavior Rules" (not
vague guidance — specific, checkable rules: public-data-only sourcing,
mandatory source+date+confidence-level tagging per claim, confirmed-vs-inferred
labeling discipline, brand-isolated storage, baseline/change-detection logic
with explicit default alert thresholds, e.g. "pricing change (any), new
landing page (immediate), ad-creative volume spike (>30% week-over-week)").
An explicit "Cross-Agent Collaboration" section defines a real handoff
contract to 8 other named agents (marketing-strategist, media-buyer,
content-creator, seo-specialist, crm-manager, cro-specialist, social-media-
manager, brand-guardian, intelligence-curator) — this is a real inter-agent
contract design, directly relevant to DOM-02 as a comparison example, though
DOM-02 was not this audit's assignment.
Verdict: Strong — one of the more rigorous single-agent contract designs
found across all of Stage -2.3/-2.4's candidates so far.

## C — Context & memory
Agent explicitly loads `profile.json`, `competitors.json`, `insights.json`
always, and conditionally loads `competitors/` (baselines/scan history),
`narrative/`, `campaigns/`, `audiences.json` — a real, structured, tiered
memory-loading discipline (always-load vs. load-when-relevant), not a single
flat context dump. `campaign-tracker.py --action save-insight` is the
documented persistence path for competitive findings (existence of the script
confirmed; its actual persistence mechanism, e.g. append-only vs. overwrite,
was NOT independently verified this pass — UNKNOWN, flag for DOM-11 relevance
if this repo is ever cross-referenced there).
Verdict: Moderate-Strong — well-designed tiered memory-loading contract;
underlying storage mechanism's append-only/overwrite behavior unverified.

## D — Reliability (DOM-18's core question: is this real research-synthesis,
## or a raw data dump / thin wrapper?)
**CONFIRMED, read directly:** `scripts/competitor-scraper.py` is real,
working scraping code — not an LLM-only "pretend to browse" mechanism. It
uses `requests` + `BeautifulSoup4` for actual HTTP fetch and HTML parsing,
rotates a real list of realistic User-Agent strings, and — per its own
docstring — "respects robots.txt" and applies rate limiting (both claims
consistent with the visible imports of `time`/`random` for jitter, though the
robots.txt-parsing logic itself was not traced to its specific implementation
line this pass). Critically, it **fails gracefully and transparently** rather
than silently degrading: if `requests` or `beautifulsoup4` are not installed,
it emits a structured JSON error (`{"fallback": true, "error":
"requests_not_installed", ...}`) with an explicit recommendation to install
dependencies or fall back to manual analysis — this is honest failure
signaling, not a mechanism that pretends to have scraped when it did not.
`scripts/competitor-tracker.py` (537 lines) and `scripts/narrative-mapper.py`
(759 lines) both exist as substantial real files (not stubs — sizes confirmed
via `wc -l`), consistent with the agent contract's description of baseline/
change-detection and narrative-territory-mapping mechanisms.
**This directly answers the DOM-18 open question flagged in Stage -2.3's
`repo-catalog.md`:** the "synthesis" step here is NOT LLM generation from a
static/pre-populated dataset (contrast with the REJECTED `younis-ali/market-
research-agent`, REJ-008) — it is a real fetch-then-structure pipeline feeding
an LLM agent with explicit source/date/confidence-tagging discipline layered
on top. **DOM-18 is adequately covered by this repo's embedded subsystem —
this is not thin/marginal coverage as flagged in Stage -2.3; it should be
promoted to full DOM-18 coverage status, not left as an open question.**
Verdict: Strong.

## E — Human control
Not the focus of this audit pass; the agent contract's "Behavior Rules" are
self-enforced by the LLM agent (prompt-level), not structurally enforced by
code — no code-level gate preventing the agent from ignoring rule 6 ("never
mix data across brands") was located this pass. This is the same class of
prompt-level-vs-structural-enforcement distinction flagged as a general risk
by `microsoft/agent-governance-toolkit` (REPO-010, audited separately) —
worth cross-referencing at Stage -2.5: this repo's rules are well-designed but
prompt-level, not code-enforced.
Verdict: Moderate — well-specified behavioral rules, enforcement mechanism is
prompt-level (LLM self-compliance) rather than structural, based on files
inspected this pass.

## F — Evaluation
**CONFIRMED, corrects the Stage -2.3 catalog's own claim (in the repo's
favor):** the catalog record cited "209 real unit tests." Direct count via
`grep -rhoE "^\s*def test_" tests` returns **402** test functions across 34
test files — the actual repo has roughly double the claimed test count. This
is a rare case of a Stage -2.3 candidate UNDERSTATING its own evidence rather
than overstating it (contrast with GOAT-Storytelling-Agent's overstated
activity, audited separately). Test files include
`test_skill_script_contracts.py` and `test_skills_index.py`, indicating the
163-skill catalog is itself under automated consistency testing, not just
manually maintained.
Verdict: Strong.

## G — Operations
`scripts/_common.py` (confirmed, read directly) implements the real
brand-isolation path resolution logic: `~/.claude-marketing/brands/{slug}/...`
with a documented fallback chain (checks for an override directory, then
falls back to `~/.claude-marketing`). This is confirmed as real, working path
logic, not just a documented convention — `audience-simulator.py` and
`auto-save-insight.py` both reference the same path scheme independently,
indicating a consistently-applied convention across scripts, not an isolated
one-off.
Verdict: Strong.

## H — Reusability
Tightly coupled to the Claude Code plugin/skill format (`SKILL.md`,
`plugin.json`, `${CLAUDE_PLUGIN_ROOT}` path convention) and to Python script
invocation via CLI args — not framework-agnostic, but the *pattern* (agent
contract with numbered behavior rules + brand-isolated storage path + tiered
memory loading + explicit cross-agent handoff contract) is clearly
describable independent of the Claude Code plugin mechanics specifically.
Verdict: Moderate.

## I — Evidence
**CONFIRMED via `gh repo view`:** 767 stars, 129 forks, MIT license, pushed
2026-08-17 (about a week before this audit — genuinely active, consistent
with the Stage -2.3 catalog's "mature, actively maintained" characterization).
0 open issues (same ambiguous signal as wind-comic — not independently
resolved). **Both material claims re-checked this pass (163 skills, unit test
count) held up or exceeded the catalog's figures** — no overstated claim
found in this repo specifically.
Verdict: Strong.

## J — License
**CONFIRMED:** MIT License, Copyright (c) 2026 Digital Marketing Pro. No
telemetry claim (per Stage -2.3 catalog) not independently re-verified this
pass (would require inspecting all outbound network calls across the
codebase — out of scope for this audit's time budget; flagged UNKNOWN, not
confirmed or refuted).
Verdict: Strong (license itself); the no-telemetry claim remains an
unverified UNKNOWN.

---

## Evidence Section (Section 9.3 exit requirement — docs vs. code disagreements)

1. **Test count**: catalog claimed "209 real unit tests"; direct count found
   402 — an understatement in the repo's favor, not an inflation. Corrected
   here.
2. **DOM-18 coverage status**: Stage -2.3 flagged this repo's competitive-
   analysis subsystem as possibly-thin, "open question for Stage -2.5/-2.6."
   This audit resolves that question: the subsystem is real, working,
   non-trivial (759+537+222 lines of real scraping/tracking/mapping code
   behind a well-specified agent contract) — **recommend closing the DOM-18
   coverage gap flagged in `repo-catalog.md`, not carrying it forward as
   unresolved.**
3. No other material doc-vs-code disagreement found — the agent contract's
   description of its own behavior matches the backing scripts' actual
   capabilities.

## Summary for Stage -2.5 Pattern Extraction

Three things worth carrying forward distinctly: (1) the **numbered, checkable
behavior-rules format** (vs. vague prose guidance) as a DOM-05 comparison
example; (2) the **brand-isolated storage path convention**
(`~/.claude-marketing/brands/{slug}/...`, consistently applied across
independent scripts) as a lightweight DOM-24 pattern, notably simpler than
`hermes-agent`'s profile-multiplexing mechanism (see REPO-001 audit) — worth
comparing the two approaches directly in Stage -2.5; (3) the
**snapshot-vs-monitoring dual-mode agent design** with explicit mode-inference
fallback as a DOM-18/DOM-19 pattern. Recommend explicitly updating
`repo-catalog.md`'s "Coverage Gaps Confirmed This Stage" section to remove
DOM-18, per the finding above.
