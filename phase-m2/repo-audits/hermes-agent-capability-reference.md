# Hermes Agent — Capability Reference

**Status: durable project reference, not a Phase -2-scoped research record.**
Built only from (1) `hermes-agent.nousresearch.com/docs` (fetched directly,
2026-08-24) and (2) the actual repository code (`NousResearch/hermes-agent`,
shallow clone inspected directly, 2026-08-24) — never guessed, never
reconstructed from general agent-framework knowledge or training-data
familiarity with other tools. This document replaces the Owner's previously
discarded "Hermes Agent Cheat Sheet" PDF, which contained fabricated content
(a nonexistent `hermes memory reindex` command, a fictitious "GEPA reflection
loop"). Every claim below is sourced; where a claim could not be verified in
either docs or code within this pass's time budget, it is marked **UNKNOWN**
rather than filled in from inference. Where docs and code were both checked
for the same claim and agree, that is noted; no disagreement was found in the
areas actually cross-checked (see the companion audit,
`nousresearch-hermes-agent.md`, Dimension I).

---

## What It Is

**Source: docs homepage + `llms.txt` (fetched directly).** "Hermes Agent is
the open-source, self-hosted AI agent built by Nous Research," MIT-licensed
(confirmed independently from the repo's own `LICENSE` file: Copyright (c)
2025 Nous Research). Runs the same agent core across CLI, a messaging
gateway (~20+ platforms), a TUI, and an Electron desktop app. **Source:
`AGENTS.md` (repo root, read directly):** "It learns across sessions (memory +
skills), delegates to subagents, runs scheduled jobs, and drives a real
terminal and browser. It is extended primarily through plugins and skills,
not by growing the core."

Supported platforms (docs): Linux, macOS, Windows, WSL2, Android.

## CLI Commands (Reference)

**Source: `hermes-agent.nousresearch.com/docs/reference/cli-commands`,
fetched directly 2026-08-24.** Full top-level command list as documented
(one-line descriptions verbatim from the docs page):

| Command | Description (verbatim from docs) |
|---|---|
| `hermes chat` | Interactive or one-shot chat with the agent. |
| `hermes model` | Interactively choose the default provider and model. |
| `hermes moa` | Configure named Mixture of Agents presets selectable from the model picker. |
| `hermes fallback` | Manage fallback providers tried when the primary model errors. |
| `hermes gateway` | Run or manage the messaging gateway service. |
| `hermes proxy` | Local OpenAI-compatible proxy that attaches OAuth provider credentials. |
| `hermes egress` | Outbound credential-injection firewall for remote terminal sandboxes. |
| `hermes lsp` | Manage Language Server Protocol integration. |
| `hermes setup` | Interactive setup wizard for all or part of the configuration. |
| `hermes whatsapp` / `hermes whatsapp-cloud` | WhatsApp bridge / official Meta Cloud API adapter. |
| `hermes slack` | Slack helpers for app manifest generation. |
| `hermes auth` | Manage credentials — add, list, remove, reset, status, logout. |
| `hermes send` | Send a one-shot message to a configured messaging platform. |
| `hermes peer` | Register peer Hermes gateways on other machines and DM their agents. |
| `hermes secrets` | Manage external secret sources like Bitwarden Secrets Manager. |
| `hermes migrate` | Diagnose and rewrite config.yaml for retired models or deprecated settings. |
| `hermes status` | Show agent, auth, and platform status. |
| `hermes cron` | Inspect and tick the cron scheduler. |
| `hermes kanban` | Multi-profile collaboration board for tasks, links, and dispatcher. |
| `hermes project` | Manage named, multi-folder workspaces (projects). |
| `hermes webhook` | Manage dynamic webhook subscriptions for event-driven activation. |
| `hermes hooks` | Inspect, approve, or remove shell-script hooks from config.yaml. |
| `hermes doctor` | Diagnose config and dependency issues. |
| `hermes security audit` | On-demand supply-chain audit (OSV.dev) for venv and dependencies. |
| `hermes approvals` | Approval-prompt tools for mining allowlist proposals. |
| `hermes dump` | Copy-pasteable setup summary for support/debugging. |
| `hermes prompt-size` | Show byte breakdown of system prompt + tool schemas. |
| `hermes debug` | Debug tools for uploading logs and system info. |
| `hermes backup` / `hermes import` | Back up Hermes home to a zip / restore from one. |
| `hermes checkpoints` | Inspect, prune, or clear checkpoint storage. |
| `hermes logs` | View, tail, and filter agent/gateway/error log files. |
| `hermes config` | Show, edit, migrate, and query configuration files. |
| `hermes skin` | List, switch, and tweak display skins. |
| `hermes console` | Open the safe Hermes command console. |
| `hermes pairing` | Approve or revoke messaging pairing codes. |
| `hermes skills` | Browse, install, publish, audit, and configure skills. |
| `hermes bundles` | Group several skills under a single slash command. |
| `hermes curator` | Background skill maintenance — status, run, pause, pin. |
| `hermes journey` | Timeline of learned skills + memories over time. |
| `hermes memory` | Configure external memory provider. |
| `hermes acp` | Run Hermes as an ACP server for editor integration. |
| `hermes mcp` | Manage MCP server configurations and run as MCP server. |
| `hermes plugins` | Manage Hermes Agent plugins. |
| `hermes portal` | Nous Portal status, subscription link, and Tool Gateway routing. |
| `hermes tools` | Configure enabled tools per platform. |
| `hermes computer-use` | Install or check the Computer Use backend. |
| `hermes pets` | Browse, install, and select animated pets. |
| `hermes sessions` | Browse, export, **prune**, rename, and delete sessions. |
| `hermes insights` | Show token/cost/activity analytics. |
| `hermes claw` | OpenClaw migration helpers. |
| `hermes import-agent` | Import a Claude Code or Codex CLI setup. |
| `hermes dashboard` | Launch the web dashboard for managing config and sessions. |
| `hermes serve` | Start the Hermes backend server (headless). |
| `hermes desktop` | Build and launch the native Electron desktop app. |
| `hermes profile` | Manage profiles — **multiple isolated Hermes instances**. |
| `hermes completion` | Print shell completion scripts (bash/zsh/fish). |
| `hermes update` | Pull latest code and reinstall dependencies. |
| `hermes uninstall` | Remove Hermes from the system. |
| `hermes --version` | Show version information. |

