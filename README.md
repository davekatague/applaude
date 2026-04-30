# Applaudé

> **Apple + Claude.** A voice-first second brain — Apple Reminders as the substrate, Claude Voice as the real-time traversal layer.

Pronounced **app-LAWD** (rhymes with "applaud"). Take the *a* off Apple, the *c* off Claude, mash them together, add an *é*. The fusion is the product: Apple's substrate (iCloud-synced, voice-accessible, agent-readable on every Apple device) plus Claude's voice traversal (talk-speed reach into your life context).

---

## What it is

Applaudé treats **Apple Reminders as a cognitive operating system**, not a to-do list. You capture atoms — small structured YAML notes — into Reminders lists; Claude (via voice, web, desktop, or Code) reads, writes, and traverses them on demand. The atoms travel: plain-text YAML with WikiLinks means the second brain isn't locked to Apple — atoms can move into other apps, processes, and locations without losing structure.

Three orientations side-by-side:

- **Karpathy's wiki** organises knowledge for *consumption*
- **Arscontexta** organises it for *thinking*
- **Applaudé** organises it for *execution* — every atom reachable mid-drive, mid-call, mid-decision

## What's in this repo

| File | Purpose |
|---|---|
| **[`SKILL.md`](./SKILL.md)** | The operating manual. How a Claude — voice, chat, desktop, or Code — should read and write Applaudé atoms. Self-editable; bumps version when learnings land. |
| **[`CHANGELOG.md`](./CHANGELOG.md)** | Project naming history (Apple Brain → Claude Chat → Applaudé), schema bumps, structural changes. |
| **[`references/schema.md`](./references/schema.md)** | Canonical schema (v1.2). Required + optional fields, type taxonomy, predicate vocabulary, sid format. |
| **[`references/lessons.md`](./references/lessons.md)** | Banked lessons (16 and counting) — what was corrected, what the durable rule is, why it matters. |
| **[`references/desktop-setup.md`](./references/desktop-setup.md)** | How to wire Claude Desktop to Apple Reminders via MCP. |
| **[`references/atom-examples.md`](./references/atom-examples.md)** | Worked atom examples — every type with annotated YAML. |

## Quick install (Claude Code)

If you run Claude Code locally and want this skill to fire when you talk about your second brain:

```bash
git clone https://github.com/davekatague/applaude.git ~/.claude/skills/applaude
```

Claude Code will pick it up the next time you start a session. The skill description front-loads the trigger phrases — say *"capture this idea,"* *"add an entity,"* *"what do I know about X,"* etc. and it will load.

For voice or iOS/desktop Claude, no install is needed — Reminders is the substrate; the skill is the operating manual a Claude reads to know how to behave on top of it.

## Status

- **v0** (current) — Reminders + voice + manual writes. Single-writer, single-human. Schema v1.2.
- **v0.5** (next) — Read-only daemon mirrors Reminders → DuckDB. Curation passes produce *draft* atoms for human review. 5 keystone questions still open (`qag3ntpr`, `qd43m0n3`, `qd5b0und`, `qc0nfl1c`, `qpr1v4cy`).
- **v1** — Daemon writes back on a schedule. Agent fields activate (`hlc`, `stamped_by`, `agent_id`). HLC enforced. Boundary trigger: first scheduled autonomous decision.

## Iterating

This repo is **a working artifact, not a finished product.** The skill is self-editable — when a Claude session corrects a mistake or surfaces a recurring pattern, the relevant atom and the skill itself get updated. Expect frequent commits.

If you're cloning this and adapting it to your own life, the personal references (Dave's name, devices, projects in `lessons.md` and atom examples) are intentional — Applaudé is *built on stories*, not abstractions. Fork it, rewrite the names, keep the structure.

## Naming

- **ASCII machine name:** `applaude` — used for the folder, the frontmatter `name` field, paths, MCP-safe identifiers. Avoids encoding fragility around the accent.
- **Display brand name:** **Applaudé** — used in conversation, prose, atom prose bodies, human-facing docs.
- **Retired:** "Apple Brain" — first working title. Only referenced when pointing at legacy artifacts that still carry the old name.

## License

MIT — see [`LICENSE`](./LICENSE). Open-source intent. Use it, fork it, rewrite it for your own brain.

---

Built by Dave Katague. April 2026 onward.
