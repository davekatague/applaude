# Applaudé

**Think out loud.
Find it later.**

Talk to it.
Everywhere.

Apple Reminders, but you can speak to it.
Syncs across every device you own. Free.

---

## What this is

Applaudé turns Apple Reminders into a structured second brain you can talk to.

Every idea, person, project, lesson and decision
becomes a small structured note — synced through iCloud to every Apple device you own.

You capture by voice.
Claude reads, writes, and links it all together.

The stack is three things you already have or can get for free: **Apple Reminders**, **iCloud**, and **Claude**.
No new app to install.

No server to run.

## Install

**→ [Read the install guide](https://davekatague.github.io/applaude/install.html)**

Four paths, in order of difficulty:

| Surface | Time | What you get |
|---|---|---|
| 📱 Mobile | Already works | Voice, chat, projects on your phone. Nothing to install. |
| 🌐 Browser | 5 minutes | Claude.ai with the Reminders connector. |
| 💻 Desktop | 15 minutes | Mac app + small Terminal install. Unlocks Cowork too. |
| ⌨️ Claude Code | Developers | Shell, files, full read-write power. |

Most people only need the first two.

## Your first 5 minutes

**1. Create four lists in Apple Reminders:** `Captures`, `Knowledge`, `Goals`, `Projects`

**2. Open Claude** (voice on iPhone, or Claude.ai in a browser)

**3. Say something like:**

> "I'm setting up Applaudé. I just read that the best way to build a habit is to attach it to something you already do. Can you save that as a knowledge atom?"

Claude writes the atom to your Knowledge list — timestamped, structured, findable later.

**4. Now ask for it back:**

> "What do I know about habits?"

That's the loop. Capture, retrieve, build.

**Seed your brain fast:** See `references/starter-kit.md` for five paste-ready atoms that give your system an anchor from day one.

## Quick start (Claude Code)

```bash
git clone https://github.com/davekatague/applaude.git ~/.claude/skills/applaude
```

Claude Code picks up the skill the next time you start a session. Say *"capture this idea"*, *"add an entity"*, *"what do I know about X"* and it loads.

## What's in this repo

| File | What it is |
|---|---|
| **[`SKILL.md`](SKILL.md)** | The operating manual. How any Claude — voice, chat, desktop, code — should read and write Applaudé. |
| **[`docs/install.html`](docs/install.html)** | The install guide. Four paths, beginner to developer. Live at [davekatague.github.io/applaude](https://davekatague.github.io/applaude/install.html). |
| **[`bridges/`](bridges/)** | Project instructions for each Claude surface — paste into Claude.ai, Desktop, or Claude Code. |
| **[`configs/`](configs/)** | Example MCP config for Claude Desktop. |
| **[`references/starter-kit.md`](references/starter-kit.md)** | Five paste-ready atoms to bootstrap your brain on day one. |
| **[`references/`](references/)** | Schema, banked lessons, atom examples, desktop setup details. |
| **[`CHANGELOG.md`](CHANGELOG.md)** | Project history, schema bumps, structural changes. |

## Where this came from

Applaudé wouldn't exist without two people who got there first.

**[Andrej Karpathy](https://karpathy.ai)** built a personal wiki that showed what it looks like to organise knowledge for reading.

**[Arscontexta](https://arscontexta.com)** took the same idea and asked: what if knowledge was organised for an agent to *think* with?

Applaudé is the third step — knowledge organised so you can *use it in real life*, mid-drive, mid-call, mid-decision. By voice. On the devices you already own.

## Status

- **v0** (current) — Reminders + voice + Claude. Schema v1.3. Single-writer.
- **v0.5** (next) — Read-only daemon mirrors Reminders to DuckDB on your Mac. Curation passes.
- **v1** — Daemon writes back on a schedule. Agent fields activate.

Coming Soon:

Automatic Applaud Knowledge Graph.
<img width="1856" height="1013" alt="CleanShot 2026-05-19 at 01 09 34" src="https://github.com/user-attachments/assets/afa1fd0f-af7a-4b26-87b0-04761fe65810" />


## License

MIT. Open-source by intent. Use it, fork it, rewrite it for your own brain.

---

Built by [Dave Katague](https://github.com/davekatague). April 2026 onward.
