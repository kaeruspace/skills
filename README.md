# Kaeru

Type `/kaeru` with your request — whether a few words or a detailed spec. Kaeru aligns intent through a focused one-question-at-a-time interview, maintains lean context files from assets, and compiles staged prompts into `PROMPT.md` for fresh-session worker agents.

## Install

```bash
# Kaeru
npx skills add kaeruspace/skills --skill kaeru

# Worker skills
npx skills add addyosmani/agent-skills --skill api-and-interface-design --skill incremental-implementation --skill test-driven-development --skill browser-testing-with-devtools --skill code-simplification --skill debugging-and-error-recovery --skill security-and-hardening --skill frontend-ui-engineering --skill code-review-and-quality
npx skills add Leonxlnx/taste-skill --skill design-taste-frontend --skill high-end-visual-design --skill minimalist-ui
npx skills add dietrichgebert/ponytail --skill ponytail --skill ponytail-review --skill ponytail-audit
npx skills add petergyang/no-ai-slop
```

If a skill is missing, the worker notes it and carries on without it.

## First run

Kaeru asks once for a persona: a character, or default (terse technical lead). It saves your choice to `AGENTS.md`, then scaffolds any missing context files from `skills/kaeru/assets/`. Change the persona anytime in `AGENTS.md`.

## Daily use

1. `/kaeru add dark mode` (or provide full feature requirements and tech preferences).
2. Answer one question at a time with concrete options until intent is aligned.
3. Once compiled, keep the `/kaeru` chat open. Open a fresh chat and run Step 1 from `PROMPT.md`.
4. **Silent Success**: If a step passes cleanly, proceed straight to the next step. No need to report back to Kaeru.
5. **Exceptions Only**: Return to the `/kaeru` chat ONLY if a worker halts with:
   - **`FAIL`**: A test failure or blocker occurred $\implies$ Kaeru rewrites that step.
   - **`PAUSE`**: An unexpected discovery, skill conflict, or scope change arose $\implies$ Kaeru realigns the plan and recompiles `PROMPT.md`.

Trivial task? Kaeru says "just do it, no plan needed" and stops.

## Task types

| Type | Steps |
|---|---|
| FULLSTACK | 1 Contracts & Security, 2 Logic & Tests, 3 UI |
| BACKEND | 1 Contracts & Security, 2 Logic & Tests |
| UI | 3 UI |
| AUDIT | 4 Audit |

## Files in your project

All files conform to the schemas in `skills/kaeru/assets/`:

| File | What it is |
|---|---|
| `AGENTS.md` | Persona and worker execution rules |
| `PRODUCT.md` | Product vision, user profiles, scope, and surface type |
| `DESIGN.md` | Tokens, typography, palette, visual dials (1–10) |
| `SYSTEM.md` | Tech stack, schema, routes, security, and live file index |
| `DECISIONS.md` | Append-only ledger of architectural choices, incident gotchas, and learned rules |
| `PROMPT.md` | Current execution plan |

Commit the first five. Add `PROMPT*.md` to `.gitignore`.

## How it works

- Intent is verified through a one-question-at-a-time interview before any code or prompt exists.
- Files carry memory between chats. Chats don't.
- Each step runs in a fresh chat with only what it needs.
- Schema and security come before UI, because they cost more to change.
- Kaeru is the only one who writes the context files. Workers read them and update the file index.
- Context files stay lean: scaffolded from assets, updated only when their domain changes; `DECISIONS.md` logs architectural choices and learned rules.
- The persona only lives in chat. Files stay plain.