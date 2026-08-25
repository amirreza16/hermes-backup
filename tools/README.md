# tools/

Optional, opt-in binaries for sub-agent use during research work. Not part
of the git history (see `.gitignore`) — this file is the reproducibility
record. Usage rules for each tool live in `AGENT-OPERATIONS.md`'s Active
Rules, not here.

## rtk

- **Source:** https://github.com/rtk-ai/rtk
- **Release installed:** `dev-0.45.1-rc.362` (asset:
  `rtk-x86_64-unknown-linux-musl.tar.gz`)
- **Binary self-reports:** `rtk 0.42.4`
- **SHA256 (of the downloaded .tar.gz):**
  `63e66689210db90048e4e7bae44f7eb617ddf9c6b02755e3a94843ae290d40ef`
- **Installed:** 2026-08-25, via `gh release download dev-0.45.1-rc.362
  --repo rtk-ai/rtk --pattern "*x86_64-unknown-linux-musl*"`
- **Path:** `tools/rtk/rtk`
- **Status:** opt-in only. No hook installed, no shell/PATH/system config
  touched. Never run `rtk init` or `rtk config` — see AGENT-OPERATIONS.md
  Active Rule 5 for what is and isn't allowed.
- **To reproduce** (e.g. after a workspace rebuild): re-run the download
  command above, or fetch a newer release if intentionally upgrading —
  note in AGENT-OPERATIONS.md's Changelog if the pinned version changes.

## lean-ctx

Evaluated 2026-08-25, not adopted — see AGENT-OPERATIONS.md Changelog for
why. Not installed here.
