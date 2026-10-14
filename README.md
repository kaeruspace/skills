# Kaeru

> Subtractive planning layer and single-task prompt generator for AI agents.<br/>
> Less text > long text with same context. Subtraction before addition. Day-One architecture over accretion.

---

## 1. What is Kaeru?

Most AI coding workflows suffer from two failure modes:
1. **The God-Prompt Drift**: Dumping a multi-step task list (`PROMPT.md`) into a single chat session. After a few steps, the model hallucinates context, drops constraints, and patches blindly.
2. **AI Slop & Accretion**: AI agents reflexively add code—bolting on boolean flags (`isV2`, `skipAuth`), nesting generic card-in-a-card UI with purple gradients, writing mock theater (`expect(mock).toHaveBeenCalled()`), and creating premature abstractions for single-use logic.

Kaeru solves this through a strict **3-tier separation of concerns**:

- **Tier 1: Human (Vision & Preflight Decision Lead)**: Holds product intent and settles architectural forks (A vs B vs C) without parsing raw code diffs. Curates permanent invariants into `DECISIONS.md`. Answers one focused question at a time.
- **Tier 2: Kaeru (Architect, Sparring Lead & Router)**: Token-lean planning grounded in context markdown files and manifests. Runs surgical Signature Peeks (~40 tokens via 1-line regex/grep). Employs anti-obvious sparring lenses. Emits **ONE single-task worker prompt directly into chat**.
- **Tier 3: Worker (Ground-Truth Realist & Fast Executor)**: Runs in fresh sessions (`Mimicry = 0`). Locked strictly to declared `[Target Files]`. Prints a 5-line `[BLUEPRINT]` confirming `[Kill List]` targets. Enforces Net LOC budgets via `git diff --stat`. Commits atomically (`feat(scope): [phase-X] <summary>`).

---

## 2. Installation & Core Skills

Kaeru integrates 32 focused skills. It enforces a fail-fast dependency check: if any required skill is missing, Kaeru stops immediately and outputs exact install commands.

```bash
# 1. Kaeru Planning Layer
npx skills add kaeruspace/skills --skill kaeru

# 2. Planning, Core Engineering & Quality (Addy Osmani)
npx skills add addyosmani/agent-skills \
  --skill interview-me \
  --skill documentation-and-adrs \
  --skill api-and-interface-design \
  --skill security-and-hardening \
  --skill incremental-implementation \
  --skill test-driven-development \
  --skill debugging-and-error-recovery \
  --skill code-simplification \
  --skill frontend-ui-engineering \
  --skill browser-testing-with-devtools \
  --skill code-review-and-quality \
  --skill constraint-driven-development \
  --skill source-driven-development \
  --skill spec-driven-development \
  --skill doubt-driven-development \
  --skill deprecation-and-migration \
  --skill performance-optimization \
  --skill idea-refine \
  --skill observability-and-instrumentation

# 3. Taste, UI Systems & Full Output Enforcement (Leonxlnx)
npx skills add Leonxlnx/taste-skill \
  --skill design-taste-frontend \
  --skill high-end-visual-design \
  --skill minimalist-ui \
  --skill industrial-brutalist-ui \
  --skill brandkit \
  --skill full-output-enforcement \
  --skill redesign-existing-projects

# 4. Pragmatic Subtraction, Auditing & Debt Reduction (Dietrich Gebert)
npx skills add dietrichgebert/ponytail \
  --skill ponytail \
  --skill ponytail-review \
  --skill ponytail-audit

# 5. Anti-Slop Writing & Logic De-slop (Peter Yang)
npx skills add petergyang/no-ai-slop
```

---

## 3. The 5 Commands (On-Demand Lazy Routing)

The core router (`skills/kaeru/SKILL.md`) stays lean (~85 lines) and lazy-loads reference documents only when needed:

| Command | Purpose | Reference Document |
|---|---|---|
| `/kaeru init` | First-run setup, dependency check, interview, automated grounding scan | [`skills/kaeru/references/commands/init.md`](skills/kaeru/references/commands/init.md) |
| `/kaeru feat <logic\|design> <prompt>` | Feature planning, anti-obvious sparring, options triad, phased prompt generation | [`skills/kaeru/references/commands/feat.md`](skills/kaeru/references/commands/feat.md) |
| `/kaeru refactor <logic\|design> <prompt>` | Domain cleanup, dead-code elimination, subtractive restructuring ($\le 0$ LOC) | [`skills/kaeru/references/commands/refactor.md`](skills/kaeru/references/commands/refactor.md) |
| `/kaeru fix <prompt>` | Bug isolation, reproduction test creation, surgical root-cause repair ($\le +25$ LOC) | [`skills/kaeru/references/commands/fix.md`](skills/kaeru/references/commands/fix.md) |
| `/kaeru audit` | Scans `git ls-files` vs `SYSTEM.md` for architectural drift and bloat | [`skills/kaeru/references/commands/audit.md`](skills/kaeru/references/commands/audit.md) |

