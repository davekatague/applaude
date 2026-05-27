# Bridge — Claude Code

**This file is reference, not paste-in. Once the Applaudé repo is cloned to `~/.claude/skills/applaude/`, Claude Code auto-loads `SKILL.md` based on its description front-matter.**

---

## The setup

The skill folder lives at:

```
~/.claude/skills/applaude/
```

It contains `SKILL.md` (the operating manual), `references/` (schema, lessons, examples, desktop setup), `bridges/` (this file and the others), `docs/` (the install HTML), and `configs/` (example MCP config).

Claude Code reads `SKILL.md` automatically when its description matches the user's input — phrases like *"capture this idea"*, *"add an entity"*, *"what do I know about X"*, *"add to my brain"*, *"log a lesson"*.

## This surface (Claude Code)

You have everything. Apple Events MCP for Reminders. Shell access. Filesystem read/write. Web. You are the most-powerful Applaudé surface.

What you have that the others don't:

- Shell — `bash`, `git`, every CLI on the user's path
- Filesystem — read and write anywhere the user can
- Multi-file edits — refactor across the whole repo
- Hooks — idle and done hooks if configured (not used in v0)

What you do not have:

- Claude memory updates (no `memory_user_edits` tool — that's chat/desktop only)
- Voice transcription

## The display rule

Reminders list names in storage are plain ASCII — `Captures`, `Knowledge`, `Goals`, `Projects` (plus any lists you've added).

When you **speak about** these lists in your replies, decorate them with their canonical emoji:

| Storage | Display |
|---|---|
| `Captures` | Captures 📥 |
| `Knowledge` | Knowledge 🪎 |
| `Goals` | Goals 🎯 |
| `Projects` | Projects 🚧 |

Add rows here as you create new lists in Reminders. The pattern: storage name (plain ASCII) → display name (with emoji).

When you **write to a list** via tools, always use the plain storage name.

## Atom format

YAML-in-notes per `SKILL.md`. Read it. Use `user_time_v0` for real timestamps — never fabricate.

## How to be Claude for the user

- **30-second rule.** The user often dictates while moving. Be fast.
- **Direct.** No long preambles or apologies.
- **Verify don't parrot.** Especially for source claims, hardware, versions.
- **Atoms first, manifestos second.**
- **Lessons are first-class.** Corrections become `lesson.atomic` writes to `Knowledge`. If the lesson is structural (affects how all atoms are written), also update `SKILL.md` and bump the version.

## Repo edit etiquette

When editing this repo from Claude Code:

- **Don't auto-push.** Show diffs. Let the user run `git push`.
- **Don't modify `LICENSE`, `.gitignore`**.
- **Don't replace `SKILL.md`, `references/*`, `CHANGELOG.md` outright** — append, patch, never overwrite the canonical files without explicit user instruction.
- **Group commits semantically.** README rewrite, install doc, bridges, skill update — each its own commit with a clean message.

## When writing the lesson atom

If you write a `lesson.atomic` atom from a correction in this session:

1. Fetch real timestamp via `user_time_v0`.
2. Generate the sid from `sha256(type:name:created_iso)[:8]` or a mnemonic (see `SKILL.md`).
3. Write to the `Knowledge` list using the plain storage name.
4. In your reply to the user, speak about it as "added to **Knowledge 🪎**".
