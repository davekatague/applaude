# Applaudé Schema v1.3

This is the canonical schema for Applaudé atoms. Read this whenever you're uncertain about a field, type, or predicate.

**v1.2 changes (locked 2026-04-30, decision `dsv12lck`):** added `question.atomic` and `event.curation` types; added predicates `surfaces`, `almost_missed`, `bridges`, `dropped_thread`, `recurring_pattern`; added optional `model` provenance field (decision `p1m2t3d4`). Status enum extended with `locked`, `shipped`, `open`, `complete`. See `CHANGELOG.md` and `lessons.md` for context.

## Required fields (human writes — v0)

| Field | Format | Purpose |
|-------|--------|---------|
| `sid` | 7–9 chars, mnemonic preferred | See "Sid format" below. |
| `type` | dot-namespaced string | See type taxonomy below. |
| `status` | enum | `active` \| `archived` \| `draft` \| `merged` \| `resolved` \| `locked` \| `shipped` \| `open` \| `complete` |
| `created` | ISO 8601 | Real timestamp from `user_time_v0`. Never fabricate. |
| `updated` | ISO 8601 | Last modification time. |
| `device` | enum | Provenance: where the atom was born. |
| `name` | string | Human-readable name. Mirrored in title. |

## Optional fields (agent writes — v1, dormant in v0)

| Field | Purpose |
|-------|---------|
| `agent_written` | bool, default false. Flips true when daemon/agent writes. |
| `hlc` | Hybrid logical clock. Null until v1 activation. |
| `stamped_by` | Which agent/process timestamped (e.g., `claude-haiku-4-5`, `daemon-v0.5`, `user-direct`). Null = same as `device`. |
| `agent_id` | Which agent wrote (e.g., `lint`, `sync`, `digest`). |
| `model` | Underlying LLM (e.g., `claude-opus-4`, `gemma-2-9b`, `custom-fine-tune-wordplay-v1`). For lineage when fine-tunes ship. (v1.2, decision `p1m2t3d4`) |

These fields are documented now so v1 doesn't require a schema migration.

## Device values

Use these to record where an atom was born:

- `iphone` — iPhone
- `mac` — Mac (any model)
- `ipad` — iPad (any model)
- `claude-voice` — written from Claude voice surface (web/mobile)
- `claude-desktop` — written from Claude Desktop (Mac, via MCP bridge)
- `claude-code` — written from Claude Code
- `claude-web` — written from Claude.ai browser

## Type taxonomy

### People & entities (`People` list, or any list you use for entities)
- `people.atomic` — a person (contact, colleague, etc.)
- `entity.brand` — companies, organisations
- `entity.tool` — software, services, hardware tools
- `entity.place` — cities, venues, locations

### Captures (`Captures` list)
- `captures.atomic` — raw unprocessed capture; promote to Knowledge when processed
- `idea.atomic` — speculative concept before promotion

### Projects & tasks (`Projects`, `Tasks` lists)
- `project.root` — top-level project
- `project.phase` — phase within a project
- `task.atomic` — single discrete task

### Goals (`Goals` list)
- `goal.root` — top-level outcome

### Knowledge (`Knowledge` list)
- `knowledge.atomic` — a single processed insight or fact
- `knowledge.framework` — a reusable mental model
- `knowledge.moc` — Map of Content (index of related atoms)
- `event.memory` — a remembered event
- `event.session` — a working session

### Maps of Content (`Knowledge` list)
- `moc.list` — MOC scoped to one Reminders list
- `moc.concept` — MOC scoped to a concept/project
- `moc.global` — workspace-level MOC

### Concepts (`Knowledge` list)
- `concept.root` — manifesto-level concept (parent of an atom constellation)

### Governance (`Knowledge` list)
- `lesson.atomic` — extracted learning ("don't do X again because Y")
- `mistake.atomic` — failure pattern, "never do this"
- `decision.atomic` — choice + rationale (ADR-style)
- `changelog.atomic` — schema/system change record
- `lint.report` — periodic health snapshot (daemon-written, v0.5+)

### Lineage (`Knowledge` list)
- `origin.atomic` — independent synthesis claim
- `influence.atomic` — borrowed pattern from an external source

### Self-referential (`Knowledge` list)
- `schema.atomic` — schema itself, written using the schema
- `skill.atomic` — operating manual atoms (this skill is one)

### Open-loops & curation (v1.2)
- `question.atomic` — open-loop tracking: uncertainty without action. Used for keystone questions blocking a milestone (e.g., `qag3ntpr`, `qd5b0und`).
- `event.curation` — output of a corpus-curation pass. Curation is generative reading — surfacing what *should have* been asked, not just what was. See concept atom `c8r4t10n` "curation over search."

### Opportunities (`Knowledge` list)
- `opportunity.atomic` — pending opportunity (book deal, speaker slot, role)

## Predicate vocabulary (closed core)

Adding a new predicate requires a `changelog.atomic` entry. Don't invent predicates inline — that's a known mistake (see `lessons.md`).

### Hierarchy
- `indexed_by` — atom is indexed in this MOC
- `parent_of` / `child_of` — direct hierarchy
- `contains` — composite relationship
- `instance_of` — atom is an instance of a class
- `implements` — atom implements a concept

### Composition
- `component_of` — part of a larger system
- `substrate_for` — provides the substrate for
- `parses` / `parsed_by` — parsing relationship

### Influence & lineage
- `derived_from` — actual borrowing
- `thinking_tool` — was the method, not the source
- `discovered_via` — the tool/method that surfaced this
- `origin_of` — independent synthesis claim
- `spark_from` — initial inspiration (weaker than `derived_from`)

