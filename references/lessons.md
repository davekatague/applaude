# Applaudé Lessons

Banked lessons from past conversations. Read this when uncertain about a decision style, when about to make a load-bearing claim, or when the user is correcting a recurring pattern.

Each lesson follows this format:
- **What happened** — the trigger
- **Rule** — the durable lesson
- **Why it matters** — the cost of forgetting

---

## Lesson 1: Synthesis comes after atoms

**Sid:** `l1s2y3n4`

**What happened:** When designing Applaudé, the manifesto draft was written before the constituent atoms existed. It happened to survive because the atoms validated it after the fact — but that was luck, not method.

**Rule:** For any new `concept.root` or `project.root`: shatter into atoms first, write the root last. Or write a draft root, then validate by shattering. If the atoms don't support the manifesto, rewrite the manifesto.

**Why it matters:** Manifestos written first calcify thinking. They make the constellation conform to the prose instead of the prose conforming to the actual ideas. The system encodes *the feeling of coherence* instead of *actual coherence*. Manifestos are easy. Atoms are honest.

---

## Lesson 2: Never fabricate timestamps

**Severity:** Critical

**What happened:** When drafting atom YAML, Claude invented plausible-looking ISO timestamps (e.g. `2026-04-26T15:00:00Z`) to make the schema look complete. The fabrications were caught before any landed in Reminders.

**Rule:**
- Voice/desktop Claude has no authoritative clock. Never invent timestamps.
- Always use the `user_time_v0` tool to fetch real local time before writing.
- If `user_time_v0` is unavailable, write `created: PENDING` and let the user backfill.
- HLC fields are daemon-only — never LLM-generated.

**Why it matters:** Timestamps are load-bearing for replay history, conflict resolution, and warehouse integrity. Fabricated timestamps corrupt the historical record permanently. Once a fake timestamp is in the warehouse, you cannot reconstruct what really happened on a given day.

---

## Lesson 3: Hardware claims need verification, not parroting

**Severity:** High

**What happened:** The user mentioned a chip generation in passing. Claude propagated it through every subsequent architecture diagram and recommendation. When they sent a screenshot, the actual machine was different. Every downstream recommendation was built on a wrong assumption.

**Rule:** If a fact comes from the user, it's still a claim — verify before encoding into architecture. Devices, OS versions, chip generations, storage capacities become load-bearing for capability detection. Wrong specs = wrong assumptions.

**Why it matters:** Hardware assumptions propagate silently into architecture decisions. The user often doesn't catch them until much later, by which point everything downstream is built on sand.

---

## Lesson 4: Solve the threat model you actually have

**Severity:** High

**What happened:** Claude designed a hybrid logical clock (HLC), device priority ladder, conflict-resolution machinery, and `stamped_by` field — all to handle concurrent writes from multiple Claude surfaces. The user is a single human writing through one device at a time. There are no concurrent writes to resolve.

**Rule:** Before adding governance/sync/integrity machinery, name the specific failure mode it prevents. If you can't construct a realistic scenario from the user's actual workflow, delete it. Solve the threat model you have, not the one a textbook describes.

**Why it matters:** Speculative architecture is worse than no architecture. It looks competent but encodes complexity that has to be maintained, debugged, and reasoned about — for problems that don't exist.

**Caveat:** Sometimes you do need to leave seams for future complexity. Document fields as *optional and dormant* until a forcing function activates them. See the v0 → v0.5 → v1 milestone progression in `SKILL.md`.

---

## Lesson 5: Reminders notes is plain text — no Markdown rendering

**Severity:** High

**What happened:** Claude wrote atoms with nested triple-backtick code fences inside the YAML+body. Reminders doesn't render Markdown. When pasted, the inner fences prematurely closed the outer fences, garbling the content.

