# Kaeru

Type `/kaeru` and a few words. Kaeru turns them into a plan, asks you one question, then writes step-by-step prompts you paste into fresh chats.

## Install

```bash
# Kaeru
npx skills add kaeruspace/skills --skill kaeru

# Worker skills
npx skills add addyosmani/agent-skills --skill api-and-interface-design --skill incremental-implementation --skill test-driven-development --skill browser-testing-with-devtools --skill code-simplification --skill debugging-and-error-recovery
npx skills add Leonxlnx/taste-skill --skill design-taste-frontend --skill high-end-visual-design --skill minimalist-ui
npx skills add dietrichgebert/ponytail --skill ponytail --skill ponytail-review --skill ponytail-audit
npx skills add raroque/vibe-security-skill
npx skills add petergyang/no-ai-slop
```

If a skill is missing, the worker notes it and carries on without it.

## First run

Kaeru asks once for a persona: a character, or default (terse technical lead). It saves your choice to `AGENTS.md`, then scaffolds any missing context files. Change the persona anytime in `AGENTS.md`.

## Daily use

1. `/kaeru add dark mode`
2. Read the reply. Answer its one question.
3. Open `PROMPT.md`. Paste Step 1 into a fresh chat. Check it passed. Then Step 2, then Step 3.
4. A step failed? Paste its Report back into `/kaeru` to rewrite only that step.

Trivial task? Kaeru says "just do it, no plan needed" and stops.

## Task types

| Type | Steps |
|---|---|
| FULLSTACK | 1 Contracts & Security, 2 Logic & Tests, 3 UI |
| BACKEND | 1 Contracts & Security, 2 Logic & Tests |
| UI | 3 UI |
| AUDIT | 4 Audit |

## Files in your project

| File | What it is |
|---|---|
| `AGENTS.md` | Persona and execution rules |
| `PRODUCT.md` | Who it's for, what's in scope |
| `DESIGN.md` | Tokens, typography, palette, visual dials |
| `SYSTEM.md` | Stack, schema, routes, and live file index |
| `DECISIONS.md` | Append-only ledger of cuts and tradeoffs |
| `PROMPT.md` | Current execution plan |

Commit the first five. Add `PROMPT*.md` to `.gitignore`.

## How it works

- You fix a wrong assumption in seconds, before any code exists.
- Files carry memory between chats. Chats don't.
- Each step runs in a fresh chat with only what it needs.
- Schema and security come before UI, because they cost more to change.
- Kaeru is the only one who writes the context files. Workers read them and update the file index.
- The persona only lives in chat. Files stay plain.