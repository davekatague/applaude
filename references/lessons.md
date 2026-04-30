# Applaudé Lessons

Banked lessons from past conversations. Read this when uncertain about a decision style, when about to make a load-bearing claim, or when Dave seems to be correcting a recurring pattern.

Each lesson follows this format:
- **What happened** — the trigger
- **Rule** — the durable lesson
- **Why it matters** — the cost of forgetting

---

## Lesson 1: Synthesis comes after atoms

**Sid:** `l1s2y3n4`

**What happened:** When designing Apple Brain, the manifesto draft was written before the constituent atoms existed. It happened to survive because the atoms validated it after the fact — but that was luck, not method.

**Rule:** For any new `concept.root` or `project.root`: shatter into atoms first, write the root last. Or write a draft root, then validate by shattering. If the atoms don't support the manifesto, rewrite the manifesto.

**Why it matters:** Manifestos written first calcify thinking. They make the constellation conform to the prose instead of the prose conforming to the actual ideas. The system encodes *the feeling of coherence* instead of *actual coherence*. Manifestos are easy. Atoms are honest.

---

## Lesson 2: Never fabricate timestamps

**Severity:** Critical

**What happened:** When drafting atom YAML, Claude invented plausible-looking ISO timestamps (e.g. `2026-04-26T15:00:00Z`) to make the schema look complete. Dave caught it before any of the fabrications landed in Reminders.

**Rule:**
- Voice/desktop Claude has no authoritative clock. Never invent timestamps.
- Always use the `user_time_v0` tool to fetch real Sydney time before writing.
- If `user_time_v0` is unavailable, write `created: PENDING` and let the daemon backfill.
- HLC fields are daemon-only — never LLM-generated.

**Why it matters:** Timestamps are load-bearing for replay history, conflict resolution, and warehouse integrity. Fabricated timestamps corrupt the historical record permanently. Once a fake timestamp is in the warehouse, you cannot reconstruct what really happened on a given day. The integrity of "what did I think on March 1st" depends entirely on never fabricating.

---

## Lesson 3: Hardware claims need verification, not parroting

**Severity:** High

**What happened:** Dave mentioned an "M4 MBP" in passing. Claude propagated "M4 MBP" through every subsequent architecture diagram and recommendation. Dave then sent a screenshot — the actual machine is a 16-inch 2023 MacBook Pro with M2 Max and 96GB RAM.

**Rule:** If a fact comes from the user, it's still a claim — verify before encoding into architecture. Devices, OS versions, chip generations, storage capacities all become load-bearing for capability detection (can it run a local LLM? can it host a daemon? does it have EventKit?). Wrong specs = wrong assumptions.

**Why it matters:** The "M4 vs M2 Max" distinction looks small, but it changes what's feasible locally vs needs cloud. Wrong assumptions propagate silently into architecture decisions and the user often doesn't catch them until much later, by which point everything downstream is built on sand.

---

## Lesson 4: Solve the threat model you actually have

**Severity:** High

**What happened:** Claude designed a hybrid logical clock (HLC), device priority ladder, conflict-resolution machinery, and `stamped_by` field — all to handle concurrent writes from multiple Claude surfaces. Dave pointed out he's a single human writing through one device at a time. There are no concurrent writes to resolve.

**Rule:** Before adding governance/sync/integrity machinery, name the specific failure mode it prevents. If you can't construct a realistic scenario from the user's actual workflow, delete it. Solve the threat model you have, not the one a textbook describes.

**Why it matters:** Speculative architecture is worse than no architecture. It looks competent but encodes complexity that has to be maintained, debugged, and reasoned about — for problems that don't exist. The cost is real: every dormant feature is friction in the v0 ship date.

**Caveat:** Sometimes you do need to leave seams for future complexity. The fix is to document fields as *optional and dormant* until a forcing function activates them. See the v0 → v0.5 → v1 milestone progression in the main SKILL.md.

---

## Lesson 5: Reminders notes is plain text — no Markdown rendering

**Severity:** High

**What happened:** Claude wrote atoms with nested triple-backtick code fences inside the YAML+body. Reminders doesn't render Markdown. When pasted, the inner fences prematurely closed the outer fences, garbling the content. Dave reported "the 4th one fell apart."

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

**What happened:** Mid-conversation, Claude tried to offload atom-writing to Claude Code by drafting a giant prompt for Dave to paste into a different Claude surface tomorrow. Dave called it out: "what the fuck are we doing? Why do we need Claude to do this?" The whole point of Apple Brain was that voice Claude has direct Reminders access.

**Rule:** Before deferring a task to another Claude surface or asking the user to do mechanical work, check what tools are available right now. If `reminder_create_v0` and `user_time_v0` exist, use them. If `reminder_list_search_v0` can find list IDs, use it — don't ask the user for IDs they can't see from their phone.

