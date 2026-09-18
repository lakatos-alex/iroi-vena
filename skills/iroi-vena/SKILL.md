---
name: iroi-vena
description: Hungarian prose craft, syntax, dialogue dynamics, genre adaptation, and file-based story continuity for agents. Applies when writing fiction, novels, short stories, chapters, or dialogue in Hungarian, maintaining story bibles and handoffs, managing character states, tuning Hungarian sentence rhythm (topic-focus), or tracking long-form continuity across chats.
license: MIT
metadata:
  author: Alex Lakatos
  version: "1.2.0"
tags:
  - writing
  - creative-writing
  - hungarian-prose
  - fiction
  - storytelling
  - persistent-memory
  - continuity
---

# Írói Véna — Hungarian Fiction Writing & Continuity Guide

A craft guide and memory workflow for drafting, revising, and maintaining continuity in Hungarian fiction. Helps curb common model habits (such as anglicized word order, stacked adjectives, overexplained emotions, and repetitive gestures) while providing practical, file-based memory conventions (Story Bible, Current State, and Handoff notes) to support consistent serial storytelling across sessions.

---

## Modular Reference Router (On-Demand Loading)

Load the specific module required for the current task using your file reading tool (e.g. `view_file` or `read_file`) before drafting or planning. Do not load the entire library into context at once:

| Craft Domain | Reference Module | When to Load? |
| :--- | :--- | :--- |
| **Persistent Memory & Scaffolding** | [persistent-memory.md](references/persistent-memory.md) | Initializing a new story, recovering state on turn 1, maintaining Story Bibles, handoff notes, and cross-chat memory. |
| **Syntax, Rhythm & Sensory Lexicon** | [hungarian-prose.md](references/hungarian-prose.md) | Drafting new prose, sentence rhythm, verbal prefix inversion, topic-focus positioning, sensory depth, Free Indirect Discourse. |
| **Dialogue Typography & Registers** | [hungarian-typography.md](references/hungarian-typography.md) | Formatting dialogue, speech tags (`–`), T/V address (`tegezés/magázás`), digital communication (SMS/chat/email). |
| **Scene Craft & Narrative Pacing** | [scene-craft.md](references/scene-craft.md) | Real-time scene construction, physical friction, scene vs. summary balance, aftermath as plot, eliminating gesture inflation. |
| **Character Psychology & Trust** | [character-and-trust.md](references/character-and-trust.md) | Character motivation, the 4 dimensions of trust, care as labor vs. control, personal boundaries, repair costs. |
| **Continuity & Knowledge Ledger** | [continuity-and-knowledge.md](references/continuity-and-knowledge.md) | Managing the 5 epistemic states, object custody, physical limitations, commitments, and preventing retroactive contradictions. |
| **Genre Adaptation & Terminology** | [genre-profiles.md](references/genre-profiles.md) | Adapting voice to Contemporary Realist, Crime/Noir, Speculative (Sci-Fi/Fantasy), or Historical/Period fiction. |

---

## Core Invariant Constraints (Szigorú műhelyszabályok)

These procedural constraints override default LLM generation tendencies:

1. **The Action Halt Rule (Állj meg a cselekvésnél):**
   When a physical gesture, transferred object, or silent exchange carries emotional meaning: **STOP**. Never append an explanatory sentence clarifying what the moment symbolizes, what the character learned, or how the reader should feel.
2. **Prohibition of Binary Explanations:**
   STRICTLY FORBIDDEN: Reflexive binary explanations, especially forms of *„nem azért…, hanem…”*, *„nem X volt, csak Y”*, or listing rejected interpretations. State the observed physical fact or immediate live thought.
3. **No Thesis Endings:**
   Do not conclude scenes with thematic summaries, relationship milestones, or speeches about hope, equality, or destiny. End on an unresolved choice, a physical sound, a fading footstep, or a closed door.
4. **No Gesture Inflation (A koreografált bábszínház tilalma):**
   Do not attach a mechanical physical reaction (*„bólintott”, „felsóhajtott”, „megvonta a vállát”, „összehúzta a szemöldökét”*) after every spoken line. If the speaker is obvious from context, use the pure dash (`–`).
5. **Banned Transitional Fillers (Lusta átvezetők tilalma):**
   NEVER use: `hirtelen`, `egyszerre csak`, `valahogy`, `mintha`, `furcsa módon`. Introduce surprises through direct physical or acoustic interruption in the sentence focus.
6. **Strict Hungarian Information Packaging:**
   Respect the pre-verbal focus position. Invert verbal prefixes behind the verb under negation or focus. Omit redundant personal pronouns (`ő`, `ők`); disambiguate third-person subjects through concrete physical action, not clumsy stock phrases (*„a lány”, „a férfi”, „az előbbi”*).
7. **Workspace Isolation & Memory Immunity:**
   ALWAYS resolve and write memory records (`docs/HANDOFF.md`, `docs/STORY_BIBLE.md`) relative to the author's active workspace root (`${workspaceRoot}`), NEVER inside the skill's installation directory (`${skillRoot}`). Writing state into `${skillRoot}` causes total memory loss on skill updates (`npx skills update`).
