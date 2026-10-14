# DECISIONS.md — Architectural Invariants & Learned Lessons

> **Strict Boundary**: Captures binding architectural decisions, hard-earned failure lessons, and permanent invariants.
> Worker agents read this file to uphold past decisions and avoid past mistakes.
> All file references MUST use **relative paths**.
>
> **Curation Mandate**: Entries are curated and confirmed by the user at task wrap-up.
> Standard clean implementations leave this file untouched.

---

## Active Invariant Ledger

| Date | Decision / Incident | Context & What Went Wrong / Rejected | Active Invariant for Future Agents (Relative Paths) |
|---|---|---|---|
| `2026-10-14` | **Human-in-the-Loop Agency** | Temptation to build a "brain-off auto-pilot" where the user rubber-stamps AI choices without seeing code or trade-offs. | **Tier 1 Agency Invariant**: The human MUST make preflight architectural decisions (A vs B vs C) and curate permanent invariants. Never generate single-key "press Enter to accept default" auto-pilots. Never hide architectural trade-offs from the human. |
| `2026-10-14` | **Anti-Meta-Tooling Bloat** | Proposed adding `scripts/verify-task.js` and `TASK.md` to nanny workers, creating repo clutter and zombie files. | **Zero-Footprint State Invariant**: No temporary task files (`TASK.md`, `PROMPT.md`) or verification scripts in project root. All phase continuity and diff tracking MUST use native Git commits (`<type>(<scope>): [phase-X] <summary>`). |
| `2026-10-14` | **Signature Peek Boundary** | Attempting to let Kaeru read full application source code during planning, burning context tokens. | **Token-Lean Planning Invariant**: Kaeru reads ONLY context files and manifests. Implementation logic bodies are strictly forbidden during planning. Kaeru may only use 1-line regex/grep queries for exported signatures (`export (type\|interface\|function\|class)`). |
| `2026-10-14` | **Day-One Standard & Anti-Slop** | Tendency of workers to bolt boolean accretion flags (`isV2`) and generate generic AI card grids with purple gradients. | **Zero-Accretion & Taste Invariant**: No accretion flags or panic-if blocks. Refactor internals to Day-One clarity. UI must enforce the Eight Core Abstractions in `DESIGN.md` (Nippon colors, 3.5:1 scale tension, *Ma* unboxed layout, 5-state surfaces). Banned AI hero clichés. |
| `2026-10-14` | **Modular Lazy-Loaded Commands** | Monolithic `SKILL.md` blowing past context windows with duplicate tables and prompt templates. | **Lazy-Routing Invariant**: Core router (`skills/kaeru/SKILL.md`) stays strictly under 200 lines. Command-specific protocols and templates are isolated in `skills/kaeru/references/commands/*.md` and read on-demand only. |
| `2026-10-14` | **Offensive Kill List Enforcement** | Workers ignoring subtractive opportunities and adding bloat under loose Net LOC honor system. | **Kill List Invariant**: Every feature and refactor prompt requires an explicit `[Kill List]`. The worker blueprint must confirm targets removed. If no targets are identified, the feature Net LOC ceiling is automatically penalized from `+60` down to `+20`. |
