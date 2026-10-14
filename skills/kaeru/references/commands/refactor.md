# Kaeru Command: `refactor`

Code and design refactoring, dead-code elimination, and structural simplification.
Triggered via `/kaeru refactor <logic|design> <description>`.

---

## Refactor Principles
1. **Domain Isolation**: `refactor: logic` = zero CSS/markup edits. `refactor: design` = zero logic/state edits.
2. **Subtractive Mandate**: Net LOC budget $\le 0$. Prune dead code, consolidate duplicates, respect Chesterton's Fence.
3. **Regression Parity**: All pre-existing automated tests must stay green.

---

## Phased Weapons
| Archetype | Phase 1 (Audit & Bounds) | Phase 2 (Restructure & Verify) | Phase 3 (Simplify & Solidify) |
|---|---|---|---|
| **`refactor: logic`** | Primary: `@api-and-interface-design` / Guard: `@doubt-driven-development` | Primary: `@test-driven-development` / Guard: `@full-output-enforcement` | Primary: `@ponytail` / Guard: `@ponytail-review` |
| **`refactor: design`** | Primary: `@redesign-existing-projects` / Guard: `@design-taste-frontend` | Primary: `@frontend-ui-engineering` / Guard: `@browser-testing-with-devtools` | Primary: `@no-ai-slop` / Guard: `@code-review-and-quality` |

---

## Single-Task Prompt Template

```markdown
# TASK: refactor: [logic | design] — [Phase 1 | Phase 2 | Phase 3]
[Target Files]: [relative paths from repo root]
[Subtractive Anchor]: Delete <deprecated paths>; Consolidate <duplicated logic/styles>
[Net LOC Budget]: <= 0 net LOC (Subtractive or LOC-neutral, verify via git diff --stat)
[Not-Doing]: [If logic: zero UI edits | If design: zero state/logic edits]

[Combat Weapons]:
- Primary: [Assigned skill]
- Guard: [Assigned guard]
- Invariant: @full-output-enforcement (zero stubs, drop-in refactoring)

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules.
Objective: [Clear refactoring outcome; zero external behavior regression]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Verify Target Files and tests. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE:
   - Phase 1: Freeze public interfaces (@api-and-interface-design) or audit dead tokens (@redesign-existing-projects).
   - Phase 2: Restructure logic slice-by-slice (@incremental-implementation) or migrate UI tokens (@frontend-ui-engineering).
   - Phase 3: Flatten complexity and prune helper functions (@ponytail, @code-simplification) or eliminate leftover CSS (@no-ai-slop).
   - FORBIDDEN: Accretion flags (`isLegacy`, `v2Mode`), orphaned types, defensive null masking, edits outside Target Files.
4. VERIFY & CURATE: Verify Net LOC with `git diff --stat` (delta <= 0). Sync SYSTEM.md/DESIGN.md. Present gotchas for DECISIONS.md. Escalate only on FAIL or PAUSE.
```
