# Kaeru Command: `refactor`

Code and design refactoring, dead-code elimination, and subtractive restructuring.  
Triggered via `/kaeru refactor <logic|design> <prompt>`.

---

## 1. Refactor Principles
1. **Domain Isolation**: `refactor: logic` = zero CSS/markup edits. `refactor: design` = zero logic/state edits.
2. **Subtractive Mandate**: Net LOC budget $\le 0$. Prune dead code, consolidate duplicates, respect Chesterton's Fence.
3. **Design Refactoring Standards** (on `refactor: design`): Consolidate rogue hex tokens to `DESIGN.md`, flatten card nesting, prune unused styles.

---

## 2. Planning Flow
1. Kaeru runs Signature Peek (~40 tokens).
2. Settles plan via 1-question preflight decision.
3. Emits **ONE single-task prompt directly into chat**.

---

## 3. Single-Task Prompt Template

```markdown
# TASK: refactor: [logic | design] — [Target Component / Module]
[Target Files]: [relative paths from repo root]
[Subtractive Anchor]: Delete <deprecated paths>; Consolidate <duplicated logic/styles>
[Kill List]: <exact dead code, redundant branch, or legacy helper to permanently remove>
[Net LOC Budget]: <= 0 net LOC (Subtractive or LOC-neutral, verify via git diff --stat)
[Not-Doing]: [If logic: zero UI edits | If design: zero state/logic edits]

[Assigned Skills]:
- Primary: @ponytail
- Guard: @doubt-driven-development
- Invariant: @full-output-enforcement (zero stubs, drop-in refactoring)

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules. [If design: DESIGN.md]
Objective: [Clear refactoring outcome; zero external behavior regression]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Verify Target Files and tests. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE:
   - Logic: Freeze interfaces -> Restructure slice-by-slice -> Flatten complexity and prune dead helpers.
   - Design: Audit dead tokens -> Consolidate to DESIGN.md -> Flatten nested containers -> Verify 390px/1440px.
   - FORBIDDEN: Accretion flags, orphaned types, defensive null masking, edits outside Target Files.
4. VERIFY & COMMIT: Verify Net LOC <= 0 via `git diff --stat`. Sync SYSTEM.md/DESIGN.md. Commit: refactor(scope): <summary>. Escalate only on FAIL or PAUSE.
```
