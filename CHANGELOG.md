# Applaudé — Changelog

Project naming history and notable structural changes for the Applaudé skill (voice-first second brain: Apple Reminders + Claude Voice).

---

## 2026-04-30 (PM) — Schema v1.2, list-namespace flip, 8 new lessons, voice/chat duality

Absorption pass over the past few days of build atoms. SKILL.md, references/lessons.md updated to match what's live in Reminders.

**List namespace — `ab.*` prefix retired:**
- Decision `dl1stnv2` (locked) supersedes the earlier same-day `92c2bc8c`. The `ab.` prefix is killed; lists now use plain human-readable names with emojis (Knowledge, Tasks 📬, Projects 🚧, Entities 🧱, Health Log 🍒, etc.). Reason: `ab.` made list names cognitively heavy in voice contexts.
- Live Reminders state agrees with `dl1stnv2`. Trust live state (lesson `l1v3st4t3`).
- SKILL.md Lists section rewritten to reflect live names + flag the supersession.

**Schema bump v1.1 → v1.2 (decision `dsv12lck`, locked):**
- New types: `question.atomic` (open-loop tracking, uncertainty without action), `event.curation` (output of curation passes per concept `c8r4t10n`).
- New predicates: `surfaces`, `almost_missed`, `bridges`, `dropped_thread`, `recurring_pattern`.
- New optional provenance fields per `p1m2t3d4`: `stamped_by` (which agent wrote it) and `model` (underlying LLM — for fine-tune lineage).
- v0.5 milestone scope refined: curation passes produce *draft* atoms for human review, not autonomous writes. v1 boundary unchanged.

**Lessons banked (Lessons 9-16 added to references/lessons.md):**
- L9 `l10n3ur0` (critical) — never offer rest/sleep/breaks unsolicited; respect neurodivergent operating modes
- L10 `l1v3st4t3` — query `reminder_list_search_v0` before any write; live Reminders is the contract
- L11 `l0ss0n-asym` — map constrained system first (voice before chat, local before cloud)
- L12 `l0ss0n-fake` — capability gaps as teaching moments, not apologies
- L13 `c8c10f34` — trust stated scope of authorship; don't add prior-art caveats unbidden
- L14 `l9unic0d` — ASCII-only for keys/sids/types/predicates; unicode in body prose only
- L15 `eed7c9ed` — taxonomy is open-ended; query, don't assume completeness
- L16 `w1w2k3n4` — wordplay/lateral thinking weak in Haiku; either step up the model or be explicit

**Voice/Chat duality framing (`ch4ng-30apr-pt2`, `phil-empathy`):**
- Voice = capture + celebrate (limited tools per `t00lm4p01`: 13 — 6 Reminders, 4 Calendar, 3 Context).
- Chat = consolidate + visualize + teach depth.
- Claude Code = build + persist.
- Claude-for-Everyone surfaces never expose SHA8 IDs, schema jargon, HLC, YAML — show simple metaphors and visual celebration. Care is the product.

**Agent vs scheduled task (`a1g3t4k`):** agency = autonomous decision-making, NOT scheduling. A timer-fired Claude Code session executing Dave's intent is human-prompted, not an agent write. v1 boundary = first scheduled autonomous decision about *what* to do.

**Open keystone questions (logged, blocking v0.5/v1):**
- `qag3ntpr` — which agent runs the v0.5 read-only projection (priority: keystone, blocks v1-daemon-writes)
- `qd43m0n3` — single-process daemon vs multi-process (blocks v0.5-daemon-build)
- `qd5b0und` — D5/Applaudé integration boundary (blocks d5-integration)
- `qc0nfl1c` — drift handling at projection layer (blocks v1-daemon-writes)
- `qpr1v4cy` — privacy scoping per projection (blocks multi-context-use)

**Onboarding demo shipped (`0nb04rt1`):** Single-file HTML at `/mnt/user-data/outputs/applaude-onboarding.html` for Stone & Chalk talk 2026-04-30. Five screens, glassmorphic phone-frame mockup, warm amber #f2c14e accent, Instrument Serif + Geist, IKEA-effect Preview screen (audience picks categories, sees their own brain in 100ms).

