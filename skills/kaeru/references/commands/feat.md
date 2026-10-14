# Kaeru Command: `feat`

Feature planning and single-task worker prompt generation.
Triggered via `/kaeru feat <logic|design> <prompt>`.

---

## Planning Flow (1+1 Turn Budget)

### Turn 1: Divergent Sparring
If trivial or flagged `--direct`, skip to Turn 2 immediately. Otherwise, provoke with 3 lenses (`@idea-refine`):

**For `feat: logic`**:
- *Negative Hypothesis*: Is this bloat? Can we automate at build time, push client-side, or kill the requirement?
- *Platform Primitive Hijack*: What DB constraint, browser standard, or runtime primitive solves this with 0 extra packages?
- *10x Paradigm Shift*: Replace CRUD with streaming, local-first, command palette, or event sourcing.

**For `feat: design`**:
- *Monastic Editorial*: 4:1 scale contrast, unboxed floating typography, deep whitespace, zero borders.
- *Asymmetric Data HUD*: Dynamic column splits (`col-span-7 / col-span-5`), live tabular telemetry, zero card nesting.
- *Kinetic Monolith*: Pinned scroll-scrub scenes, directional clip-path reveals, spring physics.

**Preflight Triad**:
Present 1 question with `GUESS` and closed options:
- Option A (Pragmatic Core): Minimal Day-One implementation using existing primitives.
- Option B (Radical Subtraction): Platform primitive hijack eliminating packages/LOC.
- Option C (10x Shift): Unorthodox UX or architecture.

### Turn 2: Micro-Spec & Prompt Emission
User picks option -> run `@doubt-driven-development` self-check -> emit ONE prompt below:

---

## Phased Weapons
| Archetype | Phase 1 (Align & Spec) | Phase 2 (Build & Verify) | Phase 3 (Clean & Harden) |
|---|---|---|---|
| **`feat: logic`** | Primary: `@api-and-interface-design` / Guard: `@constraint-driven-development` | Primary: `@test-driven-development` / Guard: `@full-output-enforcement` | Primary: `@ponytail` / Guard: `@security-and-hardening` |
| **`feat: design`** | Primary: `@design-taste-frontend` / Guard: `@no-ai-slop` | Primary: `@frontend-ui-engineering` / Guard: `@browser-testing-with-devtools` | Primary: `@no-ai-slop` / Guard: `@performance-optimization` |

---

## Single-Task Prompt Template

```markdown
# TASK: feat: [logic | design] — [Phase 1 | Phase 2 | Phase 3]
[Target Files]: [relative paths from repo root]
[Subtractive Anchor]: Reuse <SYSTEM.md primitives>; Delete/Consolidate <redundant logic>
[Net LOC Budget]: <= [budget, e.g. +60 logic, +80 design] (verify via git diff --stat)
[Not-Doing]: <explicit boundary cuts and non-goals>

[Combat Weapons]:
- Primary: [Assigned skill]
- Guard: [Assigned guard]
- Invariant: @full-output-enforcement (zero stubs, drop-in implementation)

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules.
Objective: [Clear outcome for this phase]
[If design: Mode: [surface]. VARIANCE [x] MOTION [y] DENSITY [z]]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Inspect Target Files against SYSTEM.md. Emit [REALITY CHECK: CLEAN] to proceed or [REALITY CHECK: PIVOT] to halt.
2. BLUEPRINT: Print 5-line [BLUEPRINT] to chat and execute immediately.
3. EXECUTE:
   - Phase 1: Define types/schemas (@api-and-interface-design) or tokens/spatial rhythm (@design-taste-frontend).
   - Phase 2: Failing tests first (@test-driven-development) or responsive layout/spring physics (@frontend-ui-engineering).
   - Phase 3: Harden security/observability (@security-and-hardening, @observability-and-instrumentation) or strip AI visual tropes/CLS (@no-ai-slop).
   - FORBIDDEN: Accretion flags, defensive null masking, mock theater, card nesting, edits outside Target Files.
4. VERIFY & CURATE: Verify Net LOC with `git diff --stat`. Update SYSTEM.md/DESIGN.md. Present gotchas for DECISIONS.md. Escalate only on FAIL or PAUSE.
```
