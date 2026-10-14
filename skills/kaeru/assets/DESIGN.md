# DESIGN.md — Visual System & Interaction Tokens

> **Strict Boundary**: Defines visual tokens, spatial hierarchy, and interaction physics.
> Worker agents implementing UI (Step 3) must strictly adhere to these tokens, dimensions, and dials.
> Zero rogue hex codes, zero ungrounded animations, zero AI composition clichés.

---

## 1. Aesthetic Doctrine: The Eight Core Abstractions

Every surface must ground its tokens in an intentional architectural lineage.  
**Flagship Baseline: Nippon Lapidary (日本の伝統色 & 石刻銘文)**

| # | Dimension | Flagship Abstraction | Implementation Rule |
|:---:|:---|:---|:---|
| **1** | **Chromatics** | Nippon Colors | Torinoko (`#E7E5E0`) canvas, Shironeri (`#EEECE8`) surface, Sumi (`#111215`) ink, Kincha (`#A88238`) accent ($\le 3\%$). 1px Usuzumi (`rgba(17,18,21,0.08)`) hairlines. |
| **2** | **Typography** | Lapidary & Neue Grafik | Titles: `Cinzel`/`Cormorant` monumental serif (`0.04em` tracking). Body: `Geist Sans` (`45ch–65ch`). Telemetry: `Geist Mono` (`tabular-nums`). **Min 3.5:1 scale tension**. |
| **3** | **Spatial Layout** | *Ma* & *Shakkei* (間 & 借景) | Negative space is an active subject. Eliminate card containers; typography floats directly on canvas. Asymmetric anchors. |
| **4** | **Motion** | *Iaidō* & *Shodō* (居合道 & 書道) | Directional clip-path reveals sub-250ms (*inkSlash*), organic brush wipes, 3.5s ensō ambient breathing pulse. |
| **5** | **Transitions** | *Fusuma* & *Hashigakari* (襖 & 橋掛かり) | Heavy horizontal sliding screen partitions; portal camera FOV transitions (`35°` $\rightarrow$ `51°`). Zero jarring flashes. |
| **6** | **Identity** | *Tenkoku* & *Hanko* (篆刻 & 判子) | Carved stone milestone seals (`鍛` Forge, `創` Create) in place of generic gamified XP/badges. |
| **7** | **Materiality** | *Wabi-Sabi* & *Sōan* (侘寂 & 草庵) | Translucent washi vellum (`backdrop-blur-xl`), matte unpolished stone, and shallow water reflections. |
| **8** | **Interaction** | *Teinei* & *Mono no Aware* (丁寧 & 物の哀れ) | Physical micro-depressions (`active:scale-[0.98]`). Ephemeral cues dissolve silently after 6s. |

*(Custom projects may re-skin values during setup, but must define all 8 dimensions. Never leave surfaces ungrounded).*

---

## 2. Tokens & Variables

```css
:root {
  --canvas-torinoko: #E7E5E0;
  --surface-shironeri: #EEECE8;
  --ink-sumi: #111215;
  --meta-namari: #5F5E59;
  --accent-kincha: #A88238; /* Strictly <= 3% allocation */
  --hairline-usuzumi: rgba(17, 18, 21, 0.08);
}
```

---

## 3. Visual Dials (1–10)
- `VARIANCE`: [1–10] (1 = rigid symmetry; 5 = dynamic offset split col-span-7/5; 10 = radical broken-grid tension)
- `MOTION`: [1–10] (1 = instant state switches; 5 = spring physics `cubic-bezier(0.16, 1, 0.3, 1)`; 10 = GSAP ScrollTrigger pinning)
- `DENSITY`: [1–10] (1 = expansive luxury *Ma* void; 5 = balanced ergonomics 45ch–65ch; 10 = compact tabular telemetry)

---

## 4. Anti-Slop Invariants & Surface Standards
- **Banned AI Composition Tropes**: No centered headline + floating pill badge + symmetric dual buttons + 3 icon cards. BANNED. No card-in-card nesting. BANNED. No arbitrary purple/cyan radial gradients. BANNED.
- **5-State Surface Coverage**: Every interactive surface must implement Default, Hover/Focus, Loading skeleton, Empty callout, and Error/Retry.
- **Viewport Verification**: Verified at 390px mobile and 1440px desktop. Zero horizontal overflow.
