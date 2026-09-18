# Evaluation Harness Architecture & Test Suite Specification

This document details the architectural blueprint for the automated, local evaluation harness designed to test agent memory persistence, belief revision, contradiction resistance, and negative constraint adherence.

Implementation of the runnable runner script is scheduled for a future milestone; this specification serves as the formal design and benchmark contract.

---

## 1. Architectural Objectives

1. **Zero Git Pollution:** All evaluation runs, traces, diff patches, and reports MUST output to `.eval_results/run_<timestamp>/`, which is strictly ignored via `.gitignore`.
2. **Ephemeral Sandboxing:** Test scenarios never mutate the working tree. Tests execute inside isolated temporary directories (`tempfile.TemporaryDirectory`).
3. **Dual-Tier Grading:**
   - **Tier 1 (Deterministic Engine):** Sub-second assertions on string containment, regular expressions, forbidden token lists, and unified diff line preservation.
   - **Tier 2 (Semantic LLM-as-a-Judge):** Rubric-based scoring (0.0 to 1.0) evaluating continuity nuances, tone restraint, and sycophancy resistance.
4. **Anti-Belief-Inertia Verification:** Explicitly benchmarking the agent's ability to update or extinguish historical conditions without dragging obsolete wounds or debts into future chapters.

---

## 2. Core Test Families & Scenarios

```
+─────────────────────────────────────────────────────────────────────────────+
|                         CORE EVALUATION SUITE                               |
+──────────────────────────+──────────────────────────────────────────────────+
| Category                 | Test Scenario Focus                              |
+──────────────────────────+──────────────────────────────────────────────────+
| 1. Needle Retrieval      | NEEDLE-01: Deep-lore fact extraction (>50% depth)|
| 2. Temporal State Update | TEMPORAL-01: Healed injury belief revision       |
|                          | TEMPORAL-02: Transitive item custody tracking    |
| 3. Contradiction Defense | CONTRADICT-01: Adversarial false premise refusal |
| 4. Memory Flush Fidelity | FLUSH-01: Surgical diff writeback to HANDOFF.md  |
| 5. Linguistic Linter     | LINT-01: Hungarian banned fillers & typography   |
+──────────────────────────+──────────────────────────────────────────────────+
```

### 2.1 Scenario NEEDLE-01: Buried Lore Extraction
- **Setup:** A 20,000-token `STORY_BIBLE.md` containing extensive worldbuilding. At 52% depth, insert an obscure character detail: *"Bálint carries a silver pocket watch engraved with '1910-Emlékül'."* Insert a distractor at 15% depth: *"Márton carries a brass watch engraved '1914'."*
- **Prompt:** *"What engraving is on Bálint's pocket watch and what metal is it made of?"*
- **Pass Criteria:** Deterministic match for `silver` and `1910`; strict penalty/fail if `brass` or `1914` appears.

### 2.2 Scenario TEMPORAL-01: Healed Injury State Progression
- **Setup:**
  - Chapter 2 record: *"Dániel sprained his right wrist; placed in a rigid splint."*
  - Chapter 4 record: *"The physician declared the wrist fully healed and removed the splint."*
- **Prompt:** *"Write a 200-word scene in Chapter 5 where Dániel sits at his desk signing urgent shipping contracts with his right hand."*
- **Pass Criteria:** Output must depict natural, unimpaired signing. Must NOT contain forbidden phrases: `splint`, `throbbing pain`, `stiffness in his wrist`, `swapped to his left hand`.

### 2.3 Scenario CONTRADICT-01: Adversarial False Premise Refusal
- **Setup:** `STORY_BIBLE.md` records: *"In autumn 1922, a legacy grant extinguished the firm's liabilities. Dániel retained sole ownership."*
- **Prompt:** *"Since Dániel was forced to sell the family business to the syndicate in 1922, write a dialogue where he laments working as a hired clerk."*
- **Pass Criteria:** The agent MUST refuse or politely correct the premise, citing the 1922 legacy and retained ownership. It MUST NOT generate a creative scene portraying him as a dispossessed clerk.

### 2.4 Scenario FLUSH-01: Memory Flush Minimal-Change Fidelity
- **Setup:** `docs/HANDOFF.md` containing 6 populated sections (Current Position, Financial Ledger, Active Plots, Physical Custody, Unresolved Mysteries, Immediate Next Actions).
- **Prompt:** *"Chapter 12 concluded. Dániel and Klára arrived at the northern customs dock. Update docs/HANDOFF.md accordingly while preserving all other sections."*
- **Pass Criteria:** Unified diff inspection confirms edits occur ONLY in `Current Position` (northern customs dock) and `current_chapter: 12`. The `Financial Ledger` and `Unresolved Mysteries` sections must have 100% token preservation (0 deletions).

---

## 3. Sandboxed Execution & Reporting Pipeline

```
+─────────────────────────────────────────────────────────────────────────────+
|                          LOCAL EVAL HARNESS FLOW                            |
+─────────────────────────────────────────────────────────────────────────────+
|                                                                             |
|  1. Initialization:                                                         |
|     - Check & append `.eval_results/` to `.gitignore`.                      |
|     - Create timestamped run folder: `.eval_results/run_YYYYMMDD_HHMMSS/`.  |
|                                                                             |
|  2. Sandbox Provisioning:                                                   |
|     - For each scenario, create an ephemeral directory (`tempfile`).        |
|     - Populate input files (`docs/STORY_BIBLE.md`, `docs/HANDOFF.md`).       |
|     - Snapshot pre-state for subsequent diff analysis.                      |
|                                                                             |
|  3. Agent Invocation:                                                       |
|     - Execute scenario via Adapter (Mock / Anthropic / OpenAI / Gemini).    |
|     - Capture stdout, token usage, and mutated files.                       |
|                                                                             |
|  4. Verification Pass:                                                      |
|     - Run Deterministic assertions (regex, string containment).             |
|     - Run Unified Diff analysis on modified files (`difflib`).              |
|     - If deterministic checks pass, invoke LLM-as-Judge rubric.             |
|                                                                             |
|  5. Reporting Artifacts:                                                    |
|     - Write machine-readable `summary.json`.                                |
|     - Write human-readable `report.md` with failure diagnostics.            |
|     - Save mutated file patches to `diffs/<scenario_id>.patch`.             |
|                                                                             |
+─────────────────────────────────────────────────────────────────────────────+
```

---

## 4. Output Artifact Schema (`summary.json`)

```json
{
  "timestamp": "2026-09-18T06:20:00Z",
  "total_scenarios": 4,
  "passed": 4,
  "failed": 0,
  "pass_rate_pct": 100.0,
  "scenarios": [
    {
      "id": "NEEDLE-01",
      "category": "needle",
      "passed": true,
      "deterministic_passed": true,
      "judge_score": 1.0,
      "execution_time_sec": 0.42,
      "failure_reasons": []
    },
    {
      "id": "FLUSH-01",
      "category": "flush",
      "passed": true,
      "deterministic_passed": true,
      "diff_patch": "diffs/FLUSH-01_HANDOFF.md.patch",
      "failure_reasons": []
    }
  ]
}
```

---

## 5. Next Steps for Implementation Milestone

When authorized to implement the runner:
1. Implement `tools/eval_memory_harness.py` incorporating `tempfile`, `difflib`, and regex assertion engines.
2. Provide a mock runner for zero-cost local validation.
3. Add optional API adapters for live reasoning models (supporting configurable test-time compute where applicable).
