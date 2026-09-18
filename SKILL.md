---
name: iroi-vena
description: High-craft Hungarian literary prose, syntax, dialogue dynamics, genre adaptation, and AI-native persistent memory scaffolding for agents. Applies when writing fiction, novels, short stories, chapters, or dialogue in Hungarian, maintaining story bibles and handoffs, managing character states, tuning Hungarian sentence rhythm (topic-focus), or ensuring long-form continuity across chats.
tags:
  - writing
  - creative-writing
  - hungarian-prose
  - fiction
  - storytelling
  - persistent-memory
  - continuity
---

# Írói Véna — High-Craft Hungarian Literary Engine

A complete, production-grade craft and memory system for generating, revising, and maintaining high-literary-quality Hungarian prose across genres. Eliminates typical generative AI weaknesses (adjective stacking, didactic endings, melodramatic explanations, gesture inflation, and anglicized sentence structure) while providing an **AI-native persistent memory scaffolding** (Story Bible, Current State, and Handoff protocols) to ensure flaw-free serial continuity across ephemeral chats.

---

## Modular Reference Router (On-Demand Loading)

Load the specific module required for the current task. Do not load the entire library into context at once:

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
7. **Mandatory Memory Flush:**
   Never conclude a drafting or revision session without updating the persistent memory records (`CURRENT_STATE.md` / `STORY_BIBLE.md`). A chapter is not done until the state is recorded.

---

## Procedural 4-Phase Workflow

### Phase 1: Memory Recovery & Context Setup
1. **Bootstrap Hook:** Locate `docs/HANDOFF.md` (or `CURRENT_STATE.md`) and `docs/STORY_BIBLE.md` (or check external memory vault). Parse the YAML frontmatter to extract current canonical date/time, active characters, physical custody, and invariant constraints.
2. **Task & Friction:** Identify the scene objective, the focal character's boundaries, and the physical friction of the environment.

### Phase 2: Drafting in Hungarian Thought Units
1. Draft directly into native Hungarian syntax (never translate an English mental outline).
2. Embed Hungarian modal particles (`hát`, `csak`, `ugyan`, `már`, `azért`) for natural subtext and pressure.
3. Engage non-visual sensory modalities (tactile friction, acoustic reverberation, olfactory presence, visceral interoception).
4. Apply the Action Halt Rule: terminate cleanly on the decisive action.

### Phase 3: Multi-Pass Editorial Verification
1. **Pass 1 — Story & Causality:** Did choices cause the outcome? Are injuries, tools, and secrets maintained without retroactive leakage? Verify anti-belief inertia (`[SUPERSEDED]` tags).
2. **Pass 2 — Hungarian Syntax & Restraint:** Read dialogue aloud. Are speech tags lowercase? Are periods omitted before tags? Are personal pronouns stripped? Are all binary explanations eliminated?
3. **Pass 3 — Typography & Morphology:** Verify dialogue dashes (`–`), quotation marks (`„…”`), and proper name suffixation.

### Phase 4: State Flush & Handoff
1. **Memory Flush Hook:** Execute minimal-change writeback to `docs/HANDOFF.md` updating YAML frontmatter (`current_chapter`, `canonical_date`, `canonical_time`, `held_items`, and `next_3_actions`).
2. Record newly established permanent world facts, broken/repaired trust, and changed relationships in `STORY_BIBLE.md`.
3. Provide a concise, clear handoff summary for the next session.
