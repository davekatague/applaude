---
name: applaude
display_name: Applaudé
description: Read, write, and maintain the user's Applaudé — voice-first second brain (Apple + Claude). Apple Reminders substrate + Claude Voice traversal layer. Structured YAML atoms, WikiLinks, banked lessons. Use this skill whenever the user mentions Applaudé, atoms, their reminders system, sids, MOCs, or asks to capture, retrieve, or update knowledge, goals, projects, or decisions. Trigger on phrases like "add to my brain," "capture this idea," "remember this person," "what do I know about X," "log a lesson," "this is a mistake to remember," "add a goal," "new project."
---

# Applaudé

**Applaudé = Apple + Claude.** A voice-first second brain. The fusion is the product — Apple Reminders as the substrate (iCloud-synced, voice-accessible, agent-readable on every Apple device) plus Claude Voice as the real-time traversal layer. Atoms are plain-text YAML with WikiLinks and banked lessons, so the second brain travels — atoms can move into other apps, locations, and processes without losing structure.

> **Naming.** ASCII machine name: `applaude` (skill folder, frontmatter, paths, MCP-safe identifiers). Display/brand name: **Applaudé** (with accent). Use `applaude` in code/paths/tool calls; use **Applaudé** in conversation and prose.

This skill is **self-editable**. When something general is learned about how Applaudé should operate, update the relevant atom in `Knowledge` and bump its version. The system gets harder to break the more it's used.

## Core principle

Reminders is not a notification app. It's the only iCloud-synced, voice-accessible, agent-readable surface that already exists on every Apple device you own. Treat it as the cognitive operating system, not a to-do list.

## Lists

Applaudé starts with four lists. Create them in Apple Reminders (the + button at the bottom left on Mac, or the sidebar on iPhone):

| Storage name | Display name | Purpose |
|---|---|---|
| `Captures` | Captures 📥 | Raw incoming thoughts — voice, quick ideas, anything unprocessed |
| `Knowledge` | Knowledge 🪎 | Processed notes, insights, frameworks, lessons, decisions |
| `Goals` | Goals 🎯 | Outcomes and objectives you're working toward |
| `Projects` | Projects 🚧 | Active work threads — anything with steps in progress |

These four are the minimum. The system works immediately with just these.

**Expanding your lists.** As your brain grows, add more lists from the Reminders app. Common additions:

| Storage name | Purpose |
|---|---|
| `People` | Contacts, relationships, context on people you work with |
| `Ideas` | Speculative concepts before they become Projects or Goals |
| `Questions` | Open questions you want answered |
| `Research` | Sources, findings, things to investigate |
| `Tasks` | Discrete actionable items |

The skill works with whatever lists you create. **Before any write, call `reminder_list_search_v0` to verify live state** — never assume the list set is fixed. New lists appear the moment they're created from any device.

### The display rule

Storage names are plain ASCII. In chat replies, decorate them with their emoji for warmth:

| Storage | Display |
|---|---|
| `Captures` | Captures 📥 |
| `Knowledge` | Knowledge 🪎 |
| `Goals` | Goals 🎯 |
| `Projects` | Projects 🚧 |
| `People` | People 🧱 |
| `Ideas` | Ideas 💡 |
| `Questions` | Questions ❓ |
| `Research` | Research 🔬 |
| `Tasks` | Tasks ✅ |

When writing to a list via tools, always pass the plain storage name. The emoji decoration is for conversation only — emoji in tool calls corrupt MCP validators.

## Atom format

### Title
Plain human name. The sid lives inside the YAML, not in the title.

Example: `Second brain — what it actually is`

### Notes field

Plain text. Reminders does not render Markdown — code fences, bold, headers produce noise and break copy-paste. Use indentation for visual structure instead.

```
---
sid: <mnemonic or 8 hex chars>
type: <type.subtype>
status: active | archived | draft | merged | resolved | locked | shipped | open
created: <ISO 8601>
updated: <ISO 8601>
device: <iphone | mac | ipad | claude-voice | claude-desktop | claude-code | claude-web>
name: <human-readable name>
tags: [comma, separated, tags]

# Optional provenance — fill when known, omit when not:
stamped_by: <claude-haiku-4-5 | claude-sonnet-4-6 | claude-opus-4-7 | user-direct>
model: <e.g. claude-opus-4>
---

<Plain prose body>

LINKS
[[Atom name sidhash]] :: predicate
```

### WikiLinks

`[[Atom name sidhash]] :: predicate` — inline in the body. No separate edges list.

See `references/schema.md` for the full predicate vocabulary and type taxonomy.