**Open follow-ups:**
- `references/schema.md` still reads v1.1 — needs version bump and new types/predicates added (not blocking, surfaced for next pass).
- Atom titles in Reminders still carrying SHA8 suffixes can be rewritten on next touch per `ch4ngfmt` audit pass discipline.
- `sk1ll4b-v2` baseline-first principle pending — represented in updated "What Dave will correct you on" list (#9), can be promoted to a Decision style subsection later.

---

## 2026-04-30 — Renamed to Applaudé (final name)

**Project renamed:** `Apple Brain` → `Claude Chat` → **`Applaudé`** (Apple + Claude).

**Why the final name:** Apple Brain was the first working title — descriptive but undersold the Claude side. Claude Chat was an intermediate. Applaudé captures the fusion that *is* the product: Apple's substrate (Reminders, iCloud-synced, voice-accessible) + Claude's voice traversal layer = a real-time, talk-speed second brain. The plain-text YAML schema keeps atoms portable, so the system isn't locked into Apple.

**Naming convention going forward:**
- **ASCII machine name:** `applaude` — used for the skill folder, frontmatter `name`, paths, and any MCP/CLI/tool identifier where non-ASCII could break encoding.
- **Display/brand name:** **Applaudé** (with accent) — used in conversation, prose, atom prose bodies, and human-facing docs.
- **Retired:** "Apple Brain" — only reference when pointing at a legacy filename or atom that hasn't been renamed yet.

**File-level changes (this commit):**
- `~/.claude/skills/apple-brain/` → `~/.claude/skills/applaude/` (folder rename).
- `SKILL.md` frontmatter: `name: apple-brain` → `name: applaude`, added `display_name: Applaudé`, description rewritten to lead with "Applaudé" + Apple+Claude framing.
- `SKILL.md` body: title and prominent prose mentions changed to Applaudé. Legacy "Apple Brain" mentions preserved only where they clarify the `ab.*` list namespace (which originated as "Apple Brain" abbreviation) and example atom titles still in Reminders.
- Desktop handoff doc renamed: `~/Desktop/ Applaudé - Claude Chat/apple-brain-claude-code-handoff.md` → `applaude-claude-code-handoff.md`. Body updated to use Applaudé.
- Memory: `~/.claude/projects/-Users-dave/memory/project_applaude.md` and `feedback_applaude_naming.md` written. Indexed in `MEMORY.md`.
- Global Claude Code system prompt (`~/.claude/CLAUDE.md`): one-line note added so future sessions never re-ask.

**Things deliberately NOT changed (and why):**
- **`ab.*` Reminders list names** (`ab.knowledge`, `ab.entities`, etc.) — renaming live iCloud Reminders lists would orphan or duplicate data on every Apple device. The `ab.` prefix is now a legacy-but-load-bearing namespace. Documented in SKILL.md.
- **Existing atom titles in Reminders** that still say "Apple Brain" (e.g. `Apple Brain 8e2d1f4a`, the project-root atom) — left in place. When touched in normal operation, rewrite to Applaudé.
- **Schema version** — unchanged. This is a naming change, not a schema change. Schema stays at v1.2 (`ch4ng12v`).

**Open follow-ups:**
- Rewrite the project-root atom in `ab.knowledge` from `Apple Brain 8e2d1f4a` to `Applaudé <new sid>` on next session that touches Reminders. Add a `superseded_by` link from old → new so lineage is preserved.
- Decide whether `MOC Apple Brain m1c2o3c4` should be retitled or left as a legacy MOC (probably retitle).
- Update `references/schema.md` and `references/lessons.md` to use Applaudé in prose (not blocking).

---

## Earlier history

Prior to 2026-04-30 the skill and project were called **Apple Brain**. See `references/lessons.md` for banked lessons accumulated under that name.
