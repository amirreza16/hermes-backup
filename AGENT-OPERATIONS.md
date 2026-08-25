# Agent Operations — Standing Efficiency Framework

Phase-independent. This file is NOT scoped to Phase -2 and does not expire
when this phase ends. Every future phase's CLAUDE.md / execution plan MUST
reference this file rather than duplicating or replacing it — if a future
phase needs a new CLAUDE.md, that file's opening section must point here.

Origin: created 2026-08-25, in response to the Stage -2.5 pattern-extraction
incident (see Changelog below) — ~2M tokens spent, zero durable output,
because sub-agent output was never persisted to disk.

---

## Active Rules

Kept short and current on purpose — see "Keeping This File Lean" below.
History, rationale, and evidence for these rules live in the Changelog, not
here.

### 1. Write-before-return
Any sub-agent (fork or fresh agent) producing structured output meant to
persist — a pattern record, catalog entry, audit finding, review result, or
similar — must `Write` it to its target file before returning its final
response. The invoking session verifies the file exists and is complete; it
does not reconstruct content from the sub-agent's chat summary.
Measured effect: see Changelog entry 2026-08-25 (49.3% token reduction on a
controlled test, attributable almost entirely to this rule).

### 2. No live extraction interjections
If a sub-agent's returned output is incomplete, do not `SendMessage` it
asking to repeat/re-paste content already covered — this re-bills the
sub-agent's entire inherited context on every extra turn. Read the file it
already wrote instead (Rule 1), or relaunch a fresh, better-scoped call.
Only resume a live sub-agent to hand it new work, never to re-extract old
work.

### 3. Right-size delegation
Prefer several small, single-purpose sub-agent calls with one clear file
deliverable each over one long multi-turn sub-agent asked to do many
things. Cost scales with (inherited context size) x (turn count), and
inherited context only grows larger as the project's history grows across
phases. Not yet independently token-measured — flagged as an open
measurement gap in the Changelog.

### 4. Graph-dependent tooling — deferred, with a concrete re-evaluation trigger
Do not adopt code-graph-dependent tools (tree-sitter / call-graph / git-diff
-based analysis — e.g. codebase-memory-mcp, Repowise, or future
equivalents) until the trigger condition below is met.
**Trigger condition (a detectable state, not a date or phase label):** the
first time a real, non-trivial, growing Hermes source tree exists in a
tree-sitter-supported language — not a single scaffold/hello-world commit.
When met, re-run the codebase-memory-mcp and Repowise audits fresh; do not
treat their 2026-08-25 verdicts as permanent, since the tools themselves
may also have changed by then.
**Status as of 2026-08-25:** NOT MET. Zero lines of Hermes implementation
code exist — Phase -2 is research-only.

### 5. RTK — opt-in for external-repo-heavy exploration
When doing Stage -2.3/-2.4-style work that involves cloning and reading many
files from an external repo (structure checks, source reads, maintenance
history checks), a sub-agent MAY invoke the RTK binary directly via Bash
(`/root/m2-research-workspace/tools/rtk/rtk <subcommand>`, e.g. `rtk
read`/`rtk find`/`rtk ls`/`rtk git log`) instead of native tools, for its
compression benefit. Never run `rtk init`, `rtk config`, or any subcommand
that installs a hook or modifies shell/system config — invoke only the
read-only compression subcommands by full path.
**Opt-in, not mandatory:** a sub-agent choosing not to use RTK is not a rule
violation. No automatic hook, no default-on behavior, no system-wide
integration.
Measured effect: see Changelog entry 2026-08-25 (~11.7% token reduction on
a real pilot task; lean-ctx was evaluated alongside it and rejected).

---

## Keeping This File Lean (self-governance)

- **Admission filter:** only short, imperative, evaluable standing rules
  and the *current* trigger condition for each deferred decision belong in
  Active Rules above. Incident narratives, measurement detail, and
  rationale go in the Changelog, never here. One-time Owner facts about
  Hermes itself belong in `decisions/OD-###`, not here.
- **Supersede, don't accumulate:** when a rule changes, its wording is
  replaced in place above; the Changelog records what changed and when.
  Active Rules never holds two versions of the same rule.
- **Size ceiling:** Active Rules section — soft cap 100 lines, hard stop
  150. Crossing the hard stop is a mandatory compaction pass before
  anything new is added, not a suggestion.
- **Mandatory audit checkpoint:** at every phase transition (Phase -2 ->
  -1 -> Spec Maturation -> real development), auditing this file is a
  required handoff-contract item, piggybacking on the existing handoff
  package process (Master Plan Section 19) rather than a new calendar
  cadence.
- **Changelog archive trigger:** if the Changelog section alone exceeds
  ~300 lines, archive older entries into a dated file (e.g.
  `AGENT-OPERATIONS-CHANGELOG-<year>.md`), leaving only a short "see
  archive" pointer plus the current year's entries live here.

---

## Changelog & Rationale

Append-only. Read rarely, by search, not as routine practice. Never edited
in place except to fix a factual error.

### 2026-08-25 — Write-before-return rule adopted; Stage -2.5 incident