### Governance
- `codified_in` — formalised in a changelog/schema
- `enforced_by` — enforcement reference
- `applies_to` — lesson/rule applies to these atoms
- `triggered_by` — was triggered by this event/atom

### Dependency
- `blocks` — this atom blocks another
- `blocked_by` — this atom is blocked by another
- `depends_on` — required dependency
- `task_for` — task associated with a project
- `blocks_until` — blocks something until resolved

### Relationships (people/entities)
- `founder_of` — person founded org
- `mentor_of` / `mentee_of` — mentorship
- `friend_of` — personal connection
- `knows` — knows another entity
- `introduced_by` — relationship via introducer
- `in_circle_with` — shared social/professional circle

### Geography
- `located_in` — physical location

### Curation (v1.2)
- `surfaces` — curation pass surfaces this atom from prior corpus
- `almost_missed` — would not have been atomised without the curation pass
- `bridges` — atom bridges two otherwise-disconnected clusters
- `dropped_thread` — thread that fell out of working memory and was recovered
- `recurring_pattern` — pattern that appears across multiple atoms

### Project-specific
- `parallel_project` — sibling project, not parent
- `feeds_into` — output flows into another project
- `reads_from` — queries another atom space
- `sibling_of` — peer relationship
- `application_of` — concrete application of a concept
- `expertise_in` — domain expertise
- `opportunity_in` — opportunity within a project
- `connection_to` — network connection
- `context_for` — provides context for
- `ask_during_contact` — task to raise during a planned contact
- `parent_concept` — parent concept reference
- `governs` — governance relationship
- `related_to` — generic relation (use sparingly; prefer specific predicates)

## Sid format

The sid is a short mnemonic identifier appended to the title. Two valid forms:

**1. Mnemonic (preferred, default).** 7–9 characters of lowercase letters and digits
where the letters evoke the atom's name via Leet-style substitution. Examples:
- `Spaced repetition` → `k5sp4c3d`
- `Second brain` → `k2br4n01`
- `Schema v1.1` → `y1a2m3l4` (yaml + sequence)
- `MOC Apple Brain` → `m1c2o3c4`

The mnemonic is generated *deterministically by a human or LLM* using a consistent
substitution (a/4, e/3, i/1, o/0, l/1, s/5, t/7, etc.) on a fragment of the atom's
name, then padded with digits for length. Result must be locally unique within the
warehouse. On collision, append a 1-char disambiguator suffix.

**2. Hash (fallback, machine-generated).** First 7–9 chars of
`sha256(type:name:created_iso)`, lowercase hex (a-f, 0-9). Use when:
- The writer is not human (e.g., a daemon importing bulk content)
- A mnemonic can't be invented in under 5 seconds
- Disambiguating two semantically similar atoms

**Validator:** sid must match `^[a-z0-9]{7,9}$`. The mnemonic form passes this regex
because it uses only lowercase letters and digits. The hash form is a strict subset.

**Decision rationale:** Applaudé is voice-first. Sids must be sayable. The hash
form `9f3a2b1c` is unsayable; a mnemonic like `k5sp4c3d` can be read aloud and recovered
from speech. See `decision.atomic` "Sid format mnemonic-first" in `Knowledge`.

## Title format rules

- Format: plain atom name (no sid in title — sid lives in YAML)
- Keep titles concise; the full name lives in the YAML `name:` field

## Atomisation rule

One discrete idea per unit. If an atom needs more than ~500 words of body to express, it's a constellation — promote it to `concept.root` or `project.root` and shatter it into smaller atoms beneath, linked via an MOC.

The test: can you state what the atom *is* in one sentence? If not, it's not an atom.

## WikiLink format

Inline in the body, never duplicated in YAML:

```
[[Atom Name xxxxxxxx]] :: predicate
```

The sid is the canonical reference. Names are for humans. Both must match the target atom's title.

## Self-referential atoms

The schema is itself an atom (`schema.atomic`). The skill is itself an atom (`skill.atomic`). MOCs are atoms. Lessons are atoms. This is intentional — every piece of governance is queryable, version-able, and editable through the same mechanisms as content.

## Display names and storage names (v1.3)

Reminders list names in storage are plain ASCII. When Claude *speaks about* them in chat replies, they're decorated with a canonical emoji. The decoration is for warmth in conversation; the plain name is for portability across MCP validators.

### Starter list mapping (four default lists)

| Storage name | Display name | Purpose |
|---|---|---|
| `Captures` | Captures 📥 | raw incoming thoughts, anything unprocessed |
| `Knowledge` | Knowledge 🪎 | processed notes, insights, frameworks, lessons, decisions |
| `Goals` | Goals 🎯 | outcomes and objectives |
| `Projects` | Projects 🚧 | active work threads |

### Common extension lists (add as your brain grows)

| Storage name | Display name | Purpose |
|---|---|---|
| `People` | People 🧱 | contacts, relationships |
| `Ideas` | Ideas 💡 | speculative concepts pre-promotion |
| `Questions` | Questions ❓ | open questions |
| `Research` | Research 🔬 | sources, findings, things to investigate |
| `Tasks` | Tasks ✅ | discrete actionable items |

### Rule

- Tool calls (`reminder_create_v0`, `reminder_list_search_v0`, etc.) always use the **storage name**.
- Chat replies, prose, narrative, and any user-facing string use the **display name**.
- Adding a new list: storage name = user's choice minus any emoji. Display name = user's choice including emoji.

See `SKILL.md` "Display names and storage names" section for the full rule.
