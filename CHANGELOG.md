# Applaudé — Changelog

Project naming history and notable structural changes for the Applaudé skill (voice-first second brain: Apple Reminders + Claude Voice).

---

## 2026-04-30 (PM) — Schema v1.2, list-namespace flip, 8 new lessons, voice/chat duality

**List namespace — plain names:**
- Lists now use plain human-readable names with emojis (Knowledge, Tasks, Projects, etc.). Earlier `ab.` prefix retired. Reason: prefixes made list names cognitively heavy in voice contexts.
- Always query live Reminders state before writing — never rely on cached docs.

**Schema bump v1.1 → v1.2:**
- New types: `question.atomic` (open-loop tracking, uncertainty without action), `event.curation` (output of curation passes per concept `c8r4t10n`).
- New predicates: `surfaces`, `almost_missed`, `bridges`, `dropped_thread`, `recurring_pattern`.
- New optional provenance fields: `stamped_by` (which agent wrote it) and `model` (underlying LLM — for fine-tune lineage).
- v0.5 milestone scope refined: curation passes produce *draft* atoms for human review, not autonomous writes.

**Lessons banked (Lessons 9-16):**
- L9 — query `reminder_list_search_v0` before any write; live Reminders is the contract
- L10 — map constrained system first (voice before chat, local before cloud)
- L11 — capability gaps as teaching moments, not apologies
- L12 `l9unic0d` — ASCII-only for keys/sids/types/predicates; unicode in body prose only
- L13 — taxonomy is open-ended; query, don't assume completeness
- L14 — wordplay/lateral thinking weak in smaller models; step up model or be explicit

**Voice/Chat duality framing:**
- Voice = capture + celebrate (limited tools: 6 Reminders, 4 Calendar, 3 Context).
- Chat = consolidate + visualize + teach depth.
- Claude Code = build + persist.
- Claude-for-Everyone surfaces never expose SHA8 IDs, schema jargon, HLC, YAML — show simple metaphors and visual celebration.

**Agent vs scheduled task:** agency = autonomous decision-making, NOT scheduling. A timer-fired session executing the user's intent is human-prompted, not an agent write. v1 boundary = first scheduled autonomous decision about *what* to do.

**Open keystone questions (blocking v0.5/v1):**
- `qag3ntpr` — which agent runs the v0.5 read-only projection
- `qd43m0n3` — single-process daemon vs multi-process
- `qd5b0und` — external integration boundary
- `qc0nfl1c` — drift handling at projection layer
- `qpr1v4cy` — privacy scoping per projection

---

## 2026-04-30 — Renamed to Applaudé (final name)

**Project renamed:** working title → **`Applaudé`** (Apple + Claude).

**Why the final name:** Applaudé captures the fusion that *is* the product: Apple's substrate (Reminders, iCloud-synced, voice-accessible) + Claude's voice traversal layer = a real-time, talk-speed second brain. The plain-text YAML schema keeps atoms portable, so the system isn't locked into Apple.

**Naming convention:**
- **ASCII machine name:** `applaude` — used for the skill folder, frontmatter `name`, paths, and any MCP/CLI/tool identifier where non-ASCII could break encoding.
- **Display/brand name:** **Applaudé** (with accent) — used in conversation, prose, atom prose bodies, and human-facing docs.

**Schema version** — unchanged at v1.2. This is a naming change, not a schema change.

**Open follow-ups:**
- Update `references/schema.md` and `references/lessons.md` to use Applaudé in prose.

---

## Earlier history

Prior to 2026-04-30 the skill was in development under a working title. See `references/lessons.md` for banked lessons accumulated during development.
