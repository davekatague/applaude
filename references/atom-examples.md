# Apple Brain atom examples

Worked examples of every atom type, copy-pasteable. Read this when uncertain about format for a specific type.

All examples use placeholder sids — when writing real atoms, generate from `sha256(type:name:created_iso)[:8]` after fetching real time via `user_time_v0`.

---

## Person (entity.person)

**List:** `ab.entities`
**Title:** `Mickey c7r2y9p4`

```
---
sid: c7r2y9p4
type: entity.person
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Mickey
alias: [crypto guy, your friend]
relationship: friend
tags: [network, crypto, dubai, connection-hub]
---

Mickey

Crypto guy. Your friend. Connected to both the push-email inventor and Mustafa (VC). Acts as a network hub for your Dubai connections. Source of warm introductions into high-value relationships.

ROLE
Network connector. Brings together different worlds (crypto, tech history, capital).

LINKS
[[Push-email inventor p8sh3m4l]] :: knows
[[Mustafa VC m6st4f4v]] :: knows
[[Dubai move d2b4y1m5]] :: context_for
```

---

## Tool (entity.tool)

**List:** `ab.entities`
**Title:** `Side Reminder s1d3r3m1`

```
---
sid: s1d3r3m1
type: tool.atomic
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Side Reminder
url: https://sidereminder.com
relationship_to_apple_brain: substrate
tags: [tool, substrate, mac, claude-code]
---

Side Reminder

macOS companion app for Apple Reminders. Edge-of-screen access, on-device voice (Cmd+Shift+V), CLI (sidereminder), Claude Code slash commands.

ROLE IN APPLE BRAIN
Substrate, not integration. v0 ships on top of Side Reminder.

LINKS
[[Apple Brain 8e2d1f4a]] :: substrate_for
[[Schema v1.1 y1a2m3l4]] :: parses
```

---

## Project root (project.root)

**List:** `ab.knowledge`
**Title:** `Dubai move d2b4y1m5`

```
---
sid: d2b4y1m5
type: project.root
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Dubai move
target_date: 2026-05
timeline: 2-3 weeks
tags: [project, geography, life-change, medical-critical]
---

Dubai move

Timeline: 2-3 weeks from now. Multi-phase move with critical medical, professional, and network components.

CRITICAL PATH
- ADHD medication refill via psychiatrist
- Psychiatrist Dubai recommendations + handover
- Vyvanse 60mg confirmation in 10 days

OPPORTUNITIES LIVE
- United AI incubator role
- One Billion Summit speaker
- AI advisor roles pending

NETWORK IN PLACE
- Mustafa (VC, royalty-connected)
- Mickey (crypto, connector hub)

LINKS
[[ADHD medication refill a1d2h3d]] :: blocks_until
[[United AI incubator u1t4d1a1]] :: contains
[[Mustafa VC m6st4f4v]] :: opportunity_in
```

---

## Task (task.atomic)

**List:** `ab.knowledge` (eventually `ab.tasks`)
**Title:** `ADHD medication refill a1d2h3d`

```
---
sid: a1d2h3d
type: task.atomic
status: active
severity: critical
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: ADHD medication refill before Dubai
timeline: urgent (2-3 weeks)
tags: [medical, critical-path, adhd]
---

ADHD medication refill

Critical blocking item for Dubai move. Psychiatrist contact required.

IMMEDIATE
- Contact actual psychiatrist (not untrained GPs)
- Vyvanse 60mg in place
- 10-day check-in scheduled

LINKS
[[Dubai move d2b4y1m5]] :: blocks
[[Psychiatrist handover p1s2h3o]] :: task_for
```

---

## Lesson (lesson.atomic)

**List:** `ab.knowledge`
**Title:** `Lesson never fabricate timestamps l4t1m3st`

```
---
sid: l4t1m3st
type: lesson.atomic
status: active
severity: critical
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Never fabricate timestamps
applies_to: [y1a2m3l4, sk1ll4b]
tags: [time, integrity, fabrication]
---

Lesson never fabricate timestamps

LLM-side Claude has no authoritative clock. Any timestamp written into an atom is a guess at best, fiction at worst. Both corrupt the warehouse.

RULE
- Voice/desktop Claude writes created: PENDING or omits the field
- Use user_time_v0 for real Sydney time before writing
- HLC field is daemon-only — never LLM-generated

CAUGHT BY
Dave, in conversation. Before any fabrications landed in Reminders. Pre-write catch — best case.

LINKS
[[Schema v1.1 y1a2m3l4]] :: enforced_by
[[Apple Brain skill sk1ll4b]] :: applies_to
```

---

## Decision (decision.atomic)

**List:** `ab.knowledge`
**Title:** `Decision human vs agent boundary h2v3a4w5`

```
---
sid: h2v3a4w5
type: decision.atomic
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Human vs agent write boundary
tags: [governance, schema, v1-trigger]
---

Decision human vs agent boundary

The line between v0 simple schema and v1 extended schema is whether the writer is human-prompted or schedule-triggered.

HUMAN WRITE (v0 simple schema)
- Voice → Claude → Reminders, in active human time
- Side Reminder CLI invoked by Dave
- Claude Code slash commands triggered by Dave

AGENT WRITE (v1 extended schema)
- Daemon nightly lint report
- Scheduled background sync
- Any process running on a clock or trigger Dave set earlier but isn't watching now

THE TEST
Active = human. On its own = agent. Schedules cross the line, technology doesn't.

LINKS
[[Schema v1.1 y1a2m3l4]] :: codified_in
[[Apple Brain 8e2d1f4a]] :: governs
```

