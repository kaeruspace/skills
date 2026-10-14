# Kaeru (カエル)

> **The Subtractive Planning Layer & Single-Task Combat Prompt Generator for AI Agents.**  
> *Context density over grammar. Subtraction before addition. Day-One architecture over accretion.*

---

## 1. What is Kaeru?

Most AI coding workflows suffer from two fatal failure modes:
1. **The God-Prompt Drift**: Dumping a 500-line multi-step task list (`PROMPT.md`) into a single chat session. By step 4, the model hallucinates context, forgets constraints, and litters the codebase with blind patches.
2. **AI Slop & Accretion**: AI agents reflexively add code—bolting on boolean flags (`isV2`, `skipAuth`), nesting generic card-in-a-card UI with purple gradients, writing mock theater (`expect(mock).toHaveBeenCalled()`), and creating premature abstractions for single-use logic.

**Kaeru solves this through a strict 3-tier separation of concerns**:

```
┌────────────────────────────────────────────────────────┐
│  Tier 1: Human User (Vision & Preflight Decision)      │
│  • Settles architectural forks preflight (A vs B vs C) │
│  • Curates binding invariants into DECISIONS.md        │
└───────────────────────────┬────────────────────────────┘
                            │
                            ▼
┌────────────────────────────────────────────────────────┐
│  Tier 2: Kaeru (Architect, Sparring Lead & Router)     │
│  • Token-Lean: Never reads application source code     │
│  • Reads only context files (SYSTEM, PRODUCT, DESIGN)  │
│  • Employs Anti-Obvious Provocation Engine (3 lenses)  │
│  • Emits ONE single-task worker prompt at a time       │
└───────────────────────────┬────────────────────────────┘
                            │ (Copy-pasted into fresh session)
                            ▼
┌────────────────────────────────────────────────────────┐
│  Tier 3: Worker Agent (Fresh Session Executor)         │
│  • 100% dry, technical realist (Mimicry = 0)           │
│  • Inspects target files -> Emits 5-line [BLUEPRINT]   │
│  • Enforces Net LOC Budget & Day-One architecture      │
│  • Executes straight to green; escalates on FAIL/PAUSE │
└────────────────────────────────────────────────────────┘
```

---

## 2. Installation & Core Skills Arsenal

Kaeru commands a curated arsenal of **32 battle-tested skills**. Kaeru enforces a **Fail-Fast Skill Dependency Gate**: if any required skill is missing, Kaeru halts immediately with exact install commands.

### Installation Command

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

### The 32 Skills Classified by Combat Theater

| Theater | Skills Deployed | Primary Purpose |
|---|---|---|
| **Sparring & Planning** | `@idea-refine`<br/>`@interview-me`<br/>`@constraint-driven-development`<br/>`@spec-driven-development`<br/>`@doubt-driven-development`<br/>`@documentation-and-adrs` | Divergent sparring across 3 lenses; 1 high-leverage preflight question; self-adversarial doubt verification; ADR logging. |
| **Core Architecture & Maintainability** | `@api-and-interface-design`<br/>`@source-driven-development`<br/>`@test-driven-development`<br/>`@incremental-implementation`<br/>`@full-output-enforcement`<br/>`@security-and-hardening`<br/>`@code-simplification`<br/>`@ponytail`<br/>`@observability-and-instrumentation`<br/>`@code-review-and-quality` | Immutable contracts and schemas; official doc grounding; TDD red-green-refactor loop; zero stubs / full outputs; auth & OWASP hardening; Net LOC pruning; structured metrics. |
| **Taste & UI Engineering** | `@design-taste-frontend`<br/>`@high-end-visual-design`<br/>`@minimalist-ui`<br/>`@industrial-brutalist-ui`<br/>`@brandkit`<br/>`@stitch-design-taste`<br/>`@gpt-taste`<br/>`@frontend-ui-engineering`<br/>`@browser-testing-with-devtools`<br/>`@no-ai-slop` | Anti-slop art direction; typographic tension (3.5:1 ratio); GSAP motion & spring physics; real DevTools browser inspection (390px/1440px); complete 5-state surfaces. |
| **Pruning, Refactor & Bugfix** | `@deprecation-and-migration`<br/>`@performance-optimization`<br/>`@debugging-and-error-recovery`<br/>`@redesign-existing-projects`<br/>`@ponytail-audit`<br/>`@ponytail-review` | Safe database schema evolution; Core Web Vitals optimization; systematic root-cause reproduction tests; dead code and debt elimination. |

