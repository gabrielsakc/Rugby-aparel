# Design System: THE H CONNECTION

> Rugby apparel atelier. Country-by-country catalogue. Embroidered, never printed.
> This document is the single source of truth for any new screen or surface — Stitch, Figma, marketing pages, email.

---

## 1. Visual Theme & Atmosphere

A **tactical telemetry interface meets editorial sports periodical**. Dark, mechanical, and confident — like a declassified field document published by a Swiss design studio. The interface should feel as though it has been *filed* rather than *designed*: indexed, stamped, archived.

- **Density:** Daily App Balanced (4) — generous breathing room, but data-dense where it counts (spec sheets, fixtures, telemetry ticker).
- **Variance:** Offset Asymmetric (8) — split heroes, shifted typographic lines, asymmetric bento tiles. No centred layouts.
- **Motion:** Fluid CSS Choreography (6) — restrained but perpetual. Scanlines pulse, status dots blink, ticker scrolls infinitely, scroll-entry reveals stagger.

The palette is a deactivated CRT, accented with a single hazard red. The typographic posture is heavy uppercase grotesque next to a quiet editorial italic serif. Every block of data is treated as a transmission, not decoration.

---

## 2. Color Palette & Roles

| Name | Hex | Role |
|---|---|---|
| **Carbon Bg** | `#0A0A0A` | Primary background (avoid pure `#000`) |
| **Elevated Surface** | `#111111` | Cards, hero image wells |
| **Tint Surface** | `#161616` | Hover-elevated craft cards |
| **Phosphor Ink** | `#EAEAEA` | Primary text, brand mark fill |
| **Muted Steel** | `#8A8A8A` | Secondary text, metadata |
| **Faint Steel** | `#4A4A4A` | Tertiary text, dividers' optical weight |
| **Hairline** | `rgba(234,234,234,0.08)` | 1px structural dividers |
| **Hairline Strong** | `rgba(234,234,234,0.16)` | Borders, ghost button outlines |
| **Hazard Red** | `#E61919` | THE accent — CTAs, active state, crosshairs, registration marks. Used like a stamp, not a fill. |
| **Phosphor Green** | `#4AF626` | LIVE status indicator only — never as text colour |
| **Paper** | `#F4F4F0` | Reserved for inverted blocks (CTA buttons, the H mark, banner stripes) |

**Rules:**
- Maximum **one** accent (Hazard Red). Saturation kept under control by surrounding it with neutrals.
- Phosphor Green appears in **at most one element per viewport** (a single live dot on the active fixture).
- No gradients on text. No glow shadows. No purple, no neon, no AI-blue.

---

## 3. Typography Rules

| Stack | Family | Use |
|---|---|---|
| **Display** | `Archivo Black` | All H1/H2 headlines, country names, mega footer mark. Tight tracking (`-0.04em`), line-height `0.85`, ALL CAPS. |
| **Body** | `Space Grotesk` | UI body, navigation, button text, descriptive copy. Weight 300–700. |
| **Mono** | `JetBrains Mono` | All telemetry: SKUs, coordinates, timestamps, spec table values, eyebrows, footnotes. Letter-spacing `0.16em–0.22em`, ALL CAPS. |
| **Editorial Serif** | `Fraunces` (italic, 300) | Sparingly — manifesto pull-quotes, the *"by union"* style accents inside headlines, lede copy. Lowercase, italic, light weight only. |

**Banned:** `Inter`, `Roboto`, `Times New Roman`, `Georgia`, `Garamond`. Serifs only as italic accents — never as block text.

**Hierarchy is set by weight, scale, AND voice swap** (grotesque → italic serif), not by colour or shadow.

---

## 4. Component Stylings

### Brand Mark (`H`)
- 36×36 inverted block. Off-black background swap to Phosphor Ink.
- Display font, single character, with floating `®` mark in mono at the upper-right corner (offset, not contained).
- Treats the `H` as a rugby goalpost — the literal brand metaphor.

### CTA Buttons
- Primary: solid Phosphor Ink (`#EAEAEA`) on Carbon background, with an inset arrow square that flips colour (Carbon-on-Ink). On hover the inner arrow translates `+2px / -2px` (NE diagonal). On active, the entire button drops `1px`.
- Magnetic micro-pull on cursor (`rAF`-driven, never React state).
- ASCII brackets `[ ]` enclose nav links and stamp metadata.
- No glow, no rounded pills. Sharp 90° corners everywhere.

### Cards (Bento Tiles)
- Background image clipped at `aspect-ratio: 4/5` or grid-spanned.
- Always desaturated and dimmed at rest (`grayscale(0.85) brightness(0.7)`), restored to colour on hover with a slow 1.4s ease.
- Linear gradient overlay (`rgba(10,10,10,0.85)` at bottom) ensures text legibility.
- 90° corners, no shadows. Separation comes from a 1px hairline grid (`gap: 1px` over a parent background).
- Crosshairs and corner brackets in Hazard Red mark the asset.

### Telemetry Ticker
- 32px tall horizontal strip at the very top.
- Infinite scroll (`60s linear`) using a duplicated track for seamless loop.
- Pulsing dots (Phosphor Green for status, Hazard Red for alerts).
- Mono only, `0.16em` tracking, ALL CAPS, 11px.

### Spec Tables
- Three-column grid: `key | value | unit`.
- Dashed 1px hairlines between rows (`border-top: 1px dashed`).
- Mono throughout, ALL CAPS, 10–12px.
- No backgrounds, no zebra. Pure typographic structure.

