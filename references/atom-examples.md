# Applaudé atom examples

Worked examples of every atom type, copy-pasteable. Read this when uncertain about format for a specific type.

All examples use placeholder sids — when writing real atoms, generate a mnemonic (7–9 lowercase alphanumeric chars) or `sha256(type:name:created_iso)[:8]` after fetching real time via `user_time_v0`.

---

## Capture (captures.atomic)

**List:** `Captures`
**Title:** `Idea from this morning's walk`

```
---
sid: c4pt1d34
type: captures.atomic
status: active
created: PENDING
updated: PENDING
device: iphone
name: Idea from this morning's walk
---

Frictionless inbox entry. No judgment, no structure needed yet.

What if the onboarding flow started with a voice capture rather than a form? Remove all the typing.

Process this into Knowledge or Projects during the next weekly review.
```

---

## Knowledge atom (knowledge.atomic)

**List:** `Knowledge`
**Title:** `Why spaced repetition works`

```
---
sid: k5sp4c3d
type: knowledge.atomic
status: active
created: PENDING
updated: PENDING
device: mac
name: Why spaced repetition works
tags: [learning, memory, retention]
---

Review information at increasing intervals. The spacing effect means fewer total reviews to retain something long-term.

The key insight: the brain consolidates memories during the gaps, not during the review. Anki operationalises this. Even informal re-exposure during weekly reviews gets most of the benefit.

LINKS
[[Second brain — what it actually is k2br4n01]] :: technique_for
```

---

## Person (people.atomic)

**List:** `People`
**Title:** `Sarah Chen`

```
---
sid: p3rs0n1
type: people.atomic
status: active
created: PENDING
updated: PENDING
device: iphone
name: Sarah Chen
relationship: colleague
tags: [design, product, network]
---

Product designer at a fintech startup. Met at the design systems conference last year.

Strong opinions on accessibility. Mentioned she uses voice notes for everything — worth asking about her capture workflow.

LINKS
[[Design systems conference 2026 e1v3nt02]] :: met_at
```

---

## Goal (goal.root)

**List:** `Goals`
**Title:** `Build a freelance pipeline with 3 recurring clients`

```
---
sid: g0al1r00
type: goal.root
status: active
created: PENDING
updated: PENDING
device: mac
name: Build a freelance pipeline with 3 recurring clients
tags: [career, freelance, financial]
---

Not 10 clients. Three. Recurring engagements, not one-off projects. That's the difference between a freelance business and a freelance hustle.

Success condition: three clients on monthly retainers, covering baseline expenses.

LINKS
[[Portfolio redesign for consulting positioning p0rt101]] :: achieves
[[AI workflow consulting offer p0rj1c02]] :: achieves
```

---

## Project root (project.root)

**List:** `Projects`
**Title:** `Portfolio redesign for consulting positioning`

```
---
sid: p0rt101
type: project.root
status: active
created: PENDING
updated: PENDING
device: mac
name: Portfolio redesign for consulting positioning
tags: [website, freelance, positioning]
---

Current portfolio was designed for job hunting. Need to reframe everything for inbound consulting.

STEPS
- Audit current site
- Define positioning statement
- Rewrite copy
- New case studies
- Launch

LINKS
[[Build a freelance pipeline with 3 recurring clients g0al1r00]] :: achieves
```

---

## Task (task.atomic)

**List:** `Tasks`
**Title:** `Email Sarah about her voice capture workflow`

```
---
sid: t4sk1d01
type: task.atomic
status: active
created: PENDING
updated: PENDING
device: iphone
name: Email Sarah about her voice capture workflow
---

She mentioned she uses voice notes for everything. Worth understanding her system before building my own capture habit.

LINKS
[[Sarah Chen p3rs0n1]] :: contact
```

---

## Lesson (lesson.atomic)

**List:** `Knowledge`
**Title:** `Lesson: never fabricate timestamps`

```
---
sid: l4t1m3st
type: lesson.atomic
status: active
severity: critical
created: PENDING
updated: PENDING
device: claude-voice
name: Never fabricate timestamps
applies_to: [schema, all-atoms]
tags: [time, integrity, fabrication]
---

Claude has no authoritative clock. Any timestamp written into an atom is a guess at best, fiction at worst. Both corrupt the record.

RULE
Use user_time_v0 for real local time. Write created: PENDING if unavailable. Never invent ISO timestamps.

WHY IT MATTERS
Timestamps are load-bearing for replay, history, and warehouse integrity. Fabricated dates make "what did I think on March 1st" permanently unreliable.

LINKS
[[Applauded schema k5ch3m4]] :: enforced_by
```

---

## Decision (decision.atomic)

**List:** `Knowledge`
**Title:** `Decision: human vs agent write boundary`

```
---
sid: h2v3a4w5
type: decision.atomic
status: active
created: PENDING
updated: PENDING
device: mac
name: Human vs agent write boundary
tags: [governance, schema, v1-trigger]
---

The line between v0 simple schema and v1 extended schema is whether the writer is human-prompted or schedule-triggered.

HUMAN WRITE (v0)
- Voice to Claude to Reminders, in active human time
- MCP write triggered by the user right now

AGENT WRITE (v1)
- Daemon nightly lint
- Scheduled background sync
- Any process running on a clock the user set earlier but isn't watching now

THE TEST
Active human present = human write. Running on its own = agent write.
```

---

## MOC (moc.concept)

**List:** `Knowledge`
**Title:** `MOC second brain system`

```
---
sid: m0c1br4n
type: moc.concept
status: active
created: PENDING
updated: PENDING
device: mac
name: MOC second brain system
unit_count: 8
---

Constellation map for the second brain knowledge cluster.

CORE CONCEPT
[[Second brain — what it actually is k2br4n01]] :: defines

TECHNIQUES
[[Why spaced repetition works k5sp4c3d]] :: technique_for
[[Capturing vs processing k9c4pt01]] :: technique_for

PROJECTS USING THIS SYSTEM
[[Portfolio redesign for consulting positioning p0rt101]] :: uses
[[Knowledge system setup p5f6g7h8]] :: meta_project

STATUS
Four starter lists active. Weekly review habit forming.
```
