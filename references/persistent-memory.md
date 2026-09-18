# AI-Native Persistent Memory & State Scaffolding

This reference defines the formal, machine-verifiable persistent memory architecture for AI-assisted long-form narrative generation and complex serial storytelling. It provides the procedural specifications, state schemas, lifecycle hooks, and anti-drift contracts required to maintain immaculate continuity across arbitrary session boundaries.

---

## 1. Architectural Motivation: Why Stateless Agents Fail

Large Language Models (LLMs) and autonomous reasoning agents are fundamentally stateless. Extended context windows (128k–1M+ tokens) do not solve long-horizon continuity; in practice, unmanaged context expansion introduces **Context Rot**:

1. **Belief Inertia:** Reasoning models with high test-time compute often over-rationalize obsolete narrative states. If a character is injured in Chapter 2, the agent may hallucinate lingering physical limitations in Chapter 8 despite explicit recovery in Chapter 4, anchoring to salient historical tokens.
2. **Epistemic Leakage:** Without hard knowledge partitioning, agents exhibit omniscient bleed—characters make decisions based on secrets revealed only in external viewpoints or private narrator commentary.
3. **Premature Reconciliation:** Models exhibit strong conversational sycophancy and friction-aversion, reflexively resolving interpersonal conflicts within 2–3 paragraphs and collapsing long-term dramatic tension.
4. **Context Tax & Attention Dilution ("Lost in the Middle"):** Naively injecting multi-thousand-word lore encyclopedias on every turn consumes 10–30% of the active token budget, dilutes attention weights, and degrades complex sentence-level instruction adherence by 10–15%.
5. **Honor-System Writeback Failure:** Under cognitive load or tool exhaustion, agents consistently skip post-generation state persistence unless constrained by deterministic lifecycle gates.

---

## 2. Two-Tier Memory Topology

To prevent token bloat, split-brain desynchronization, and memory amnesia, the system enforces a strict separation between **Invariant Ground Truth** and **Dynamic Working State**:

```
+─────────────────────────────────────────────────────────────────────────────+
|                         TWO-TIER MEMORY TOPOLOGY                            |
+─────────────────────────────────────────────────────────────────────────────+
|                                                                             |
|  TIER 1: INVARIANT GROUND TRUTH (`docs/STORY_BIBLE.md`)                     |
|  - Immutable world physical limits and canonical non-negotiables             |
|  - Core character psychological baselines and vulnerabilities               |
|  - Inter-character Trust Matrix (4 dimensions: competence, honesty,         |
|    vulnerability, accepting assistance)                                     |
|  - Epistemic Ledger (who knows what, when, and who holds false beliefs)     |
|  - Read on bootstrap; updated ONLY during major structural milestones       |
|                                                                             |
|                                     │                                       |
|                                     ▼                                       |
|                                                                             |
|  TIER 2: DYNAMIC RELAY BATON (`docs/HANDOFF.md` or `CURRENT_STATE.md`)      |
|  - Compact, single-file active context baton (< 1,000 words)                |
|  - Structured YAML Frontmatter for deterministic machine parsing            |
|  - Active plot friction, exact chronological timestamp, physical custody    |
|  - Immediate Next 3 Actions (zero startup ambiguity for next session)       |
|  - Rewritten / compacted at the conclusion of every session (Memory Flush)  |
|                                                                             |
+─────────────────────────────────────────────────────────────────────────────+
```

---

## 3. Machine-Readable Schema: `HANDOFF.md`

The active handoff document MUST begin with a validated YAML frontmatter block, followed by standardized markdown sections.

```markdown
---
schema_version: "1.0"
session_id: "YYYY-MM-DD-run-XX"
story_title: "The Silent Quarter"
current_chapter: 12
canonical_date: "1924-11-04"
canonical_time: "21:45"
location: "Harbor warehouse district, pier 4"
active_characters:
  - name: "Dániel"
    status: "Healthy, cold"
    held_items: ["customs ledger", "brass flashlight"]
  - name: "Klára"
    status: "Alert, observing"
    held_items: ["field notebook", "pocket watch"]
open_threads:
  - id: "THREAD-01"
    summary: "Unscheduled cargo vessel docking at pier 7"
    severity: "HIGH"
  - id: "THREAD-02"
    summary: "Discrepancy in the customs manifest for crate 402"
    severity: "MEDIUM"
next_3_actions:
  1: "Cross the railway spur toward warehouse B without alerting the guard."
  2: "Verify seal serial numbers against the master bill of lading."
  3: "Question the night dispatcher regarding the late departure of the tugboat."
invariant_constraints:
  - "Heavy freezing drizzle reduces visibility to fifty paces."
  - "Dániel and Klára must maintain formal professional address around crew members."
last_updated: "2026-09-18T22:00:00Z"
---

# Active Narrative State

## 1. Scene Setting & Physical Atmosphere
Exact physical environment, ambient temperature, sensory friction, and weather conditions.

## 2. Active Plot Friction & Dramatic Objective
What is actively resisting the protagonist? What immediate loss is at stake?

## 3. Epistemic Divergence & Secrets
- Character A knows: [X]
- Character B believes (falsely): [Y]
- Reader knows: [X and Y]

## 4. Physical Custody Register
- Key to warehouse B: In Dániel's coat pocket.
- Customs ledger: Locked in the inspector's leather satchel.
```

