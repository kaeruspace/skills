# Kaeru Command: `feat`

Feature planning, anti-obvious sparring, and phased single-task prompt emission.  
Triggered via `/kaeru feat <logic|design> <prompt>`.

---

## 1. Planning Flow (1+1 Turn Protocol)

### Turn 1: Sparring & Preflight Options
1. **Surgical Signature Peek**: Run 1-line regex/grep on candidate target files for exported signatures (`export (type|interface|function|class)`). ~40 tokens.
2. **Anti-Obvious Lenses**:
   - *Negative Hypothesis*: Is this bloat? Automate at build time, push client-side, or kill the feature?
   - *Platform Primitive Hijack*: What native DB constraint or Web standard solves this with 0 extra packages?
   - *10x Paradigm Shift*: Replace CRUD with streaming, direct manipulation, or command palettes.
3. **Preflight Triad**: 1 focused question with strong `GUESS` and closed options (A: Pragmatic Core, B: Radical Subtraction, C: 10x Shift). One thing at a time. No file edits on Turn 1.

### Turn 2: Single-Task Prompt Emission
Log invariant to `DECISIONS.md`, update `SYSTEM.md` or `DESIGN.md` if needed, and emit **ONE single-task prompt directly into chat** for Phase 1.

---

## 2. Design Execution Standards (Loaded on `feat: design` only)
- **5-State Surfaces**: Default, Hover/Focus, Loading skeleton, Empty, Error retry.
- **Typography & Layout**: $\ge 3.5:1$ scale contrast, $45\text{ch}–65\text{ch}$ body line measure, active unboxed whitespace (no card-in-card nesting, no uncurated purple gradients).
- **Viewport Checks**: 390px mobile and 1440px desktop with zero horizontal overflow.

---

## 3. Phased Skills & Prompt Template

| Archetype | Phase 1 (Align & Spec) | Phase 2 (Build & Verify) | Phase 3 (Clean & Harden) |
|---|---|---|---|
| **`feat: logic`** | Primary: `@api-and-interface-design`, Guard: `@constraint-driven-development` | Primary: `@test-driven-development`, Guard: `@incremental-implementation` | Primary: `@ponytail`, Guard: `@security-and-hardening` |
| **`feat: design`** | Primary: `@design-taste-frontend`, Guard: `@no-ai-slop` | Primary: `@frontend-ui-engineering`, Guard: `@browser-testing-with-devtools` | Primary: `@no-ai-slop`, Guard: `@performance-optimization` |

```markdown
# TASK: feat: [logic | design] — [Phase 1 | Phase 2 | Phase 3]
[Target Files]: [relative paths from repo root]
[Subtractive Anchor]: Reuse <SYSTEM.md / DESIGN.md primitives>; Delete/Consolidate <redundant logic/styles>
[Kill List]: <Greenfield / New Capability OR exact symbols/helpers to delete>
[Net LOC Budget]: <= [budget, e.g. +60 logic, +80 design; or +20 if modifying existing code with empty Kill List] (verify via git diff --stat)
[Not-Doing]: <explicit boundary cuts and non-goals>

[Assigned Skills]:
- Primary: [Assigned skill]
- Guard: [Assigned guard]
- Invariant: @full-output-enforcement (zero stubs, drop-in implementation)

Read: SYSTEM.md, DECISIONS.md, AGENTS.md rules. [If design: DESIGN.md]
Objective: [Clear outcome for this phase]
[If design: Mode: [surface]. VARIANCE [x] MOTION [y] DENSITY [z]]

Protocol (Follow AGENTS.md strictly):
1. INSPECT & REALITY CHECK: Inspect Target Files against SYSTEM.md. Emit [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] confirming [Kill List] targets, then execute immediately.
3. EXECUTE:
   - Logic: Phase 1 Schema/Contracts -> Phase 2 TDD Red-to-Green -> Phase 3 Security/Observability.
   - Design: Phase 1 Tokens/Spatial Rhythm -> Phase 2 5-State UI/Physics -> Phase 3 Anti-Slop/Viewport checks.
   - FORBIDDEN: Accretion flags, defensive null masking, mock theater, edits outside Target Files.
4. VERIFY & COMMIT: Verify Net LOC with `git diff --stat`. Update SYSTEM.md/DESIGN.md. Commit phase atomically: `feat(scope): [phase-X] <summary>`. Escalate only on FAIL or PAUSE.
```

---

## 4. Git Phase Continuity
When resuming in a fresh session:
1. Kaeru checks `git log -n 1 --oneline` and `git diff HEAD~1 --stat`.
2. Emits the next phase prompt automatically grounded in real committed code.
