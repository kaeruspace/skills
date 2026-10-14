# Kaeru Command: `init`

First-run setup, dependency check, and automated codebase grounding protocol.  
Triggered via `/kaeru init` or when context files are missing.

---

## Initialization Workflow

### 1. Preserve Existing Files
If `AGENTS.md`, `PRODUCT.md`, `SYSTEM.md`, `DESIGN.md`, or `DECISIONS.md` exist, rename to `*.old.md` to preserve prior context.

### 2. Skill Dependency Gate (Fail Fast)
Verify core skills exist in `.agents/skills/` (planning, engineering, taste, refactoring).  
If ANY required skill is missing, **FAIL FAST immediately** with `[KAERU DEPENDENCY GATE: BLOCKED]` and output exact install commands. Halt until present.

### 3. Preflight Setup Interview (`@interview-me`)
Ask one focused question at a time:
```markdown
### Kaeru Setup & Mission Alignment
1. Persona & Mimicry Dial [0 | 1 | 2]: Character name, depth (0 = dry, 1 = subtle [Default], 2 = deep persona).
2. Trust & Pushback Dial [0 | 1 | 2]: (0 = high trust, 1 = sparring [Default], 2 = anti-bloat inquisitor).
3. Project Mission & Surface: Core problem (1-2 sentences), Audience, Surface (`Persuade` | `Operate` | `Read` | `Experience`).
4. Aesthetic Direction: Visual doctrine, initial dials: VARIANCE [1–10], MOTION [1–10], DENSITY [1–10].
5. Immediate Objective: What do you want to build or achieve first?
```
Save entries to `AGENTS.md`, `PRODUCT.md`, and `DESIGN.md`.

### 4. Grounding Scan (Auto-Populate `SYSTEM.md`)
1. Copy lean templates from `skills/kaeru/assets/` to project root.
2. Scan repository (relative paths only):
   - Git ref: `git rev-parse --short HEAD` and timestamp.
   - Manifests: runtime, database/ORM, UI, and test toolchain.
   - File Index: `git ls-files` categorized into config, routes, models, libs, components, tests.
   - Schemas & Routes: extract active models and route entry points (mark Greenfield if none).
   - Reusable Primitives: scan utilities and UI components for subtractive inventory.
3. Write verified facts into `SYSTEM.md`.

### 5. Transition to Planning
Feed Immediate Objective directly into Turn 1 planning (`feat` or `fix`).
