# DESIGN.md — Visual System & Interaction Tokens

> **Strict Boundary**: Visual tokens, spatial hierarchy, and interaction physics. Zero rogue hex codes.

---

## 1. Aesthetic Doctrine: Eight Core Abstractions
| Dimension | Concept | Implementation Rule |
|---|---|---|
| **Chromatics** | Natural Material Palette | Canvas (`#E7E5E0`), Surface (`#EEECE8`), Ink (`#111215`), Accent (`#A88238`, $\le 3\%$), Hairline (`rgba(17,18,21,0.08)`). |
| **Typography** | Monumental Serif & Sans | Display: `Cinzel`/`Cormorant` (tracking `0.04em`). Body: `Geist Sans` (`45ch–65ch`). Min 3.5:1 scale contrast. |
| **Spatial Layout** | Active Whitespace | Unboxed typography floating on canvas. Zero card-in-card nesting. |
| **Motion** | Directional Reveals | Directional clip-path reveals (<250ms), spring physics `cubic-bezier(0.16, 1, 0.3, 1)`. |
| **Transitions** | Panel Partitions | Sliding partitions, smooth camera FOV transitions (`35°` to `51°`). Zero abrupt flashes. |
| **Identity** | Milestone Seals | Carved stone milestone seals instead of generic gamified XP badges. |
| **Materiality** | Tactile Surfaces | Translucent vellum (`backdrop-blur-xl`), matte unpolished stone. |
| **Interaction** | Tactile Response | Physical micro-depressions (`active:scale-[0.98]`). Ephemeral cues dissolve after 6s. |

---

## 2. Tokens & Dials
```css
:root { --canvas: #E7E5E0; --surface: #EEECE8; --ink: #111215; --meta: #5F5E59; --accent: #A88238; --hairline: rgba(17, 18, 21, 0.08); }
```
- `VARIANCE`: `[1–10]` (1 = rigid symmetry; 5 = dynamic split col-span-7/5; 10 = broken-grid tension)
- `MOTION`: `[1–10]` (1 = instant switch; 5 = spring physics; 10 = GSAP scroll pinning)
- `DENSITY`: `[1–10]` (1 = expansive open space; 5 = balanced 45ch–65ch; 10 = compact telemetry)

---

## 3. Surface & Viewport Rules
- **5-State Surfaces**: Default, Hover/Focus, Loading skeleton, Empty state, Error retry.
- **Viewport Checks**: 390px mobile and 1440px desktop with zero horizontal overflow.
