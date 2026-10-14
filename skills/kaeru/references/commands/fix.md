# Kaeru Command: `fix`

Bug isolation, reproduction testing, and surgical root-cause repair.  
Triggered via `/kaeru fix <prompt>`.

---

## 1. Fix Principles
1. **Verified Reproduction**: Write minimal failing automated test first; verify it fails on untouched code.
2. **Surgical Root Cause**: Fix root cause directly. Zero defensive `?.` masking, zero accretion wrapper flags.
3. **Blast Radius**: Zero unsolicited refactoring outside bug targets. Net LOC $\le +25$.

---

## 2. Planning Flow
1. Kaeru analyzes error trace / report and checks exported signatures (~40 tokens).
2. Settles fix strategy via 1-question preflight decision.
3. Emits **ONE single-task prompt directly into chat**.

---

## 3. Single-Task Prompt Template (Emitted Directly into Chat)

```markdown
# TASK: fix: [Bug Summary]
[Target Files]: [relative paths: reproduction test + failing source]
[Subtractive Anchor]: Fix at root cause; zero speculative wrapper layers.
[Net LOC Budget]: <= +25 net LOC (Surgical patch only, verify via git diff --stat)
[Not-Doing]: Zero unsolicited refactoring outside bug blast radius.

[Assigned Skills]:
- Primary: @debugging-and-error-recovery
- Guard: @test-driven-development
- Invariant: @full-output-enforcement

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules.
Objective: [Locate root cause, reproduce with test, apply surgical fix]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Inspect Target Files and trace data flow. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE:
   - Trace root cause (@debugging-and-error-recovery).
   - Write failing reproduction test and verify FAILURE (@test-driven-development).
   - Apply surgical root-cause patch (@incremental-implementation) -> Turn test green.
   - FORBIDDEN: Defensive null masking, accretion flags (`if (isFixEnabled)`), mock theater, editing files outside Target Files.
4. VERIFY & COMMIT: Verify full test suite green. Verify Net LOC <= +25 via git diff --stat. Commit: fix(scope): <summary>. Escalate only on FAIL or PAUSE.
```