**No `hermes memory reindex` command exists in this list** — confirming the
discarded cheat-sheet PDF's claim was fabricated, as the Owner already
suspected.

## Multi-Instance / Multi-Tenancy (`hermes profile`, DOM-24)

**Source: docs (`hermes profile` description) + code, cross-checked.**
`hermes profile` is a documented, first-class command for managing "multiple
isolated Hermes instances." At the code level (`docs/profile-routing.md`,
read directly, plus `gateway/profile_routing.py`, `gateway/run.py`):

- A single gateway process can serve multiple profiles, each with a fully
  separate home directory (`HERMES_HOME`) — separate `MEMORY.md`, `USER.md`,
  `SOUL.md`, sessions, and tools.
- Routing which inbound message goes to which profile is configured via
  `profile_routes` in `config.yaml`, keyed on platform +
  `guild_id`/`chat_id`/`thread_id`, with most-specific-route-wins matching.
  Requires `gateway.multiplex_profiles: true`.
- **FACT, verified via `gh api` commit history:** this profile-routing feature
  (`gateway/profile_routing.py`) was merged into mainline 2026-08-10/11 — it
  is a recent addition, not a long-standing capability.
- **Not yet in mainline:** a lighter-weight, automatic per-context memory
  scoping (`context_id`, PR #47552, still open as of 2026-08-24) that would
  isolate memory writes per DM/channel/thread *without* requiring a whole
  separate profile per context. See the companion audit's Dimension C for
  full sourcing.

**Practical implication for "add a new page without a from-scratch project":**
achievable today via `hermes profile` + `profile_routes`, but each new
isolation boundary currently means provisioning a full separate profile
(separate memory/skills/session state), not a cheap per-context flag.

## Memory System

**Source: code (`plugins/memory/`), docs page for this topic not
successfully fetched this pass (guessed URLs returned 404; not further
pursued within this pass's time budget — flag for a follow-up fetch attempt
via the docs site's own navigation/search rather than a guessed URL).**

Eight pluggable memory backends found as real, non-stub plugins (each with
`plugin.yaml` + `README.md` + implementation): `holographic` (native
default, SQLite-backed), `mem0`, `honcho`, `supermemory`, `openviking`,
`retaindb`, `hindsight`, `byterover`. Declarative facts are written to
`MEMORY.md`/`USER.md` (small, ~200-char entries per `tools/write_approval.py`'s
own docstring). The `holographic` backend supports hard deletion of stored
facts (`DELETE FROM facts` etc., `plugins/memory/holographic/store.py`) —
call-site reachability (user-command-only vs. autonomous) is **UNKNOWN**,
not traced this pass.

**Session/transcript retention:** `hermes_state.py`'s
`maybe_auto_prune_and_vacuum(retention_days=90)` permanently deletes ended
sessions and their on-disk transcripts after 90 days of inactivity by
default — but its only call site (`gateway/run.py`) gates it behind
`auto_prune: false` by default (config opt-in required to activate). `hermes
sessions` CLI command (docs) confirms "prune" as a documented, user-facing
operation as well.

## Skills System

**Source: code (`skills/` tree) + docs nav confirming a "Skills System" page
exists (page content not fetched this pass).** Skills are directories
containing a `SKILL.md` file (confirmed structure matches, e.g.
`skills/creative/ascii-video/SKILL.md`, `skills/social-media/xurl/SKILL.md`)
— directly compatible in shape with the Claude Skills model referenced
elsewhere in this Phase -2 research (Stage -2.2's skill-catalog.md). A
`skills/social-media/` category exists natively, containing at least an
`xurl` (X/Twitter) skill. Relevant CLI: `hermes skills` (browse/install/
publish/audit/configure), `hermes bundles` (group skills under one slash
command), `hermes curator` (background skill maintenance).

## MCP Integration

**Source: code (`optional-mcps/` directory exists at repo root) + docs nav
confirming an "MCP Integration" page and a "Use MCP with Hermes" guide exist
(page content not fetched this pass).** Relevant CLI: `hermes mcp` (manage
MCP server configs and run Hermes itself as an MCP server).

## Scheduling / Cron (DOM-13)

**Source: code (`cron/` directory: `scheduler.py`, `jobs.py`,
`executions.py`, `lifecycle_guard.py`, `monitor.py`) + a named architecture
doc, `docs/chronos-managed-cron-contract.md` (existence confirmed, full
content not read this pass).** Relevant CLI: `hermes cron` (inspect and tick
the scheduler).

## Cost / Usage Tracking (DOM-16)

**Source: code (`agent/billing_usage.py`, `agent/billing_view.py`,
`agent/usage_pricing.py`, `agent/aux_accounting.py`) + a named architecture
doc, `docs/billing-lifecycle.md` (existence confirmed, full content not read
this pass).** Relevant CLI: `hermes insights` (token/cost/activity
analytics). **UNKNOWN:** whether this subsystem enforces budget caps or only
tracks/reports usage — module names suggest tracking; enforcement behavior
not confirmed either way this pass.

## Human Control / Approval

**Source: code (`tools/write_approval.py`, read in full) + CLI reference
(`hermes approvals`, `hermes hooks`, `hermes pairing`).** A real approval-gate
mechanism (`write_approval`) exists for memory/skill writes specifically,
distinguishing interactive (foreground) writes from autonomous
(`background_review`) writes. **Defaults to disabled** ("write freely" is the
pre-gate/default behavior). No publish-specific or platform-send-confirmation
approval gate was found in this pass's targeted search — **UNKNOWN**, not
confirmed absent, pending a fuller sweep.

## License

MIT (confirmed directly from the repository's `LICENSE` file, Copyright (c)
2025 Nous Research).

---

## Explicitly Not Covered This Pass

The following docs sections are named in the site's navigation (confirmed via
direct fetch of the docs homepage) but their page content was not
successfully fetched within this pass's time budget (guessed URL slugs
returned 404, and the site's real slugs were not otherwise discovered): Memory
System detail page, Skills System detail page, MCP Integration detail page,
Configuration (full `config.yaml` schema), Bot Mode, Voice Mode, Security,
per-platform setup guides. A future pass should navigate from
`hermes-agent.nousresearch.com/docs/` directly (or fetch `/llms-full.txt`,
~1.8MB, confirmed to exist) rather than guessing slugs, to close these gaps
without re-doing the code-level work already captured here and in the
companion audit file.