*(Implicit routing: `/kaeru <text>` without a command prefix automatically dispatches to the matching handler).*

---

## 4. The 5 Constitutional Context Files

State is maintained across 5 root files. Zero temporary verification scripts or task files (`TASK.md` and `PROMPT.md` are strictly banned):

| File | Holds | Strict Boundary |
|---|---|---|
| `AGENTS.md` | Persona settings, dials (0–2), "Say NO" mandate, pure code/execution rules. | Code execution only. Zero UI clutter. |
| `PRODUCT.md` | Vision, audience, surface classification (`Persuade`, `Operate`, `Read`, `Experience`), journeys, non-goals. | Product scope and intent only. |
| `DESIGN.md` | Aesthetic doctrine, Eight Core Abstractions, palette tokens, visual dials (1–10). | UI tokens, typography, visual rules only. |
| `SYSTEM.md` | **Subtractive Anchor**: Tech stack, schema, routes, reusable primitives, file index. | Grounded topology map (relative paths). |
| `DECISIONS.md` | Permanent architectural invariants and learned failure lessons. Append-only ledger. | Binding rules and gotchas only. |

---

## 5. Dials: Persona Mimicry & Trust (Configured in `AGENTS.md`)

- **Mimicry Depth Dial `[0 | 1 | 2]` (Default: `1`)**:
  - `Level 0`: Pure engineer. Terse, objective, direct, zero mannerisms.
  - `Level 1`: Recognizable cadence, worldview, perspective, and dry wit (Default).
  - `Level 2`: Full immersion in character voice and idioms while maintaining subtractive rigor.
- **Trust & Pushback Dial `[0 | 1 | 2]` (Default: `1`)**:
  - `Level 0`: Assumes you know exactly what you want. Minimum pushback, maximum brevity.
  - `Level 1`: Sharp questions, active pushback against bloat, challenges unstated assumptions (Default).
  - `Level 2`: Anti-bloat inquisitor. Treats every requirement as guilty of bloat until proven innocent.

---

## 6. How Kaeru Operates (The 1+1 Turn Protocol)

### Turn 1: Anti-Obvious Sparring & Preflight Options
1. **Surgical Signature Peek**: 1-line regex/grep on candidate target files for exported signatures (`export (type|interface|function|class)`). Token cost: ~40 tokens.
2. **Anti-Obvious Lenses**: Evaluates ideas across Negative Hypothesis (is this bloat?), Platform Primitive Hijack (native DB/Web standard?), and 10x Paradigm Shift (kill CRUD boilerplate).
3. **Preflight Triad**: Kaeru presents 1 focused question with a strong `GUESS` and closed options (A: Pragmatic Core, B: Radical Subtraction, C: 10x Shift). One thing at a time. No file edits on Turn 1.

### Turn 2: Convergence & Single-Task Prompt Emission
Upon choice, Kaeru logs invariants to `DECISIONS.md`, updates context files, and emits **ONE single-task prompt directly into chat** for the active phase.

---

## 7. Git Phase Continuity & Worker Execution

1. **The 5-Line Blueprint**: Worker prints before coding (`Goal`, `Files`, `Pattern`, `Kill List Targets`, `Invariant`).
2. **Atomic Phase Commits**: When green, worker commits: `<type>(<scope>): [phase-X] <summary>`.
3. **Zero-Drift Resumption**: In a fresh chat session, Kaeru inspects `git log -n 1 --oneline` and `git diff HEAD~1 --stat` to detect the completed phase and emit the next phase prompt automatically grounded in real committed code.
4. **Net LOC Budgets & The Greenfield Rule (Verified with `git diff --stat`)**:
   - `feat: logic`: $\le +60$ net LOC.
   - `feat: design`: $\le +80$ net LOC.
   - `refactor`: $\le 0$ net LOC (subtractive or neutral).
   - `fix`: $\le +25$ net LOC (surgical patch only).
   - *Greenfield Rule*: Brand-new code sets `[Kill List: Greenfield / New Capability]` (full budget). Modifying existing code with an empty Kill List is penalized to $\le +20$ LOC to punish accretion.
5. **Day-One Standard**: Zero accretion flags (`isV2`, `skipAuth`), zero defensive null-masking in domain logic, zero mock theater.
6. **Design Standards (Loaded on `design` tasks only)**: Eight Core Abstractions (`DESIGN.md`), 5-state surfaces, and responsive verification (390px/1440px).
7. **Exceptions Only**: Workers report back to Kaeru ONLY on `FAIL` (unresolvable test/build break) or `PAUSE` (target lock breach).