### Forms
- Single hairline border around the entire row. Border turns Hazard Red on `:focus-within`.
- Submit button is a solid block flush against the input, no gap.
- Placeholder text is mono, ALL CAPS, faint steel.

### Fixture Rows
- Five-column grid (`80px / 1fr / 1.4fr / 1fr / 100px`).
- Hover slides padding inward (`padding-inline: 16px`) — like a record being pulled from a drawer.
- Status dots: green = live (animated), red = pre-order, faint = queued.

---

## 5. Layout Principles

- **Container max-width:** `1480px`, padded with a fluid `clamp(16px, 2vw, 32px)`.
- **Sectional rhythm:** `clamp(80px, 12vw, 180px)` vertical padding between major sections.
- **Bento Grid:** 12-column CSS Grid with explicit `span-N` modifiers. Gap of `1px` over a hairline-coloured parent — no `border` declarations on tiles themselves.
- **Hero is asymmetric:** Headline column (1.4fr) + image aside (1fr). Lines within the headline shift left/right in 8vw increments to break the Bootstrap reflex.
- **No 3-equal-column feature rows.** When three things must appear together (the Craft section), they live in a hairline-divided 1×3 grid where each tile has its own number, icon, and footnote — never identical visual treatments.
- **No centred hero layouts.** Variance is locked at 8.
- **No `h-screen`.** Any full-viewport block uses `min-h-[100dvh]`.

### Responsive Collapse
- `< 1024px`: Bento collapses to a single vertical stack (`display: flex; flex-direction: column`). Drop spec sheets stack image above metadata. Nav links hide behind a (future) hamburger.
- `< 640px`: Brand text label hides (mark only). Manifesto column metadata stacks linearly. Footer collapses to single column.

---

## 6. Motion & Interaction

- **Easing:** `cubic-bezier(0.32, 0.72, 0, 1)` for UI transitions; `cubic-bezier(0.16, 1, 0.3, 1)` for entry reveals. **Never** linear, never `ease-in-out`.
- **Entry reveals:** `IntersectionObserver`-driven. `translateY(24px)` + `opacity 0` → resolved over `1s`. Stagger via `data-delay="1..6"` attributes (80ms multiplier).
- **Perpetual loops:** Ticker (60s), status-dot pulse (1.4s), scanline overlay (static but ever-present).
- **Hover physics:** Tiles' images zoom slowly (6s) and de-saturate to colour. CTA buttons pull magnetically toward the cursor (rAF).
- **Hardware-accelerated only.** All motion via `transform` and `opacity`. No `top/left/width/height` animations.
- **Backdrop blur** restricted to the sticky nav and overlays — never on scrolling content.

---

## 7. Iconography & Materiality

- Icon weight: 1.4–1.5 stroke. Source: hand-drawn primitives in inline SVG (no Lucide, no FontAwesome). Standardised across the site.
- **Crosshairs** at hero image corners, **registration brackets** (`[ ]`) around nav links, **slash markers** (`//`) in mono ID strings — these are the visual language of the brand. Use them, do not invent new ones.
- **Scanlines:** fixed `repeating-linear-gradient` overlay at 50% opacity, `mix-blend-mode: multiply`. Applied once, globally.
- **Noise:** SVG `feTurbulence` baked into a fixed background overlay at 6% opacity, `mix-blend-mode: overlay`. Never on scrolling containers.
- **Country flags / crests:** never displayed as full-bleed flags. Always reduced to a 2-letter ISO tag in mono, sometimes accompanied by longitude (`AR / 54° W`).

---

## 8. Voice & Copy

- Filed, not written. Indexed, not catalogued.
- Numbers are organic, never round. `184 PCS REMAINING`, `€78,40`, `12.4 KST`, `30°C wash`.
- Dates are uppercase mono with day prefix: `SAT · MAY 26`, `02/06/2026`.
- Telemetry units: `GSM`, `KST`, `PMS`, `°C`, `EN ISO 3758`, `GOTS`. Use real industry codes.
- Match results, fixture data, drop windows are written as **transmissions**: short, declarative, all caps for headers.
- **Banned phrases:** "Elevate", "Seamless", "Unleash", "Next-Gen", "Game-changer", "Scroll to explore", "Learn more", "Game-changing", "Discover".

---

## 9. Anti-Patterns (Banned)

- No emojis anywhere — code, content, alt text.
- No `Inter`. No `Roboto`. No system serif fallback as a display choice.
- No pure black `#000000`. Use Carbon `#0A0A0A`.
- No outer glows on buttons. No rounded pill containers. No 3D glassmorphism.
- No purple, no neon, no AI-blue gradient.
- No 3-equal-column "feature" rows.
- No centred hero with text-over-image.
- No "John Doe" / "Acme Corp" / "Lorem Ipsum" placeholders. Use real-feel names (`Hugo Etcheverry`, `Studio San Isidro`).
- No fake round numbers (`100%`, `99.99%`). Use `184 PCS`, `12.4 KST`, `04.62`.
- No bouncing chevrons, scroll-arrows, or "swipe down" prompts.
- No oversaturated stock photos. Imagery is desaturated, grain-treated, monochrome by default.
- No `h-screen`. Always `min-h-[100dvh]`.

---

## 10. The H

The brand mark is a single character: **H**. It is also the rugby goalpost. Treat it with the discipline of a logotype — never stretched, never coloured (only inverted), never animated. The full lockup is `H/CONNECTION` with the slash carrying as much weight as the letters. The footer renders `THE H CONNECTION®` at 18vw — the largest type in the entire system, used **once** per page.
