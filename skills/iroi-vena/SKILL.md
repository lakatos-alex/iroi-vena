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

Load the specific module required for the current task using your file reading tool (`view_file` or `read_file`) before drafting or planning. Do not load the entire library into context at once:

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
   When a physical gesture or silent exchange carries the emotional weight of a beat: **STOP**. Never append an explanatory sentence stating what the moment symbolized or how the character felt.
2. **Prohibition of Binary Explanations:**
   FORBIDDEN: Reflexive binary formulations (*„nem azért…, hanem…”*, *„nem X volt, csak Y”*). State the observed physical fact or immediate thought directly.
3. **No Thesis Endings:**
   Conclude scenes on an unresolved choice, a physical sound, or a sensory action—never on thematic summaries, relationship milestone speeches, or grand moral conclusions.
4. **No Gesture Inflation (A koreografált bábszínház tilalma):**
   Do not attach mechanical reactions (*„bólintott”, „felsóhajtott”, „megvonta a vállát”*) to every dialogue line. Use the pure dash (`–`) when the speaker is clear from context.
5. **Banned Transitional Fillers:**
   NEVER use: `hirtelen`, `egyszerre csak`, `valahogy`, `mintha`, `furcsa módon`. Introduce shifts through direct physical or acoustic interruption in the pre-verbal focus.
6. **Strict Hungarian Information Packaging:**
   Respect pre-verbal focus position. Invert verbal prefixes behind the verb under negation or focus. Strip redundant pronouns (`ő`, `ők`); identify subjects via concrete action rather than stock labels (*„a férfi”, „a lány”*).
7. **Workspace Isolation & Memory Immunity:**
   ALWAYS resolve and write memory records (`docs/HANDOFF.md`, `docs/STORY_BIBLE.md`) relative to `${workspaceRoot}`, NEVER inside `${skillRoot}`. State written to `${skillRoot}` is wiped on skill updates (`npx skills update`).
8. **Mandatory Memory Flush:**
   Never conclude a drafting session without updating persistent memory records (`docs/HANDOFF.md`, and `docs/STORY_BIBLE.md` when canon facts change). A chapter is not complete until state is recorded.
9. **The Tangible Title Rule (Kézzelfogható címadás szabálya):**
   Never generate abstract, didactic, or relative-clause titles (*„Aki…”*, *„Ami…”*, *„A ház, amely…”*). Derive titles strictly from a tangible object, a concrete location, or an observable physical condition (e.g. *„A kék mappa”*, *„A hibás relé”*, *„A zátony felőli szél”*, *„Két vödör forró víz”*).

---

## Procedural 4-Phase Workflow

### Phase 1: Memory Recovery & Context Setup
1. **Bootstrap Hook:** Locate `docs/HANDOFF.md`, `docs/STORY_BIBLE.md`, and `docs/START_NEXT_CHAT.md` in `${workspaceRoot}` (or external vault via `IROIVENA_MEMORY_DIR` / `.iroi-vena.json`). If missing, initialize from `${skillRoot}/templates/`.
2. **The 3-Chapter Lookback Hook:** Before drafting, identify and cite:
   - The immediate preceding chapter.
   - **2–3 relevant earlier chapters** where active items, injuries, promises, or address agreements originated.
3. **The 5 Scene Anchors Contract:** Before writing, lock in:
   - *Anchor 1 (Chronology & Climate):* Exact date, time, and weather/temperature resistance.
   - *Anchor 2 (Physical Labor / Work):* The concrete manual task occupying characters' hands.
   - *Anchor 3 (Address Register):* Active `tegezés` or `magázás`, accounting for any third party present.
   - *Anchor 4 (Independent Boundaries):* The focal character's non-negotiable limit where someone pushes back or says no.
   - *Anchor 5 (Custody of Tangibles):* Exact physical location of key items (pocket, bag, drawer).

### Phase 2: Drafting in Hungarian Thought Units
1. Draft directly into native Hungarian syntax without translating an English outline.
2. Embed modal particles (`hát`, `csak`, `ugyan`, `már`, `azért`) for authentic subtext and pressure.
3. Engage non-visual sensory modalities (tactile friction, acoustic reverberation, olfactory presence, interoception).
4. Apply the Action Halt Rule: terminate cleanly on the decisive action.

### Phase 3: Multi-Pass Editorial Verification
1. **Pass 1 — Causality & Continuity:** Did choices cause the outcome? Are active injuries and items preserved? Verify anti-belief inertia (`[SUPERSEDED]` tags).
2. **Pass 2 — Syntax & Restraint:** Read dialogue aloud. Check lowercase speech tags, stripped periods before tags, pronoun economy, and absence of binary cliches.
3. **Pass 3 — Typography & Morphology:** En-dashes (`–`), Hungarian quotation marks (`„…”`), correct suffixation on names.
4. **Pass 4 — Mechanical Linter:** Scan for residual drafting markers (`TODO`, `TBD`, placeholders `[...]`). Ensure dialogue punctuation conforms strictly to AkH. 260.

### Phase 4: State Flush & Handoff
1. **Memory Flush Hook:** Surgical writeback to `docs/HANDOFF.md` updating YAML frontmatter (`current_chapter`, `canonical_date`, `canonical_time`, `referenced_prior_chapters`, `held_items`, `next_3_actions`).
2. **Update Story Bible:** Record new permanent world facts, changed relationships, or `[SUPERSEDED]` tags in `docs/STORY_BIBLE.md`.
3. **Regenerate Fast-Start Baton:** Refresh `docs/START_NEXT_CHAT.md` using [templates/START_NEXT_CHAT.template.md](templates/START_NEXT_CHAT.template.md), providing a ready-to-paste ~150-word prompt for turn 1 of the next session.
