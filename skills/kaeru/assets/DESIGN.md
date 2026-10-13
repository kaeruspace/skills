# DESIGN.md — Visual System & Interaction Tokens

> **Strict Boundary**: This document defines the visual system, aesthetic tokens, and visual dials.
> Worker agents implementing UI (Step 3) must match these tokens and dials.

---

## 1. Aesthetic Doctrine

- **Visual Theme**: [e.g. Editorial Stone & Carbon Ink]
- **Core Philosophy**: [e.g. Tactile restraint, zero AI slop, no generic glowing cards or unneeded gradient borders]
- **Layout Principles**: [e.g. Unboxed layout, crisp typography, disciplined whitespace]

---

## 2. Tokens & Variables

### Palette
- **Background**: [e.g. `#E7E5E0` (Stone)]
- **Foreground / Ink**: [e.g. `#111215` (Carbon)]
- **Muted / Border**: [e.g. `#D4D0C8`]
- **Accent**: [e.g. `#8B1D1D` or subtle mineral tone]

### Typography
- **Display / Headings**: [e.g. `Cinzel` / Serif]
- **Body / Reading**: [e.g. `Geist Sans` / Sans-serif]
- **Monospace / Tabular**: [e.g. `Geist Mono` / Monospace]

---

## 3. Visual Dials (1–10)

Project baseline dials for worker agents:
- `VARIANCE`: [1–10] (1 = rigid symmetry & uniformity; 10 = organic asymmetry & dynamic layouts)
- `MOTION`: [1–10] (1 = instant state transitions; 10 = fluid physics & choreographed motion)
- `DENSITY`: [1–10] (1 = expansive luxury whitespace; 10 = high-density tabular / data-dense)

---

## 4. Component & State Standards

- **State Coverage**: Every interactive element must define default, hover/focus, loading, empty, and error states.
- **Responsive Viewports**: Tested against mobile (390px) and desktop (1440px).
