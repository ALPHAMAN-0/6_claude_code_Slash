# 06 — Slash command + subagent + skill, all inside Claude Code

> Claude Code example: a slash command orchestrates a research subagent and a formatting skill to produce a travel trip brief.

**Tags:** `claude-code` `anthropic` `claude` `ai-agents` `subagents` `slash-commands` `agentic-workflows` `llm` `automation` `prompt-engineering`

The whole thing runs **in the Claude Code app**, driven by **slash syntax**.
Nothing to compile or host — Claude Code auto-discovers the files under
`.claude/` and wires them together.

```
06-claude-code-slash/
└── .claude/
    ├── commands/trip-plan.md        ← slash command:  /trip-plan   (entry point)
    ├── agents/trip-researcher.md    ← subagent:       does the research
    └── skills/trip-brief/SKILL.md   ← skill:          formats the output
```

## How the three pieces connect

1. **`/trip-plan <destination>`** — a **slash command** (`.claude/commands/trip-plan.md`).
   `$ARGUMENTS` receives whatever you type after the command. This is the entry
   point and the orchestration prompt.
2. It delegates research to the **`trip-researcher` subagent**
   (`.claude/agents/trip-researcher.md`) — its own context window, its own
   allowed tools (`WebSearch`, `WebFetch`), running on a cheaper model.
3. It formats the researcher's facts using the **`trip-brief` skill**
   (`.claude/skills/trip-brief/SKILL.md`), which Claude loads on demand.

So: **slash command orchestrates → subagent researches → skill formats.** All
three are just Markdown files; Claude Code is the runtime.

## Run it

```bash
cd 06-claude-code-slash
claude                 # open the Claude Code app in this directory
```

Then type:

```
/trip-plan Lisbon 2026-08-15
```

Claude Code kicks off the command, spawns the `trip-researcher` subagent to
gather weather + flight facts, then hands them to the `trip-brief` skill and
prints the finished brief.

- Type `/` to see `trip-plan` in the slash-command list.
- These live in the **project** `.claude/`. Move them to `~/.claude/` to make the
  command, subagent, and skill available in every project.

## File-format cheat-sheet

| File | Frontmatter keys | Invoked by |
|------|------------------|------------|
| `commands/trip-plan.md` | `description`, `argument-hint`, `allowed-tools`, `model` | typing `/trip-plan ...` |
| `agents/trip-researcher.md` | `name`, `description`, `tools`, `model` | the main agent delegating (Task tool), or auto-delegation |
| `skills/trip-brief/SKILL.md` | `name`, `description` | loaded on demand when relevant |