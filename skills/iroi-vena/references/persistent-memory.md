# File-Based Story Memory & State Tracking

This reference describes a file-based memory workflow for long-form fiction projects. It outlines state schemas, handoff conventions, and lifecycle steps to help agents track narrative continuity across chat sessions.

---

## 1. Principles: Why Structured Memory is Required

Models are stateless across sessions. Long-horizon fiction without managed state tracking leads to:
- **Belief Inertia:** Clinging to obsolete states (e.g. treating a healed injury as an active impairment).
- **Epistemic Leakage:** Characters acting on secrets known only to the narrator or other viewpoints.
- **Attention Dilution:** Injecting entire lore archives on every turn degrades instruction following.

To resolve this, the system separates **Invariant Ground Truth** (`docs/STORY_BIBLE.md`) from **Dynamic Working State** (`docs/HANDOFF.md` and `docs/START_NEXT_CHAT.md`).

---

## 2. Two-Tier Memory Topology

```
+─────────────────────────────────────────────────────────────────────────────+
|                         TWO-TIER MEMORY TOPOLOGY                            |
+─────────────────────────────────────────────────────────────────────────────+
|                                                                             |
|  TIER 1: INVARIANT GROUND TRUTH (`docs/STORY_BIBLE.md`)                     |
|  - Immutable world rules, canonical timelines, and core psychological baselines|
|  - Inter-character Trust Matrix (competence, honesty, vulnerability, help)   |
|  - Epistemic Ledger (who knows what, when, and false beliefs)               |
|  - Read on bootstrap; updated ONLY during major structural milestones       |
|                                                                             |
|                                     │                                       |
|                                     ▼                                       |
|                                                                             |
|  TIER 2: DYNAMIC RELAY BATON (`docs/HANDOFF.md`)                             |
|  - Compact active context baton (< 1,000 words)                             |
|  - Structured YAML Frontmatter with referenced prior chapters               |
|  - Active plot friction, exact timestamp, and physical custody register     |
|  - Immediate Next 3 Actions for turn 1 of the following session             |
|  - Rewritten / compacted at the conclusion of every session (Memory Flush)  |
|                                                                             |
|                                     │                                       |
|                                     ▼                                       |
|                                                                             |
|  TIER 2B: TURN-1 FAST-START BATON (`docs/START_NEXT_CHAT.md`)               |
|  - Ultra-condensed ~150-word pasteable prompt for fresh chat sessions       |
|  - Synthesizes current chapter, active friction, and immediate target       |
|  - Automatically refreshed on session conclusion during Memory Flush        |
|                                                                             |
+─────────────────────────────────────────────────────────────────────────────+
```

---

## 3. Schema & Specifications: `HANDOFF.md`

`docs/HANDOFF.md` is the active relay baton between sessions. The authoritative template with full syntax and comments is maintained in [../templates/HANDOFF.template.md](../templates/HANDOFF.template.md).

### Required YAML Frontmatter Fields:
| Field | Type | Description |
| :--- | :--- | :--- |
| `schema_version` | String | Schema version (e.g. `"1.0"`). |
| `session_id` | String | Unique session identifier (`YYYY-MM-DD-run-XX`). |
| `story_title` | String | Working title of the story. |
| `current_chapter` | Integer | Active or most recently concluded chapter number. |
| `canonical_date` | String | In-universe calendar date (`YYYY-MM-DD`). |
| `canonical_time` | String | In-universe time of day (`HH:MM`). |
| `referenced_prior_chapters` | List | 2–3 specific past chapters where active items, injuries, or agreements originated. |
| `location` | String | Exact physical location and ambient constraints. |
| `active_characters` | List | Characters present, including name, status, and held items. |
| `open_threads` | List | Unresolved immediate plot threads with priority/severity. |
| `next_3_actions` | Map | Exactly 3 immediate, concrete actions for turn 1 of the next session. |
| `invariant_constraints` | List | Non-negotiable physical, atmospheric, or social constraints. |
| `last_updated` | String | ISO 8601 timestamp. |

### Core Markdown Sections:
1. **Scene Setting & Physical Friction:** Ambient temperature, physical obstacles, weather resistance.
2. **Active Plot Friction & Objective:** Immediate goal, stakes, and active resistance.
3. **Epistemic Divergence & Secrets:** Who knows what, who holds false beliefs, what the reader knows.
4. **Physical Custody Register:** Specific item custody and location (which pocket, bag, or shelf).

