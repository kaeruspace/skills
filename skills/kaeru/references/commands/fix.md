# Kaeru Command: `fix`

Bug isolation, reproduction testing, and surgical root-cause patching.
Triggered via `/kaeru fix <description>`.

---

## Fix Principles
1. **Verified Reproduction**: Write minimal failing automated test first; verify it fails on untouched code.
2. **Surgical Root Cause**: Fix root cause directly. Zero defensive `?.` masking, zero accretion wrapper flags.
3. **Blast Radius**: Zero unsolicited refactoring outside bug targets. Net LOC $\le +25$.

---

## Phased Weapons
| Archetype | Phase 1 (Isolate & Repro) | Phase 2 (Patch & Verify) | Phase 3 (Harden & Prevent) |
|---|---|---|---|
| **`fix: bug`** | Primary: `@debugging-and-error-recovery` / Guard: `@test-driven-development` | Primary: `@test-driven-development` / Guard: `@full-output-enforcement` | Primary: `@ponytail` / Guard: `@security-and-hardening` |

---

## Single-Task Prompt Template

```markdown
# TASK: fix: bug — [Phase 1 | Phase 2 | Phase 3]
[Target Files]: [relative paths: reproduction test + failing source]
[Subtractive Anchor]: Fix at root cause; zero speculative wrapper layers.
[Net LOC Budget]: <= +25 net LOC (Surgical patch only, verify via git diff --stat)
[Not-Doing]: Zero unsolicited refactoring outside bug blast radius.

[Combat Weapons]:
- Primary: [Assigned weapon]
- Guard: [Assigned guard]
- Invariant: @full-output-enforcement

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules.
Objective: [Locate root cause, reproduce with test, apply surgical fix]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Inspect Target Files and trace data flow. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE:
   - Phase 1: Trace root cause (@debugging-and-error-recovery) -> Write failing reproduction test and verify FAILURE (@test-driven-development).
   - Phase 2: Surgical root-cause patch (@incremental-implementation) -> Turn reproduction test green.
   - Phase 3: Boundary checks (@security-and-hardening) + minimal net diff (@ponytail) + structured logs if opaque (@observability-and-instrumentation).
   - FORBIDDEN: Defensive null masking, accretion flags (`if (isFixEnabled)`), mock theater, editing files outside Target Files.
4. VERIFY & CURATE: Verify full test suite green. Present gotcha for DECISIONS.md. Escalate only on FAIL or PAUSE.
```