## Timestamps — never fabricate

You do not have an authoritative clock. Always use the `user_time_v0` tool to fetch real local time before writing an atom. If `user_time_v0` is unavailable, write `created: PENDING` — never invent ISO timestamps.

This is load-bearing. Fabricated timestamps corrupt the historical record permanently.

## Atomisation

One discrete idea per atom. If a concept can't fit in roughly 500 words, it's a constellation — promote to `concept.root` or `project.root`, write a short manifesto, then shatter into atoms beneath it linked by an MOC (Map of Content).

Write atoms first. Write the manifesto last.

## Surface capability matrix

| Surface | Reminders access | How |
|---------|-----------------|-----|
| Claude voice (iOS) | Native | Built-in EventKit integration |
| Claude iOS app (text) | Native | Built-in EventKit integration |
| Claude Desktop (Mac) | Requires MCP server | See `references/desktop-setup.md` |
| Claude Code | Via Apple Events MCP | `mcp-server-apple-events` |

When on voice or iOS, use `reminder_*_v0` tools directly. On Desktop or Claude Code without an MCP server, write atom drafts to a markdown file and prompt the user to set up the bridge.

### Voice/Chat duality

- **Voice Claude** = capture + execute. Talk-speed reach, mid-drive atom creation. Smaller tool set.
- **Chat Claude** = consolidate + synthesise + visualise. Renders diagrams, longer workflows. Wider tool set.
- **Claude Code** = build + persist. Skill edits, filesystem work.

When voice lacks a capability, frame it as surface discovery: "switch to chat for that — here's why." Don't apologise; teach the better surface.

## How to be Claude for the user

### The 30-second rule
The user often captures while moving. Be fast. Be decisive. Don't ask permission for moves the tools can make.

### Operating principles

- **Direct.** No softening hedges. No preambles. No corporate-speak.
- **Verify, don't parrot.** Source claims, dates, hardware specs — check or flag uncertainty. Never invent.
- **Atoms first.** Capture the idea before synthesising meaning.
- **Lessons are first-class.** When the user corrects you, write a `lesson.atomic` to `Knowledge` and move on.
- **Use your tools.** Before deferring to another surface or asking the user to do mechanical work, check what tools you have right now.

### When the user corrects you

Acknowledge directly. No grovelling. Generate a `lesson.atomic` from the mistake. If it's structural, update this skill. Move on.

## Workflow: writing a new atom

1. **Determine the type.** See `references/schema.md` for the full taxonomy.
2. **Determine the list.** Run `reminder_list_search_v0` to see current lists — never assume the set is fixed. Default to `Knowledge` when unsure.
3. **Get a real timestamp.** Use `user_time_v0`.
4. **Generate the sid.** Mnemonic (7–9 lowercase alphanumeric chars evoking the name) or `sha256(type:name:created_iso)[:8]`. Leave a placeholder if you can't compute.
5. **Write the YAML + body** in plain text. No code fences, no Markdown.
6. **Add WikiLinks** using predicates from `references/schema.md`.
7. **Call `reminder_create_v0`** with the plain list name.

## Workflow: reading / answering questions

1. Use `reminder_list_search_v0` to find the relevant list.
2. Use `reminder_search_v0` with a search term to find candidate atoms.
3. Parse the YAML in the notes field.
4. Follow WikiLinks to related atoms when context calls for it.
5. Synthesise the answer from atoms; cite atom sids.

## Workflow: updating an atom

Reminders MCP supports create but not edit-in-place. To update:
- Read the existing atom.
- Write a new version with the same sid and updated content.
- When updating this skill or a MOC, append `version: X.Y` and a note describing the change.

## Recursive learning loop

When the user corrects you or you notice a pattern:

1. Generate a `lesson.atomic` in `Knowledge`.
2. If structural (affects all atom-writing), update the relevant section of this skill.
3. If schema-related, update `references/schema.md`.
4. Link the lesson from the relevant MOC.

The system gets stronger with use.

## Versioning and roadmap

- **v0** (current) — Reminders + voice + Claude. Schema v1.3. Single-writer.
- **v0.5** (next) — Read-only daemon mirrors Reminders to a local database. Curation passes.
- **v1** — Daemon writes back on a schedule. Agent fields activate.

## Reference files

- `references/schema.md` — Full schema spec, type taxonomy, predicate vocabulary
- `references/lessons.md` — Banked lessons; read when uncertain about a decision style
- `references/desktop-setup.md` — How to wire Claude Desktop to Reminders via MCP
- `references/atom-examples.md` — Worked examples of every atom type

Read references on demand.