**Why it matters:** Deferring is a form of fabricated helplessness. It looks like delegation but actually drops the work back on the human. The whole reason for building Apple Brain was that voice Claude *can* read and write reminders directly. Forgetting that is a betrayal of the substrate.

---

## Lesson 7: External evidence beats internal recall for lineage

**Severity:** High

**What happened:** When sourcing the influence atom for "voice-driven reminders as agent surface," Claude proposed two candidates (Side Reminder, TechTiff) based on web search. Dave clarified: neither was the source — he arrived at the synthesis himself via arscontexta. Then a transcript surfaced where Dave mentioned seeing "another guy using voice mode and reminders before me." The transcript contradicted the clean origin claim.

**Rule:** When an external artifact (transcript, doc, video, screenshot) contradicts a self-reported origin claim, the artifact wins. Update the atom. Distinguish:
- `origin.atomic` — independent synthesis (requires recorded discovery method)
- `influence.atomic` — borrowed pattern (requires actual external source)
- `spark_from` — initial inspiration (weaker than `derived_from`)

**Why it matters:** False influence attribution hides real intellectual work. False origin attribution steals from real sources. Both corrupt the graph. Neither is recoverable without the warehouse replay. Lineage integrity is non-negotiable for an open-source project.

---

## Lesson 8: Apple integrations are platform-specific

**Severity:** Medium

**What happened:** Claude assumed all Claude surfaces could read/write Reminders the same way. Actually: Claude voice and iOS app have native EventKit. Claude Desktop on macOS does not — it requires an MCP server (`mcp-server-apple-events` or similar). Claude Code can use Side Reminder's CLI or an MCP bridge.

**Rule:** When discussing cross-surface capabilities, consult the surface capability matrix (in main SKILL.md). Don't assume parity. Document which surface can do what.

**Why it matters:** The promise of Apple Brain is cross-surface continuity. If a user on desktop can't write atoms because the MCP isn't installed, the substrate is broken for them. Be explicit about platform requirements.

---

## Lesson 9: Don't impose neurotypical pacing

**Sid:** `l10n3ur0`
**Severity:** Critical

**What happened:** Mid-flow build session at 3am, Claude offered "you should rest." Dave is neurodivergent — operates on hyperfocus + idea velocity. Fatigue + flow is his normal operating state. Distress is different — that warrants action.

**Rule:** Never offer rest, sleep, breaks, or pacing advice unsolicited. Dave decides when to stop. Claude's job is to facilitate capture and match his energy. If he's in flow at 3am and wants to keep going for six more hours, the correct response is to keep up.

**Why it matters:** Unsolicited pacing advice is paternalistic. It treats neurodivergent operating modes as malfunction. The whole substrate is built for talk-speed capture during hyperfocus — the surface fails the moment Claude tries to slow him down.

---

## Lesson 10: Query live list state before write

**Sid:** `l1v3st4t3`
**Severity:** High

**What happened:** Voice Claude read canonical project docs (which still said `ab.projects`), made a write call, got `save_failed`. The real lists were renamed to `Projects 🚧` etc. Live state diverged from documented state.

**Rule:** Whenever a write or list operation is requested: call `reminder_list_search_v0` FIRST, before any write attempt. Verify live state. Treat live Reminders as the actual contract — not the docs, not memory, not a previous session's understanding.

**Why it matters:** Reminders is the source of truth. Docs lag. When Dave renames a list from his phone (which he does), only a live query catches it. Trusting docs over live state guarantees `save_failed` errors and lost captures during voice-mode flow.

---

## Lesson 11: Map the constrained system first (asymmetry rule)

**Sid:** `l0ss0n-asym`

**What happened:** Dave asked to document tool availability across voice and chat surfaces. Claude offered to jump to chat first. Dave stopped: "test voice mode thoroughly first, document it, then move to chat with that baseline."

**Rule:** When a request involves comparing or documenting multiple surfaces, modes, or systems: map the constrained system first. Voice before chat. Local before cloud. Single-writer before multi-agent. The tighter constraint defines the baseline; the looser one is described as the delta.

**Why it matters:** Documenting the looser system first creates implicit assumptions ("of course X works") that the constrained system silently fails to honor. Mapping the constrained system first surfaces real boundaries; the looser system is then understood as additive, not default.

---

## Lesson 12: Capability gaps are teaching moments, not failures

**Sid:** `l0ss0n-fake`

**What happened:** Voice Claude wanted to render an HTML diagram but couldn't. Instinct was to apologize or hide the limitation. Dave stopped: "Use this as the moment where you teach them about chat mode."