---

## 4. Anti-Belief-Inertia & Invalidation Protocol

To prevent reasoning models from perpetuating obsolete conditions:

### 4.1 The `[SUPERSEDED]` Invalidation Marker
When an established condition, injury, debt, or relational status changes, the previous record in `STORY_BIBLE.md` MUST NOT simply be deleted without a trace (which leads to hallucinated revival). It MUST be explicitly flagged:

```markdown
- [SUPERSEDED by Ch-08]: Dániel sprained left ankle [RESOLVED: Fully healed, bandage removed].
- [SUPERSEDED by Ch-05]: Unpaid warehouse bond [RESOLVED: Settled via municipal transfer].
```
Frontier reasoning models instantly register `[SUPERSEDED]` tags as hard negative suppression tokens, extinguishing belief inertia.

### 4.2 Active Compaction Cadence
- When `HANDOFF.md` exceeds 1,200 words, an automated **compaction pass** is triggered.
- Completed tasks and historical notes are collapsed into a single one-line summary in the log archive (`docs/EDITORIAL_LOG.md`).
- Only active friction, current items, and the immediate next 3 actions remain in `HANDOFF.md`.

---

## 5. Operational Lifecycle Hooks & Contracts

Every agent invocation MUST execute through three contractual phases:

### Phase 1: Bootstrap Hook (Pre-Execution Ingestion)
1. **Locate State Files:** Locate `docs/HANDOFF.md` (or external memory directory).
2. **Parse YAML Frontmatter:** Extract `current_chapter`, `canonical_date`, `active_characters`, and `invariant_constraints`.
3. **State Confirmation:** In reasoning traces, verify:
   - What is the current canonical date/time?
   - What physical limitations or injuries are active vs `[SUPERSEDED]`?
   - What items are currently held by whom?

### Phase 2: Execution & Constraint Gate
- Generate prose or plan chapters strictly constrained by the active state.
- **Negative Constraint Guard:** If user prompts contradict canonical records (e.g., demanding a character use a sold item or visit an inaccessible location), the agent MUST politely refuse the premise and preserve canon.

### Phase 3: Memory Flush Hook (Mandatory Post-Execution Writeback)
Before concluding any task that advances the story:
1. **State Delta Calculation:** Identify new facts introduced, items transferred, wounds sustained or healed, and promises made.
2. **Minimal-Change Writeback:** Update `docs/HANDOFF.md` using surgical diff edits. Do NOT delete untouched invariant sections.
3. **Advance Chapter & Timestamp:** Increment chapter count and update canonical time.
4. **Update Immediate Next 3 Actions:** Re-populate the 3 concrete next steps for the subsequent agent session.

---

## 6. Memory Topologies: In-Repo vs. External

The persistent memory system operates across two workspace configurations:

### Configuration A: In-Repo Workspace (Standard)
Memory files reside directly inside the project root:
```text
project-root/
├── docs/
│   ├── STORY_BIBLE.md          <- Permanent Canon & Trust Matrix
│   ├── HANDOFF.md              <- Active Working Baton
│   ├── WORKFLOW.md             <- Chapter Guidelines & Targets
│   └── EDITORIAL_LOG.md        <- Append-only Compaction Archive
```

### Configuration B: Out-of-Repo External Vault (Obsidian / Centralized)
For distributed setups or private user journals:
- The agent checks for an environment variable `IROIVENA_MEMORY_DIR` or a config key in `skill.json`.
- If set (e.g., `C:/Users/Alex/Documents/ObsidianVault/Stories/MyNovel/`), the agent reads and writes `STORY_BIBLE.md` and `HANDOFF.md` from the specified external directory while editing prose in the local workspace.
- If no local `docs/HANDOFF.md` exists and no external path is configured, the agent initializes a fresh `docs/HANDOFF.md` template during the Bootstrap Hook.