**Incident:** Stage -2.5 (Pattern Extraction) ran 2026-08-24 as 6 parallel
forks (plus one wasted duplicate `Agent` call the coordinator caught live
as a mistake). Verified directly from local session transcripts
(`/root/.claude/projects/-root-m2-research-workspace/.../subagents/`):
~1.95M fresh tokens spent (2 of 6 forks — core-architecture and
social-media-ops — accounted for 86% of that; not evenly distributed),
plus ~39.7M cache-read tokens (billed far cheaper, but a real signal of
how many total turns occurred). Root cause: forks returned pattern records
only as chat summaries, never wrote them to a file (zero `Write` calls
across all 6 forks). This forced repeated `SendMessage` follow-ups asking
forks to "paste it all again verbatim," each re-paying the fork's full
inherited context. Outcome: the coordinator reached "44 pattern records
extracted" then moved on to other work — no `pattern-extraction.md` or
equivalent was ever written. The entire 44-record catalog and the ~2M
tokens spent producing it were never persisted and are lost; Stage -2.5
must be redone.

**Fix adopted:** Active Rule 1 (write-before-return) above.

**Measured effect (controlled A/B test, 2026-08-25):** paired test, same 2
real audit files (`gitroomhq-postiz-app.md`,
`indranilbanerjee-digital-marketing-pro.md`) fed to two forks inheriting
the same session context, same 6-pattern-record extraction task — only the
protocol differed.
- Baseline (chat-only + 1 follow-up round-trip, replicating the real
  failure): 168,413 + 169,755 = **338,168 tokens**, 2 turns, 4 tool calls.
- Treatment (write-before-return, no follow-up needed): **171,362
  tokens**, 1 turn, 3 tool calls.
- **Result: 166,806 tokens saved, 49.3% reduction.** Decomposition:
  169,755 tokens (102% of the saving) came from eliminating the
  round-trip turn entirely; offset by 2,949 tokens (-2%) of extra cost in
  the treatment's single turn, from writing full detail for all 6 records
  immediately instead of 1-full/5-summarized. Net matches the observed
  delta exactly.
- **Stated limits:** n=1 per condition, not repeated — a real data point,
  not a guaranteed constant. Only Rule 1 was isolated by this test; Rule 3
  (right-size delegation) has no measurement yet. Test ran at a much
  smaller scale (2 files, 1 round-trip) than the real incident (26 files,
  multiple round-trips per fork across up to ~50 turns) — the fix is
  expected to compound at that scale but this was not directly measured.
- Full reasoning and the raw per-turn numbers are in the Phase -2 session
  transcript, 2026-08-25.

**Not yet done:** Stage -2.5 has not been re-run under the new rule. The
lost 44-record catalog has not been reconstructed.

### 2026-08-25 — lean-ctx / RTK pilot; RTK approved opt-in, lean-ctx rejected, document-graph deferred

**Design:** real, temporary, fully-reversible 3-way pilot — same
Stage -2.3-style task (shallow-clone + lightweight triage of two real,
fresh repos, `charmbracelet/glow` and `junegunn/fzf`, untouched elsewhere
in this project) run three ways: native tools, RTK's CLI subcommands,
lean-ctx's CLI subcommands. Write-before-return applied in all three,
isolating only the compression-tool variable. Both tools installed from
official GitHub release binaries into a scratch `/tmp` directory for the
test only; fully deleted afterward (confirmed via `git status` and
directory listing — no trace left).

**Results:**
- Baseline (native): **256,354 tokens**, 9 tool calls.
- RTK: **226,395 tokens** (-29,959, **-11.7%**), 9 tool calls. No
  restrictions encountered; worked cleanly on freshly cloned repos outside
  the project root with zero configuration.
- lean-ctx: **224,173 tokens** (-32,181, **-12.6%**), 11 tool calls — but
  only via a workaround. Its actual compression mechanism (`read -m
  full/map/signatures`) enforces a hardcoded sandbox locked to the
  directory it first ran in; it refused to read the cloned target repos at
  all ("path escapes project root"). Lifting this requires a persistent
  `~/.config/lean-ctx/config.toml` edit, out of scope for an
  evaluation-only pilot. The fork fell back to a weaker path (`lean-ctx -c
  "cat <file>"`), which on one large source file compressed 590 of 644
  lines away — aggressively enough that the fork had to separately read
  the uncompressed file to actually understand the code, eating into the
  measured saving in real terms.

**Verdict:**
- Both real, both far below vendor claims (60-90%), both an order of
  magnitude smaller than write-before-return's measured 49.3%.
- **RTK: approved, opt-in only** — Active Rule 5 above.
- **lean-ctx: not adopted.** Structural mismatch with a workflow that
  constantly explores content outside one fixed root, plus a real
  comprehension-loss risk under aggressive compression — both observed
  directly, not inferred.

**Document-relationship graph (separate question, same session):**
assessed against the corpus as it actually stands — 25 domains, 32 skills,
49 repos, 31 sources, 8 rejected candidates, 6 Owner decisions (~156
entities). Tested whether the existing informal approach (consistent
`DOM-##`/`SKL-###`/etc. IDs + grep) already works: searching `DOM-11`
alone surfaced 16 real, relevant files across catalogs, decisions, and
audits. **Deferred, not built** — grep+consistent-IDs already functions at
this scale, and Stage -2.6/-2.7 already own this cross-referencing work by
design. Re-evaluation trigger: ~450-500+ entities, or a recurring (not
hypothetical) need for multi-hop queries grep can't answer.

**Update, 2026-08-25 (same day):** Owner approved and RTK installed —
`tools/rtk/rtk`, pinned to release `dev-0.45.1-rc.362`
(`rtk 0.42.4`, sha256 `63e66689...290d40ef`), not committed to git
(`.gitignore`'d, provenance recorded in `tools/README.md`). No hook, no
PATH/shell/system change. Active Rule 5's path now points at a real,
verified-working binary.