8. **Mandatory Memory Flush:**
   Never conclude a drafting or revision session without updating the persistent memory records (`${workspaceRoot}/docs/HANDOFF.md`, and `docs/STORY_BIBLE.md` when canon facts change). A chapter is not done until the state is recorded.
9. **The Tangible Title Rule (Kézzelfogható címadás szabálya):**
   Never generate abstract, didactic, or relative-clause titles (*„Aki…”, „Ami…”, „A ház, amely…”*, *„A megújuló remény”*). Chapter and scene titles must derive strictly from a tangible physical object, a concrete location, or an observable physical condition (e.g. *„A kék mappa”*, *„A hibás relé”*, *„A zátony felőli szél”*, *„Két vödör forró víz”*).

---

## Procedural 4-Phase Workflow

### Phase 1: Memory Recovery & Context Setup
1. **Bootstrap Hook:** Locate `${workspaceRoot}/docs/HANDOFF.md`, `${workspaceRoot}/docs/STORY_BIBLE.md`, and `${workspaceRoot}/docs/START_NEXT_CHAT.md` (or check external memory vault configured via `IROIVENA_MEMORY_DIR` or `.iroi-vena.json`).
   - If missing in `${workspaceRoot}`, bootstrap immediately from templates:
     - `${skillRoot}/templates/HANDOFF.template.md` -> `${workspaceRoot}/docs/HANDOFF.md`
     - `${skillRoot}/templates/STORY_BIBLE.template.md` -> `${workspaceRoot}/docs/STORY_BIBLE.md`
     - `${skillRoot}/templates/START_NEXT_CHAT.template.md` -> `${workspaceRoot}/docs/START_NEXT_CHAT.md`
   - Parse the YAML frontmatter to extract current canonical date/time, active characters, physical custody, and invariant constraints.
2. **The 3-Chapter Lookback Hook:**
   - Before drafting or planning new scenes, explicitly locate and cite:
     a) The immediate preceding chapter.
     b) **2–3 relevant earlier chapters** where the active items, physical conditions, promises, or T/V relationships originated or last shifted.
   - Never treat an established capability or relationship step as a novel discovery.
3. **Pre-Draft Contract (The 5 Scene Anchors):**
   Before generating prose, verify and lock in:
   - *Anchor 1 (Chronology & Climate):* Exact date, time of day, and physical weather/temperature resistance.
   - *Anchor 2 (Physical Labor / Work):* What concrete manual/physical task occupies the characters' hands during the scene?
   - *Anchor 3 (Address Register):* Who addresses whom with `tegezés` or `magázás`, and does a third party's presence impose formal address?
   - *Anchor 4 (Independent Boundaries):* What is the focal character's non-negotiable limit in this scene? Where does someone say NO or push back?
   - *Anchor 5 (Custody of Tangibles):* Where are critical physical items located right now (which pocket, bag, shelf)?

### Phase 2: Drafting in Hungarian Thought Units
1. Draft directly into native Hungarian syntax (never translate an English mental outline).
2. Embed Hungarian modal particles (`hát`, `csak`, `ugyan`, `már`, `azért`) for natural subtext and pressure.
3. Engage non-visual sensory modalities (tactile friction, acoustic reverberation, olfactory presence, visceral interoception).
4. Apply the Action Halt Rule: terminate cleanly on the decisive action.

### Phase 3: Multi-Pass Editorial Verification
1. **Pass 1 — Story & Causality:** Did choices cause the outcome? Are injuries, tools, and secrets maintained without retroactive leakage? Verify anti-belief inertia (`[SUPERSEDED]` tags).
2. **Pass 2 — Hungarian Syntax & Restraint:** Read dialogue aloud. Are speech tags lowercase? Are periods omitted before tags? Are personal pronouns stripped? Are all binary explanations eliminated?
3. **Pass 3 — Typography & Morphology:** Verify dialogue dashes (`–`), quotation marks (`„…”`), and proper name suffixation.
4. **Pass 4 — Mechanical & Marker Linter:** Scan output for residual LLM drafting artifacts (`TODO`, `TBD`, placeholder tokens `[...]`, or cut-off generation fragments). Ensure dialogue dashes (`– `) are uniform and periods are stripped before lowercase speech tags.

### Phase 4: State Flush & Handoff
1. **Memory Flush Hook:** Execute minimal-change writeback to `${workspaceRoot}/docs/HANDOFF.md` updating YAML frontmatter (`current_chapter`, `canonical_date`, `canonical_time`, `referenced_prior_chapters`, `held_items`, and `next_3_actions`).
2. Record newly established permanent world facts, broken/repaired trust, and changed relationships in `${workspaceRoot}/docs/STORY_BIBLE.md`.
3. **Regenerate Fast-Start Baton:** Refresh `${workspaceRoot}/docs/START_NEXT_CHAT.md` using `${skillRoot}/templates/START_NEXT_CHAT.template.md`. Provide a single, ~100–150 word pasteable prompt containing the active status and immediate target for turn 1 of the next session.
