# CLAUDE.md

- No manifest present (no package.json/go.mod/pyproject.toml/Cargo.toml) → no build/test/lint commands found.
- Run it: `cd "6_Claude_clode_Slash" && claude`, then type `/trip-plan <destination>` (README.md:33-44).

## Rules observed
- New commands need `description`/`argument-hint`/`allowed-tools`/`model` frontmatter (README.md:58).
- New agents need `name`/`description`/`tools`/`model` frontmatter (README.md:59).
- New skills need `name`/`description` frontmatter (README.md:60).
- These live in project-scoped `.claude/`; move to `~/.claude/` only if the intent is to make them global (README.md:51-52).

## Read first
- `README.md` — full wiring: command → subagent → skill, plus the frontmatter cheat-sheet
- `6_Claude_clode_Slash/.claude/commands/trip-plan.md` — the entry point / orchestration prompt
- `6_Claude_clode_Slash/README.md` — nested walkthrough of the same three pieces

Architecture: see ARCHITECTURE.md — read before structural changes
