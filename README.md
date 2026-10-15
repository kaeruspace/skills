# Kaeru

> Subtractive planning layer and prompt generator for AI agents.  
> Signal density > narrative volume. Strip conversational fluff, never truncate operational protocols.

---

## 1. What is Kaeru?

Most agentic workflows fail from **prompt drift** and **code accretion**: models lose context over long sessions, introduce premature abstractions, duplicate existing utilities, and hoard dead code.

Kaeru splits engineering into three distinct roles:

- **You (Human)**: Sets product vision, decides architecture, and curates binding rules in `RULES.md`.
- **Kaeru (In Chat)**: Discovers intent, spars on technical directions, checks exported signatures (~40 tokens), and emits single-task worker prompts. Never writes implementation code.
- **Worker (Fresh Session)**: Silent executor (`Personality = 0`). Locked to declared `[Target Files]`, follows `RULES.md`, prints a 5-line `[BLUEPRINT]`, respects Net LOC limits, and commits atomically.

---

## 2. The 5 Root Files

State lives in 5 project files. Never create temporary task files or scratch scripts:

| File | Holds | Strict Boundary |
|---|---|---|
| `PRODUCT.md` | Product vision, in-scope capabilities, surface classification, non-goals. | Scope and intent only. |
| `CODEBASE.md` | Tech stack, directory topology, reusable primitives, conventions. | Codebase map (relative paths). |
| `DESIGN.md` | Master palette tokens, contrast rules, banned UI tropes, layout constraints. | Visual tokens and layout rules. |
| `RULES.md` | Architectural invariants, Net LOC budgets, and clean-code rules. | Binding rules; curated by human. |
| `AGENTS.md` | Persona settings, dials, and interaction style. | Persona and roles only. |

---

## 3. Installation

Kaeru coordinates 28 active skills across planning, engineering, taste, subtraction, and anti-slop writing:

```bash
# Kaeru Planning Layer
npx skills add kaeruspace/skills --skill kaeru

# Core Engineering & Planning
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

# Taste, Systems & Output Enforcement
npx skills add Leonxlnx/taste-skill \
  --skill design-taste-frontend \
  --skill high-end-visual-design \
  --skill minimalist-ui \
  --skill redesign-existing-projects \
  --skill full-output-enforcement

# Subtraction, Review & Audit
npx skills add dietrichgebert/ponytail \
  --skill ponytail \
  --skill ponytail-review \
  --skill ponytail-audit

# Anti-Slop Writing
npx skills add petergyang/no-ai-slop
```

---

## 4. Commands & Auto-Routing

Invoke with `/kaeru` or `/kaeru <command>`.

### Command Matrix

| Command | Focus | Primary & Guard Skills | Net LOC Budget |
|---|---|---|---|
| `/kaeru init` | Back up context, verify skills, scan codebase | Dependency Gate + Codebase grounding scan | 0 lines |
| `/kaeru feat logic <prompt>` | Spec $\to$ TDD $\to$ Harden | Phase 1: `@spec-driven-development` + `@api-and-interface-design` (Guard: `@constraint-driven-development`)<br/>Phase 2: `@test-driven-development` + `@incremental-implementation`<br/>Phase 3: `@security-and-hardening` + `@performance-optimization` + `@observability-and-instrumentation` (Review: `@ponytail-review`) | $\le +60$ lines |
| `/kaeru feat design <prompt>` | Tokens $\to$ UI $\to$ Polish | Phase 1: `@design-taste-frontend` + `@no-ai-slop`<br/>Phase 2: `@frontend-ui-engineering` + `@browser-testing-with-devtools`<br/>Phase 3: Surface-adaptive: `Persuade` $\to$ `@high-end-visual-design`; `Operate` $\to$ `@minimalist-ui` (Review: `@code-review-and-quality`) | $\le +80$ lines |
| `/kaeru refactor logic <prompt>` | Clean internals & prune dead code | `@ponytail` + `@code-simplification` + `@deprecation-and-migration` (Guard: `@doubt-driven-development`). Zero CSS/markup edits. | $\le 0$ lines |
| `/kaeru refactor design <prompt>` | Migrate tokens & flatten UI hierarchy | `@redesign-existing-projects` + `@frontend-ui-engineering` (Guard: `@browser-testing-with-devtools`). Zero logic/state edits. | $\le 0$ lines |
| `/kaeru fix <prompt>` | Reproduction test + root-cause patch | `@debugging-and-error-recovery` + `@test-driven-development` + `@incremental-implementation` | $\le +25$ lines |
| `/kaeru audit` | Detect drift, duplicate helpers, and dead weight | `@ponytail-audit` + `@doubt-driven-development` | $< 0$ lines |

### Implicit Natural Language Routing

