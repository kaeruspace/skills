# DESIGN.md: Visual System & Design Rules

> [!IMPORTANT]
> **TEMPLATE NOTICE**: This file is a starter template. When initializing Kaeru in an actual project, update all design tokens according to your project specifications and remove this notice once configured.

> **Strict Boundary**: Visual tokens, spatial hierarchy, and layout constraints. Zero rogue hex values.

---

## 1. Core Palette Tokens

| Role | Token Name | Hex Code | Contrast & Usage |
|---|---|---|---|
| **Canvas Light** | `canvas-light` | `#F4F1EA` | Light mode base background; low-glare warm ground. |
| **Surface Light** | `surface-light` | `#FDFCF7` | Light mode raised cards, dialogs, and modals. |
| **Border Light** | `border-light` | `#E3DED5` | Light mode 1px perimeter borders and input boundaries. |
| **Canvas Dark** | `canvas-dark` | `#0C0D0F` | Dark mode base background; deep neutral charcoal. |
| **Surface Dark** | `surface-dark` | `#17181C` | Dark mode raised cards and elevated surfaces. |
| **Border Dark** | `border-dark` | `#26272E` | Dark mode 1px perimeter borders and input boundaries. |
| **Text Primary** | `text-primary` | `#0C0D0F` / `#FDFCF7` | Dynamic text: `#0C0D0F` on light (18.9:1 AAA), `#FDFCF7` on dark (18.9:1 AAA). |
| **Text Muted** | `text-muted` | `#66645E` / `#88857E` | Secondary metadata: `#66645E` on light (5.5:1 AA), `#88857E` on dark (5.2:1 AA). |
| **Accent Gold** | `accent-gold` | `#C59B4B` | Interactive focus rings, active navigation pills, badge containers (≤4%). |
| **Apex Red** | `apex-red` | `#962424` | Primary CTA, critical states, destructive alerts (≤1%). |

---

## 2. Design Rules

### Rule 1: Polarity & Contrast Invariants
- **Never Raw Gold Text on Light Canvas**: Accent Gold (`#C59B4B`) against Light Canvas is 2.3:1 (fails contrast). In Light Mode, Gold must be used only as a solid container with dark text (`#0C0D0F`, 7.5:1 AAA) or as a 1px border.
- **Never Raw Red Text on Dark Canvas**: Apex Red (`#962424`) against Dark Canvas is 2.2:1. In Dark Mode, Red must be used only as a solid button with white text (`#FDFCF7`, 7.9:1 AAA) or framed with a 1px gold hairline.
- **Red on Light**: High contrast as text, icons, and badges directly on light surfaces (7.9:1 AAA).
- **Gold on Dark**: High contrast as active navigation pills, focus rings, and metric highlights (7.5:1 AAA).

### Rule 2: Volume Allocation (The 70 / 25 / 4 / 1 Law)
- **70% Foundation**: Canvas and Surface. Clean whitespace without decorative clutter.
- **25% Structure & Typography**: High-contrast text, 1px perimeter borders, and muted metadata.
- **4% Accent Gold**: Active tab indicators, input focus rings, and badge containers.
- **≤1% Apex Red**: At most one primary CTA per viewport, or destructive action buttons.

### Rule 3: Depth Through Tone Step, Never Muddy Shadows
- **No Black Blur Shadows**: Generic blurred box shadows (`shadow-md`, `rgba(0,0,0,0.3)`) are banned.
- **Elevation via Tone Step**: Elevation is achieved by shifting from Canvas to Surface (`canvas-light` to `surface-light`, or `canvas-dark` to `surface-dark`), bounded by a 1px border (`border-light` or `border-dark`).

### Rule 4: Banned AI UI Composition Tropes
- **The AI Hero Cliché**: Centered headline + floating pill badge + symmetric dual buttons + 3 icon cards $\implies$ BANNED.
- **Arbitrary Glow Blobs**: Purple, cyan, or neon radial gradients behind card containers $\implies$ BANNED.
- **Card-in-Card Nesting**: Cards containing sub-cards $\implies$ BANNED. Use 1px border dividers or active whitespace.
- **Rogue Hex Codes**: Ad-hoc gray, blue, or purple hex values $\implies$ BANNED. All colors must trace to declared tokens.

### Rule 5: Surface States & Responsiveness
- **5-State Surfaces**: Every interactive element or container must define 5 states: Default, Hover/Focus, Loading skeleton, Empty state, and Error retry.
- **Viewport Invariants**: 390px mobile (single-column, zero horizontal overflow) and 1440px desktop.

---

## 3. Surface Adaptation (Configured in PRODUCT.md)
- **`Persuade` / `Experience` Surfaces** (Landing pages, marketing, showcases):
  - Emphasize scale contrast ($\ge 3.5:1$), unboxed typography, and kinetic precision (`@high-end-visual-design`).
- **`Operate` / `Read` Surfaces** (Dashboards, tools, docs):
  - Emphasize tabular telemetry, compact density, flat bento grids, and zero decorative distraction (`@minimalist-ui`).