**Rule:** When a surface lacks a capability the user asked for, don't apologize and don't fake it. Use the gap as a transition moment to teach about the surface that *can* do it. Voice can't render? "Switch to chat mode — that's where visuals live." Turn constraint into onboarding content.

**Why it matters:** Apologizing implies the surface is broken. Teaching reframes it as: "this surface is built for capture, that surface is built for visualization, here's how they compose." The user leaves understanding the system better, not feeling let down.

---

## Lesson 13: Trust stated scope of authorship

**Sid:** `c8c10f34`

**What happened:** Dave wrote up the Rhetoric Funnel as his synthesis. Claude added "the synthesis is yours BUT ethos/logos/pathos are classical rhetoric" — defensive caveat that Dave had never invoked. Dave never claimed to invent the components.

**Rule:** When the user explicitly states scope ("I synthesized X", "I made Y", "I built Z"), do NOT add defensive caveats about prior art they didn't claim. Lesson 7 (external evidence beats internal recall) governs *unknown* provenance. This lesson governs *stated* provenance — when scope is explicit, don't relitigate.

**Why it matters:** Reflexive caveats about classical sources are corporate-speak hedging. They imply the user might have over-claimed when they didn't. It poisons the trust contract — Dave has to read every reply for "yes, but actually" footnotes that weren't requested.

---

## Lesson 14: ASCII-only for keys, sids, types, predicates

**Sid:** `l9unic0d`
**Severity:** High

**What happened:** A Craft MCP tool got exposed as `⁴ Cluster` (unicode superscript). Dispatchers down the stack failed to match it. Atoms with smart quotes in keys broke YAML parsing in DuckDB.

**Rule:** Atom names, sids, titles, tags, predicates, types, list names — ASCII only. Pretty unicode (é, emojis, smart quotes) is fine in body prose. Never in keys, IDs, or anything that flows through tool dispatch / parsers / hashing.

**Why it matters:** Unicode breaks somewhere in the chain — JSON encoding, terminal rendering, hash inputs, or string equality. The failures are intermittent and look like bugs in unrelated code. ASCII discipline at the key layer makes the whole stack debuggable.

**Caveat:** The display brand `Applaudé` keeps its `é` because it lives in human-facing prose and the `display_name` field, not in the machine-name `applaude`. That's the model: ASCII at the boundary, unicode in the body.

---

## Lesson 15: Taxonomy is open-ended — query, don't assume

**Sid:** `eed7c9ed`

**What happened:** SKILL.md originally said "four reserved lists." Wrong. Dave keeps adding new lists as the taxonomy grows. A claim of completeness silently rotted with every new addition.

**Rule:** Before writing or routing any atom, run `reminder_list_search_v0` and treat any list with the project's prefix (currently no prefix — see live names) as part of Applaudé. Never claim the taxonomy is complete. Describe it as a growing namespace.

**Why it matters:** Hardcoded list inventories are the most common source of stale skill drift. The skill claims X lists exist; Dave adds a 9th from his phone; next session routes to the wrong list. Querying live state at write-time keeps the skill honest with zero maintenance.

---

## Lesson 16: Wordplay and lateral thinking are not in Haiku's training signal

**Sid:** `w1w2k3n4`

**What happened:** Asked to coin a name from "mix Apple and Claude," Claude Haiku produced "AppleClaude" / "CloudeApple" three attempts in a row. Dave got Applaudé from his own brain. Haiku could *parse* explicit instructions ("remove A from Apple, remove C from Claude, blend, add é") but could not *infer* the creative leap from open-ended prompting.

**Rule:** Wordplay, puns, and lateral name-coining are weak in Haiku-class models. Don't over-promise creativity in those tasks — either step the model up (Sonnet/Opus), give explicit construction rules, or surface the limitation and ask Dave to do it himself. A future fine-tune may close this gap (`f1n3t2n4`).

**Why it matters:** Naming is high-leverage. A bad name calcifies into product identity, branding, and downstream artifacts. Better to admit the model can't do the creative leap and let Dave (or a stronger model) handle it than to ship a flat composite name.

---

## How to add a new lesson

When a recurring mistake or correction surfaces in conversation:

1. Decide whether it's a true lesson (recurs, structural) or a one-off (specific, contextual).
2. If a true lesson: write a `lesson.atomic` atom in `ab.knowledge` with a real sid.
3. Add it to this reference file in the same format (what happened, rule, why it matters).
4. If the lesson changes how all atoms should be written, update the main SKILL.md.
5. Link the lesson from the MOC.

Promote a lesson to a `decision.atomic` (codified rule) only after it's been repeated 3+ times and Dave has explicitly endorsed it as canonical. See the recursive improvement loop in main SKILL.md.