When invoked as `/kaeru <prompt>` without an explicit command prefix:
- **Missing context files (`CODEBASE.md`, `RULES.md`)** $\implies$ `/kaeru init`
- **Bug, crash, broken test, regression** $\implies$ `/kaeru fix`
- **Refactor, cleanup, dead code, simplify** $\implies$ `/kaeru refactor <logic|design>`
- **Audit, drift, bloat inspection** $\implies$ `/kaeru audit`
- **New feature, route, schema, UI screen** $\implies$ `/kaeru feat <logic|design>`
- **Trivial change ($\le 10$ LOC, typo)** $\implies$ Fast-path bypass (direct prompt emission)

---

## 5. How Kaeru Operates (The 1+1 Turn Protocol)

### Fast-Path Bypass ($\le 10$ LOC)
Tasks modifying $\le 10$ net lines (typos, single config tweaks) or flagged `--direct` bypass multi-turn sparring and emit a 1-step direct worker prompt immediately.

### Turn 1: Direction Discovery & Anti-Obvious Sparring
1. **Intent & Signature Check** (`@interview-me`): Clarify underlying intent with at most 1 focused question. Run a 1-line regex/grep on candidate files for exported signatures (~40 tokens). Never read implementation code bodies during planning.
2. **Anti-Obvious Lenses** (`@idea-refine`, `@source-driven-development`):
   - *Negative Hypothesis*: Is this feature bloat? Can we eliminate the requirement or invert responsibility?
   - *Platform Primitive Hijack*: What DB constraint or Web standard solves this with 0 extra packages?
   - *10x Paradigm Shift*: Replace boilerplate CRUD with direct manipulation, streaming, or local-first architecture.
3. **Unrigged Architectural Directions**: Present 2–3 distinct technical directions. For each, articulate **Concept**, concrete **Mechanics** (data flow and relative file touch points), and explicit **Trade-offs**. Zero file edits on Turn 1.

### Turn 2: Micro-Spec, Doubt Gate & Prompt Emission
1. **Micro-Spec** (`@spec-driven-development`): Formulate `[Target Files]`, `[Assigned Skills]`, `[Objective]`, `[Kill List]`, `[Net LOC Budget]`, and `[Not-Doing]`.
2. **Pre-Emission Doubt Gate** (`@doubt-driven-development`):
   - *Grounding*: Are signatures verified (~40 tokens) without unverified assumptions about `CODEBASE.md`?
   - *Subtractive Anchor*: Is there an explicit `[Kill List]`? (Modifying existing code without deletions caps budget to $\le +20$).
   - *Chesterton's Fence*: Are existing tests preserved and edits strictly bounded to `[Target Files]`?
3. **Emit Prompt**: Log new invariants to `RULES.md`, update context files if scope changed, and emit the canonical worker prompt into chat.

---

## 6. Canonical Worker Prompt & Execution

### Canonical Worker Prompt Schema

Every execution phase emits this prompt into chat for a fresh-session worker agent:

```markdown
# TASK: <type>(<scope>): <Title> [Phase X]
[Target Files]: <relative paths from repo root>
[Assigned Skills]:
- Primary: <skill>
- Guard: <skill>
- Review: <skill>
- Invariant: @full-output-enforcement (zero stubs, complete drop-in execution)

[Objective]: <Clear, unambiguous outcome for this phase>
[Kill List]: <Greenfield / New Capability OR exact symbols/files to delete>
[Net LOC Budget]: <= <budget> lines (verified via git diff --stat)
[Not-Doing]: <explicit boundary cuts and non-goals>

Read: RULES.md, CODEBASE.md, AGENTS.md. [If design: DESIGN.md]
Protocol:
1. REALITY CHECK: Verify Target Files match CODEBASE.md. Output [REALITY CHECK: CLEAN] or [REALITY CHECK: PIVOT].
2. BLUEPRINT: Print 5-line [BLUEPRINT] confirming [Kill List] targets, then execute immediately.
3. EXECUTE: Follow assigned skills and clean-code rules. Modify only declared [Target Files].
4. VERIFY & COMMIT: Run test suite. Verify Net LOC with `git diff --stat`. Commit atomically: `<type>(<scope>): [phase-X] <summary>`. Escalate only on FAIL or PAUSE.
5. CURATE: If unexpected gotchas or non-obvious fixes occurred, output candidate invariant:
   [CANDIDATE INVARIANT FOR RULES.md]
   • Gotcha: <what failed or misled>
   • Rule: <imperative rule with relative paths>
   Save to RULES.md? (Reply "Y" to append, or Enter to skip)
```

### The 5-Line Blueprint

Before modifying code, workers print this blueprint without waiting for user approval:

```markdown
[BLUEPRINT]
• Goal: <1 sentence what is being built or fixed>
• Files: <relative paths + 1-line responsibility each>
• Pattern: <architecture pattern: e.g. Server Action + Zod, Compound Reducer>
• Kill List Targets: <exact symbols or files confirmed for deletion>
• Invariant: <security rule or interface contract preserved>
```

### Native Git Phase Continuity

When resuming a multi-phase task in a fresh session:
1. Kaeru checks `git log -n 1 --oneline` and `git diff HEAD~1 --stat`.
2. Identifies the completed phase directly from committed history.
3. Emits the next phase prompt from git state. Zero temporary state files or transcript dumps.