# SYSTEM.md — Architecture & Codebase Map

> **Specification & System Topology**  
> Last verified: `[git-hash]` `[YYYY-MM-DD]`
>
> **Strict Boundary**: Maps current system topology (stack, schema, routes, security, index). Code audits belong in Step 4 audits.

---

## 1. Tech Stack & Dependencies

| Layer | Technologies & Dependencies | Purpose / Notes |
|---|---|---|
| **Framework & Core** | [e.g. Next.js, React] | [Runtime description] |
| **Language & Toolchain** | [e.g. TypeScript, Bun/Node] | [Compiler and tooling] |
| **Database & ORM** | [e.g. Neon PostgreSQL, Drizzle ORM] | [Data persistence] |
| **Styling & UI** | [e.g. Tailwind CSS] | [Styling engine] |
| **State & Async** | [e.g. Zustand, TanStack Query] | [State management] |

---

## 2. Schema & Data Models

Canonical data models, database tables, and validation schemas:

### [Model / Table Name]
- **`id`**: Primary key
- **`[field_name]`**: Type, nullability, constraints
- **`created_at`**: Timestamp

---

## 3. Routes & Endpoints

| Route / Endpoint | HTTP Method | Type | Primary Responsibilities |
|---|---|---|---|
| `/` | `GET` | Page | Main entry point |
| `/api/[endpoint]` | `POST` | API Route | Validation and persistence |

---

## 4. Security Boundaries & Permissions

- **Server-Side Validation**: All input clamped and sanitized before processing.
- **Authentication & Authorization**: Identity verification and access gates.
- **Fallback & Resilience**: Behavior when external services or environment variables are missing.

---

## 5. File & Route Index

**Header Line:** `Last verified: [git-hash] [YYYY-MM-DD]`

Categorized listing of source files and their structural roles:
- `app/` or `src/`: Routing and layout entry points.
- `components/`: UI components and widgets.
- `lib/` or `utils/`: Shared utilities and domain services.
- `db/`: Database client, schema, and migrations.
