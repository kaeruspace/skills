# CODEBASE.md: Architecture & Primitives Map

> [!IMPORTANT]
> **TEMPLATE NOTICE**: This file is a starter template. When initializing Kaeru in an actual project, update all data according to your project specifications and remove this notice once configured.

---

## 1. Tech Stack & Dependencies
- **Runtime & Toolchain**: [e.g. Node 20 / Bun / TypeScript 5.x]
- **Framework & Routing**: [e.g. Next.js App Router / Vite + React / Fastify]
- **Database & Persistence**: [e.g. PostgreSQL + Drizzle ORM / SQLite + Prisma]
- **UI, Styling & Animation**: [e.g. Tailwind CSS, Lucide-React (light stroke), Framer Motion]
- **Validation & Schemas**: [e.g. Zod / Valibot]
- **Test Runner**: [e.g. Vitest / Jest / Playwright]

---

## 2. Directory Topology (Relative Paths)
```
/
├── src/
│   ├── app/ (or routes/)     # Page routes, layouts, and server endpoints
│   ├── components/           # Reusable UI components (atomic, composable)
│   ├── lib/                  # Shared utilities, database client, auth config
│   ├── models/ (or schema/)  # Canonical database schemas and Zod types
│   └── hooks/                # Custom React/framework hooks
├── tests/                    # Integration and unit tests
└── package.json
```

---

## 3. Reusable Primitives (Check Before Writing Code)
> AI agents must consult this inventory before creating new helpers, schemas, or components:
- **Database Client**: `[e.g. src/lib/db.ts]`: Canonical DB connection; never instantiate secondary clients.
- **Validation Wrapper**: `[e.g. src/lib/validate.ts]`: Validates inputs at trust boundary and fails fast.
- **Auth Session**: `[e.g. src/lib/auth.ts]`: Session getter and permission gate.
- **Button / Input Primitives**: `[e.g. src/components/ui/button.tsx]`: Enforces DESIGN.md tokens and 5-state interactivity.
- **Toast / Notifications**: `[e.g. src/components/ui/toast.tsx]`: Ephemeral notification container.

---

## 4. Architectural Conventions & Data Flow
- **Boundary Validation**: Validate all external input (forms, query params, webhook payloads) with Zod at entry. Domain internals receive strictly typed data.
- **Data Mutation**: Use server actions or dedicated route handlers. Never mutate database state directly in client components.
- **Error Handling**: Fail fast on invalid state. Return structured `{ success: false, error: string }` objects; never swallow errors in silent `catch {}` blocks.
- **State Management**: Keep state local and lifted only when required. Avoid global stores for transient UI states.

---

## 5. Development & Verification Commands
- **Dev Server**: `[e.g. npm run dev]`
- **Test Suite**: `[e.g. npm test]`
- **Typecheck / Lint**: `[e.g. npm run typecheck && npm run lint]`
- **Build**: `[e.g. npm run build]`
