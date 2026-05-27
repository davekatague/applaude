# Applaudé starter kit

Five atoms to paste in when you're just getting started. They give your brain an anchor and something to link future atoms to.

Paste each one into Reminders manually (title in the title field, everything below in the notes field), or ask Claude to write them for you:

> "I'm setting up Applaudé. Can you create a starter knowledge atom for how the system works, a goal for learning it, and a project for getting my setup right?"

---

## Atom 1 — How my second brain works (knowledge.atomic)

**List:** `Knowledge`
**Title:** `How my second brain works`

```
---
sid: k2br4n01
type: knowledge.atomic
status: active
created: PENDING
updated: PENDING
device: mac
name: How my second brain works
tags: [meta, applaud, system]
---

One idea per note. Plain YAML at the top, plain prose below. No markdown formatting because Reminders doesn't render it.

Every atom has a type (knowledge.atomic, lesson.atomic, task.atomic, etc.), a status, a timestamp, and a short mnemonic ID called a sid.

WikiLinks connect atoms: [[Another atom sid]] :: predicate

The four starter lists:
- Captures — raw unprocessed ideas, anything new
- Knowledge — processed notes, insights, lessons, decisions
- Goals — outcomes you're working toward
- Projects — active work with steps in progress

Capture fast. Process later. Link when it matters.

LINKS
[[Why I started this brain k3wh4s7t]] :: meta
```

---

## Atom 2 — Why I started this (knowledge.atomic)

**List:** `Knowledge`
**Title:** `Why I started this brain`

```
---
sid: k3wh4s7t
type: knowledge.atomic
status: active
created: PENDING
updated: PENDING
device: mac
name: Why I started this brain
tags: [meta, motivation, system]
---

Write the reason here. Two to four sentences.

What was the moment you realised you needed a better system for your thinking? What keeps falling through the cracks? What do you want to be able to find in six months?

This atom is for future-you. Update it when your reasons change.

LINKS
[[How my second brain works k2br4n01]] :: context_for
```

---

## Atom 3 — Get Applaudé set up properly (project.root)

**List:** `Projects`
**Title:** `Get Applaudé set up properly`

```
---
sid: p10nbd01
type: project.root
status: active
created: PENDING
updated: PENDING
device: mac
name: Get Applaudé set up properly
tags: [meta, setup, onboarding]
---

Setup checklist:
- Create 4 starter lists in Reminders (Captures, Knowledge, Goals, Projects)
- Set up whichever Claude surface you use (voice, Claude.ai, Desktop)
- Paste the bridge instructions into a Claude.ai project
- Write first 5 real atoms from your own life
- Establish a capture habit — voice or chat, at least once a day for a week

Done when: first week of real captures complete and weekly review done once.

LINKS
[[How my second brain works k2br4n01]] :: implements
```

---

## Atom 4 — First goal (goal.root)

**List:** `Goals`
**Title:** `[your goal here]`

```
---
sid: g04l1001
type: goal.root
status: active
created: PENDING
updated: PENDING
device: mac
name: [your goal here]
tags: [personal]
---

Replace this with your first real goal.

Keep it specific enough to know when you've hit it. Vague goals don't work — "be healthier" is not a goal, "run three times a week for eight weeks" is.

Success condition: [one sentence that's unambiguously true when done]

LINKS
[[Get Applaudé set up properly p10nbd01]] :: tracked_in
```

---

## Atom 5 — First lesson (lesson.atomic)

**List:** `Knowledge`
**Title:** `Lesson: capture fast, process later`

```
---
sid: l5c4pt1x
type: lesson.atomic
status: active
created: PENDING
updated: PENDING
device: mac
name: Capture fast, process later
tags: [meta, capture, habit]
---

The most common reason second brains fail: trying to perfectly categorise and tag in the same moment you have the idea.

The fix: use Captures as a frictionless inbox. Just get it in. Don't judge. Don't structure.

Processing is a separate pass — weekly review, or whenever Captures feels cluttered. Move good captures into Knowledge or Projects. Archive the rest.

WHY IT MATTERS
Thinking while capturing kills both activities. The brain wants to hold the thought, not file it.

LINKS
[[How my second brain works k2br4n01]] :: technique_for
```

---

## After pasting

Say to Claude:

> "I've pasted my starter atoms. Can you read my Knowledge list and tell me what's there?"

If the connection is working, Claude will list your atoms. From there, try:

> "I just read something interesting about [X]. Can you add it to my Captures?"
> "What do I know about my goals right now?"
> "Create a knowledge atom about [idea from today]."

The more you use it, the more useful it gets.