---

## Origin (origin.atomic)

**List:** `ab.knowledge`
**Title:** `Origin reminders as agent surface v1c2c3s4`

```
---
sid: v1c2c3s4
type: origin.atomic
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Reminders as voice-driven agent surface
discovered_via: [a1r2s3c4]
spark_from: [v1d2e3o4]
tags: [origin, voice, reminders, synthesis]
---

Origin reminders as agent surface

Independent synthesis. Emerged from running arscontexta against multiple unrelated problems and noticing that Apple Reminders was the only surface satisfying all four constraints (voice, mesh, agent permissions, decay resistance).

DISTINGUISHES FROM
- Karpathy's wiki (consumption, not execution)
- Side Reminder (existed before, but not the trigger)
- Building a Second Brain (human cognitive, not agent cognitive)

WHY THIS MATTERS
Origin atoms exist so the lineage is honest.

LINKS
[[Arscontexta pattern a1r2s3c4]] :: thinking_tool
[[Voice-to-Claude-Code video v1d2e3o4]] :: spark_from
```

---

## Influence (influence.atomic)

```
---
sid: k1a2r3p4
type: influence.atomic
status: active
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Karpathy LLM wiki
url: https://github.com/karpathy/...
tags: [influence, knowledge-graph, ai]
---

Influence Karpathy LLM wiki

Andrej Karpathy's pattern: dump raw sources into a folder, LLM continuously maintains a wiki of interlinked markdown files. Strong for knowledge ingestion and discovery.

DIVERGES FROM APPLE BRAIN
Karpathy's wiki is consumption-oriented. Apple Brain is execution-oriented. Reminders integration removes friction Karpathy's filesystem approach can't match.

LINKS
[[Apple Brain 8e2d1f4a]] :: derived_from
```

---

## MOC (moc.concept)

**List:** `ab.knowledge`
**Title:** `MOC Apple Brain m1c2o3c4`

```
---
sid: m1c2o3c4
type: moc.concept
status: active
created: 2026-04-27T02:36:22+1000
parent: 8e2d1f4a
unit_count: 13
---

MOC Apple Brain

Constellation map. Updated whenever atoms are added, archived, or restructured.

SUBSTRATE
[[Side Reminder s1d3r3m1]] :: substrate_for

ARCHITECTURE
[[Schema v1.1 y1a2m3l4]] :: component_of
[[Apple Brain skill sk1ll4b]] :: governs

GOVERNANCE
[[Lesson synthesis after atoms l1s2y3n4]] :: codified_in

PROJECTS UNDER APPLE BRAIN UMBRELLA
[[Dubai move d2b4y1m5]] :: parallel_project
[[United AI incubator u1t4d1a1]] :: parallel_project
[[Personality cloning ethics p1c2l3n]] :: parallel_project

ENTITIES
[[Mickey c7r2y9p4]] :: appears_in
[[Mustafa VC m6st4f4v]] :: appears_in
[[Push-email inventor p8sh3m4l]] :: appears_in

STATUS
v0 substrate live. 13 seed atoms written. Schema v1.1 active. Daemon not yet built.
```

---

## Skill (skill.atomic)

```
---
sid: sk1ll4b
type: skill.atomic
status: active
version: 1.0
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Apple Brain skill
self_editable: true
tags: [skill, governance, recursive]
---

Apple Brain skill

[Full skill content lives in the SKILL.md file of this skill folder. The atom in Reminders is a pointer to canonical version.]

CANONICAL SOURCE
This skill folder, version 1.0.

LINKS
[[Apple Brain 8e2d1f4a]] :: governs
[[Schema v1.1 y1a2m3l4]] :: enforced_by
[[D5 d5m3sh1]] :: sibling_of
```

---

## Opportunity (opportunity.atomic)

```
---
sid: c1b2m3h
type: opportunity.atomic
status: draft
created: 2026-04-27T02:36:22+1000
updated: 2026-04-27T02:36:22+1000
device: iphone
name: Children's book — AI + mental health series
ai_angle: voice cloning, AI therapists
tags: [opportunity, mental-health, ai, dubai]
---

Children's book mental health opportunity

Psychiatrist mentioned a children's book series about mental health (Australian animals). Suggested writing an AI-themed book.

WHY THIS MATTERS
Connects to voice cloning work (dementia, stroke recovery). Positions you for therapeutic AI angle. Valuable for Dubai positioning with United AI.

NEXT STEP
Ask psychiatrist for: series name, submission process, age group.

LINKS
[[Personality cloning ethics p1c2l3n]] :: application_of
[[Psychiatrist handover p1s2h3o]] :: ask_during_contact
```

---

## Schema (schema.atomic)

The schema atom is itself written in the schema. Self-referential. See the live `Schema v1.1 y1a2m3l4` atom in `ab.knowledge` for the canonical instance, and `references/schema.md` in this skill folder for the full spec.
