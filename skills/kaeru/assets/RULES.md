# RULES.md: Architectural Invariants & Execution Rules

> [!IMPORTANT]
> **TEMPLATE NOTICE**: This file is a starter template. When initializing Kaeru in an actual project, update all rules according to your project specifications and remove this notice once configured.

---

## 1. Architectural Invariants

### Rule 1: Human Agency & Unrigged Exploration
The human makes the final architectural and design calls. Planners must present distinct directions with explicit trade-offs. Never reduce planning to a multiple-choice quiz with a pre-selected default. Never hide architectural costs or trade-offs.

### Rule 2: Zero-Footprint State
No temporary task files (`TASK.md`, `PROMPT.md`) or verification scripts in repo root. All phase continuity and diff tracking use native Git commits (`<type>(<scope>): [phase-X] <summary>`).

### Rule 3: Signature Peek Boundary
Planners read only context files and manifests. Implementation logic bodies are forbidden during planning. Inspect code bodies only through 1-line regex/grep queries for exported signatures (`export (type|interface|function|class)`).

### Rule 4: Mandatory Kill List
Every feature and refactor prompt requires an explicit `[Kill List]`. The worker blueprint must confirm targets removed. If no targets are identified when modifying existing code, the feature Net LOC ceiling drops to $\le +20$ lines.

### Rule 5: Subtractive Mandate & Net LOC Budgets
All code changes are governed by strict Net LOC ceilings verified via `git diff --stat`:
- `feat: logic`: $\le +60$ net lines
- `feat: design`: $\le +80$ net lines
- `refactor`: $\le 0$ net lines
- `fix`: $\le +25$ net lines
- `audit`: $< 0$ net lines
- **Greenfield Rule**: Brand-new code sets `[Kill List: Greenfield / New Capability]` (full budget). Modifying existing code with an empty Kill List is penalized to $\le +20$ lines.

### Rule 6: The Signal-Density Mandate ("Less Text")
High signal density > narrative volume. Strip conversational pleasantries, generic intros, and boilerplate fluff.
**NEVER truncate, omit, or compress operational protocols, verification checks, decision gates, or architectural invariants.**

---

## 2. Code Execution & Clean Code Rules

### Rule 7: Target File Lock
Workers modify only declared `[Target Files]`. Touching external files requires an immediate `PAUSE` and escalation.

### Rule 8: Relative Paths Only
All paths and imports must be relative to repo root (`src/lib/db.ts`). Zero absolute paths.

### Rule 9: Reality Check & The 5-Line Blueprint
Before writing code, workers must inspect target files against `CODEBASE.md` and report:
- `[REALITY CHECK: CLEAN]`: Codebase matches documented topology.
- `[REALITY CHECK: PIVOT]`: Discrepancy found; halt immediately with a concise discrepancy report.

Once clean, print this 5-line blueprint before writing code (do not wait for approval):
```markdown
[BLUEPRINT]
• Goal: <1 sentence what is being built or fixed>
• Files: <relative paths + 1-line responsibility each>
• Pattern: <architecture pattern: e.g. Server Action + Zod, Compound Reducer>
• Kill List Targets: <exact symbols or files confirmed for deletion>
• Invariant: <security rule or interface contract preserved>
```

### Rule 10: Day-One Standard (The 6 Clean Code Rules)
1. **No Temporary Flags**: No boolean flags (`isV2`, `skipAuth`, `useNewLogic`). Refactor core paths directly.
2. **No Defensive Null Masking**: No `?.`, `?? null`, or silent catches in domain logic. Validate at boundaries; fail fast.
3. **No Mock Theater**: Test real state transitions and outputs, not whether mock functions were called.
4. **No Duplicate Helpers**: Always check and reuse `CODEBASE.md` primitives before creating new utilities.
5. **No Premature Abstractions**: No single-use factories or speculative wrappers. Keep simplest form.
6. **No Stubs or Placeholders**: No `// TODO`, empty `catch {}`, or unfinished escape blocks.

### Rule 11: Domain Isolation in Refactoring
- `refactor: logic`: Must not edit CSS, markup, or component styles.
- `refactor: design`: Must not edit business logic, database queries, or state transitions.

### Rule 12: Chesterton's Fence
Never delete or replace code without understanding why it was added. Verify existing tests pass before refactoring, and keep regression tests passing after pruning.

### Rule 13: Skill Dependency Gate
Verify required skills exist in `.agents/skills/`. If any required skill is missing, halt execution and report the missing skill with the exact install command.

### Rule 14: Fast-Path Rule (Trivial Tasks)
If a task touches $\le 10$ net lines (typo, single-line bugfix, small config tweak) or is flagged `--direct`: bypass multi-turn sparring and execute directly in a single step.

### Rule 15: Atomic Phase Commits & Invariant Curation
Commit atomically when green: `<type>(<scope>): [phase-X] <summary>`. Escalate to Kaeru only on unresolvable test/build break (`FAIL`) or target file lock breach (`PAUSE`).

Upon task completion, if non-obvious gotchas or failure lessons were encountered, present a candidate invariant for `RULES.md`:
```markdown
[CANDIDATE INVARIANT FOR RULES.md]
• Gotcha: <what failed, misled, or required non-obvious handling>
• Rule: <imperative rule with relative paths for future sessions>
Save to RULES.md? (Reply "Y" to append, or Enter to skip)
```