---

## 4. Anti-Belief-Inertia & Invalidation Protocol

### 4.1 The `[SUPERSEDED]` Invalidation Marker
When an established condition, injury, debt, or relational status changes, the previous record in `STORY_BIBLE.md` MUST NOT be deleted without a trace. It must be explicitly tagged:

```markdown
- [SUPERSEDED by Ch-08]: Dániel sprained left ankle [RESOLVED: Fully healed, bandage removed].
- [SUPERSEDED by Ch-05]: Unpaid warehouse bond [RESOLVED: Settled via municipal transfer].
```

Reasoning models register `[SUPERSEDED]` tags as hard negative suppression tokens, preventing belief inertia.

### 4.2 Compaction Cadence
- When `HANDOFF.md` exceeds 1,200 words, trigger a **compaction pass**.
- Collapse completed sub-tasks and resolved friction into single-line summaries in `docs/EDITORIAL_LOG.md`.
- Keep only active friction, current custody, and the immediate next 3 actions in `HANDOFF.md`.

---

## 5. Operational Lifecycle Hooks & Contracts

### Phase 1: Bootstrap Hook (Pre-Execution Ingestion)
1. **Locate Memory Root:** Check `IROIVENA_MEMORY_DIR` or `.iroi-vena.json` in `${workspaceRoot}`. Otherwise use `${workspaceRoot}/docs/`.
   - *Guard:* NEVER write memory files inside `${skillRoot}`.
2. **Template Bootstrap:** If missing, initialize from templates:
   - `${skillRoot}/templates/HANDOFF.template.md` -> `${workspaceRoot}/docs/HANDOFF.md`
   - `${skillRoot}/templates/STORY_BIBLE.template.md` -> `${workspaceRoot}/docs/STORY_BIBLE.md`
   - `${skillRoot}/templates/START_NEXT_CHAT.template.md` -> `${workspaceRoot}/docs/START_NEXT_CHAT.md`
3. **Parse State:** Extract date/time, active characters, physical custody, and constraints from `HANDOFF.md`.
4. **Verify Context:** Check active vs `[SUPERSEDED]` injuries, item custody, and referenced prior chapters.

### Phase 2: Execution & Constraint Gate
- Generate prose or plan chapters strictly within active constraints.
- **Negative Constraint Guard:** If user prompts contradict canon (e.g. using a sold item), politely refuse and preserve canonical integrity.

### Phase 3: Memory Flush Hook (Mandatory Post-Execution Writeback)
Before concluding any session that advances the story:
1. **Calculate State Delta:** Identify new facts, transferred items, and healed or sustained conditions.
2. **Surgical Writeback:** Update `HANDOFF.md` via minimal-change edits. Advance chapter number and canonical timestamp.
3. **Update Next 3 Actions:** Record 3 concrete steps for the next session.
4. **Update Story Bible:** Add new immutable facts or apply `[SUPERSEDED]` tags in `STORY_BIBLE.md`.
5. **Regenerate Fast-Start Baton:** Refresh `docs/START_NEXT_CHAT.md` using [../templates/START_NEXT_CHAT.template.md](../templates/START_NEXT_CHAT.template.md).

---

## 6. Workspace Isolation & Topologies

To prevent state loss across skill updates (`npx skills update` or git pulls), skills remain strictly read-only:

- **Installed Skill (`${skillRoot}`):** `.cursor/skills/iroi-vena/` or `.agents/skills/...` — contains read-only guidelines and templates. Replaced on update.
- **Author Workspace (`${workspaceRoot}`):** Contains the manuscript, `docs/STORY_BIBLE.md`, and `docs/HANDOFF.md`. Immune to skill updates.

### Configuration Modes:
- **Mode A (Standard In-Workspace):** `docs/` inside the author's novel repository.
- **Mode B (External Vault):** Configure external path via `IROIVENA_MEMORY_DIR` environment variable or `.iroi-vena.json` (`{"memory_dir": "/path/to/vault"}`).
- **Mode C (Skill Clone Guard):** If developing the skill directly from clone, live story files are gitignored. Always write creative projects in a separate workspace.