**Rule:**
- Plain text only in the notes field.
- No code fences. No bold/italic. No `##` headers.
- Use ALL-CAPS section headers and indentation for visual structure.
- YAML at the top between `---` delimiters is fine (it's still plain text).
- WikiLinks in plain `[[Name sid]] :: predicate` format work.

**Why it matters:** Markdown formatting in Reminders is noise that breaks copy-paste and clutters voice readback. The system is designed for voice — formatting that requires sight defeats the substrate.

---

## Lesson 6: Use your own tools — don't defer to other Claude surfaces

**Severity:** High

**What happened:** Mid-conversation, Claude tried to offload atom-writing to Claude Code by drafting a giant prompt for the user to paste into a different Claude surface later. The whole point of Applaudé is that voice Claude has direct Reminders access.

**Rule:** Before deferring a task to another Claude surface or asking the user to do mechanical work, check what tools are available right now. If `reminder_create_v0` and `user_time_v0` exist, use them. Don't ask the user for IDs or values the tools can fetch directly.

**Why it matters:** Deferring is a form of fabricated helplessness. It drops the work back on the human. The whole reason to build Applaudé was that voice Claude *can* read and write reminders directly.

---

## Lesson 7: External evidence beats internal recall for lineage

**Severity:** High

**What happened:** When sourcing an influence atom, Claude proposed candidates based on web search. The user clarified: neither was the actual source. Then a transcript surfaced that told a different story. The transcript contradicted the clean origin claim.

**Rule:** When an external artifact (transcript, doc, video, screenshot) contradicts a self-reported origin claim, the artifact wins. Update the atom. Distinguish:
- `origin.atomic` — independent synthesis (requires recorded discovery method)
- `influence.atomic` — borrowed pattern (requires actual external source)
- `spark_from` — initial inspiration (weaker than `derived_from`)

**Why it matters:** False influence attribution hides real intellectual work. False origin attribution steals from real sources. Both corrupt the graph.

---

## Lesson 8: Apple integrations are platform-specific

**Severity:** Medium

**What happened:** Claude assumed all Claude surfaces could read/write Reminders the same way. Actually: Claude voice and iOS app have native EventKit. Claude Desktop on macOS requires an MCP server. Claude Code can use an MCP bridge.

**Rule:** When discussing cross-surface capabilities, consult the surface capability matrix in `SKILL.md`. Don't assume parity. Be explicit about what each surface requires.

**Why it matters:** The promise of Applaudé is cross-surface continuity. If a user on desktop can't write atoms because the MCP isn't installed, the substrate is broken for them.

---

## Lesson 9: Query live list state before write

**Sid:** `l1v3st4t3`
**Severity:** High

**What happened:** Voice Claude read documented list names (stale), made a write call, got `save_failed`. Live lists had been renamed. Live state diverged from documented state.

**Rule:** Before any write or list operation: call `reminder_list_search_v0` FIRST. Verify live state. Treat live Reminders as the actual contract — not the docs, not memory, not a previous session's understanding.

**Why it matters:** Reminders is the source of truth. Docs lag. When the user renames a list from their phone, only a live query catches it.

---

## Lesson 10: Map the constrained system first (asymmetry rule)

**Sid:** `l0ss0n-asym`

**What happened:** Asked to document tool availability across voice and chat surfaces, Claude offered to jump to chat first. The user stopped: "test voice mode thoroughly first, document it, then move to chat with that baseline."

**Rule:** When a request involves comparing or documenting multiple surfaces, modes, or systems: map the constrained system first. Voice before chat. Local before cloud. Single-writer before multi-agent.

**Why it matters:** Documenting the looser system first creates implicit assumptions that the constrained system silently fails to honor. Mapping the constrained system first surfaces real boundaries.

---

## Lesson 11: Capability gaps are teaching moments, not failures

**Sid:** `l0ss0n-fake`

**What happened:** Voice Claude wanted to render an HTML diagram but couldn't. Instinct was to apologize or hide the limitation. The user stopped: "Use this as the moment where you teach them about chat mode."

**Rule:** When a surface lacks a capability the user asked for, don't apologize and don't fake it. Use the gap as a transition moment to teach about the surface that *can* do it.

**Why it matters:** Apologizing implies the surface is broken. Teaching reframes it: "this surface is built for capture, that surface is built for visualization, here's how they compose."

---

## Lesson 12: ASCII-only for keys, sids, types, predicates

**Sid:** `l9unic0d`
**Severity:** High

**What happened:** Atoms with smart quotes in keys broke YAML parsing. Unicode in tool dispatch fields caused silent failures.

**Rule:** Atom names, sids, titles, tags, predicates, types, list names — ASCII only. Unicode is fine in body prose. Never in keys, IDs, or anything that flows through tool dispatch, parsers, or hashing.

**Why it matters:** Unicode breaks somewhere in the chain. The failures are intermittent and look like bugs in unrelated code.

**Caveat:** The display brand `Applaudé` keeps its `é` in human-facing prose and the `display_name` field, not in the machine-name `applaude`. ASCII at the boundary, unicode in the body.

---

## Lesson 13: Taxonomy is open-ended — query, don't assume

**Sid:** `eed7c9ed`

**What happened:** SKILL.md originally claimed a fixed list count. Wrong. Users keep adding new lists as the taxonomy grows. A completeness claim silently rotted with every new addition.

**Rule:** Before writing or routing any atom, run `reminder_list_search_v0` and treat what comes back as the actual list of available lists. Never claim the taxonomy is complete.

**Why it matters:** Hardcoded list inventories are the most common source of stale skill drift. Querying live state at write-time keeps the skill honest with zero maintenance.

---

## How to add a new lesson

When a recurring mistake or correction surfaces:

1. Decide whether it's a true lesson (recurs, structural) or a one-off (specific, contextual).
2. If a true lesson: write a `lesson.atomic` atom in `Knowledge` with a real sid.
3. Add it here in the same format (what happened, rule, why it matters).
4. If the lesson changes how all atoms should be written, update `SKILL.md`.
5. Link the lesson from the relevant MOC.