---

## 3. The 5 Commands (Token-Lean Reference Routing)

Kaeru uses on-demand lazy routing: the core skill file (`SKILL.md`) stays lean (~170 lines) and reads **only the specific reference document** for the invoked command:

| Command | Purpose | Reference Document |
|---|---|---|
| `/kaeru init` | First-run setup, dependency gate, persona interview, automated codebase grounding scan | [`skills/kaeru/references/commands/init.md`](file:///c:/Users/jaat/kaeruspace/skills/skills/kaeru/references/commands/init.md) |
| `/kaeru feat <logic\|design> <prompt>` | Feature planning, 3 anti-obvious lenses, preflight triad, phased prompt emission | [`skills/kaeru/references/commands/feat.md`](file:///c:/Users/jaat/kaeruspace/skills/skills/kaeru/references/commands/feat.md) |
| `/kaeru refactor <logic\|design> <prompt>` | Code/design refactoring, dead code elimination, ponytail audit/review | [`skills/kaeru/references/commands/refactor.md`](file:///c:/Users/jaat/kaeruspace/skills/skills/kaeru/references/commands/refactor.md) |
| `/kaeru fix <prompt>` | Bug isolation, failing automated reproduction test, surgical root-cause patch | [`skills/kaeru/references/commands/fix.md`](file:///c:/Users/jaat/kaeruspace/skills/skills/kaeru/references/commands/fix.md) |
| `/kaeru audit` | Context & codebase health audit, drift detection (`git ls-files`), dead-weight pruning | [`skills/kaeru/references/commands/audit.md`](file:///c:/Users/jaat/kaeruspace/skills/skills/kaeru/references/commands/audit.md) |

*(Implicit routing: `/kaeru <text>` without a command prefix automatically dispatches to the correct handler).*

---

## 4. The 5 Project Context Files

Kaeru operates using 5 structured markdown files in the repository root. These files persist architectural memory between chats:

| File | Holds | Strict Boundary |
|---|---|---|
| `AGENTS.md` | Persona, dials (0–2), worker execution rules, target file lock, adapt-vs-pause matrix | Workers execute dry (`Mimicry = 0`). Files stay plain. |
| `PRODUCT.md` | Vision, target audience, surface classification (`Persuade`, `Operate`, `Read`, `Experience`), journeys | Scope boundaries & explicit non-goals. |
| `DESIGN.md` | Aesthetic doctrine, Eight Core Abstractions, palette tokens, visual dials (1–10) | UI tokens, typography, and visual rules only. |
| `SYSTEM.md` | **Subtractive Anchor**: Tech stack, canonical schema, routes, reusable primitives, relative file index | Topology & reusable inventory. Grounded via scan. |
| `DECISIONS.md` | Binding architectural choices, incident gotchas, permanent agent invariants | Curated by user at task completion. |

*Pre-existing context files are safely backed up to `*.old.md` during `/kaeru init`.*

---

## 5. Dials: Persona Mimicry & Trust (Configured in `AGENTS.md`)

### Mimicry Depth Dial `[0 | 1 | 2]` (Default: `1`)
- **Level 0 (Zero Persona / Dry Technical)**: Pure engineer. Terse, objective, direct, zero mannerisms.
- **Level 1 (Subtle Flavor - Default)**: Recognizable cadence, worldview, perspective, and dry wit blended with engineering precision.
- **Level 2 (Deep Persona Mimicry)**: Full immersion in character voice, idioms, and attitude while maintaining technical accuracy and subtractive rigor.

### Trust & Pushback Dial `[0 | 1 | 2]` (Default: `1`)
- **Level 0 (High Trust / Direct Execution)**: Assumes you know exactly what you want. Minimum pushback, dry trade-offs, maximum brevity.
- **Level 1 (Calibrated Trust / Sparring Partner - Default)**: Sharp questions, active pushback against bloat, challenges unstated assumptions.
- **Level 2 (Zero Trust / Anti-Bloat Inquisitor)**: Treats every requirement as guilty of bloat until proven innocent. Aggressive roasts of complexity and visual slop, demands radical subtraction.

---

## 6. How Kaeru Operates (The 1+1 Turn Protocol)

### Turn 1: Anti-Obvious Sparring & Preflight Options
Kaeru unleashes the **Anti-Obvious Provocation Engine**:
1. **Negative Hypothesis (Lens 1)**: Attacks the premise. Why might this feature be toxic bloat? Can we invert responsibility or eliminate the step entirely?
2. **Platform Primitive Hijack (Lens 2)**: Exploit native database constraints (generated columns, triggers) or web standards (CSS subgrid, `@starting-style`, native Web Streams) to solve the problem with **ZERO external dependencies** and minimal LOC.
3. **10x Paradigm Shift (Lens 3)**: Replace boilerplate CRUD with high-leverage paradigms (optimistic streams, command palettes, spatial canvases).
4. **The Preflight Triad**: Kaeru presents 1 focused question, a strong `GUESS`, and closed options (A: Pragmatic Core, B: Radical Subtraction, C: 10x Paradigm Shift).

### Turn 2: Convergence & Single-Task Worker Prompt
Upon your choice, Kaeru performs internal doubt verification (`@doubt-driven-development`), updates relevant context files, and emits **one single-task prompt directly into chat**.

---

## 7. The Worker Execution Protocol (Fresh Sessions)

You copy-paste Kaeru's prompt into a **fresh session**. The worker executes under strict invariants:

1. **Reality Check Before Coding**:
   - `[REALITY CHECK: CLEAN]`: Reality matches `SYSTEM.md` $\implies$ print blueprint and execute straight to green.
   - `[REALITY CHECK: PIVOT]`: Discrepancy discovered $\implies$ halt immediately and report pivot to paste back to Kaeru.
2. **The Mandatory 5-Line Blueprint**:
   ```markdown
   [BLUEPRINT]
   • Goal: <1 sentence what is being built or fixed>
   • Files: <relative paths only + 1-line responsibility each>
   • Pattern: <architecture pattern: e.g. Server Action + Zod, Compound Reducer>
   • Subtractive Delta: <primitives/lines deleted or net LOC ceiling>
   • Invariant: <the non-negotiable security boundary or contract preserved>
   ```
3. **Net LOC Budgets & Accretion Ceilings (Verified with `git diff --stat`)**:
   - `feat: logic`: $\le +60$ net LOC
   - `feat: design`: $\le +80$ net LOC
   - `refactor`: $\le 0$ net LOC (subtractive or LOC-neutral)
   - `fix`: $\le +25$ net LOC (surgical patch only)
   - `audit: prune`: $< 0$ net LOC (net negative required)
4. **The Day-One Standard**:
   - Zero accretion flags (`isV2`, `skipAuth`) or panic-if blocks. Code must read as if planned from Day 1.
   - Zero defensive null masking (`?.` or `?? null`) inside domain logic. Validate once at trust boundaries; fail fast.
   - Zero premature abstractions (no single-implementation factories or dynamic dispatchers).
   - Zero mock theater (`expect(mock).toHaveBeenCalled()`). Assert real deterministic state transitions.
5. **The Eight Core Abstractions of Design (in `DESIGN.md`)**:
   - **Chromatics**: Nippon Colors (Torinoko canvas `#E7E5E0`, Sumi ink `#111215`, Kincha accent $\le 3\%$ budget).
   - **Typography**: Epigraphic *Capitalis Monumentalis* display titles with **enforced 3.5:1 scale tension** over Swiss body (`45ch–65ch`).
   - **Spatial Layout**: *Ma* (unboxed typography floating on raw stone, zero card borders).
   - **Motion**: *Iaidō* directional reveals (sub-250ms), physical spring physics (`cubic-bezier(0.16, 1, 0.3, 1)`).
   - **Anti-Slop Cliché Ban**: Zero centered AI hero layouts (badge + buttons + 3 icon cards), zero purple/cyan radial glow blobs, zero card-in-card nesting.
   - **5-State Surfaces**: Default, Hover/Focus, Loading skeleton, Empty state, Error retry.
6. **Exception-Only Escalation**:
   - Workers execute autonomously straight to green without asking diff-review questions.
   - Escalate back to Kaeru in **ONLY TWO STATES**:
     - `FAIL`: Unresolvable test/build break after systematic root-cause debugging.
     - `PAUSE`: Target file lock breach, exported signature change, or major codebase divergence.