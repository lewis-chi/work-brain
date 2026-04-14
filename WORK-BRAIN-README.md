# Work-Brain Skills for Claude Code

A set of Claude Code slash commands that turn an Obsidian vault (`~/obsidian/work-brain/`) into a persistent "second brain" for engineering work. Notes are stored as plain Markdown with YAML frontmatter, cross-linked with `[[wiki-links]]`, and indexed by [QMD](https://github.com/query-md/qmd) for full-text and vector search.

## Quick Reference

| Command | What it does |
|---------|-------------|
| `/resume` | **Start of session.** Reads the vault index, recent daily notes, and open threads so you can pick up where you left off. Auto-filters by the current git repo. |
| `/wrap-up` | **End of session.** Creates (or appends to) a daily note capturing what was done, decided, and learned. Promotes open threads to the vault index. |
| `/save [topic]` | Save knowledge or insights from the conversation to `02_knowledge/`. Searches for existing notes first to avoid duplicates. |
| `/save-decision [desc]` | Record a technical/architectural decision to `03_decisions/` using a lightweight ADR format. Supersedes older decisions on the same topic. |
| `/save-lesson [what happened]` | Log a mistake or lesson learned to `mistakes-and-lessons.md`. |
| `/threads <sub>` | Quick CRUD for open threads in `VAULT-INDEX.md` -- `list`, `add`, `done`, `move`, `rename`. |
| `/brain <query>` | Search the vault (keyword + vector) without writing anything. |
| `/consolidate [area]` | Audit the vault for contradictions, duplicates, stale content, and knowledge worth promoting. Run periodically. |

## Vault Structure

```
~/obsidian/work-brain/
  VAULT-INDEX.md          # Dashboard: active projects, open threads, recent decisions
  mistakes-and-lessons.md # Running log of incidents and resolved lessons
  00_daily/               # Daily session notes (YYYY-MM-DD.md)
  01_projects/            # Per-project reference files (created after 3+ sessions)
  02_knowledge/           # Persistent knowledge (architecture/, tooling/, etc.)
  03_decisions/           # Decision records (ADR-style)
  04_archive/             # Stale/superseded content
```

## How It Works

1. **Start a session** -- `/resume` loads context from the vault, filtered to the repo you're currently in. Pass `all` to see everything, or a date/topic to target a specific session.

2. **Work normally** -- use `/save`, `/save-decision`, `/save-lesson`, or `/threads add` whenever something worth remembering comes up.

3. **End the session** -- `/wrap-up` reviews the conversation and writes a structured daily note with context, decisions, facts learned, and open threads. It also updates `VAULT-INDEX.md`.

4. **Maintain the vault** -- `/consolidate` finds contradictions between notes, merges duplicates, promotes recurring facts to knowledge files, and suggests archiving stale content.

## Key Design Principles

- **Plain Markdown + Obsidian compatible** -- notes work in any editor, but linking and graph view are best in Obsidian.
- **Repo-aware** -- `/resume` and `/wrap-up` auto-detect the current git repo and filter/tag sessions accordingly.
- **Search-before-write** -- all write commands search QMD first to avoid duplicates and surface related notes.
- **Never fabricate** -- skills only record what was actually discussed in the conversation.
- **Non-destructive** -- `/consolidate` asks before archiving or merging; `/wrap-up` appends to existing daily notes rather than overwriting.
- **QMD-indexed** -- a PostToolUse hook keeps the QMD index up to date automatically after file writes.

## Requirements

- [QMD](https://github.com/query-md/qmd) installed and configured with a `work-brain` collection pointing at the vault
- Obsidian vault at `~/obsidian/work-brain/` (or update paths in the skill files)
- Claude Code with these skills installed in `~/.claude/skills/`

## Non-Work-Brain Skills

Two other skills live alongside these but aren't part of the work-brain system:

- `/terminal-title` -- auto-sets the terminal window title based on the current task (useful when running multiple Claude Code instances)
- `/simplify` -- reviews changed code for reuse, quality, and efficiency
