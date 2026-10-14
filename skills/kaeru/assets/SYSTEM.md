# SYSTEM.md — Architecture & Subtractive Codebase Map

> Last verified: `[git-hash]` `[YYYY-MM-DD]` | Relative paths only.  
> Consult this inventory before writing code: reuse primitives, consolidate duplicates, prune dead weight.

---

## 1. Tech Stack & Dependencies
- **Runtime / Language**: [Runtime, toolchain, compiler]
- **Framework & Core**: [Server framework, routing model]
- **Data & Persistence**: [Database, ORM/driver, cache]
- **UI & State**: [Styling engine, state primitives]

---

## 2. Schema & Canonical Models
[Canonical tables, types, or validation schemas]

---

## 3. Routes & Endpoints
[Active routes, endpoints, HTTP methods, and responsibilities]

---

## 4. Security Boundaries & Invariants
- Server-side validation at trust boundaries; fail fast on invalid state.
- Authentication/authorization model and permission gates.
- Anti-Sycophancy Mandate: reject agency surrender or ungrounded bloat.

---

## 5. Reusable Primitives (Subtractive Inventory)
> Check here before writing new functions, schemas, or components:
- `[Primitive / Helper]`: `[relative/path]` — [Purpose & Usage]

---

## 6. Deprecation & Pruning Candidates
- None identified (clean baseline).

---

## 7. File & Route Index
[Categorized relative paths: config, routes, models, libs, components, tests]
